.. Rockstor documentation master file, created by
   sphinx-quickstart on Thu Oct 17 09:09:17 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Rockstor
===================

Rockstor is an Open Source GPLv2 + **Linux & BTRFS based** Network Attached
Storage **(NAS) Appliance**, with **Private Cloud** capabilities.
**Rockstor 4 is "Built on openSUSE"** while our near legacy 3 and older
versions used CentOS 7 with newer elrepo kernels.
Our focus is on easy install and use.

We extend our advanced NAS features, via docker, to host an ever growing range
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
**RPi 400** SBCs: the latter requires at least a Leap 15.3 profile.

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

+--------------------------------+---------+--------------------------------+
| Feature                        | status  | notes                          |
|                                |         |                                |
+================================+=========+================================+
| Online pool management         | beta    |                                |
+--------------------------------+---------+--------------------------------+
| Online share management        | beta    |                                |
+--------------------------------+---------+--------------------------------+
| CoW snapshots                  | beta    |                                |
+--------------------------------+---------+--------------------------------+
| sharing via NFS(v3 and v4)     | prod    | Network File System cross      |
|                                |         | platform enterprise file access|
+--------------------------------+---------+--------------------------------+
| sharing via SMB                | beta    | also known as CIFS / Samba     |
+--------------------------------+---------+--------------------------------+
| Time Machine backups           | beta    | via Samba exports              |
+--------------------------------+---------+--------------------------------+
| WebDAV                         | planned |                                |
+--------------------------------+---------+--------------------------------+
| SFTP                           | beta    | Secure File Transport Protocol |
+--------------------------------+---------+--------------------------------+
| Asynchronous share             | beta    | replicate shares between       |
| replication                    |         | multiple Rockstor appliances   |
+--------------------------------+---------+--------------------------------+
| WebUI                          | prod    | efficient management through   |
|                                |         | Chrome browser                 |
+--------------------------------+---------+--------------------------------+
| SSH                            | prod    | standard bash shell            |
+--------------------------------+---------+--------------------------------+
| RESTful API                    | prod    | integrate applications with    |
|                                |         | Rockstor                       |
+--------------------------------+---------+--------------------------------+
| Active directory               | beta    |                                |
+--------------------------------+---------+--------------------------------+
| LDAP                           | prod    | Lightweight Directory Access   |
+--------------------------------+---------+--------------------------------+
| NIS                            | prod    | Network Information System     |
+--------------------------------+---------+--------------------------------+
| NTP client                     | prod    | set system time from NTP server|
+--------------------------------+---------+--------------------------------+
| SNMP                           | beta    | enterprise monitoring facility |
+--------------------------------+---------+--------------------------------+
| S.M.A.R.T                      | beta    | disk health information system |
+--------------------------------+---------+--------------------------------+
| Docker based Plugin system     | beta    | We call these Rock-ons         |
+--------------------------------+---------+--------------------------------+
| Critical event alerts          | beta    | via email notification system  |
+--------------------------------+---------+--------------------------------+
| Scheduled tasks                | beta    | snapshots and scrubs           |
+--------------------------------+---------+--------------------------------+
| Config Backup and Restore      | beta    | for recovery / migration use   |
+--------------------------------+---------+--------------------------------+
| UPS support via NUT            | beta    | Configure a UPS from the GUI   |
+--------------------------------+---------+--------------------------------+
