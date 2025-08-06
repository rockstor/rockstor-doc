.. _bareos_rockon:

Bareos Backup Server Rock-on
============================

Please be aware of the common prerequisites for all Rockstor
:ref:`rockons_intro`; specifically the :ref:`rockons_preinstall` and
:ref:`rockons_root` requirement.


.. _bareos_whatis:

What is Bareos
--------------

`Bareos <https://docs.bareos.org/IntroductionAndTutorial/WhatIsBareos.html>`_
BAckup and REcovery `Open Source <https://github.com/bareos/bareos>`_ software:
network-based, enterprise class, and multiply
`certified <https://www.bareos.com/product/certifications/>`_.
Compatible with all major operating systems as Clients,
with VM, raw partition, Database, etc backup options.
There is also
`compatibility <https://docs.bareos.org/Appendix/DisasterRecoveryUsingBareos.html#bare-metal-recovery-of-bareos-clients>`_
with `Relax-and-Recover (ReaR) <https://relax-and-recover.org/>`_.
Bareos is a 2010 AGPL-3.0 Licensed fork of the then 10 years old `Bacular <https://www.bacula.org/>`_,
see also `Bacular Systems <https://www.baculasystems.com/>`_,
where the supported/enterprise variant is no longer open source, i.e. an open core model.

For flexibility the Bareos software stack is comprised of
`distinct services <https://www.bareos.com/software/>`_:

- Director - Overall controller.
- Catalog - Database (Postgres) for the Director.
- Storage - Archives agent; HDD/SSD, SAS, SDS, Tape, Ceph, GlusterFS, S3, etc.
- File - Client software.
- Webui - Web user interface to the Director.

This Rock-on honours the above separation of concerns by hosting one of each of the above in discrete docker containers.
Constituting a Bareos server set, with a Director-local File/Client instance:
enabling the default `BackupCatalog` job which include all shared server-side configuration.
:ref:`Rocknets <rockons_networking>` are then used to establish the required inter-service communication.
Registered Client machines can then reference the Rockstor IP: where all relevant ports are surfaced.
I.e. Registered Bareos clients connect to this Rock-ons instantiated services and backup "To" the Rockstor server.

.. note::
    This rock-on uses docker images authored by the Rockstor maintainers.
    These instantiate the
    `Bareos Community Repository <https://download.bareos.org/current/>`_
    `current` variant packages within official OpenSuse Leap containers.

.. warning::
    The Community Repository packages are UNSUPPORTED by
    `bareos.com <https://www.bareos.com/>`_
    the commercial entity of Bareos the software project.
    We plan, upon rock-on install, to conditionally use the
    `Official Bareos Subscription Repository <https://download.bareos.com/bareos/release/>`_,
    assuming non-empty Bareos subscription credentials are passed.
    With sufficient interest we will seek upstream assistance with this endeavour.

.. _bareos_doc:

Bareos Documentation
--------------------

From the `Bareos website <https://www.bareos.com/>`_:

- Manual: https://docs.bareos.org/
- Tutorial: https://docs.bareos.org/IntroductionAndTutorial.html
- Webui: https://docs.bareos.org/IntroductionAndTutorial/BareosWebui.html
- Adding a Client: https://docs.bareos.org/IntroductionAndTutorial/Tutorial.html#adding-a-client
- Training: https://www.bareos.com/learn/training/

.. _bareos_pre:

Pre-install requirements
------------------------

The requirements for this Rock-on are as follows:

1. Ensure Rockstor's :ref:`email_notifications` have been configured and tested.
   This is critical to inform you of;
   Backup/Restore success/failure, to receive recovery bootstrap files,
   tape-change instructions etc.
2. Ensure SSH access to the Rockstor server (default as 'root' user).
   Ideally required to ease retrieval of the exported client configuration.
   During more recent Rockstor TW/SR based installer,
   there is a SSH key enrolment process.

.. _bareos_usergroup:

Create Bareos User & Group
^^^^^^^^^^^^^^^^^^^^^^^^^^

There is a requirement to match the User ID and Group ID within the container,
with those within the host: Rockstor in this case.
The following two command, run as the 'root' user, will ensure this is the case:

.. code-block:: bash

   groupadd --system --gid 105 bareos
   useradd --system --uid 105 --comment 'bareos' --home-dir /var/lib/bareos -g bareos -G disk,tape --shell /bin/false bareos

