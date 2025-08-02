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
It is a 2010 AGPL-3.0 Licensed fork of `Bacular <https://www.bacula.org/>`_,
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