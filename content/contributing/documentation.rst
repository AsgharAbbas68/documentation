:show-content:

=============
Documentation
=============

.. toctree::
   :titlesonly:

   documentation/content_guidelines
   documentation/rst_cheat_sheet
   documentation/rst_guidelines

This introductory guide will help you acquire the tools and knowledge you need to write
documentation, whether you plan to make a minor content change or document an application from
scratch.

.. seealso::
   :doc:`Discover other ways to contribute to Odoo <../contributing>`

Read the :ref:`introduction to the reStructuredText language <contributing/documentation/rst-intro>`
if you are not familiar with it. Then, you have two courses of action to start contributing to the
documentation, depending on whether you want to propose minor changes to existing content or you
instead want to work on significant changes to new and existing content.

- **For minor changes**, for example, adding a paragraph or fixing a typo, we recommend **using the
  GitHub interface**. This is the easiest and fastest way to submit your changes, and it is suitable
  for non-technical people. Jump directly to the
  :ref:`contributing/documentation/first-contribution` section to get started.
- **For more complex changes**, it is necessary to **use Git** and work from a local copy of the
  documentation. Follow the instructions in the :ref:`contributing/documentation/setup` section to
  first prepare your environment.

.. _contributing/documentation/rst-intro:

reStructuredText (RST)
======================

The documentation is written in **reStructuredText** (RST), a `lightweight markup language
<https://en.wikipedia.org/wiki/Lightweight_markup_language>`_ consisting of regular text augmented
with markup, which allows including headings, images, notes, and so on. This might seem a bit
abstract, but there is no need to worry; :abbr:`RST (reStructuredText)` is not hard to learn,
especially if you intend to make minor changes to the content.

If you need to learn about a specific markup, head over to our :doc:`cheat sheet for RST
<documentation/rst_cheat_sheet>`; it contains all the information you should ever need for the
documentation of Odoo.

.. important::
   We kindly ask you to observe a set of :doc:`content <documentation/content_guidelines>` and
   :doc:`RST <documentation/rst_guidelines>` guidelines as you write documentation. This ensures
   that you stay consistent with the rest of the documentation and facilitates the approval of your
   content changes as the Odoo team reviews them.

.. seealso::
   - :doc:`documentation/content_guidelines`
   - :doc:`documentation/rst_cheat_sheet`
   - :doc:`documentation/rst_guidelines`

.. _contributing/documentation/setup:

Environment setup
=================

The instructions below help you prepare your environment for making local changes to the
documentation and then push them to GitHub. Skip this section and go to
:ref:`contributing/documentation/first-contribution` if you have already completed this step or want
to make changes from the GitHub interface.

#. .. include:: create_github_account.rst
#. .. include:: configure_github_account.rst
#. Go to `github.com/odoo/documentation <https://github.com/odoo/documentation>`_ and click on the
   :guilabel:`Fork` button in the top right corner to create a fork (:dfn:`your own copy`) of the
   repository on your account. This creates a copy of the codebase to which you can make changes
   without affecting the main codebase. Skip this step if you work at Odoo.
#. .. include:: install_git.rst
#. .. include:: configure_git_authorship.rst
#. Clone the sources with Git and navigate into the local repository.

   .. code-block:: console

      $ git clone git@github.com:odoo/documentation.git
      $ cd documentation

#. Configure Git to push changes to your fork rather than to the main codebase. In the commands
   below, replace `<your_github_account>` with the name of the GitHub account on which you created
   the fork. Skip this step if you work at Odoo.

   .. code-block:: console

      $ git remote add dev git@github.com:<your_github_account>/documentation.git

#. Configure Git to ease the collaboration between writers coming from different systems.

   .. tabs::

      .. group-tab:: Linux and macOS

         .. code-block:: console

            $ git config --global core.autocrlf input
            $ git config commit.template `pwd`/commit_template.txt

      .. group-tab:: Windows

         .. code-block:: console

            $ git config --global core.autocrlf true
            $ git config commit.template %CD%\commit_template.txt

