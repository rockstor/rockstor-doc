.. _contributedocs:

Contributing to Rockstor documentation
======================================

Steps for contributing to **rockstor-doc** repo are similar to contributing to **rockstor-core**, 
as we follow the same fork and pull request model.
We will assume you have basic proficiency with Git and are familiar with using a text editor or IDE of your choice.
Emacs, Vim, Eclipse and PyCharm are some recommendations.
Or you may be able to use an online editor such as https://www.tutorialspoint.com/compilers/online-restructure-editor.htm.

Environment setup
-----------------

Clone the repository
^^^^^^^^^^^^^^^^^^^^

We will assume that you have your laptop ready with Git and an editor installed.
Since we rely on github services, you need to create a profile on github.com.
Once you have your profile set-up on `github.com <https://github.com>`_, follow
these steps:

Go to `rockstor-doc repo <https://github.com/rockstor/rockstor-doc>`_ and click on the **Fork** button.
This will fork the repository into your profile which serves as your private Git remote called *origin*.
The next few Git steps are demonstrated on a Linux terminal.
They work the same on a Mac too.

.. code-block:: console

    you@laptop:~> mkdir ~/dev; cd ~/dev
    you@laptop:~/dev> git clone git@github.com:your_github_username/rockstor-doc.git

The above command creates a local **rockstor-doc** Git repo in a new directory by the same name (rockstor-doc) inside the new "~/dev" directory.
Change into it.

.. code-block:: console

    you@laptop:~/dev> cd rockstor-doc

Configure this new Git repo with your name and email address.
This is required to accurately record collaboration.

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> git config user.name "Firstname Lastname"
    you@laptop:~/dev/rockstor-doc> git config user.email your_email_address

Add a remote called upstream to periodically rebase your local repository with changes in the upstream made by other contributors.

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> git remote add upstream https://github.com/rockstor/rockstor-doc.git

If desired, you can now verify these settings are correct by displaying the Git configuration for the local repository:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> git config --list --local


Installing Sphinx
^^^^^^^^^^^^^^^^^

Unlike for code contributions, there is no need for a dedicated virtual machine to build the documentation.
Indeed, source pages for Rockstor's documentation are written in `reStructuredText <https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_ (*.rst* files) that can be easily edited manually to fit our needs.
We then use the documentation generator `Sphinx <https://www.sphinx-doc.org>`_ to generate the HTML content from these *.rst* files.
`Sphinx official documentation <https://www.sphinx-doc.org/en/master/#>`_ gives guidelines for its installation on various platforms.
We thus refer to their instructions on how to install Sphinx: `Installing Spinx <https://www.sphinx-doc.org/en/master/usage/installation.html>`_.

Once you have Sphinx installed, you'll need 1 more Sphinx extension before you're fully ready.
The `sphinxext-rediraffe <https://github.com/wpilibsuite/sphinxext-rediraffe>`_ extension is used to generate redirections for pages that no longer exist or have been moved.
While you may not use the functionality of this extension in your page, when you execute :code:`make html` to check your work, 
you will need it for :code:`make` to complete successfully.

To install **sphinxext-rediraffe**, use this command:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> sudo pip3 install --user sphinxext-rediraffe


.. _dockersphinx:

Using Sphinx as a Docker container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sphinx can also be used as a Docker container, without needing to install it on your computer.
As the base `docker-sphinx <https://github.com/sphinx-doc/sphinx-docker-images>`_ image does not contain the **sphinxext-rediraffe** extension needed to build Rockstor's documentation,
we need to use a custom Docker image.
This can easily be done using a `custom Dockerfile <https://github.com/rockstor/rockstor-doc/blob/master/docker/Dockerfile>`_.
For convenience, we provide `the corresponding Docker image <https://github.com/rockstor/rockstor-doc/pkgs/container/rockstor-doc>`_.
Its use is documented below.

Making changes
--------------

