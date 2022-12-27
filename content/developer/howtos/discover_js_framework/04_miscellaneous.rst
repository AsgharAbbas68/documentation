========================
Chapter 4: Miscellaneous
========================

In the previous task, we learned how to create fields and views. There is still much more to
discover in the feature-rich Odoo web framework, so let's dive in and explore more in this chapter!

.. graph TD
..     subgraph "Owl"
..         C[Component]
..         T[Template]
..         H[Hook]
..         S[Slot]
..         E[Event]
..     end

..     subgraph "odoo"[Odoo Javascript framework]
..         Services
..         Translation
..         lazy[Lazy loading libraries]
..         SCSS
..         action --> Services
..         rpc --> Services
..         orm --> Services
..         Fields
..         Views
..         Registries
..     end

..     odoo[Odoo JavaScript framework] --> Owl

.. image:: 04_miscellaneous/previously_learned.svg
   :align: center
   :alt: What we learned in chapter 3
   :width: 60%

.. admonition:: Goal

   .. image:: 04_miscellaneous/kitten_mode.png
      :align: center
      :alt: kitten mode

.. spoiler:: Solutions

   The solutions for each exercise of the chapter are hosted on the `official Odoo tutorials
   repository <https://github.com/odoo/tutorials/commits/{BRANCH}-solutions/awesome_tshirt>`_.

1. Interacting with the notification system
===========================================

.. note::

  This task depends on the previous exercise.

After using the "Print Label" button for some t-shirt tasks, it is apparent that there should be
some feedback that the `print_label` action is completed (or failed, for example, the printer is not
connected or ran out of paper).

.. exercise::
   #. Display a :ref:`notification <frontend/services/notification>` message when the action
      is completed succesfully, and a warning if it failed.
   #. If it failed, the notification should be permanent.

   .. image:: 04_miscellaneous/notification.png
      :align: center
      :scale: 60%
      :alt: notification message

.. seealso::

  - `example: code using the notification service
    <{GITHUB_PATH}/addons/web/static/src/views/fields/image_url/image_url_field.js>`_

2. Add a systray item
=====================

Our beloved leader want to keep a close eyes on new orders. He want to see the number of new,
unprocessed orders at all time. Let's do that with a systray item.

A :ref:`systray <frontend/registries/systray>` item is an element that appears in the system tray,
which is a small area located in the right of the navbar. The systray is used to display
notifications and provide access to certain features.

.. exercise::

   #. Create a systray component that connects to the statistics service we made previously.
   #. Use it to display the number of new orders.
   #. Clicking on it should open a list view with all of these orders.
   #. Bonus point: avoid doing the initial rpc by adding the information to the session info. The
      session info is given to the web client by the server in the initial response.

   .. image:: 04_miscellaneous/systray.png
      :align: center
      :alt: new systray item

.. seealso::

  - `example: systray item <{GITHUB_PATH}/addons/web/static/src/webclient/user_menu/user_menu.js>`_
  - `example: adding some information to the "session info"
    <{GITHUB_PATH}/addons/barcodes/models/ir_http.py>`_
  - `example: reading the session information
    <{GITHUB_PATH}/addons/barcodes/static/src/barcode_service.js#L5>`_

3. Real life update
===================

So far, the systray item from above does not update unless the user refreshes the browser. Let us
do that by calling periodically (for example, every minute) the server to reload the information

.. exercise::

   #. Modify the systray item code to get its data from the tshirt service.
   #. The tshirt service should periodically reload its data.

Now the question arises: how is the systray item notified that it should rerender itself? It can be
done in various ways, but for this training, we will chose to use the most *declarative* approach:

.. exercise::

   #. Modify the tshirt service to return a `reactive
      <{OWL_PATH}/doc/reference/reactivity.md#reactive>`_ object. Reloading data should update the
      reactive object in place.
   #. The systray item can then perform a `useState` on the service return value.
   #. This is not really necessary, but you can also *package* the calls to `useService` and
      `useState` in a custom hook `useStatistics`.

