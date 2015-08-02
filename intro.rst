
Introduction
============

Rockstor is a **free enterprise class file storage platform**. At the
foundation, it is a CentOS flavored Linux operating system tailored for storage
use cases. Rockstor brings together technologies including the Linux kernel,
BTRFS filesystem, SystemTap and our own free software stack to deliver a
compelling solution.

Rockstor's proposition is the following

1. Rockstor provides powerful features, a few of them include dynamic volume
management, snapshots, thin provisioning etc..

2. Rockstor provides smart features including Analytics, data driven
visualization and programmable orchestration.

3. Rockstor is free software and will remain
so.

4. The above unique combination translates to lower capital and operational
costs of your storage infrastructure.


Supported use cases
-------------------

Rockstor addresses the **NAS/Filer** use case. It can be installed on bare
metal or as a virtual machine.


Features
--------

Below is the list of all features supported in Rockstor at a glance. Features
in *prod* status are production ready where as *beta* indicates features not
yet ready for prime time. Some unsupported and planned features are also
listed.

+-----------------------------+---------+--------------------------------+
| Feature                     | support | notes                          |
|                             | status  |                                |
+=============================+=========+================================+
| Online pool management      | beta    |                                |
+-----------------------------+---------+--------------------------------+
| Online share management     | beta    |                                |
+-----------------------------+---------+--------------------------------+
| Unlimited CoW snapshots     | beta    |                                |
+-----------------------------+---------+--------------------------------+
| sharing via NFS(v3 and v4)  | prod    | Network File System cross      |
|                             |         | platform enterprise file access|
+-----------------------------+---------+--------------------------------+
| sharing via SMB             | beta    | also known as CIFS / Samba     |
+-----------------------------+---------+--------------------------------+
| sharing via AFP             | beta    | Apple File Protocol            |
+-----------------------------+---------+--------------------------------+
| WebDAV                      | planned |                                |
+-----------------------------+---------+--------------------------------+
| SFTP                        | beta    | Secure File Transport Protocol |
+-----------------------------+---------+--------------------------------+
| Asynchronous share          | beta    | replicate shares between       |
| replication                 |         | multiple Rockstor appliances   |
+-----------------------------+---------+--------------------------------+
| WebUI                       | prod    | efficient management through   |
|                             |         | Chrome browser                 |
+-----------------------------+---------+--------------------------------+
| SSH                         | prod    | standard bash shell            |
+-----------------------------+---------+--------------------------------+
| RESTful API                 | prod    | integrate applications with    |
|                             |         | Rockstor                       |
+-----------------------------+---------+--------------------------------+
| Active directory            | beta    |                                |
+-----------------------------+---------+--------------------------------+
| LDAP                        | prod    | Lightweight Directory Access   |
+-----------------------------+---------+--------------------------------+
| NIS                         | prod    | Network Information System     |
+-----------------------------+---------+--------------------------------+
| NTP client                  | prod    | set system time from NTP server|
+-----------------------------+---------+--------------------------------+
| SNMP                        | beta    | enterprise monitoring facility |
+-----------------------------+---------+--------------------------------+
| S.M.A.R.T                   | beta    | disk health information system |
+-----------------------------+---------+--------------------------------+
| Smart probes                | beta    | on demand deep insights        |
+-----------------------------+---------+--------------------------------+
| Smart probe data            | beta    | visualization of on demand     |
| visualization               |         | deep insights                  |
+-----------------------------+---------+--------------------------------+
| NFS server side analytics   | beta    |                                |
+-----------------------------+---------+--------------------------------+
| Docker based Plugin system  | beta    | We call these Rock-ons         |
+-----------------------------+---------+--------------------------------+
| Critical event alerts       | planned |                                |
+-----------------------------+---------+--------------------------------+
| Scheduled tasks             | beta    | snapshots and scrubs           |
+-----------------------------+---------+--------------------------------+
| Config Backup and Restore   | beta    | for recovery / migration use   |
+-----------------------------+---------+--------------------------------+