.. _bareos_shares:

Create Shares
^^^^^^^^^^^^^

The following :ref:`Share <shares>` names are arbitrary but will help in following this how-to:

Create the following, `(bareos:bareos)` indicates the required user:group for each.

- **bareos-catalog** Used by the Postgres/DB container for the CATALOG.
- **bareos-backups** (bareos:bareos) - BACKUP location for the Storage service.
- **bareos-dir-config** (bareos:bareos) - Director/Storage/File shared configuration.
- **bareos-dir-data** (bareos:bareos) - Director/Storage/File shared running state.
- **bareos-webui** - Webui configuration.

.. _bareos_rocknet:

Create Rocknet
^^^^^^^^^^^^^^

The Rockon install process automatically creates the following docker networks:
BareosDirToDB, BareosDirToStorage, BareosDirToFd, and BareosDirToWebui.
However, due to current Rockstor limitations, the following Rocknet must be created by-hand.

Visit: System - Network - :ref:`Add Connection <network_add_connection>` within the Web-UI.

- Name: **BareosFdToStorage**
- Type: :ref:`docker <network_add_connection_docker>`

.. _bareos_install:

Installing Bareos Rock-on
-------------------------

Ensure the above :ref:`bareos_pre` and navigate to
Rockons - All (Tab), then click **Install** on the **Bareos Backup Server** entry.

.. _bareos_shares_select:

Bareos Shares
^^^^^^^^^^^^^

In the following we use the suggested shared from our earlier :ref:`bareos_shares` step.
Note that these names are also indicated in each fields label.

.. image:: /images/interface/docker-based-rock-ons/bareos_shares.png
   :width: 100%
   :align: center

.. _bareos_ports:

Bareos Ports
^^^^^^^^^^^^

The Director and Storage ports must be set to the number indicated.
The WebUI can use an alternative port.

.. image:: /images/interface/docker-based-rock-ons/bareos_ports.png
   :width: 100%
   :align: center

.. _bareos_envars:

Bareos Passwords & Email
^^^^^^^^^^^^^^^^^^^^^^^^

Enter the desired passwords,
and the email Sender & Receiver email addresses from your :ref:`email_current`.

.. image:: /images/interface/docker-based-rock-ons/bareos_envars.png
   :width: 100%
   :align: center

.. _bareos_post:

Post-install requirements
-------------------------

After the above install completes, the **BareosFdToStorage** Rocknet must be applied.

1. Switch the `Bareos Backup Server` Rock-on **OFF** (required to add Rocknets).
2. Click the **Spanner** icon.
3. Click the **Networking** Button on the resulting dialog.
4. Select **BareosFdToStorage** for each of *bareos-fd* & *bareos-storage*; linking them via the rocknet.

As in the following image of the settings (spanner) dialog:

.. image:: /images/interface/docker-based-rock-ons/bareos_rocknet.png
   :width: 100%
   :align: center

After confirmation via the dialog resulting from the 'Next' button,
the Rock-on should restart automatically.

.. _bareos_webui:

Bareos Webui
------------

Within the Rock-on listing click the "Bareos Backup Server UI" button.

Webui login
^^^^^^^^^^^

- Director: bareos-dir - Other directors can be selected once added to the configuration.
- User: admin - preconfigured in this install
- Password: ********** - from :ref:`bareos_envars` above

Post login the default Webui is displayed:

.. image:: /images/interface/docker-based-rock-ons/bareos_webui.png
   :width: 100%
   :align: center

.. _bareos_bconsole:

Bareos Console
---------------

Aside from the :ref:`bareos_webui`,
there is also the Bareos Console or `bconsole <https://docs.bareos.org/TasksAndConcepts/BareosConsole.html>`_:
a dedicated CLI (Command Line Interface).

.. note::

    For convenience the WebUI embedded **bconsole** configured by this Rock-on is a fully privileged instance.

.. warning::
    As of Bareos 24, the WebUI embedded **bconsole** is limited to one-line commands, i.e. non-functional dialogs.

Full bconsole
^^^^^^^^^^^^^

A full Director-local :ref:`bareos_bconsole` is available from within the bareos-dir container.

.. note::

    Likely required for advanced operations only,
    or when a more interactive or multi-line Bareos operation is required.

Via 'root' user SSH on the Rockstor host:

.. code-block:: bash

    docker exec -it bareos-dir sh
    bconsole