.. seealso::

  - `owl: page on reactivity <{OWL_PATH}/doc/reference/reactivity.md>`_
  - `example: use of reactive in a service
    <{GITHUB_PATH}/addons/web/static/src/core/debug/profiling/profiling_service.js#L30>`_

4. Add a command to the command palette
=======================================

Now, let us see how we can interact with the command palette. The command palette is a feature that
allows users to quickly access various commands and functions within the application. It is accessed
by pressing `CTRL+K` in the Odoo interface.

.. exercise::

   Let us modify the image preview field (from a previous exercise) to add a command to the command
   palette to open the image in a new browser tab (or window).

   Make sure that the command is only active whenever a field preview is visible in the screen.

   .. image:: 04_miscellaneous/new_command.png
      :align: center
      :alt: new command

.. seealso::

  - `example: using the useCommand hook
    <{GITHUB_PATH}/addons/web/static/src/core/debug/debug_menu.js#L15>`_
  - `code: command service <{GITHUB_PATH}/addons/web/static/src/core/commands/command_service.js>`_

5. Monkey patching a component
==============================

Often, it is possible to do what we want by using existing extension points that allow
customization, such as registering something in a registry. But it happens that we want to modify
something that has no such mechanism. In that case, we have to fall back on a less safe form of
customization: monkey patching. Almost everything in odoo can be monkey patched.

Bafien, our beloved leader, heard that employees perform better if they are constantly being
watched. Since he is not able to be there in person for each and every one of his employees, he
tasked you with the following: update the Odoo user interface to add a blinking red eye in the
control panel. Clicking on that eye should open a dialog with the following message: "Bafien is
watching you. This interaction is recorded and may be used in legal proceedings if necessary. Do
you agree to these terms?".

.. exercise::

   #. Create the `control_panel_patch.js` file, as well as corresponding css and xml files.
   #. :ref:`Patch <reference/patching>` the `ControlPanel` template to add some icon next to the
      breadcrumbs (you may want to use the `fa-eye` or `fa-eyes` icon).

      .. note::

         There are two ways to inherit a template using XPath: by specifying
         `t-inherit-mode="primary"`, which creates a new, independent template with the desired
         modifications, or by using `t-inherit-mode="extension"`, which modifies the original
         template in place.

      .. code-block:: css

         .blink {
           animation: blink-animation 1s steps(5, start) infinite;
           -webkit-animation: blink-animation 1s steps(5, start) infinite;
         }
         @keyframes blink-animation {
           to {
             visibility: hidden;
           }
         }
         @-webkit-keyframes blink-animation {
           to {
               visibility: hidden;
           }
         }

      Make sure it is visible in all views!
   #. Import the `ControlPanel` component and the `patch` function.
   #. Update the code to display the message on click by using the dialog service (you can use the
      `ConfirmationDialog`).

   .. image:: 04_miscellaneous/bafien_eye.png
      :align: center
      :scale: 60%
      :alt: eye of Bafien

   .. image:: 04_miscellaneous/confirmation_dialog.png
      :align: center
      :scale: 60%
      :alt: confirmation dialog

.. seealso::

   - `code: patch function <{GITHUB_PATH}/addons/web/static/src/core/utils/patch.js#L16>`_
   - `code: ControlPanel component
     <{GITHUB_PATH}/addons/web/static/src/search/control_panel/control_panel.js>`_
   - `font awesome website <https://fontawesome.com/>`_
   - `code: dialog service <{GITHUB_PATH}/addons/web/static/src/core/dialog/dialog_service.js>`_
   - `code: ConfirmationDialog
     <{GITHUB_PATH}/addons/web/static/src/core/confirmation_dialog/confirmation_dialog.js>`_
   - `example: using the dialog service
     <{GITHUB_PATH}/addons/board/static/src/board_controller.js#L88>`_
   -  `example: XPath with t-inherit-mode="primary"
      <{GITHUB_PATH}/addons/account/static/src/components/account_move_form/account_move_form_notebook.xml#L4>`_
   -  `example: XPath with t-inherit-mode="extension"
      <{GITHUB_PATH}/calendar/static/src/components/activity/activity.xml#L4>`_

