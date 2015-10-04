.. _contributedocs:

Contributing to Rockstor documentation
--------------------------------------

Steps for contributing to **rockstor-doc** repo are similar to contributing to
**rockstor-core**, as we follow the same fork and pull request model. We’ll
assume you have basic proficiency with Git and are familiar with using a
texteditor or IDE of your choice. Emacs, Vim, Eclipse and PyCharm are some
recommendations. We’ll further assume that you have your laptop ready with git
and an editor installed. Since we rely on github services, you need to create a
profile on github.com.

Once you have your profile set-up on github.com, follow these steps

Go to `rockstor-doc repo <https://github.com/rockstor/rockstor-doc>`_ and click
on the **Fork** button. This will fork the repository into your profile which
serves as your private git remote called origin. The next few git steps are
demonstrated on a Linux terminal. They work the same on a Mac too. Your IDE may
have ways to completely avoid the terminal, but using the terminal makes you
look cool. ::

	[you@your_laptop ~/projects]# git clone git@github.com:your_github_username/rockstor-doc.git

The above command creates a local **rockstor-doc** git repo in a new directory
by the same name(rockstor-doc). Change into it. ::

	[you@your_laptop ~/projects]# cd rockstor-doc

Configure this new git repo with your name and email address. This is required
to accurately record collaboration. ::

	[you@your_laptop rockstor-doc]# git config user.name "Firstname Lastname"
	[you@your_laptop rockstor-doc]# git config user.email your_email_address

Add a remote called upstream to periodically rebase your local repository with
changes in the upstream made by other contributors. ::

	[you@your_laptop rockstor-doc]#git remote add upstream https://github.com/rockstor/rockstor-doc.git


Making changes
--------------

We'll assume you have identified an issue(eg: #1234) from the `github issue
tracker <https://github.com/rockstor/rockstor-doc/issues>`_ to work on. If you
want to document something for which there is no issue, feel free to create
one.

First, start with the latest documentation by rebasing your local repo's master
branch with the upstream ::

        [you@your_laptop rockstor-doc]# git checkout master
        [you@your_laptop rockstor-doc]# git pull --rebase upstream master

Checkout a new/separate branch for your issue. For example::

        [you@your_laptop rockstor-doc]# git checkout -b issue#1234_brief_label

You can then start making changes in this branch. Once done you can add your
changes ::

	[you@your_laptop rockstor-doc]# git add new_file_added.rst existing_file.rst


We strongly encourage you to commit changes a certain way to help other
contributors and keep the merge process smooth. Below guidelines are more
pertinent to code contributions, but feel free to be as perfect as you like. As
a guiding principle, separate your changes into one or more logically
independent commits. ::

	[you@your_laptop rockstor-doc]# git commit new_file_added.rst existing_file.rst

We request that you divide a commit message into three parts. Start the message
with a single line summary, about 50-70 characters in length. Add a blank line
after that. If you want to add more than a summary to your commit message,
describe the change in more detail in plain text format where each line is no
more than 80 characters. This description should be in present tense. Below is
a fictional example::

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

If you'd like credit for your patch or if you are a frequent contributor, you
should add your name to the AUTHORS file.


Unlike for code contributions, there is no need for a build VM. We use `Sphinx
<http://sphinx-doc.org/contents.html>`_ to generate the html content from .rst
files we edit. Installation procedure varies if you are on Mac or Linux, so
follow the appropriate installation guide for Sphinx.


Installing Sphinx
^^^^^^^^^^^^^^^^^

Sphinx official documentation gives guidelines for installating Sphinx on various platforms. Follow
the documentation `here <http://sphinx-doc.org/latest/install.html>`_.

If you want to create a video to explain Rockstor feature or functionality, you need to
install an extra Sphinx package. If you prefer uploading your videos to Rockstor Youtube channel,
please, send an email to support@rockstor.com ::

	[you@your_laptop /path/to/rockstor-doc]# sudo pip install sphinxcontrib.youtube

Generating html files with Sphinx
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As you edit the content in .rst files, you can periodically generate html files
and review them in your browser. To generate or update the HTML files, use the
following command ::

        [you@your_laptop /path/to/rockstor-doc]# make html

HTML files are generated in _build/html directory. From a separate terminal
window, you can have a simple Python webserver always serving up this content
with the following command ::

        [you@your_laptop /path/to/rockstor-doc/_build/html]# python -m SimpleHTTPServer 8000

You can now go to http://localhost:8000 in your browser to review your
changes. The webserver is to be started only once and it will continue to serve
the files and changes you make to them.

After making any changes to a .rst file, run *make html* as shown above and
refresh your browser.

Once you are satisfied with changes and committed them to your branch following
the steps outlined here, you can open a pull request.

As you continue to work on an issue, commit and push changes to the issue
branch of your fork.  You can periodically push your changes to github with the
following command::

	[you@your_laptop ]# cd /path/to/rockstor-doc
	[you@your_laptop rockstor-doc] git push origin your_branch_name

When you finish work for the issue and are ready to submit, create a pull
request by clicking on the “pull request” button on github. This notifies the
maintainers of your changes. As a best practice only open one pull request per
issue containing all relevant changes.
