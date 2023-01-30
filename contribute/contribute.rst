
.. _contributetorockstor:

Contributing to Rockstor - Overview
===================================

Rockstor is free and open source software and we are proud of our developer and user community.
Anyone can contribute in a number of different ways.

.. _storageexperts:

Non developers
--------------

There is a lot you can do other than coding that is essential to the project.
First, please join our `community discussion forum <https://forum.rockstor.com>`_.
It's the central location where all discussions take place.
If you need help, want to share an idea, suggest a new feature, etc...,
the forum is a great place to start.
Being active on the forum is very helpful to the project and the community as a whole.

Contributions such as testing and reporting bugs are tremendously helpful and greatly appreciated.
Please see our :ref:`update_channels` section and specifically the :ref:`testing_channel`
sub section for information on how to track the latest fixes and features.

You can also contribute to the documentation of the project.
In many cases this is crucial and our documentation often lags behind the code.
For more information see :ref:`contributedocs`

Finally Rockstor's continued development and distribution also depends on
all those choosing to subscribe to the :ref:`stable_channel` updates where all the
:ref:`testing_channel` work end up.

.. _developers:

Developers
----------

Developing Rockstor as an open storage platform is a non trivial endeavour.
If you are passionate about Open Source and Storage like us, you are in the right place.
The `community discussion forum <https://forum.rockstor.com>`_ is the place to start.

Our development process is relatively simple and straight forward.
We use `Git <https://git-scm.com/>`_ for source code management and
`Rockstor on GitHub <https://github.com/rockstor>`_ for issue tracking.
There is currently one main code repository called
`rockstor-core on GitHub <https://github.com/rockstor/rockstor-core>`_.
This repository has 2 main git branches:

- master
    Used to build the Stable channel packages.
- testing
    Main target for development, and used to build our testing channel packages.

.. note::

    Unless your development contribution is both a trivial and critical fix,
    it likely belongs as a modification against the testing channel only.
    If all is well during field testing via our testing channel packages,
    the exact same patch may be cherry-picked for inclusion in the stable release.

Begin by `Creating your own forking <https://github.com/rockstor/rockstor-core/fork>`_ via GitHub's Web-UI.

.. warning::
    You must **untick** *"Copy the master branch only"* if you intend to contribute to the testing channel.

After you've forked the rockstor-core repo, clone your personal GitHub fork onto your laptop/desktop.
The high level flow of an individual contribution is as follows.

1. Search for an existing issue or start a new issue using the `Issue Tracker <https://github.com/rockstor/rockstor-core/issues>`_.
2. Make and test code changes locally on a Rockstor install with the rpm package removed.
3. Submit your changes in a single `pull request <https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests>`_.
4. Use the issue tracker for discussions as necessary.
5. Close the issue when your pull request is merged.

Let's walk through this process in detail.

.. _assumptions:

Assumptions
~~~~~~~~~~~

In the following sections we assume:

1. You have a basic working knowledge of the linux command line, git, and GitHub.
2. **laptop** = your local laptop or desktop with git, ssh client, and an editor/IDE installed.
3. **~/dev/rockstor-core** = your (laptop/desktop) local git clone & dev branch directory.
4. **buildvm** = your target build machine's hostname; the name chosen during the rockstor install.

TIP: you can add your buildvm's IP address to :code:`/etc/hosts` on your laptop (linux assumed).
E.g.:

.. code-block:: console

    you@laptop:~> grep "buildvm" /etc/hosts
    192.168.2.170   buildvm

Then, a :code:`ping -c2  buildvm` on your laptop should complete without error and
:code:`ssh root@buildvm` should provide a root user shell on the target buildvm machine
(assuming they are both on the same network).

.. _localrepo:

Local git repo setup
--------------------

Since we rely on GitHub services, you need to create a profile on `github.com <https://github.com/>`_.

Go to `rockstor-core repo <https://github.com/rockstor/rockstor-core>`_ and click on the "Fork" button.

.. warning::
    You must **untick** *"Copy the master branch only"* if you intend to contribute to the testing channel.

You should then have a fork of this repository in your own GitHub profile.
This repo then serves as your private git remote called *origin*.
The next few git steps are demonstrated on a Linux terminal;
they should, however, also work with little or no modification in an OSX console.

Clone, in turn, your GitHub profile's fork of rockstor-core onto your local machine.
You can do this in any directory but the following assumes the :code:`~/dev` directory.

.. code-block:: console

        you@laptop:~> mkdir ~/dev; cd ~/dev
        you@laptop:~/dev> git clone https://github.com/your_github_username/rockstor-core.git