<<<<<<< HEAD
         Replace `<username>` with your GitHub username. If you work at Odoo, replace it with
         `odoo`.

#. In order to ease the collaboration between writers coming from many different systems and teams,
   execute the following group of commands that correspond to your :abbr:`OS (Operating System)` in
   a terminal.

   - Windows:

     .. code-block:: doscon

        $ cd documentation/
        $ git config --global core.autocrlf true
        $ git config commit.template %CD%\commit_template.txt

   - Linux or Mac OS:

     .. code-block:: console

        $ cd documentation/
        $ git config --global core.autocrlf input
        $ git config commit.template `pwd`/commit_template.txt

.. _contributing/python:

Python
~~~~~~

Because the documentation is written in :abbr:`RST (reStructuredText)`, it needs to be built
(:dfn:`converted to HTML`) in order to display nicely. This is done by the documentation generator
which takes the original :abbr:`RST (reStructuredText)` files as input, transforms the markups
in a human-readable format, and outputs HTML files to be read in your web browser.

The documentation generator that we use is called `Sphinx <http://www.sphinx-doc.org/en/master/>`_.
and is written in `Python <https://en.wikipedia.org/wiki/Python_(programming_language)>`_. You have
to install Python in order to use Sphinx. For the record, Sphinx is the program and Python the
programming language, but you do not need to know much more about them so don't panic!

Python comes with its own package manager: `pip
<https://en.wikipedia.org/wiki/Pip_(package_manager)>`_. It allows installing Python dependencies in
a single command.

#. Download and install the recommended release (`see README file
   <https://github.com/odoo/documentation/tree/15.0/README.md>`_) of **Python 3** on your machine.
#. Make sure to have **pip** installed on your machine (on Windows, you can install pip alongside
   Python).
#. Execute the following commands in a terminal to verify that both installations finished
   successfully:
||||||| parent of f0fc35af (temp)
         Replace `<username>` with your GitHub username. If you work at Odoo, replace it with
         `odoo`.

#. In order to ease the collaboration between writers coming from many different systems and teams,
   execute the following group of commands that correspond to your :abbr:`OS (Operating System)` in
   a terminal.

   - Windows:

     .. code-block:: doscon

        $ cd documentation/
        $ git config --global core.autocrlf true
        $ git config commit.template %CD%\commit_template.txt

   - Linux or Mac OS:

     .. code-block:: console

        $ cd documentation/
        $ git config --global core.autocrlf input
        $ git config commit.template `pwd`/commit_template.txt

.. _contributing/python:

Python
~~~~~~

Because the documentation is written in :abbr:`RST (reStructuredText)`, it needs to be built
(:dfn:`converted to HTML`) in order to display nicely. This is done by the documentation generator
which takes the original :abbr:`RST (reStructuredText)` files as input, transforms the markups
in a human-readable format, and outputs HTML files to be read in your web browser.

The documentation generator that we use is called `Sphinx <http://www.sphinx-doc.org/en/master/>`_.
and is written in `Python <https://en.wikipedia.org/wiki/Python_(programming_language)>`_. You have
to install Python in order to use Sphinx. For the record, Sphinx is the program and Python the
programming language, but you do not need to know much more about them so don't panic!

Python comes with its own package manager: `pip
<https://en.wikipedia.org/wiki/Pip_(package_manager)>`_. It allows installing Python dependencies in
a single command.

#. Download and install the recommended release (`see README file
   <https://github.com/odoo/documentation/tree/{BRANCH}/README.md>`_) of **Python 3** on your machine.
#. Make sure to have **pip** installed on your machine (on Windows, you can install pip alongside
   Python).
#. Execute the following commands in a terminal to verify that both installations finished
   successfully:
