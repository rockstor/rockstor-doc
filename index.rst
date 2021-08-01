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

+--------------------------------+---------+---------------------------------+
| Feature                        | status  | notes                           |
+================================+=========+=================================+
| Web-UI                         | prod    | System management via browser   |
+--------------------------------+---------+---------------------------------+
| Web-UI Live Dashboard          | prod    | Overview of system activity     |
+--------------------------------+---------+---------------------------------+
| Online Pool management         | prod    | Re-naming capability planned    |
+--------------------------------+---------+---------------------------------+
| Online Share management        | prod    | Re-naming capability planned    |
+--------------------------------+---------+---------------------------------+
| Snapshots                      | prod    | Instant btrfs subvol snapshots  |
+--------------------------------+---------+---------------------------------+
| Sharing via NFS                | prod    | Network File-System cross       |
|                                |         | platform enterprise file access |
+--------------------------------+---------+---------------------------------+
| Sharing via SMB                | prod    | Also known as CIFS / Samba      |
+--------------------------------+---------+---------------------------------+
| Apple Time Machine Backups     | beta    | Samba options in Rockstor v4    |
+--------------------------------+---------+---------------------------------+
| SFTP                           | prod    | Secure File Transport Protocol  |
+--------------------------------+---------+---------------------------------+
| Asynchronous Share             | beta    | Replicate btrfs subvols between |
| Replication                    |         | multiple Rockstor appliances    |
+--------------------------------+---------+---------------------------------+
| SSH                            | prod    | Standard bash shell             |
+--------------------------------+---------+---------------------------------+
| Active Directory               | prod    | Rockstor v4 uses sssd           |
+--------------------------------+---------+---------------------------------+
| LDAP                           | prod    | Rockstor v4 uses sssd           |
+--------------------------------+---------+---------------------------------+
| NIS                            | prod    | Network Information System      |
+--------------------------------+---------+---------------------------------+
| NTP Client                     | prod    | System time from NTP server     |
+--------------------------------+---------+---------------------------------+
| SNMP                           | prod    | Enterprise monitoring facility  |
+--------------------------------+---------+---------------------------------+
| S.M.A.R.T                      | prod    | Dsk health information system   |
+--------------------------------+---------+---------------------------------+
| IPv4 Network Config via Web-UI | prod /  | Includes Teaming & Bonding /    |
| / IPv6                         | planned | IPv6 currently disabled at boot |
+--------------------------------+---------+---------------------------------+
| Docker Based Plugin System     | prod    | We call these Rock-ons          |
+--------------------------------+---------+---------------------------------+
| Docker Private Networking      | beta    | We call these Rocknets, v4 only |
+--------------------------------+---------+---------------------------------+
| Email Alerts                   | prod    | Via root user email forwarding  |
+--------------------------------+---------+---------------------------------+
| Scheduled Tasks                | prod /  | Snapshots & Scrubs /            |
|                                | beta    | Reboot, Shutdown & Suspend.     |
+--------------------------------+---------+---------------------------------+
| Config Backup and Restore      | beta    | Reinstate subset of config.     |
|                                |         | Rock-ons auto reinstalled.      |
+--------------------------------+---------+---------------------------------+
| UPS Support via NUT            | prod    | Configure a UPS from the Web-UI |
+--------------------------------+---------+---------------------------------+
| Shell in Web-UI                | prod    | Via "Shell In A Box"            |
+--------------------------------+---------+---------------------------------+
| SSL Certificate Entry          | prod    | Add your own cert via Web-UI    |
+--------------------------------+---------+---------------------------------+
| Log Manager                    | prod    | View & download system logs     |
+--------------------------------+---------+---------------------------------+
| User & Group Management        | prod    | Can choose if Rockstor managed  |
+--------------------------------+---------+---------------------------------+
