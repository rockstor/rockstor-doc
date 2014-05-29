
.. _contributetorockstor:

Contribute to Rockstor
======================

Rockstor is a free and open source software and we are proud of our budding
developer and user community. You can contribute in a few different ways.

.. _storageexperts:

Storage experts
---------------

Domain experts have been involved in RockStor development right from the
beginning. While RockStor started with visionary ideas of Smart capabilities
and Open paradigm, the core team has expertise in the Storage industry.

RockStor is a community effort and we believe that domain experts are essential
in making RockStor a successful platform. If you are a Storage administrator,
Systems engineer, Linux administrator, Filesystems expert, technical manager or
simply a geek! with deep interest in the Storage infrastructure space, we
welcome you to join our community.

You can contribute to Rockstor by

1. Participating in feature request and specification process via `RockStor
issue tracker <https://github.com/organizations/rockstor/dashboard/issues>`_.

2. Join and participate in our `mailing list
<http://sourceforge.net/mailarchive/forum.php?forum_name=rockstor-devel>`_.

3. Test stable and release candidates of
RockStor.

4. Report bugs to help other community members via `RockStor issue tracker
<https://github.com/organizations/rockstor/dashboard/issues>`_.

.. _developers:

Software Engineers
------------------

Developing RockStor to deliver on its unique value proposition of Smart,
Powerful and Open storage platform is a major effort. If you are passionate
about Open source and Storage like us, you are in the right company. We welcome
you to join our community.

Our development process is very simple and straight forward. `Github
<https://github.com>`_ is our
primary framework for all collaboration including issue tracking, design and
development collaboration. Before you make any contribution subject to
copyright, we ask you to fillout an online Contributor License
Agreement(CLA). We tried to keep the agreement as simple as possible. Please
click `here <http://rockstor.com/cla.html>`_ to submit the form.

We use the wonderful tool `Git <http://git-scm.com/>`_ for source code
management and `Github <https://github.com/organizations/rockstor>`_ for issue
tracking, hosting and collaboration in general. You can use the "git" command
line tool on Linux or alternatively use `Eclipse <http://www.eclipse.org/>`_
with `Egit <http://wiki.eclipse.org/EGit/User_Guide>`_ plugin. The development
process is as follows:

1. Search for an existing issue or start a new issue using the `Rockstor Issue
Tracker <https://github.com/organizations/rockstor/dashboard/issues>`_

2. You can also just start a conversation on our mailing list before creating a
new issue.

3. Submit your changes as a `pull request
<https://help.github.com/articles/using-pull-requests>`_.

4. Use the issue tracker for discussions as
necessary.

5. Close the issue when your pull request is
merged.

Get started
-----------

Since we rely on github services, you need to create a profile on `Github
<https://github.com/>`_.

The main RockStor repository is called rockstor-core. Go to its `main page
<https://github.com/rockstor/rockstor-core>`_ and click on the "Fork"
button. This will fork the rockstor-core repository into your profile which
serves as your own parallel git universe. The process is the same for any other
repository.

Clone your forked rockstor repository onto your local developmet environment
::

        git clone https://github.com/your_github_username/rockstor-core.git

Configure your git client with your name and email address. This is helpful in
keeping an accurate record of collaboration::

        git config --global user.name "Firstname Lastname"
        git config --global user.email your_email_address

Setup your fork's master branch to sync with the main repository. Here's the
command to set it up for rockstor-core repository::

        git remote add rockstor-core https://github.com/rockstor/rockstor-core.git

Here is the command to subsequently pull updates and sync up your master
branch::

        git pull --rebase rockstor-core master

Making changes
--------------

We request that you commit your changes a certain way to help other developers
and keep the merge process smooth. As a guiding principle, separate your
changes into one or more logically independent commits.

When you start working on an issue, create a separate branch for that issue
with the issue number as part of the name. You can then start working and
commiting changes in that branch. Here is the command to create a new branch::

        git checkout -b issue#1234_brief_label

We request that you divide a commit message into three parts. Start the message
with a single line summary, about 70 characters in length. Add a blank line
after that. Finally, describe the change in more detail in plain text format
where each line is no more than 80 characters. This description should be in
present tense. Below is a fictional example::

        foobar functinality for rockstor

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

Build Environment
-----------------

You need a build environment to test and develop your changes. A simple
solution is to create a RockStor virtual machine using `VirtualBox
<https://www.virtualbox.org/>`_. You can find detailed setup process `here
<http://rockstor.com/vbox_setup.html>`_.

Testing changes
---------------

Test changes in your build environment before committing. To test your changes,
rsync your changes to the build environment::

        rsync -avz --exclude=.git rockstor-core/ root@your_rockstor_vm:deploy_dir/

If you are deploying for the first time or like a clean deployment, execute the
following command in your deploy directory::

        [root@your_rockstor_vm deploy_dir]# python27 bootstrap.py

The next step is to build RockStor with your new changes. This takes a long
time for a clean deployment, but subsequent deployments execute very quickly::

        [root@your_rockstor_vm deploy_dir]# ./bin/buildout -N

Once the deployment succeeds as indicated by the above step, start the rockstor
services which are managed by supervisord. First start the supervisord process
with::

        [root@your_rockstor_vm deploy_dir]# ./bin/supervisord -c etc/supervisord.conf

You will notice that all three rockstor services, namely, nginx, gunicorn and
smart_manager are in STOPPED state::

        [root@your_rockstor_vm deploy_dir]# ./bin/supervisorctl status
        gunicorn                         STOPPED    Not started
        nginx                            STOPPED    Not started
        smart_manager                    STOPPED    Not started

If they are not running, start all three rockstor services
::

        [root@your_rockstor_vm deploy_dir]# ./bin/supervisorctl start nginx gunicorn smart_manager
        nginx: started
        gunicorn: started
        smart_manager: started

You should be able to login via WebUI, CLI or test directly using the API.

Database migrations
-------------------

We use `South <http://south.aeracode.org/>`_ to manage database migrations for RockStor. Due to the fact that running south to generate migrations requires all dependencies installed, it is easier to generate the migration in the deployment directory instead of the development directory, and copy the changes back to the development directory.

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
