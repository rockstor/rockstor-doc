.. Rockstor documentation master file, created by
   sphinx-quickstart on Thu Oct 17 09:09:17 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Rockstor
===================

Rockstor (:ref:`rockstor_license`) is a **Linux & BTRFS based** Network Attached
Storage **(NAS) Appliance**, with **Private Cloud** capabilities.
**Rockstor 4 is "Built on openSUSE"**
and :ref:`our_kiwi_ng_installer` is licensed according to the
:ref:`installer_license`.
**We focus on easy-install, setup, and use.**

We extend our advanced NAS features, via Docker, to host an ever growing range
of easy to install apps we call :ref:`rockons_intro`.
This in turn moves us nicely into the realms of a private cloud server.

See our :ref:`features_overview` section for a list of features & capabilities:
available and planned.

Rockstor 4 can be installed on commodity x86_64 and ARM64 hardware.
AArch64 server compatibility relies on
`Embedded Boot <https://github.com/ARM-software/ebbr>`_ or
`Server boot <https://github.com/ARM-software/sbsa-acs>`_ standards, e.g. like
the recently released
`Ten64 <https://www.crowdsupply.com/traverse-technologies/ten64>`_ platform.
The designers of which `Traverse technologies <https://traverse.com.au/>`_
are a valued contributor to our
`rockstor-core <https://github.com/rockstor/rockstor-core>`_,
`rockstor-installer <https://github.com/rockstor/rockstor-installer>`_, and
`rockon-registry <https://github.com/rockstor/rockon-registry>`_ GitHub
repositories. We also have installer profiles for the **Raspberry Pi4** and
**RPi 400** SBCs.

.. toctree::
   :maxdepth: 1

   introduction/features
   installation/install
   interface/uis
   data_loss
   ups-setup/ups_setup
   howtos
   contribute_section
   faq
   support


.. _featurestable:

Features
--------

Below is a summary of all features supported by Rockstor. Features
in *prod* status are production ready where as *beta* indicates a features is
not yet ready for prime time. Some unsupported and planned features are also
listed.

.. table::
   :widths: 45 10 45

   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Feature                                          | status  | notes                                                      |
   +==================================================+=========+============================================================+
   | :ref:`Web-UI <webui>`                            | prod    | System management via browser                              |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Web-UI Live :ref:`dashboard`                     | prod    | Overview of system activity                                |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Online :ref:`Pool<pools>` management             | prod    | Renaming capability planned                                |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Online :ref:`Share<shares>` management           | prod    | Renaming capability planned                                |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`snapshots`                                 | prod    | Instant btrfs subvol snapshots                             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Sharing via :ref:`NFS<nfs>`                      | prod    | Network File System enterprise file access                 |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Sharing via :ref:`Samba<samba_export>`           | prod    | Also known as CIFS / Samba                                 |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Apple Time Machine Backups                       | beta    | :ref:`Samba<samba_export>` options in Rockstor             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`sftp`                                      | prod    | Secure File Transport Protocol                             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Asynchronous Share                               | beta    | Rockstor's Btrfs send/receive wrapper                      |
   | :ref:`Replication<sharereplication>`             |         |                                                            |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | SSH                                              | prod    | Standard bash shell                                        |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`activedirectory`                           | prod    | Rockstor v4 uses sssd                                      |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`ldap`                                      | prod    | Rockstor v4 uses sssd                                      |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`nis`                                       | prod    | Network Information System                                 |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`NTP<ntp>` Client                           | prod    | System time from NTP server                                |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | SNMP                                             | prod    | Enterprise monitoring facility                             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`S.M.A.R.T<smart>`                          | prod    | Disk health information system                             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | IPv4 Network Config via Web-UI                   | prod    | Includes Teaming & Bonding                                 |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | IPv6 Network Config via Web-UI                   | planned | Possible at command line                                   |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Docker Based Plugin System                       | prod    | We call these :ref:`Rock-ons<rockons_intro>`               |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Docker Private Networking                        | beta    | We call these :ref:`Rocknets<rockons_networking>`          |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`Email Alerts<email_notifications>`         | prod    | Via root user email forwarding                             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`Scheduled Tasks<tasks>`                    | prod    | Snapshot Scrub Reboot Shutdown Suspend                     |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`Config Backup and Restore<config_backup>`  | beta    | Reinstate config subset. Rock-ons reinstalled              |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | UPS Support via :ref:`NUT<ups_setup>`            | prod    | Configure a UPS from the Web-UI                            |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Shell in Web-UI                                  | prod    | Via "Shell In A Box"                                       |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | SSL Certificate Entry                            | prod    | Add your own cert via Web-UI                               |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | Log Manager                                      | prod    | View & download system logs                                |
   +--------------------------------------------------+---------+------------------------------------------------------------+
   | :ref:`User<users>` & Group Management            | prod    | Can choose if Rockstor managed                             |
   +--------------------------------------------------+---------+------------------------------------------------------------+