Use the ``exit`` command repeatedly to leave the bconsole, the container shell, and the Rockstor console itself.

.. _bareos_client_reg:

Client Registration
-------------------

Bareos Clients must be **Added** to, or **Registered** with, at least one **Bareos Director**.
I.e. each client can be backed-up by more than one Director.
The following instructions assume:

1. Client machine runs Linux with command ``hostname`` output of **tuxlap**. Replace appropriately.
2. **/home** only midday (13:00) backup. See :ref:`bareos_doc` for other examples.
3. Rockstor and **tuxlap** can ping one-another by the provided IPs or hostnames.

Using an unrestricted / admin bconsole, default in this Rock-on's Webui:

.. code-block:: bash

    *configure add client name=tuxlap-fd address=client.ip.or.hostname passive=yes password=secret-here

.. note::

    "*" is the bconsole prompt;
    and `Passive Client <https://docs.bareos.org/TasksAndConcepts/NetworkSetup.html#section-passiveclient>`_
    avoids many common firewall, NAT, & name resolution issues.

.. note::

    Show current clients via: ``*show clients``.
    Remove clients via:
    1. ``*purge jobs client=tuxlap-fd``,
    2. (bareos-dir container) `bareos-dbcheck <https://docs.bareos.org/Appendix/BareosPrograms.html#bareos-dbcheck>`_

The above creates:

1. `/etc/bareos/bareos-dir-export/client/tuxlap-fd/bareos-fd.d/director/bareos-dir.conf` for client-side use.
2. `/etc/bareos/bareos-dir.d/client/tuxlap-fd.conf` director-side config.

**Where `/etc/bareos` maps to the `bareos-dir-config` Share.**

.. note::

    A machine with hostname **tuxlap** is given a Client name of **tuxlap-fd** (fd = File Daemon).

.. _bareos_client_install:

Client Install
--------------

To use a Bareos Backup Server,
a machine must have the Bareos Client/File software installed.
Ideally a similar version to that on the Server, the :ref:`bareos_webui` shows running/connected versions.

- See: `Installing a Bareos Client <https://docs.bareos.org/IntroductionAndTutorial/InstallingBareosClient.html>`_
- Minimal install: **bareos-filedaemon**
- Desktop / Laptop: **bareos-client** (bareos-filedaemon, bareos-bconsole, and bareos-traymonitor)

E.g. openSUSE Leap 15.6 Desktop/Laptop (community, current assumed) :

.. code-block:: bash

    wget https://download.bareos.org/current/SUSE_15/add_bareos_repositories.sh
    sh ./add_bareos_repositories.sh
    zypper refresh
    zypper install bareos-client

The above create:

File/Client config
^^^^^^^^^^^^^^^^^^

From **bareos-filedaemon** package:

1. `/etc/bareos/bareos-fd.d/client/myself.conf` This Client's `Name`, e.g. "tuxlap-fd".
2. `/etc/bareos/bareos-fd.d/director/bareos-dir.conf` Full (admin console) Authorized Director credentials.
3. `/etc/bareos/bareos-fd.d/director/bareos-mon.conf` Tray-monitor (bareos-mon password) status credentials.
4. `/etc/bareos/tray-monitor.d/client/FileDaemon-local.conf` 'localhost' File/Client credentials (bareos-mon password)

Replace 2. with Director exported credentials as generated in :ref:`bareos_client_reg` above.

.. code-block:: bash

    sudo scp root@rockstor-ip:///mnt2/bareos-dir-config/bareos-dir-export/client/tuxlap-fd/bareos-fd.d/director/bareos-dir.conf /etc/bareos/bareos-fd.d/director/bareos-dir.conf
    sudo systemctl stop bareos-fd.service
    sudo systemctl start bareos-fd.service

*I.e. Client retrieves credentials exported by the director during registration on the Rockstor server.*

.. note::

    Alternatively match credentials by hand,
    however exported credentials contain a hashed password, which is preferred.

From **bareos-bconsole** package:

1. `/etc/bareos/bconsole.conf` 'localhost' director **bconsole** credentials.

For a client-side unrestricted / admin **bconsole**:

- Change 'localhost' to Rockstor's hostname or IP.
- Change password to match bconsole.conf in the root of Share:
  `bareos-dir-config` (/mnt2/bareos-dir-config/bconsole.conf)

A restricted / `named console <https://docs.bareos.org/Configuration/Console.html#using-named-consoles>`_
is also configurable.