6. Fetching orders from a customer
==================================

Let's see how to use some standard components to build a powerful feature, combining autocomplete,
fetching data, fuzzy lookup. We will add an input in our dashboard to easily search all orders from
a given customer.

.. exercise::

   #. Update the `tshirt_service` to add a method `loadCustomers`, which returns a promise that
      returns the list of all customers (and only performs the call once).
   #. Import the `AutoComplete` component from `@web/core/autocomplete/autocomplete`.
   #. Add it to the dashboard, next to the buttons in the control panel.
   #. Update the code to fetch the list of customers with the tshirt service, and display it in the
      autocomplete component, filtered by the `fuzzyLookup` method.

   .. image:: 04_miscellaneous/autocomplete.png
      :align: center
      :scale: 60%
      :alt: autocomplete input

.. seealso::

   - `code: AutoComplete <{GITHUB_PATH}/addons/web/static/src/core/autocomplete/autocomplete.js>`_
   - `code: fuzzyLookup <{GITHUB_PATH}/addons/web/static/src/core/utils/search.js>`_

7. Reintroduce Kitten Mode
==========================

Let us add a special mode to Odoo: whenever the url contains `kitten=1`, we will display a kitten in
the background of odoo, because we like kittens.

.. exercise::

   #. Create a `kitten_mode.js` file.
   #. Create a `kitten` service, which should check the content of the active url hash with the
      help of the :ref:`router service <frontend/services/router>`.
   #. If `kitten` is set, we are in kitten mode. This should add a class `.o-kitten-mode` on
      document body.
   #. Add the following css in `kitten_mode.scss`:

      .. code-block:: css

         .o-kitten-mode {
           background-image: url(https://upload.wikimedia.org/wikipedia/commons/5/58/Mellow_kitten_%28Unsplash%29.jpg);
           background-size: cover;
           background-attachment: fixed;
         }

         .o-kitten-mode > * {
           opacity: 0.9;
         }

   #. Add a command to the command palette to toggle kitten mode. Toggling the kitten mode should
      toggle the `.o-kitten-mode` class and update the current url accordingly.

   .. image:: 04_miscellaneous/kitten_mode.png
      :align: center
      :alt: kitten mode

8. Lazy loading our dashboard
=============================

This is not really necessary, but the exercise is interesting. Imagine that our awesome dashboard
is a large application, with potentially multiple external libraries, lots of code/styles/templates.
Also, suppose that the dashboard is only used by some users in some business flows, so we want to
lazy load it, in order to speed up the loading of the web client in most cases.

So, let us do that!

.. exercise::

   #. Modify the manifest to create a new :ref:`bundle <reference/assets_bundle>`
      `awesome_tshirt.dashboard`.
   #. Add the awesome dashboard code to this bundle. If needed you can create folders and move files
      .
   #. Remove the code from the `web.assets_backend` bundle so it is not loaded twice.

So far, we removed the dashboard from the main bundle, but it should now be lazily loaded. Right
now, there is no client action registered in the action registry.

.. exercise::

   #. Create a new file `dashboard_loader.js`.
   #. Copy the code registering `AwesomeDashboard` to the dashboard loader.
   #. Register `AwesomeDashboard` as a `LazyComponent`.
   #. Modify the code in the dashboard loader to use the lazy component `AwesomeDashboard`.

.. seealso::

  - :ref:`odoo: assets documentation <reference/assets>`
  - `code: LazyComponent <{GITHUB_PATH}/addons/web/static/src/core/assets.js#L255>`_
