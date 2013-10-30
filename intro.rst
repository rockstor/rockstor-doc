
Introduction
============

Rockstor is a **free enterprise class storage platform**. At the foundation, it
is a CentOS flavored Linux operating system tailored for storage
usecases. Rockstor brings together technologies including the Linux kernel,
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
costs of your storage infratructure.

Supported usecases
------------------

Rockstor addresses the **NAS/Filer** usecase. It can be installed on bare
metal or as a virtual machine.


Features
--------

Below is the list of all features supported in Rockstor at a glance. Features
in *prod* status are production ready where as *beta* indicates features not
yet ready for primetime. Some unsupported and planned features are also listed
for clarity.

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
| sharing via NFS(v3 and v4)  | prod    |                                |
+-----------------------------+---------+--------------------------------+
| sharing via SMB             | beta    |                                |
+-----------------------------+---------+--------------------------------+
| WebDAV                      | planned |                                |
+-----------------------------+---------+--------------------------------+
| FTP/SFTP                    | planned |                                |
+-----------------------------+---------+--------------------------------+
| Asynchronous share          | beta    | replicate shares between       |
| replication                 |         | multiple Rockstor appliances   |
+-----------------------------+---------+--------------------------------+
| WebUI                       | prod    | efficient management through   |
|                             |         | Firefox browser                |
+-----------------------------+---------+--------------------------------+
| CLI                         | beta    |                                |
+-----------------------------+---------+--------------------------------+
| RESTful API                 | prod    | integrate applications with    |
|                             |         | Rockstor                       |
+-----------------------------+---------+--------------------------------+
| Active directory            | beta    |                                |
+-----------------------------+---------+--------------------------------+
| LDAP                        | prod    |                                |
+-----------------------------+---------+--------------------------------+
| NIS                         | prod    |                                |
+-----------------------------+---------+--------------------------------+
| Smart probes                | beta    | ondemand deep insights         |
+-----------------------------+---------+--------------------------------+
| Smart probe data            | beta    |                                |
| visualization               |         |                                |
+-----------------------------+---------+--------------------------------+
| NFS server side analytics   | beta    |                                |
+-----------------------------+---------+--------------------------------+
| Critical event alerts       | planned |                                |
+-----------------------------+---------+--------------------------------+
| Scheduled tasks             | planned | snapshots, replication, scurbs |
+-----------------------------+---------+--------------------------------+