From **bareos-traymonitor** package:

1. `/etc/bareos/tray-monitor.d/monitor/bareos-mon.conf`

- Change `bareos-mon.conf` password to match that in Share: `bareos-dir-config` /bareos-dir.d/console/bareos-mon.conf
- `Example Traymonitor configuration <https://docs.bareos.org/Configuration/Monitor.html#example-traymonitor-configuration>`_
  for further bareos-mon.conf additions.

Optionally add Director tray-monitoring:

.. code-block:: bash

    sudo mkdir /etc/bareos/tray-monitor.d/director
    sudo nano /etc/bareos/tray-monitor.d/director/bareos-mon.conf  # contents follows:

    Director {
      Name = bareos-mon
      address = Rockstor-IP_or_hostname
    }

Optionally add Storage tray-monitoring:

.. code-block:: bash

    sudo mkdir /etc/bareos/tray-monitor.d/storage/
    sudo nano /etc/bareos/tray-monitor.d/storage/bareos-mon.conf  # contens follows:

    Storage {
      Name = bareos-storage
      Address = Rockstor-IP_or_hostname
      Password = "as-per_Share:bareos-dir-config bareos-sd.d/director/bareos-mon.conf"
    }

With both optional additions:

.. code-block:: bash

    tree /etc/bareos/tray-monitor.d/

    /etc/bareos/tray-monitor.d/
    ├── client
    │   └── FileDaemon-local.conf
    ├── director
    │   └── bareos-mon.conf
    ├── monitor
    │   └── bareos-mon.conf
    └── storage
        └── bareos-mon.conf


Open port 9102
^^^^^^^^^^^^^^

The Director calls the client on this port.
Enable incoming connections; assumes client firewalld: openSUSE, Fedora, RedHat.

Any source IP:

.. code-block:: bash

    sudo firewall-cmd --permanent --zone=public --add-port=9102/tcp
    sudo firewall-cmd --reload


Or a specific source IP (e.g. 192.168.2.115).

.. code-block:: bash

    sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.2.115" port protocol="tcp" port="9102" accept'
    sudo firewall-cmd --reload

Status of run-time firewall configuration:

.. code-block:: bash

    sudo firewall-cmd --list-all

Status Check
^^^^^^^^^^^^

Establish if the Director can communicate with the new client.

.. code-block:: bash

    *status client=tuxlap-fd

Backup Job
----------

A Bareos `Job <https://docs.bareos.org/Configuration/Director.html#directorresourcejob>`_ associates;
a `Client <https://docs.bareos.org/Configuration/Director.html#client-resource>`_,
a `FileSet <https://docs.bareos.org/Configuration/Director.html#fileset-resource>`_,
a `Storage <https://docs.bareos.org/Configuration/Director.html#storage-resource>`_.
a `Pool <https://docs.bareos.org/Configuration/Director.html#pool-resource>`_, and
a `Schedule <https://docs.bareos.org/Configuration/Director.html#schedule-resource>`_.
These are all known as Director Resources.
`JobDefs <https://docs.bareos.org/Configuration/Director.html#jobdefs-resource>`_
are Job Defaults honoured if not overridden by a specific Job.
They primarily define shared settings across, for example, multiple similar clients.
Each Job can then be setup by overriding only, for example, the Client.

I.e. A job defines: what (FileSet) on which (Client) is to be backed-up/restored to/from which
(Storage / Bareos Pool).

`Pool` in this context is a set of Bareos Storage Volumes,
akin but unrelated to Rockstor's :ref:`Pools` as sets of disks.

Linux /home Backup Job
^^^^^^^^^^^^^^^^^^^^^^

Named **backup-tuxlap** for the **tuxlap-fd** client :ref:`registered <bareos_client_reg>` earlier.

.. code-block:: bash

    *configure add job name=backup-tuxlap client=tuxlap-fd jobdefs=LinuxHomeJob

Job Estimate
^^^^^^^^^^^^

Useful to examine the expected file count, Backup size, and optionally a filelist.
From `bconsole commands <https://docs.bareos.org/TasksAndConcepts/BareosConsole.html#console-commands>`_.


.. code-block:: bash

    estimate job=backup-tuxlap

- Adding `listing` to the above command requests what files are to be backed-up
- Adding `level=Incremental` or `level=Differential` will set the type of backup to be estimated.

