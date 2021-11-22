
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

Developing Rockstor as an open storage platform is non trivial endeavour.
If you are passionate about Open Source and Storage like us, you are in the right place.
The`community discussion forum <https://forum.rockstor.com>`_ is the place to start.

Our development process is relatively simple and straight forward.
We use `Git <https://git-scm.com/>`_ for source code management and
`Rockstor on Github <https://github.com/rockstor>`_ for issue tracking.
There is currently one main code repository called
`rockstor-core on Github <https://github.com/rockstor/rockstor-core>`_.
Begin by `forking it <https://github.com/rockstor/rockstor-core/fork>`_ via GitHub's Web-UI.

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
3. **~/dev/rockstor-core**: = your (laptop/desktop) local git clone & dev branch directory.
4. **buildvm**: is your target build machine's hostname; the name chosen during the rockstor install.

TIP: you can add your buildvm's IP address to /etc/hosts on your laptop (linux assumed).
E.g.

.. code-block:: console

    you@laptop:~> grep "buildvm" /etc/hosts
    192.168.2.170   buildvm

Then a :code:`ping -c2  buildvm` on your laptop should complete without error.
And :code:`ssh root@buildvm` should provide a root user shell on the target buildvm machine.
Assuming they are both on the same network.

.. _localrepo:

Local git repo setup
--------------------

Since we rely on GitHub services, you need to create a profile on `github.com <https://github.com/>`_.

Go to `rockstor-core repo <https://github.com/rockstor/rockstor-core>`_ and click on the "Fork" button.
You should then have a fork of this repository in your own GitHub profile.
This repo then serves as your private git remote called origin.
The next few git steps are demonstrated on a Linux terminal.
They should also work with little or no modification in an OSX console.

Clone, in turn, your GitHub profiles fork of rockstor-core onto your local machine.
You can do this in any directory; but the following assume the ~/dev directory.

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