=======
#. Install the latest release of `Python <https://wiki.python.org/moin/BeginnersGuide/Download>`_
   and `pip <https://pip.pypa.io/en/stable/installation/>`_ on your machine.
#. Install the Python dependencies of the documentation with pip.
>>>>>>> f0fc35af (temp)

   .. code-block:: console

      $ pip install -r requirements.txt

   Verify that the installation directory of the Python dependencies is included in your system's
   `PATH` variable.

   .. tabs::

      .. group-tab:: Linux and macOS

         Follow the `guide to update the PATH variable on Linux and macOS
         <https://unix.stackexchange.com/a/26059>`_ with the installation path of the Python
         dependencies (by default :file:`~/.local/bin`).

      .. group-tab:: Windows

         Follow the `guide to update the PATH variable on Windows
         <https://www.howtogeek.com/118594/how-to-edit-your-system-path-for-easy-command-line-access/>`_
         with the installation path of the Python dependencies.

#. Install Make.

   .. tabs::

      .. group-tab:: Linux and macOS

         .. code-block:: console

            $ sudo apt install make -y

      .. group-tab:: Windows

         Follow the `guide to install Make on Windows
         <https://www.technewstoday.com/install-and-use-make-in-windows>`_.

#. `Install pngquant <https://pngquant.org/>`_.
#. That's it! You are ready to :ref:`make your first contribution
   <contributing/documentation/first-contribution>` with Git.

<<<<<<< HEAD
Now that your machine is all set up, it is time to do the same for your version of the documentation
files. As it would not be convenient to have several people working on the version 13.0 in parallel
(conflicts of content would occur all the time), and in order to be able to create a :abbr:`PR
(Pull Request)`, you must `create a new branch
<https://www.atlassian.com/git/tutorials/using-branches>`_ starting from the branch 13.0. In other
words, you copy the entirety of this version’s files and give it another name. For this example, we
will go with ``13.0-my_contribution``.
||||||| parent of f0fc35af (temp)
Now that your machine is all set up, it is time to do the same for your version of the documentation
files. As it would not be convenient to have several people working on the version {BRANCH} in
parallel (conflicts of content would occur all the time), and in order to be able to create a
:abbr:`PR (Pull Request)`, you must `create a new branch
<https://www.atlassian.com/git/tutorials/using-branches>`_ starting from the branch {BRANCH}. In
other words, you copy the entirety of this version’s files and give it another name. For this
example, we will go with ``{BRANCH}-my_contribution``.
=======
.. _contributing/documentation/first-contribution:
>>>>>>> f0fc35af (temp)

Make your first contribution
============================

