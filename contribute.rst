
.. _contributetorockstor:

Contribute to Rockstor
======================

Rockstor is free and open source software and we are proud of our budding
developer and user community. Anyone can contribute in a number of different ways.

.. _storageexperts:

Non developers
---------------

There is a lot you can do other than coding that is essential to the
project. First, please join our `community discussion forum
<http://forum.rockstor.com>`_. It's the central location where all discussions
take place. If you need help, want to share an idea, suggest a new feature etc..
the forum is a great place to start. Being active there could be very helpful to
the project and our community.

Contributions such as testing and reporting bugs are tremendously helpful and
greatly appreciated.

You can also contribute to the documentation of the project. For details go to
the `rockstor-doc repository on Github
<https://github.com/rockstor/rockstor-doc>`_.

.. _developers:

Developers
----------

Developing Rockstor to deliver on its unique value proposition of being a
Smart, Powerful, and Open storage platform is a major effort. If you are
passionate about Open Source and Storage like us, you are in the right
company. We welcome you to join our community. Please begin by joining our
`community discussion forum <http://forum.rockstor.com>`_.

Our development process is simple and straight forward. There is currently one
main repository called `rockstor-core on Github
<https://github.com/rockstor/rockstor-core>`_. Begin by `forking it
<https://github.com/rockstor/rockstor-core#fork-destination-box>`_.

We use the wonderful `Git <http://git-scm.com/>`_ for source code
management and `Rockstor on Github <https://github.com/rockstor>`_ for issue
tracking. We'll assume you have basic proficiency with Git and are familiar
with it using a text editor or IDE of your choice. Emacs, Vim,
Eclipse and PyCharm are some recommendations. We'll further assume that you
have your laptop ready with git and an editor installed.

After you've forked the rockstor-core repo, clone the fork onto your
laptop. The high level flow of a new contribution is as follows.

1. Search for an existing issue or start a new issue using the `Issue
Tracker <https://github.com/organizations/rockstor/dashboard/issues>`_.

2. Make code changes
.

3. Submit your changes in a single `pull request
<https://help.github.com/articles/using-pull-requests>`_.

4. Use the issue tracker for discussions as necessary
.

5. Close the issue when your pull request is merged
.

Let's walk through this process in detail.

Local git repo setup
--------------------

Since we rely on github services, you need to create a profile on `github.com
<https://github.com/>`_.

Go to `rockstor-core repo <https://github.com/rockstor/rockstor-core>`_ and
click on the "Fork" button. This will fork the repository into your profile
which serves as your private git remote called origin. The next few git steps are
demonstrated on a Linux terminal. They work the same on a Mac too. Your IDE may
have ways to completely avoid the terminal, but using the terminal makes you
`look cool <https://www.youtube.com/watch?v=51lGCTgqE_w>`_.

Your development machine can be a Linux system or a Mac. In my case, it's a
Lenovo laptop running Ubuntu. There are other contributors using Mac, so this
process works the same in both cases.

Clone your fork of rockstor-core repo onto your local development
environment. You can do this in any directory, but chances are you have a
project directory appropriate for this. Let's assume you have a projects
directory in your home(~/projects) for the repo. ::

        [you@your_laptop ~/projects]# git clone git@github.com:your_github_username/rockstor-core.git

The above command creates a local rockstor-core git repo in a new directory by
the same name(rockstor-core). Change into it::

        [you@your_laptop ~/projects]# cd rockstor-core

Configure this new git repo with your name and email address. This is required
to accurately record collaboration::

        [you@your_laptop rockstor-core]# git config user.name "Firstname Lastname"
        [you@your_laptop rockstor-core]# git config user.email your_email_address

Add a remote called upstream to periodically rebase your local repository with
changes in the upstream made by other contributors::

        [you@your_laptop rockstor-core]# git remote add upstream https://github.com/rockstor/rockstor-core.git


Making changes
--------------

We'll assume you have identified an issue(eg: #1234) from the `github issue tracker
<https://github.com/rockstor/rockstor-core/issues>`_ to work on. First, start
with the latest code by rebasing your local repo with upstream::

        [you@your_laptop rockstor-core]# git pull --rebase upstream master

Checkout a new/separate branch for your issue. For example::

        [you@your_laptop rockstor-core]# git checkout -b issue#1234_brief_label

You can then start making changes in this branch.

We strongly encourage you to commit changes a certain way to help other
developers and keep the merge process smooth. As a guiding principle, separate
your changes into one or more logically independent commits.