Assuming you have identified or created an issue to work on (eg: #1234) from
`GitHub issue tracker <https://github.com/rockstor/rockstor-core/issues>`_.
First ensure your local code fork is up-to-date by rebasing on upstream:

.. code-block:: console

        you@laptop:~/dev/rockstor-core> git checkout master
        you@laptop:~/dev/rockstor-core> git pull --rebase upstream master

Then checkout a new/issue-specific branch, e.g.:

.. code-block:: console

        you@laptop:~/dev/rockstor-core> git checkout -b 1234_issue_title

You can then start making changes in this dedicated branch.

We strongly encourage the following commit guidelines.
As a guiding principle, separate your changes into one or more logically independent commits.
This can help with the review process but only do this on larger more complex contributions.
Otherwise we advise to squash your local 'working steps' commits into a single commit before submission.

We request that you divide a commit message into two parts.
Start the message with a single line summary, about 70 characters in length ending in #issue-number.
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
or if you are using a Linux desktop then the
`Virtual Machine Manager (VMM) <https://virt-manager.org>`_
is a more native option.
VMM is used in our :ref:`kvmsetup` howto.
A 'real' machine is another option and may be required in some scenarios,
i.e. where a hardware compatibility feature is being developed.

.. _buildvm_os:

Build VM OS
~~~~~~~~~~~

It is suggested that a fresh Rockstor install be used for the target development machine OS.
I.e. the resulting install from a
`rockstor-installer <https://github.com/rockstor/rockstor-installer>`_
Pre-built installers are available from our `Downloads page <https://rockstor.com/dls.html>`
Only v4 "Built on openSUSE" and newer bases are considered.
V3 and older (CentOS based) instances are now deprecated and no longer developed.

N.B. the existing rpm based rockstor instance will be destroyed, hence the 'fresh' suggestion.

Alternatively an upstream (openSUSE) JeOS instance is also an option:
but only if:

- It's root filesystem is btrfs and setup for boot to snapshot.
- It uses NetworkManager not wicked for it's network configuration.
- Shellinabox is installed and enabled/running under systemd.
- Apparmour is disabled if installed: "systemctl disable apparmor".

.. _remove_rpm:

Remove the Existing Rockstor RPM install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The prior existing rpm install must be removed as it will otherwise interfere.
The following does this, updates the os, and installs the dev dependencies.
Around 30 packages will already be installed and a similar number will be added:
if you are using the suggested rockstor-installer derived os instance.
This change will be around 60 MB download and 250 MB installed.

.. code-block:: console

    zypper --non-interactive remove rockstor
    rm -rf /opt/rockstor  # remove dangling rockstor rpm related files.
    zypper refresh
    zypper up --no-recommends
    zypper --non-interactive install avahi samba docker nut nginx nfs-kernel-server \
    at gcc python-devel gcc-c++ postgresql10-server libblkid-devel \
    dnf-yum dnf-plugins-core python2-distro python3-distro firewalld python2-setuptools \
    python2-requests python2-chardet python-xml cryptsetup which dnf-yum dnf-plugins-core \
    python3-python-dateutil python2-six python2-psycopg2 python2-pyzmq python2-pyzmq-devel \
    sssd sssd-tools sssd-ad sssd-ldap sssd-dbus python-dbus-python dmraid

.. _buildvm_setup:

Build VM initial setup
----------------------

Transfer the code from your laptop to the build VM.
A password will likely be requested and this is for the buildvm machine's root user.

.. code-block:: console

        you@laptop:~> rsync -avz --exclude=.git ~/dev/rockstor-core/ root@buildvm:/opt/rockstor-dev/

And via your ssh session to, or console on, **the target buildvm machine** (as root):

.. code-block:: console

        buildvm:~ # zypper --non-interactive install python2-pip
        buildvm:~ # pip2 install zc.buildout

We now have all the tools and code in place on the buildvm machine ready to:

1. configure
2. build

.. _code_config:

1. Code configure/re-configure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: console

        buildvm:~ # cd /opt/rockstor-dev/
        buildvm:/opt/rockstor-dev # buildout bootstrap

.. _code_build:

2. Code build
~~~~~~~~~~~~~
This step can take a few minutes, depending on cpu and internet speed.
An internet connection is required as the process downloads all required Python eggs/wheels etc.
We are running the bin/buildout script generated/updated in :ref:`code_config` step above.
This stage takes considerably longer if you have also just configured/reconfigured the code.

.. code-block:: console


         buildvm:/opt/rockstor-dev # bin/buildout -N -c buildout.cfg

The build process, towards the end, enables and starts the following rockstor systemd services.
**All are installed in /etc/systemd/system/**
Note that all paths indicated are within the rockstor source tree.

.. code-block:: console

    rockstor-pre.service  # starts bin/initrock after postgresql.service
    rockstor  # starts bin/supervisord -c etc/supervisord.conf after rockstor-pre.service
    rockstor-bootstrap  # starts bin/bootstrap after rockstor.service

If a custom HDD power (APM) and/or spin-down setting is enabled, the following service is added.
But only if the drive is confirmed as rotational.

.. code-block:: console

    rockstor-hdparm.service  # Configures drives APM & spindown settings via hdparm

It is entirely safe to disable and delete the rockstor-hdparm.service.
The only consequence is a return to defaults for all drives on next power cycle.
N.B. power cycle, not necessarily reboot; as drive settings are often reboot sticky.
And so require an actual power cycle to return to their.
The rockstor-hdparm.service is our way to re-establish custom config on boot-up.
The Rockstor Web-UI references this file itself for the current settings.
There is no db component to this configuration setting.

At this point the Rockstor Web-UI should be available to verify your changes.
In our example setup the URL from **laptop** would be :code:`https://buildvm/`.

It is very important to ensure that your code changes survive a reboot.
Sometimes, especially when db changes are made, this can be an issue.
Be sure to check that the resulting build behaves as expected over:

1. A config reset - removing /opt/rockstor-dev/.initrock and rebooting,
2. Several reboots

In (1.) above a db wipe is initiated helping to test the self-start code capability.
See the initrock script and it's systemd trigger service: rockstor-init.

A note on updating
``````````````````
A source install will consider any rpm version to be an update.
And this 'update' will necessarily delete all prior settings / db setup.
This is by design as a source release is intended only for development.
Identifying itself as *ROCKSTOR UNKNOWN VERSION* withing the top-right of the Web-UI.
For example if work on say a hardware compatibility issue is submitted,
upon that work being merged and released in the next rpm version the author can 'update' in-place.
There-by returning the specific hardware instance to a recognised upgrade path.
Providing also for a double-check on if the released rpm, fix included, works as intended.
The source install can, in-turn, now simply be removed via :code:`rm -rf /opt/rockstor-dev/`.
Rpm installs live exclusively in /opt/rockstor, bar their associated systemd units.

All :ref:`import_data` and :ref:`config_backup` functionality is supported similarly;
as there is no source difference between a source and rpm install, just the packaging/update/support service.
Unless of course there has been a breaking change involved in the submitted code.
Breaking changes in these areas are strongly discouraged but unavoidable at time.
An example: one cannot restore a new features settings to an older Rockstor instance.

Change -> Test cycle
--------------------

Changes fall into two main categories.

1. Backend changes involving python coding.
2. Frontend changes involving javascript, html and css.

To test any change, you need to transfer files from your laptop to the VM:

.. code-block:: console

        you@laptop:~> rsync -avz --exclude=.git ~/dev/rockstor-core/ root@buildvm:/opt/rockstor-dev/

If you made any javascript, html or css changes,
you need to collect the static files with the following after the above transfer:

.. code-block:: console

        buildvm:~ # /opt/rockstor-dev/bin/buildout -c /opt/rockstor-dev/buildout.cfg install collectstatic

N.B. An overall :ref:`code_config` may be required before this will work without error.

Then, refresh the browser to test new changes in the Web-UI.

Terminal hint
~~~~~~~~~~~~~
Consider having multiple terminals open simultaneously.

- One for transferring files.
- One for running commands on the VM.
- Another for browsing through the logs.

When making backend changes, you may want to view/tail logs.
Everything that your code or any rockstor service logs goes into the following logs:

.. code-block:: console

    buildvm:~ # ls -la /opt/rockstor-dev/var/log
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
    -rw-r--r-- 1 root root    274 Nov 21 18:13 supervisord_nginx_stderr.log
    -rw-r--r-- 1 root root      0 Nov 21 16:52 supervisord_nginx_stdout.log
    -rw-r--r-- 1 root root    694 Nov 21 18:14 supervisord_ztask-daemon_stderr.log
    -rw-r--r-- 1 root root      0 Nov 21 16:52 supervisord_ztask-daemon_stdout.log

rockstor.log should be the first place to look for errors or debug logs.

Some things such as rockstor-pre/bootstrap are logged directly to the system log.
And so are accessible via commands such as:

.. code-block:: console

    journalctl  # akin to "less /var/log/messages" of old. N.B. cursor/page keys to navigate.
    journalctl -f  # tail system log
    journalctl --no-pager  # to avoid line truncation.

When making frontend changes, "Developer Tools" in Chrome/Firefox are critically important.
You can `inspect elements <https://developer.chrome.com/docs/devtools/dom/>`_ for html/css changes.
Log to the browser console from javascript code with console.log().
And use the debugger to step through javascript; all from your browser.

Adding third party Javascript libraries
---------------------------------------

The frontend code uses third party javascript libraries such as jquery,bootstrap, d3 and many others.
These are not part of the rockstor-core repository but are dynamically generated during the build.
They are placed in the below directory on your build VM:

.. code-block:: console

    buildvm:~ # ls /opt/rockstor-dev/static/js/lib/
    additional-methods.min.js    cubism.v1.js                 jquery.flot.resize.js        jquery.validate.js
    backbone-0.9.2.js            d3-tip.js                    jquery.flot.stack.js         json2.js
    backbone.routefilter.min.js  d3.v3.min.js                 jquery.flot.stackpercent.js  jsonform.js
    bootstrap-datepicker.js      DataTables-addons            jquery.flot.time.js          later.min.js
    bootstrap-editable.min.js    dataTables.bootstrap.min.js  jquery.flot.tooltip_0.5.js   LICENSE
    bootstrap.js                 gentleSelect                 jquery.i18n                  moment.min.js
    bootstrap-switch.min.js      handlebars-v4.0.5.js         jquery-migrate-1.2.1.min.js  prettycron.js
    bootstrap-timepicker.js      humanize.js                  jquery.shapeshift.js         select2
    Chart.min.js                 jquery-1.9.1.min.js          jquery.sparkline.min.js      simple-slider.min.js
    chosen.jquery.js             jquery.dataTables.min.js     jquery.tablesorter.js        socket.io.min.js
    clipboard.min.js             jquery.flot.axislabels.js    jquery.tools.min.js          socket.io.min.js.map
    cocktail.js                  jquery.flot.js               jquery.touch-punch.min.js    underscore-1.3.2.js
    cron                         jquery.flot.navigate.js      jquery-ui.min.js             underscore.js

If you need to add a new library,
place all of it's files in the above lib directory (on buildvm) and continue your development process.
After you open the pull request on the rockstor-core repo,
it's time to open a separate pull request for merging the additional libaries.
This separate pull request must be opened on another repository named
`rockstor-jslibs <https://github.com/rockstor/rockstor-jslibs>`_,
which mirrors the contents of the lib directory shown above.
The fork and pull-request process for rockstor-jslibs is the same as for the rockstor-core repo.

Database migrations
-------------------

We use `PostgreSQL10 <https://www.postgresql.org/>`_ as the database backend for Rockstor.
There are two databases:

1. storageadmin
2. smart_manager

Depending on your issue you may need to add a Django model, delete one, or change fields of an existing model.
After editing models you need to create a database migration file and apply it.

We used `South <https://south.aeracode.org/>`_ to manage database migrations for a while,
but since updating to Django 1.8, migrations are natively supported.
The steps have changed only slightly.
Generate the migration on buildvm and copy the resulting file back to your laptop.
This migration file should now be added to the git soruce control.
It represents a necessary part of your proposed changes and enables the update mechanism.

E.g.for model changes in storageadmin application, create a migration file using:

.. code-block:: console

        buildvm:~ # /opt/rockstor-dev/bin/django makemigrations storageadmin

The above command generates a migration file in
:code:`/opt/rockstor-dev/src/rockstor/storageadmin/migrations/`. Apply the
migration with:

.. code-block:: console

        buildvm:~ # /opt/rockstor-dev/bin/django migrate storageadmin

For model changes in the smart_manager application, create a migration file
using:

.. code-block:: console

        buildvm:~ # /opt/rockstor-dev/bin/django makemigrations smart_manager

Run the migration with:

.. code-block:: console

        buildvm:~ # /opt/rockstor-dev/bin/django migrate --database=smart_manager smart_manager

.. _shipchanges:

Shipping changes
----------------

As you continue to work on an issue, commit and push changes to the issue branch of your fork.
You can periodically push your changes to GitHub with the following command:

.. code-block:: console

        you@laptop:~> cd ~/dev/rockstor-core; git push origin 1234_issue_title

When you finish the associated issue changes, and are ready to submit your pull/merge reqeust,
create a pull request by clicking on the "pull request" button on GitHub.
This notifies the maintainers of your changes.
As a best practice only open one pull request per issue containing all relevant changes.

Commit history cleanup
----------------------

As you work on an issue in your feature/issue branch, you may have committed multiple times.
This is good practice as you have 'save points' and a backup of sorts.
But submitting your pull request please squash all commits into one at the very end.
Or if a pull request is non trivial, or spans multiple logically distinct areas.
Try and squash your working commit history to a meaningfully, simple to understand, set.
This will help to keep the upstream branch histories cleaner,
and makes it easier to research, or revert, issue related changes.
This can help a lot when tracking down regressions.

Squashing commits into one is relatively straight-forward.
Most editors and IDEs with git intergration make this relatively easy to do so.
If you've never done this before, this
`short how-to <https://levelup.gitconnected.com/how-to-squash-git-commits-9a095c1bc1fc>`_
may help.
See also `PyCharm's excellent git capabilities <https://www.jetbrains.com/help/pycharm/edit-project-history.html>`_.

Contributing and testing from another Rockstor contributor fork
---------------------------------------------------------------

If you want to test and/or contribute starting from another user's fork, you can add his/her fork (or single branch).

Adding another user's forked repo to your remotes:

.. code-block:: console

        your@laptop:~/dev/rockstor-core> git remote add other_user_name git@github.com:other_user_name/rockstor-core.git

Fetching another user's branch from the above added remote fork:

.. code-block:: console

        your@laptop:~/dev/rockstor-core> git fetch other_user_name remote_branch_name

After fetching another contributor's branch you can checkout from it and start your development,
or create a complete new branch starting from one of theirs.
Github pull requests can then be made directly to the Rockstor repo or other user's forks/branches.
