.. Rockstor documentation master file, created by
   sphinx-quickstart on Thu Oct 17 09:09:17 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Rockstor
===================

Rockstor is a **Linux/BTRFS based Network Attached Storage (NAS) and private
cloud solution**. It is distributed as a CentOS flavored Linux
operating system with a newer kernel and Rockstor application software bundled
together to easily install a system and manage your data.

Rockstor supports advanced NAS features powered by BTRFS and other Linux
technologies. It also supports hosting of various apps based on Docker
technology which extends its feature set beyond NAS and transforms the system
into a private cloud server. See :ref:`features_overview` for a full list
of features available and planned.

Rockstor can be installed on commodity hardware or as a virtual machine on
hypervisors like Xen, KVM and VMWare.

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