We request that you divide a commit message into three parts. Start the message
with a single line summary, about 70 characters in length. Add a blank line
after that. If you want to add more than a summary to your commit message,
describe the change in more detail in plain text format where each line is no
more than 80 characters. This description should be in present tense. Below is
a fictional example::

        foobar functionality for rockstor

        Add a new file to implement the algorithm called recursive transaction
        launcher to generate transactional foobars recursively during runtime
        based on dependency tree of foos and bars.

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

Build VM
--------

You need a Virtual Machine (VM) to build and test your changes. An easy
solution is to create a RockStor VM using either Oracle's `VirtualBox
<https://www.virtualbox.org/>`_ or if you are using a Linux desktop then
`Virtual Machine Manager <https://virt-manager.org>`_ is also an option. You
can find a `VirtualBox Rockstor install demo
<https://www.youtube.com/watch?v=00k_RwwC5Ms>`_ on our `YouTube channel
<https://www.youtube.com/channel/UCOr8Q4DA7gYDpeSv09BVCRQ>`_ and a
:ref:`kvmsetup` in our documentation. It need not be a VM, but using a physical
machine just for this purpose could be an overkill.

Note that when you first create the build VM, rockstor rpm package will already
be installed. The package files are located in /opt/rockstor. Further more, the
rockstor service should be running. We don't want that as it interferes with
our development activity. Further down in this document, there is a buildout
step. When that is run the first time, the rpm package and it's effects are
removed.

Helpful terms
-------------

In the following sections we use some terms in the commands; this is a short
explanation of these terms:-

1. **laptop**: This is your laptop or desktop computer.

2. **rockstor-core**: This is a directory on your laptop containing your local
   rockstor-core repo. In my case, it's ~/Learnix/rockstor-core

2. **build_vm**: IP address of your build VM. In my case, I use Virtualbox
   with host-only adapter and get an ip in 192.168.56.101-254 range.

3. **build_dir**: The directory on the build VM where you like to copy the code to
   and build. In my case, I picked /opt/build/.

Build VM initial setup
----------------------

Transfer the code from your laptop to the build VM ::

        [you@laptop ]# rsync -avz --exclude=.git /path/to/rockstor-core/ root@build_vm:/path/to/build_dir/

If you are building for the first time or like a clean build, execute the
following command in your deploy directory on the VM ::

        [root@build_vm ]# python /path/to/build_dir/bootstrap.py -c /path/to/build_dir/buildout.cfg

The next step is to build Rockstor with your new changes. This takes a long
time for a clean build, but subsequent builds finish quickly ::

        [root@build_vm ]# /path/to/build_dir/bin/buildout -N -c /path/to/build_dir/buildout.cfg

Once the buildout step above succeeds we can start the rockstor services; these are
managed by supervisord, so start the supervisord process with ::

        [root@build_vm ]# /path/to/build_dir/bin/supervisord -c /path/to/build_dir/etc/supervisord.conf

Now start all the required services with this command
::

        [root@build_vm ]# /path/to/build_dir/bin/supervisorctl start all

You should now be able to login to the WebUI and verify your changes.

Change -> Test cycle
--------------------

Changes fall into two categories. (1) Backend changes involving python coding
and (2) Frontend changes involving javascript, html and css.

To test any change, you need to transfer files from your laptop to the VM::

        [you@laptop ]# rsync -avz --exclude=.git /path/to/rockstor-core/ root@build_vm:/path/to/build_dir/

If you made any javascript, html or css changes, you need to collect static
files with this command::

        [root@build_vm ]# /path/to/build_dir/bin/buildout -c /path/to/build_dir/buildout.cfg install collectstatic

Then, refresh the browser to test new changes in the WebUI. It's best to have
aliases setup for above commands and have it all integrated into your
editor(Emacs anyone?). At the very least you should have multiple terminal
tabs open; one for transferring files, one for running commands on the VM, and
another for browsing through the logs.