.. tabs::

   .. tab:: Contribute from the GitHub interface
      #. .. include:: create_github_account.rst
      #. Verify that you are browsing the documentation in the version that you intend to change.
         The version can be selected from the dropdown in the top menu.
      #. Head to the page that you want to change and click on the :guilabel:`Edit on GitHub` button
         in the top right corner of the page.
      #. Click on the :guilabel:`Fork this repository` button to create a fork (:dfn:`your own
         copy`) of the repository on your account. This creates a copy of the codebase to which you
         can make changes without affecting the main codebase. Skip this step if you work at Odoo.

         .. image:: documentation/fork-repository.png
            :scale: 60%

<<<<<<< HEAD
#. Switch to the version 13.0:
||||||| parent of f0fc35af (temp)
#. Switch to the version {BRANCH}:
=======
      #. Make the desired changes while taking care of following the :doc:`content
         <documentation/content_guidelines>` and :doc:`RST <documentation/rst_guidelines>`
         guidelines.
>>>>>>> f0fc35af (temp)

         .. tip::
            Click on the :guilabel:`Preview changes` button to review your contribution in a more
            human-readable format. Be aware that the preview is not able to handle all markups
            correctly. Notes and tips, for instance, are shown as plain text.

<<<<<<< HEAD
      $ git checkout 13.0
||||||| parent of f0fc35af (temp)
      $ git checkout {BRANCH}
=======
      #. Scroll to the bottom of the page and fill out the small form to propose your changes. In
         the first text box, write a very short summary of your changes. For instance, "Fix a typo"
         or "Add documentation for invoicing of sales orders". In the second text box, explain *why*
         you are proposing these changes. Then, click on the :guilabel:`Propose changes` button.
>>>>>>> f0fc35af (temp)

<<<<<<< HEAD
#. Create your own branch which will be a copy of 13.0:
||||||| parent of f0fc35af (temp)
#. Create your own branch which will be a copy of {BRANCH}:
=======
         .. image:: documentation/propose-changes.png
            :scale: 60%
>>>>>>> f0fc35af (temp)

      #. Review your changes and click on the :guilabel:`Create pull request` button.
      #. Tick the :guilabel:`Allow edits from maintainer` checkbox. Skip this step if you work at
         Odoo.
      #. Review the summary that you wrote about your changes and click on the :guilabel:`Create
         pull request` button again.
      #. .. include:: check_mergeability_status.rst
      #. .. include:: handle_reviews.rst
      #. .. include:: documentation/changes_approved.rst

<<<<<<< HEAD
      $ git checkout -b 13.0-my_contribution
||||||| parent of f0fc35af (temp)
      $ git checkout -b {BRANCH}-my_contribution
=======
   .. tab:: Contribute with Git
>>>>>>> f0fc35af (temp)

      .. important::
         Some steps of this guide require to be comfortable with Git. Here are some `tutorials
         <https://www.atlassian.com/git/tutorials>`_ and an `interactive training
         <https://learngitbranching.js.org/>`_ if you are stuck at some point.

      Now that your environment is set up, you can start contributing to the documentation. In a
      terminal, navigate to the directory where you cloned the sources and follow the guide below.

      #. Choose the version of the documentation to which you want to make changes. Keep in mind
         that contributions targeting an :doc:`unsupported version of Odoo
         </administration/maintain/supported_versions>` are not accepted. This guide assumes that
         the changes target the documentation of Odoo {CURRENT_VERSION}, which corresponds to branch
         `{CURRENT_BRANCH}`.
      #. Create a new branch starting from branch {CURRENT_BRANCH}. Prefix the branch name with the
         base branch: `{CURRENT_BRANCH}-...`. If you work at Odoo, suffix the branch name with your
         Odoo handle: `{CURRENT_BRANCH}-...-xyz`.

         .. example::

            .. code-block:: console

               $ git switch -c {CURRENT_BRANCH}-explain-pricelists

            .. code-block:: console

<<<<<<< HEAD
     #. Delete :file:`my-image.png`.
     #. Rename :file:`my-image-fs8.png` to :file:`my-image.png`.
   - If your changes include renaming or moving an RST file to a new location, follow the `manual
     for redirect rules <https://github.com/odoo/documentation/tree/13.0/redirects/MANUAL.md>`_ to
     create the appropriate redirect rule(s).
||||||| parent of f0fc35af (temp)
     #. Delete :file:`my-image.png`.
     #. Rename :file:`my-image-fs8.png` to :file:`my-image.png`.
   - If your changes include renaming or moving an RST file to a new location, follow the `manual
     for redirect rules <https://github.com/odoo/documentation/tree/{BRANCH}/redirects/MANUAL.md>`_
     to create the appropriate redirect rule(s).
=======
               $ git switch -c {CURRENT_BRANCH}-explain-pricelists-xyz
