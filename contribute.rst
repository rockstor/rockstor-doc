
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
take place. If you need help, share an idea, suggest a new feature etc.. Forum
is a great place to start. Being active there could be very helpful to the
project and our community.

Contributions such as testing and reporting bugs is tremendously helpful and
greatly appreciated.

You can also contribute to the documentation of the project. For details go to
the `rockstor-doc repository on Github
<https://github.com/rockstor/rockstor-doc>`_

.. _developers:

Developers
----------

Developing RockStor to deliver on its unique value proposition of being a
Smart, Powerful, and Open storage platform is a major effort. If you are
passionate about Open Source and Storage like us, you are in the right
company. We welcome you to join our community. Please begin by joining our
`community discussion forum <http://forum.rockstor.com>`_.

Our development process is simple and straight forward. There is currently one
main reposistory called `rockstor-core on Github
<https://github.com/rockstor/rockstor-core>`_. Begin by `forking it
<https://github.com/rockstor/rockstor-core#fork-destination-box>`_.

We use the wonderful tool `Git <http://git-scm.com/>`_ for source code
management and `Rockstor on Github <https://github.com/rockstor>`_ for issue
tracking. We'll assume you have basic proficiency with Git and are familiar
with working with it from the text editor or IDE of your choice. Emacs, Vim,
Eclipse and PyCharm are some recommendations. We'll further assume that you
have your laptop ready with git and an editor.

After you've forked the rockstor-core repo, clone the fork onto your
laptop. The high level flow of a new contribution is as follows.

1. Search for an existing issue or start a new issue using the `Issue
Tracker <https://github.com/organizations/rockstor/dashboard/issues>`_

2. Make code changes.

3. Submit your changes as a `pull request
<https://help.github.com/articles/using-pull-requests>`_.

4. Use the issue tracker for discussions as
necessary.

5. Close the issue when your pull request is
merged.

Let's walk through this process in detail.

Local git repo setup
--------------------

Since we rely on github services, you need to create a profile on `github.com
<https://github.com/>`_.

Go to `rockstor-core repo <https://github.com/rockstor/rockstor-core>`_ and
click on the "Fork" button. This will fork the repository into your profile
which serves as your private git remote called origin. Next few git steps are
demonstrated on a Linux terminal. They work the same on a Mac too. Your IDE
may have ways to completely avoid the terminal for these steps.

Clone your rockstor-core fork onto your local development environment
::

        git clone https://github.com/your_github_username/rockstor-core.git

Now change into the directory the above command should have created::

        cd rockstor-core

Configure this new git repo with your name and email address. This is helpful in
keeping an accurate record of collaboration::

        git config user.name "Firstname Lastname"
        git config user.email your_email_address

Add a remote called upstream to periodically rebase your local repository with
changes in the upstream made by other contributors.

        git remote add upstream https://github.com/rockstor/rockstor-core.git


Making changes
--------------

We'll assume you have identified an issue(#1234) from the `issue tracker
<https://github.com/rockstor/rockstor-core/issues>`_ to work on. First, start
with the latest code by rebasing your local repo with upstream::

        git pull --rebase upstream master

To start making changes, create a separate branch for your issue. For example::

        git checkout -b issue#1234_brief_label

You can then start making changes in that branch.

We strongly encourage you to commit changes a certain way to help other
developers and keep the merge process smooth. As a guiding principle, separate
your changes into one or more logically independent commits.

We request that you divide a commit message into three parts. Start the message
with a single line summary, about 70 characters in length. Add a blank line
after that. Finally, describe the change in more detail in plain text format
where each line is no more than 80 characters. This description should be in
present tense. Below is a fictional example::

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

If you'd like credit for your patch or you are a frequent contributor, add your
name to the AUTHORS file.

Build VM
--------

You need a Virtual Machine(VM) to test and develop your changes. An easy solution
is to create a RockStor VM using either Oracle's `VirtualBox
<https://www.virtualbox.org/>`_ or if you are using a Linux desktop then
`Virtual Machine Manager <https://virt-manager.org>`_ is also an option. You
can find a `VirtualBox Rockstor install demo
<https://www.youtube.com/watch?v=00k_RwwC5Ms>`_ on our `YouTube channel
<https://www.youtube.com/channel/UCOr8Q4DA7gYDpeSv09BVCRQ>`_ and a
:ref:`kvmsetup` in our documentation.