When making backend changes, you may want to see debug logs and
errors. Everything that you or any rockstor service logs goes into the following
directory on your VM::

    [root@build_vm ]# ls -l /path/to/build_dir/var/log
    total 280
    -rw-r--r-- 1 root root 106912 Jun 23 19:49 gunicorn.log
    -rw-r--r-- 1 root root 119533 Jun 23 19:49 rockstor.log
    -rw-r--r-- 1 root root     25 Jun 23 19:19 supervisord_data-collector_stderr.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_data-collector_stdout.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_gunicorn_stderr.log
    -rw-r--r-- 1 root root      8 Jun 23 16:27 supervisord_gunicorn_stdout.log
    -rw-r--r-- 1 root root  27980 Jun 23 19:49 supervisord.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_nginx_stderr.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_nginx_stdout.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_replication_stderr.log
    -rw-r--r-- 1 root root      8 Jun 23 15:33 supervisord_replication_stdout.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_smart_manager_stderr.log
    -rw-r--r-- 1 root root      8 Jun 23 15:33 supervisord_smart_manager_stdout.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_task-scheduler_stderr.log
    -rw-r--r-- 1 root root      8 Jun 23 15:33 supervisord_task-scheduler_stdout.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_ztask-daemon_stderr.log
    -rw-r--r-- 1 root root      0 Jun 23 15:33 supervisord_ztask-daemon_stdout.log
    -rw-r--r-- 1 root root    996 Jun 23 19:49 ztask.log

rockstor.log should be the first place to look for errors or debug logs.

When making frontend changes, Developer Tools in Chrome/Firefox are your
friends. You can `inspect elements
<https://developer.chrome.com/devtools/docs/dom-and-styles#inspecting-elements>`_
for html/css changes, log to the browser console from javascript code with
console.log(), and use the debugger and step through javascript from your
browser.

Adding third party Javascript libraries
---------------------------------------

The frontend code uses third party javascript libraries such as jquery,
bootstrap, d3 and many others. These are not part of the rockstor-core
repository but are dynamically generated during the buildout step. They are
placed in the below directory on your build VM::

    [root@build_vm ]# ls /path/to/build_dir/static/js/lib
    backbone-0.9.2.js            cocktail.js   humanize.js                jquery.flot.stack.js         jquery.sparkline.min.js    json2.js              socket.io.min.js
    backbone.routefilter.min.js  cron          jquery-1.9.1.min.js        jquery.flot.stackpercent.js  jquery.tablesorter.js      jsonform.js           underscore-1.3.2.js
    bootstrap-datepicker.js      cubism.v1.js  jquery.flot.axislabels.js  jquery.flot.time.js          jquery.tools.min.js        later.min.js
    bootstrap.js                 d3-tip.js     jquery.flot.js             jquery.flot.tooltip_0.5.js   jquery.touch-punch.min.js  moment.min.js
    bootstrap-timepicker.js      d3.v3.min.js  jquery.flot.navigate.js    jquery-migrate-1.2.1.min.js  jquery-ui.min.js           prettycron.js
    chosen.jquery.js             gentleSelect  jquery.flot.resize.js      jquery.shapeshift.js         jquery.validate.js         simple-slider.min.js

If you need to add a new library, place all of it's files in the lib
directory(on the build VM, obviously) and continue your development
process. After you open the pull request for rockstor-core repo, it's time to
open a separate pull request for merging these libaries into upstream. This
separate pull request must be opened for another repository named
`rockstor-jslibs <https://github.com/rockstor/rockstor-jslibs>`_, which
mirrors the contents of the lib directory shown above. The fork and
pull-request process is same as it is for this(rockstor-core repo) one.


Database migrations
-------------------

We use `PostgreSQL <http://www.postgresql.org/>`_ as the database backend for
Rockstor. There are two databases, (1) storageadmin and (2)
smart_manager. Depending on your issue you may need to add a Django model,
delete one, or change fields of an existing model. After editing models you
need to create a migration and apply it.

We use `South <http://south.aeracode.org/>`_ to manage database migrations. Due
to the fact that running south to generate migrations requires all dependencies
installed, it is easier to generate the migration on your VM and copy the
migration file back to your laptop and add it in git once you are satisfied.

For model changes in storageadmin application, create a migration file using
::

        [root@build_vm ]# /path/to/build_dir/bin/django schemamigration storageadmin --auto

The above command generates a migration file in
/path/to/build_dir/src/rockstor/storageadmin/migrations/ Apply the migration with::

        [root@build_vm ]# /path/to/build_dir/bin/django migrate storageadmin --database=default

For model changes in the smart_manager application, create a migration file using
::

        [root@build_vm ]# /path/to/build_dir/bin/django schemamigration smart_manager --auto

Run the migration with
::

        [root@build_vm ]# /path/to/build_dir/bin/django migrate smart_manager --database=smart_manager


Shipping changes
----------------

As you continue to work on an issue, commit and push changes to the issue
branch of your fork. You can periodically push your changes to github with the
following command::

        [you@laptop ]# cd /path/to/rockstor-core; git push origin your_branch_name

When you finish work for the issue and are ready to submit, create a pull
request by clicking on the "pull request" button on github. This notifies the
maintainers of your changes. As a best practice only open one pull request per
issue containing all relevant changes.