>>>>>>> f0fc35af (temp)

      #. Make the desired changes while taking care of following the :doc:`content
         <documentation/content_guidelines>` and :doc:`RST <documentation/rst_guidelines>`
         guidelines.
      #. Compress all PNG images that you added or modified.

         .. code-block:: console

            $ pngquant path/to/image.png
            $ mv path/to/image-fs8.png path/to/image.png

      #. Write a `redirect rule
         <https://github.com/odoo/documentation/tree/{BRANCH}/redirects/MANUAL.md>`_ for every RST
         file that your renamed.
      #. Build the documentation with :command:`make`. Then, open :file:`_build/index.html` in your
         web browser to browse the documentation with your changes.

         .. tip::
            Use :command:`make help` to learn about other useful commands.

      #. Commit your changes. Write a clear commit message as instructed in the :doc:`Git guidelines
         <development/git_guidelines>`.

         .. code-block:: console

            $ git add .
            $ git commit

      #. Push your change to your fork, for which we added the remote alias `dev`.

         .. example::

            .. code-block:: console

               $ git push -u dev {CURRENT_BRANCH}-explain-pricelists

         If you work at Odoo, push your changes directly to the main codebase whose remote alias is
         `origin`.

         .. example::

<<<<<<< HEAD
      $ git add *
      $ git commit
      $ git push -u origin 13.0-my_contribution
||||||| parent of f0fc35af (temp)
      $ git add *
      $ git commit
      $ git push -u origin {BRANCH}-my_contribution
=======
            .. code-block:: console
>>>>>>> f0fc35af (temp)

               $ git push -u origin {CURRENT_BRANCH}-explain-pricelists-xyz

      #. Open a :abbr:`PR (Pull Request)` on GitHub to submit your changes for review.

         #. Go to the `compare page of the odoo/documentation codebase
            <https://github.com/odoo/documentation/compare>`_.
         #. Select **{CURRENT_BRANCH}** for the base.
         #. Click on :guilabel:`compare across forks`.
         #. Select **<your_github_account>/odoo** for the head repository. Replace
            `<your_github_account>` with the name of the GitHub account on which you created the
            fork. Skip this step if you work at Odoo.
         #. Review your changes and click on the :guilabel:`Create pull request` button.
         #. Tick the :guilabel:`Allow edits from maintainer` checkbox. Skip this step if you work at
            Odoo.
         #. Complete the description and click on the :guilabel:`Create pull request` button again.

<<<<<<< HEAD
   .. image:: documentation/compare-across-forks.png

#. In the dropdown for the selection of the base branch (i.e., the version of the documentation that
   your changes concern), make sure to select the version that your changes target (here **13.0**).

   .. image:: documentation/select-branches-fork.png

#. Double-check your :abbr:`PR (Pull Request)` and, when ready, click again on the **Create pull
   request** button to submit your changes for review by a redactor at Odoo.

   .. image:: documentation/create-pull-request.png

#. You're done! If your changes are approved straight away they will appear in the documentation the
   very next day. It may also be the case that the reviewer has a question or a remark, so make sure
   to check your notifications or your emails, depending on your account settings.


.. _win-add-to-path: https://www.howtogeek.com/118594/how-to-edit-your-system-path-for-easy-command-line-access/
||||||| parent of f0fc35af (temp)
   .. image:: documentation/compare-across-forks.png

#. In the dropdown for the selection of the base branch (i.e., the version of the documentation that
   your changes concern), make sure to select the version that your changes target (here
   **{BRANCH}**).

   .. image:: documentation/select-branches-fork.png

#. Double-check your :abbr:`PR (Pull Request)` and, when ready, click again on the **Create pull
   request** button to submit your changes for review by a redactor at Odoo.

   .. image:: documentation/create-pull-request.png

#. You're done! If your changes are approved straight away they will appear in the documentation the
   very next day. It may also be the case that the reviewer has a question or a remark, so make sure
   to check your notifications or your emails, depending on your account settings.


.. _win-add-to-path: https://www.howtogeek.com/118594/how-to-edit-your-system-path-for-easy-command-line-access/
=======
      #. .. include:: check_mergeability_status.rst
      #. .. include:: handle_reviews.rst
      #. .. include:: documentation/changes_approved.rst
>>>>>>> f0fc35af (temp)