We will assume you have identified an issue (eg: #1234) from the `github issue tracker <https://github.com/rockstor/rockstor-doc/issues>`_ to work on.
If you want to document something for which there is no issue, feel free to create one.

First, start with the latest documentation by rebasing your local repo's master branch with the upstream.

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> git checkout master
    you@laptop:~/dev/rockstor-doc> git pull --rebase upstream master

Checkout a new/separate branch for your issue. For example:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> git checkout -b issue#1234_brief_label

You can then start making changes in this branch.


Guidelines
^^^^^^^^^^

To keep in line with Rockstor's goal to make its features as accessible as possible, 
this documentation should strive to keep non-technical users as its primary target.

To remain consistent, for Headings, use sentence case (only the first word and proper nouns are capitalized).

As such, the use of external references and links to additional documentation to provide the reader with further technical information is encouraged.
For content additions/changes please stick to one sentence per line as this helps with translations and reviews of changes.
Really long sentences may be broken at punctuation points, as well as dependent (subordinate) clauses.
See `Semantic Linefeeds <https://rhodesmill.org/brandon/2012/one-sentence-per-line/>`_ which cites Brian W. Kernighan with some simple rules:

.. note::

        Most documents go through several versions (always more than you expected) before they are finally finished.

        Accordingly, you should do whatever possible to make the job of changing them easy.

        First, when you do the purely mechanical operations of typing, type so subsequent editing will be easy.

        Start each sentence on a new line.
        
        Make lines short, and break lines at natural places, such as after commas and semicolons, rather than randomly.
        
        Since most people change documents by rewriting phrases and adding, deleting and rearranging sentences, 
        these precautions simplify any editing you have to do later.
        
        — Brian W. Kernighan, 1974


Building HTML files with Sphinx
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As you edit the content in *.rst* files, you can periodically generate HTML files and review them in your browser.
To generate or update the HTML files, use the following command:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> make html

If you use our :ref:`docker image<dockersphinx>`, you can use the following
command:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> docker run --rm -v $PWD:/docs ghcr.io/rockstor/rockstor-doc:master make html

HTML files are generated in the :code:`_build/html` directory.
From a separate terminal window, you can have a simple Python webserver always serving up this content with the following command:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> pushd ./_build/html; python3 -m http.server 8000; popd

You can now go to :code:`http://localhost:8000` in your browser to review your changes.
The webserver is to be started only once and it will continue to serve the files and changes you make to them.

After making any changes to a *.rst* file, run :code:`make html` as shown above and refresh your browser to display your changes.

In order to check hyperlinks that are part of the changed files,
it is also recommended to run the `linkcheck <https://www.sphinx-doc.org/en/master/usage/builders/index.html>`_ tool that comes with Sphinx. 
During PR submission that link check is also run automatically.
If you don't make changes to any existing links or don't add new ones, it is not as important.
As above, with Sphinx installed you can run it directly in the documentation directory:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> make linkcheck

If you use our :ref:`docker image<dockersphinx>`, you can use the following
command:

.. code-block:: console

    you@laptop:~/dev/rockstor-doc> docker run --rm -v $PWD:/docs ghcr.io/rockstor/rockstor-doc:master make linkcheck

If linkcheck errors occur in documents you have not modified and they are not in scope of your changes, 
you can probably ignore them and/or open another issue on github to address required changes (so this knowledge is not lost over time).


Submit your changes
-------------------

Once you are satisfied with your changes, you can start preparing them for submission.


Add and commit your changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^

First, let's add your changes:

.. code-block:: console

        you@laptop:~/dev/rockstor-doc> git add new_file_added.rst existing_file.rst


Then, you can commit them. We strongly encourage you to commit changes in a certain way to help other contributors, 
and to keep the merge process smooth.
The guidelines below pertain more to code contributions but feel free to be as perfect as you like.
As a guiding principle, separate your changes into one or more logically independent commits.

.. code-block:: console

        you@laptop:~/dev/rockstor-doc> git commit new_file_added.rst existing_file.rst

We request that you divide a commit message into three parts.
Start the message with a single line summary, about 50-70 characters in length.
Add a blank line after that.
If you want to add more than a summary to your commit message, 
describe the change in more detail in plain text format where each line is no more than 80 characters.
This description should be in present tense. Below is a fictional example:

.. code-block:: console

        foobar functionality documentation for rockstor

        This document describes foobar functionality. This feature is based on algorithm called
        recursive transaction launcher to generate transactional foobars.

        # Please enter the commit message for your changes. Lines starting
        # with '#' will be ignored, and an empty message aborts the commit.
        # On branch issue#1234_test
        # Changes to be committed:
        #   (use "git reset HEAD <file>..." to unstage)
        #
        #       new file:   foobar.py
        #

If you would like credit for your patch or if you are a frequent contributor, you should add your name to the `rockstor-doc AUTHORS <https://github.com/rockstor/rockstor-doc/blob/master/AUTHORS>`_ file.


Moving pages
^^^^^^^^^^^^

If your changes involve a page relocation or removal, we need to ensure any eventual external link to it remains valid and provide a valid redirection.
To do so, we leverage the excellent Sphinx extension `sphinxext-rediraffe <https://github.com/wpilibsuite/sphinxext-rediraffe>`_.
Indeed, Rediraffe can simplify the process by comparing your current Git branch to your *master* branch and automatically write redirections for pages that were renamed or relocated.
To do so, you simply need to run the :code:`rediraffewritediff` builder:

.. code-block:: console

        you@laptop:~/dev/rockstor-doc> sphinx-build -b rediraffewritediff . _build/rediraffe

If you use the Docker image, you must use the following command:

.. code-block:: console

        you@laptop:~/dev/rockstor-doc> docker run --rm -v $PWD:/docs ghcr.io/rockstor/rockstor-doc:master sphinx-build -b rediraffewritediff . _build/rediraffe

You should now see the needed redirects in :code:`redirects.txt`.

.. note::
        Make sure to commit your changes with Git **before** running the :code:`rediraffewritediff` builder as the latter will otherwise not         be able to detect your changes.

While we strive to limit such occasions, special circumstances might require the deletion of one or more pages.
As **sphinxext-rediraffe** cannot yet automatically write a redirection for a deleted page, one needs to manually instruct it.
Fortunately, this is as simple as writing a new line in :code:`redirects.txt`, listing the name of the deleted page and the name of the page to which it should redirect.
Below is an excerpt of :code:`redirects.txt` detailing redirections for deleted files:

.. code-block:: text

        # Deleted files
        # "deleted_file.rst" "redirection_target.rst"
        "intro.rst" "index.rst"
        "analytics.rst" "index.rst"
        "benchmarks.rst" "index.rst"

In the example above, the now deleted files :code:`intro.rst`, :code:`analytics.rst`, and :code:`benchmarks.rst`, are all redirected to :code:`index.rst`.


Pushing changes
^^^^^^^^^^^^^^^

As you continue to work on an issue, commit and push your changes to the issue branch of your fork.
You can periodically push your commits to Github with the following command:

.. code-block:: console

        you@laptop:~/dev/rockstor-doc> git push origin your_branch_name



Create a pull request
^^^^^^^^^^^^^^^^^^^^^

Once you're finished with your work for the issue and are ready to submit, create a pull request by clicking on the **pull request** button on Github.
This notifies the maintainers of your changes.
As a best practice, only open one pull request per issue containing all the relevant changes.

To expedite the review, please follow these two tips:

* Make sure that the Sphinx :code:`make html` command completes successfully without generating any error.
  You can also verify that all tests ran by the Github Actions complete without error or warning.
  In the event one of these tests fails, you can click on the *Details* button to inspect the Github Action's logs and identify the problem.

* When you make a pull request, adding a "Fixes #number-of-issue" on its own line will automatically close the related issue when it gets merged.
  Just a nice thing to have and also provides a link to the relevant issue.
  See `GitHub documentation <https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue>`_ for details.