In the following sections, we use some terms in the commands. Here's a short
explanation of these terms

1. rockstor-core : This is the directory containing your local rockstor-core
   repo on your laptop. In my case, it's ~/Learnix/rockstor-core

2. your_rockstor_vm : IP address of your build VM. In my case, I use Virtualbox
   with host-only adapter and get an ip in 192.168.56.101-254 range.

3. deploy_dir: The directory on your build VM where the code is transfered
   to. In my case, it's /opt/deploy


Build VM initial setup
----------------------

After making changes to code, transfer the code from your laptop to the build
VM ::

        [you@your_laptop ]# rsync -avz --exclude=.git /path/to/your/rockstor-core/ root@your_rockstor_vm:deploy_dir/

If you are deploying for the first time or like a clean deployment, execute the
following command in your deploy directory::

        [root@your_rockstor_vm deploy_dir]# python bootstrap.py

The next step is to build Rockstor with your new changes. This takes a long
time for a clean deployment, but subsequent deployments execute very quickly::

        [root@your_rockstor_vm deploy_dir]# ./bin/buildout -N

Once the deployment step above succeeds, start rockstor services that are
managed by supervisord. First start the supervisord process with::

        [root@your_rockstor_vm deploy_dir]# ./bin/supervisord -c etc/supervisord.conf

Now start all required services with this command
::

        [root@your_rockstor_vm deploy_dir]# ./bin/supervisorctl start all

You should now be able to login to the WebUI and verify your changes.

Change -> Test cycle
--------------------

Changes fall into two categories. (1) Backend changes involving python coding
and (2) Frontend changes involving javascript, html and css.

To test any change, you need to transfer files from your laptop to the VM
::
        [you@your_laptop ]# rsync -avz --exclude=.git /path/to/your/rockstor-core/ root@your_rockstor_vm:deploy_dir/

If you made any javascript, html or css changes, you need to collect static
files with this command::

        [root@your_rockstor_vm deploy_dir]# ./bin/buildout install collectstatic

Then, refresh the browser to test new changes in the WebUI. It's best to have
aliases setup for above commands and have it all integrated into your
editor(Emacs anyone?). At the very least, you should have multiple terminal
tabs open, one for transferring files, one for running commands on the vm and
another for browsing through the logs

When making backend changes, you may want to see debug logs and
errors. Everything that you or any rockstor service logs go into this directory
on your VM::

        [root@your_rockstor_vm ]# ls -l /path/to/your/deploy_dir/var/log
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

When making frontend changes, Developer tools in Chrome/Firefox are your
friend. You could `inspect elements
<https://developer.chrome.com/devtools/docs/dom-and-styles#inspecting-elements>`_
for html/css changes, log to the browser console from javascript code with
console.log() and also use the debugger and step through javascript from your
browser.

Database migrations
-------------------

If you made any changes to Django models, you'll need to create migrations. We
use `South <http://south.aeracode.org/>`_ to manage database migrations. Due to
the fact that running south to generate migrations requires all dependencies
installed, it is easier to generate the migration in the deployment directory
instead of the development directory, and copy the changes back to the
development directory.

Follow these steps to make a change to the storageadmin models and generate the
corresponding migration after you have added or updated a model. (The procedure is similar for changes to the smart_manager models)

For model changes in storageadmin, from your deploy_dir, run
::

        [root@your_rockstor_vm deploy_dir]# ./bin/django schemamigration storageadmin --auto

This will generate the required migration file in the
src/rockstor/storageadmin/migrations directory. Run the migration with::

        [root@your_rockstor_vm deploy_dir]# ./bin/django migrate storageadmin --database=default

If your migration is successful, copy the changed model file and the generated
migration file back to your development environment

For model changes in the smart_manager application, run
::

        [root@your_rockstor_vm deploy_dir]# ./bin/django schemamigration smart_manager --auto

Run the migration with
::

        [root@your_rockstor_vm deploy_dir]# ./bin/django migrate smart_manager --database=smart_manager

Shipping changes
----------------

As you continue to work on an issue, commit and push changes to the issue
branch of your fork. You can periodically push your changes to github with the
following command::

        git push origin your_branch_name

When you finish work for the issue and are ready to submit, create a pull
request by clicking on the "pull request" button on github. This notifies the
maintainers of your changes. As a best practice, only open one pull request per
issue containing all relevant changes.