The above creates a local rockstor-core git repo in a new directory by
the same name: "rockstor-core". Change into this new directory/repo clone via:

.. code-block:: console

        you@laptop:~/dev> cd rockstor-core

Configure this new git repo with your name and email address. This is required
to accurately record collaboration:

.. code-block:: console

        you@laptop:~/dev/rockstor-core> git config user.name "Firstname Lastname"
        you@laptop:~/dev/rockstor-core> git config user.email your_email_address

Add a remote called **upstream** to periodically rebase your local repository with upstream changes by other contributors:

.. code-block:: console

        you@laptop:~/dev/rockstor-core> git remote add upstream https://github.com/rockstor/rockstor-core.git

.. _makechanges:

Making changes
--------------

Assuming you have identified or created an issue to work on (eg: #1234) from our
`GitHub issue tracker <https://github.com/rockstor/rockstor-core/issues>`_,
first ensure your local code fork is up-to-date by rebasing on upstream:

.. code-block:: console

        you@laptop:~/dev/rockstor-core> git checkout testing
        you@laptop:~/dev/rockstor-core> git pull --rebase upstream testing

Then checkout a new/issue-specific branch, e.g.:

.. code-block:: console

        you@laptop:~/dev/rockstor-core> git checkout -b 1234_issue_title

You can then start making changes in this dedicated issue-specific branch,
which is itself based on the upstream testing branch in this example.

We strongly encourage the following commit guidelines.
As a guiding principle, separate your changes into one or more logically independent commits.
This can help with the review process but only do this on larger more complex contributions.
Otherwise we advise to squash your local 'working steps' commits into a single commit before submission.

We request that you divide a commit message into two parts.
Start the message with a single line summary, max 70 characters in length ending in #issue-number.
Add a blank line after that.
Further details can then follow in paragraphs less than 80 characters wide.
Below is a fictional example:

.. code-block:: console

        foobar functionality for rockstor #1234

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

.. _buildvm:

Build VM
--------

You need a Virtual Machine (VM) to build and test your changes.
An easy solution is to create a Rockstor VM using either Oracle's
`VirtualBox <https://www.virtualbox.org/>`_
or, if you are using a Linux desktop,
the `Virtual Machine Manager (VMM) <https://virt-manager.org>`_
is a more native option.
Please see our :ref:`kvmsetup` howto for more details on using VMM.
A 'real' machine is another option and may be required in some scenarios,
i.e. where a hardware compatibility feature is being developed.

.. _buildvm_os:

Build VM OS
~~~~~~~~~~~

It is suggested that a fresh Rockstor install be used for the target development machine OS,
i.e. the resulting install from a
`rockstor-installer <https://github.com/rockstor/rockstor-installer>`_.
Pre-built installers are available from our `Downloads page <https://rockstor.com/dls.html>`_.
Note that only v4 "Built on openSUSE" and newer bases are considered
as v3 and older (CentOS-based) instances are now deprecated and no longer developed.

.. note::

    The existing rpm-based Rockstor instance will be destroyed, hence the 'fresh' suggestion.

Alternatively, an upstream (openSUSE) JeOS instance is also an option, but only if:

- Its root filesystem is btrfs and setup for boot to snapshot.
- It uses NetworkManager and not wicked for its network configuration.
- Shellinabox is installed and enabled/running under systemd.
- Apparmor is disabled if installed: :code:`systemctl disable apparmor`.

.. _remove_rpm:

Remove the Existing Rockstor RPM install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The prior existing rpm install must be removed as it will otherwise interfere.
The following does this, updates the OS, and installs the missing build dependencies.
Only 1 dependency (:code:`wget`) will be installed if you are using the suggested Rockstor installers.
This will download less than 800 KiB, and slightly more than 3 MiB will be used after installation.

.. code-block:: text

    buildvm:~ # zypper --non-interactive remove rockstor
    buildvm:~ # rm -rf /opt/rockstor  # remove dangling rockstor rpm-related files.
    buildvm:~ # zypper refresh
    buildvm:~ # zypper up --no-recommends
    buildvm:~ # zypper --non-interactive install wget

.. _buildvm_setup:

Build VM initial setup
----------------------

Transfer the code from your laptop to the build VM.
A password will likely be requested and this is for the buildvm machine's root user.

.. code-block:: console

        you@laptop:~> rsync -avz --exclude=.git ~/dev/rockstor-core/ root@buildvm:/opt/rockstor/

We now have all the tools and code in place on the buildvm machine ready to:

1. Build
2. Test

.. _code_build:

1. Code build
~~~~~~~~~~~~~

This step can take a few minutes, depending on CPU and internet speed.
An internet connection is required as the process downloads and installs all required `Python dependencies <https://github.com/rockstor/rockstor-core/blob/testing/poetry.lock>`_
as well as `JavaScript libraries <https://github.com/rockstor/rockstor-jslibs>`_.
Beginning with v4.5.4-0, Rockstor now leverages the Python packaging and dependency management tool `Poetry <https://python-poetry.org/>`_.
We thus provide a single build script (`build.sh <https://github.com/rockstor/rockstor-core/blob/testing/build.sh>`_)
that will install Poetry, Rockstor's dependencies, and then build Rockstor in one command.
As a result, this step may take a bit of time the first time it is run, but should be much faster on subsequent builds.

.. code-block:: text

         buildvm:~ # cd /opt/rockstor
         buildvm:/opt/rockstor # sh build.sh

The build process should end with a list of further instructions (detailed below).
Simply run each of these steps:

.. code-block:: text

         1. Run 'cd /opt/rockstor'.
         2. Run 'systemctl start postgresql'.
         3. Run 'export DJANGO_SETTINGS_MODULE=settings'.
         4. Run 'poetry run initrock' as root (equivalent to rockstor-pre.service).
         5. Run 'systemctl enable --now rockstor-bootstrap'.

.. note::

   If the :code:`build.sh` command does not end with the instructions above,
   look into the build log recorded in :code:`/opt/rockstor/poetry-install.txt`.

The build process, towards the end, enables and starts the following rockstor systemd services.

.. note::

   All are installed in :code:`/usr/lib/systemd/system/`

Note that all paths indicated below are within the rockstor source tree.

.. code-block:: console

    rockstor-pre.service  # starts .venv/bin/initrock after postgresql.service
    rockstor  # starts .venv/bin/supervisord -c etc/supervisord.conf after rockstor-pre.service
    rockstor-bootstrap  # starts .venv/bin/bootstrap after rockstor.service

If a custom HDD power (APM) and/or spin-down setting is enabled, the following service is added,
but only if the drive is confirmed as rotational:

.. code-block:: console

    rockstor-hdparm.service  # Configures drives APM & spindown settings via hdparm

It is entirely safe to disable and delete the rockstor-hdparm.service.
The only consequence is a return to defaults for all drives on next power cycle.

.. note::

   *N.B.*: power cycle, not necessarily reboot, may be required as drive settings are often reboot sticky
   and so require an actual power cycle to return to their defaults.
   The rockstor-hdparm.service is our way to re-establish custom config on boot-up.
   The Rockstor Web-UI references this file itself for the current settings,
   and no database component is thus linked to this configuration setting.

.. _code_test:

2. Code test
~~~~~~~~~~~~

At this point the Rockstor Web-UI should be available to verify your changes.
In our example setup, the URL from **laptop** would be :code:`https://buildvm/`.

It is very important to ensure that your code changes survive a reboot.
Sometimes, especially when database changes are made, this can be an issue.
Be sure to check that the resulting build behaves as expected over:

1. A config reset - removing :code:`/opt/rockstor/.initrock` and rebooting
2. Several reboots

In (1.) above, a database wipe is initiated helping to test the self-start code capability.
See the :code:`initrock.py` script and its systemd trigger service: :code:`rockstor-pre.service` for more details.

We also have **automated tests** in place that cover our API's and core critical path functionality.
It is expected that any changes to critical path code e.g. filesystem management/updates/Web-UI/services,
include counterpart contributions to prove the expected function, if required.
This is an oft neglected element in software development
but we are attempting to better our own standing in this regard.

The following will run all tests following the source installation detailed above:

.. code-block:: text

    buildvm:~ # cd /opt/rockstor/src/rockstor
    buildvm:/opt/rockstor/src/rockstor # poetry run django-admin test -v 2

All included tests, **numbering over 200**, are expected to pass;
however, it is always worth checking our `current issues <https://github.com/rockstor/rockstor-core/issues>`_
for known failures in this area.

A note on updating
``````````````````
A source install will consider any rpm version to be an update.
And this 'update' will necessarily delete all prior settings/database setup.
This is by design as a source release is intended only for development.
Identifying itself as *ROCKSTOR UNKNOWN VERSION* within the top-right of the Web-UI.
For example, if work on a hardware compatibility issue is submitted,
the author can 'update' in-place upon that work being merged and released in the next rpm version,
This would thus return the specific hardware instance to a recognised upgrade path
and also verify that the released rpm, fix included, works as intended.

All :ref:`import_data` and :ref:`config_backup` functionality is supported similarly
as there is no source difference between a source and rpm install, just the packaging/update/support service,
unless of course there has been a breaking change involved in the submitted code.
Breaking changes in these areas are strongly discouraged but unavoidable at times.
An example: one cannot restore a new feature's settings to an older Rockstor instance.

Change -> Test cycle
--------------------

Changes fall into two main categories.

1. Backend changes involving Python coding.
2. Frontend changes involving JavaScript, HTML and CSS.

To test any change, you need to transfer files from your laptop to the VM:

.. code-block:: console

        you@laptop:~> rsync -avz --exclude=.git ~/dev/rockstor-core/ root@buildvm:/opt/rockstor/

If you made any JavaScript, HTML or CSS changes,
you need to collect the static files with the following after the above transfer:

.. code-block:: text

        buildvm:~ # cd /opt/rockstor
        buildvm:~ # export DJANGO_SETTINGS_MODULE=settings
        buildvm:~ # poetry run django-admin collectstatic --no-input --verbosity 2

N.B. An overall :ref:`code_build` may be required before this will work without error.

Then, refresh the browser to test the new changes in the Web-UI.

Terminal hint
~~~~~~~~~~~~~
Consider having multiple terminals open simultaneously.

- One for transferring files.
- One for running commands on the VM.
- Another for browsing through the logs.

When making backend changes, you may want to view/:code:`tail` logs.
By default, Rockstor's log level is set to INFO.
To increase the log level to DEBUG, you can use the following script:

.. code-block:: text

        buildvm:~ # cd /opt/rockstor
        buildvm:~ # export DJANGO_SETTINGS_MODULE=settings
        buildvm:~ # poetry run debug-mode ON

Everything that your code or any Rockstor service logs goes into the following files:

.. code-block:: text

    buildvm:~ # ls -la /opt/rockstor/var/log
    total 128
    drwxr-xr-x 1 root root    618 Nov 21 16:52 .
    drwxr-xr-x 1 root root      6 Nov 21 16:51 ..
    -rw-r--r-- 1 root root   1002 Nov 21 18:13 gunicorn.log
    -rw-r--r-- 1 root root   1895 Nov 21 18:14 huey.log
    -rw-r--r-- 1 root root 101124 Nov 21 18:27 rockstor.log
    -rw-r--r-- 1 root root   1907 Nov 21 18:14 supervisord_data-collector_stderr.log
    -rw-r--r-- 1 root root      0 Nov 21 16:52 supervisord_data-collector_stdout.log
    -rw-r--r-- 1 root root   1388 Nov 21 18:14 supervisord_gunicorn_stderr.log
    -rw-r--r-- 1 root root      0 Nov 21 16:52 supervisord_gunicorn_stdout.log
    -rw-r--r-- 1 root root   2638 Nov 21 18:14 supervisord.log
    -rw-r--r-- 1 root root    694 Nov 21 18:14 supervisord_ztask-daemon_stderr.log
    -rw-r--r-- 1 root root      0 Nov 21 16:52 supervisord_ztask-daemon_stdout.log

:code:`rockstor.log` should be the first place to look for errors or debug logs.

Some things such as rockstor-pre/bootstrap are logged directly to the system log
and are thus accessible via commands such as:

.. code-block:: console

    journalctl  # akin to "less /var/log/messages" of old. N.B. cursor/page keys to navigate.
    journalctl -f  # tail system log
    journalctl --no-pager  # to avoid line truncation.

When making frontend changes, "Developer Tools" in Chrome/Firefox are critically important.
You can `inspect elements <https://developer.chrome.com/docs/devtools/dom/>`_ for HTML/CSS changes.
Log to the browser console from your JavaScript code with :code:`console.log()` statements,
and use the debugger to step through JavaScript; all from your browser.

Adding third party Javascript libraries
---------------------------------------

The frontend code uses third party JavaScript libraries such as jQuery, Bootstrap, D3.js and many others.
These are not part of the rockstor-core repository but are dynamically generated during the build.
They are unzipped into the below directory on your build VM by the build script (build.sh):

.. code-block:: console

    /opt/rockstor/static/js/lib/

If you need to add a new library,
place all of its files in the above lib directory (on buildvm) and continue your development process.
After you open the pull request on the rockstor-core repo,
it's time to open a separate pull request for merging the additional libraries.
This separate pull request must be opened on another repository named
`rockstor-jslibs <https://github.com/rockstor/rockstor-jslibs>`_,
which mirrors the contents of the lib directory shown above.
The fork and pull-request process for rockstor-jslibs is the same as for the rockstor-core repo.

Database migrations
-------------------

We use `PostgreSQL13 <https://www.postgresql.org/>`_ as the database backend for Rockstor.
There are two databases:

1. storageadmin
2. smart_manager

Depending on your issue you may need to add a Django model, delete one, or change fields of an existing model.
After editing models you need to create a database migration file and apply it.

In the past, we used `South <https://south.aeracode.org/>`_ to manage database migrations for a while
but since updating to Django 1.8, migrations are natively supported.
The steps have changed only slightly.

1. Generate the migration on buildvm and copy the resulting file back to your laptop.
2. Add this migration file to the git source control. It represents a necessary part of your proposed changes and enables the update mechanism.

E.g. for model changes in the storageadmin application, create a migration file using:

.. code-block:: text

        buildvm:~ # cd /opt/rockstor
        buildvm:~ # export DJANGO_SETTINGS_MODULE=settings
        buildvm:~ # poetry run django-admin makemigrations storageadmin

The above command generates a migration file in
:code:`/opt/rockstor/src/rockstor/storageadmin/migrations/`.
Apply the migration with:

.. code-block:: text

        buildvm:~ # cd /opt/rockstor
        buildvm:~ # export DJANGO_SETTINGS_MODULE=settings
        buildvm:~ # poetry run django-admin migrate storageadmin

For model changes in the smart_manager application, create a migration file using:

.. code-block:: text

        buildvm:~ # cd /opt/rockstor
        buildvm:~ # export DJANGO_SETTINGS_MODULE=settings
        buildvm:~ # poetry run django-admin makemigrations smart_manager

Run the migration with:

.. code-block:: text

        buildvm:~ # cd /opt/rockstor
        buildvm:~ # export DJANGO_SETTINGS_MODULE=settings
        buildvm:~ # poetry run django-admin migrate --database=smart_manager smart_manager

.. _shipchanges:

Shipping changes
----------------

As you continue to work on an issue, commit and push changes to the issue branch of your fork.
You can periodically push your changes to GitHub with the following command:

.. code-block:: console

        you@laptop:~> cd ~/dev/rockstor-core; git push origin 1234_issue_title

When you finish the associated issue changes and are ready to submit your pull/merge reqeust,
create a pull request by clicking on the "pull request" button on GitHub.

.. warning::
    Be very careful to select the correct upstream branch to which you want to contribute.
    This will very likely be the same branch you initially checked out above, i.e. **testing**.
    For specific reasons, the *testing* branch is not the default in GitHub currently.
    You will be required to select *testing* if you are not working against master directly.

This pull-request process notifies the maintainers of your proposed changes.
As a best practice, only open one pull request per issue, containing all relevant changes.

Commit history cleanup
----------------------

As you work on an issue in your feature/issue branch, you may have committed multiple times.
This is good practice as you have 'save points' and a backup of sorts.
Before submitting your pull request, however, please squash all commits into one at the very end.
This will help to keep the upstream branch histories cleaner,
and make it easier to research, or revert, issue-related changes.
This can also help a lot when tracking down regressions.

.. note::
   If a pull request is non trivial, or spans multiple logically distinct areas,
   try to squash your working commit history to a meaningfully, simple to understand, set.

Squashing commits into one is relatively straight-forward.
Most editors and IDEs with git integration make this relatively easy to do so.
If you've never done this before, this
`short how-to <https://levelup.gitconnected.com/how-to-squash-git-commits-9a095c1bc1fc>`_
may help.
See also `PyCharm's excellent git capabilities <https://www.jetbrains.com/help/pycharm/edit-project-history.html>`_.

Contributing and testing from another Rockstor contributor fork
---------------------------------------------------------------

If you want to test and/or contribute starting from another user's fork, you can add their fork (or single branch).

To add another user's forked repo to your remotes:

.. code-block:: console

        your@laptop:~/dev/rockstor-core> git remote add other_user_name git@github.com:other_user_name/rockstor-core.git

To fetch another user's branch from the remote fork added above:

.. code-block:: console

        your@laptop:~/dev/rockstor-core> git fetch other_user_name remote_branch_name

After fetching another contributor's branch, you can checkout from it and start your development
or create a complete new branch starting from one of theirs.
GitHub pull requests can then be made directly to the appropriate Rockstor repo or other user's forks/branches.
