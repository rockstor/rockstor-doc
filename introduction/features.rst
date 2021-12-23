.. _features_overview:

Introduction
============

.. toctree::
   :caption: Further details are in the following sections:
   :maxdepth: 1

   concepts


User friendly Web-UI
--------------------

Rockstor Web-UI is designed to efficiently manage large and complex storage
infrastructure. It is also designed for intuitive user experience, which
eliminates the need to read extensive documentation and learning to be able to
use it. Below are the feature highlights. See :ref:`webui` for a more detailed
explanation.

* Secure access via HTTPS.

* Efficiently perform storage management including pool and share creation,
  snapshots, NFS exports, etc...

* Efficiently perform necessary system management including
  directory services, user management, etc...

* Customize dashboard per admin user by choosing relevant widgets and their
  layout.

* Visualize smart probe data for deeper insights.

* Manage other Rockstor appliances by quick switching.

* Extend functionality using Docker-based plugins called *Rock-ons*.

* Contact Rockstor support.

Online Disk Management
----------------------

* :ref:`Rescan <scandisks>` the system for any new disks and make them
  available instantly for pools (hardware support may be necessary).

* :ref:`Visualize <dashboard>` top disks based on activity.

* Act on disk alerts, repair and remove disks from the system if necessary
  without unnecessary disruption. See our :ref:`disks` section for more
  details.

Online Pool Management
----------------------

* :ref:`Create pools <createpool>` instantly using the Web-UI or CLI.

* :ref:`Resize pools <poolresize>` online by adding or removing whole disk
  drives.

* :ref:`Schedule scrub <poolscrub>` operations for periodic maintenance.

Online Share and Snapshot Management
------------------------------------

* :ref:`Create a share <createshare>` instantly using the Web-UI or CLI.

* :ref:`Resize shares online <resizeshare>`, thin provision or over provision
  according to your needs.

* Export shares via :ref:`NFS <nfs>`, :ref:`Samba <samba_export>`, and
  :ref:`SFTP <sftp>` protocols.

* :ref:`Create snapshots <createsnapshot>` for shares instantly or
  :ref:`schedule snapshots <schedulesnapshot>` to be created periodically.

* Create unlimited number of snapshots for a given share.

* Toggle snapshot visibility to the end user via NFS or Windows
  :ref:`Shadow Copy <windowsshadowcopy>`.

* :ref:`Rollback a share <rollingbackshare>` to one of its snapshots.

Share Replication
-----------------

* Replicate shares from one Rockstor appliance to others. See our
  :ref:`sharereplication` section for further details.

Directory Services
------------------

* :ref:`ldap`

* :ref:`nis`

* :ref:`activedirectory`

NFS Analytics
-------------

Server side NFS analytics are available with Rockstor's smart probes. These
probes can be run on demand to collect insightful information about NFS
workloads. The following probes are available

* Call metadata for the entire system.

* Share specific call metadata.

* Client specific call metadata.

* Call metadata for each pair of Client and Share

* Call metadata with specific uid and gid information.


A Docker-based Plugin System
----------------------------

Used to extend Rockstor's features; we call these :ref:`rockons_intro`.

Email Notifications
-------------------

Rockstor includes an easy to use Postfix configuration facility to enable
:ref:`email_notifications` on system events and drive health status.

S.M.A.R.T Drive Monitoring
--------------------------

The S.M.A.R.T technology in most modern drives is integrated into Rockstor so
that many aspect of a drive's status can be examined. It is possible, thanks to
smartmontools, to receive emails via Rockstor's notification system when drives
have heath issues or when they reach a warning or critical temperature, or even
if their temperature varies by more than a configured value over time.

See our guide on using :ref:`smart` in Rockstor.

UPS Managed Shutdown
--------------------

By integrating the well established `NUT <https://networkupstools.org/>`_
software package and providing a Web-UI, :ref:`rockstor_nut_config` aims to
make UPS setup easy and straight forward -- Defaulting to graceful system
Shutdown in the event of power outage and a UPS battery low state. If
:ref:`email_notifications` have been enabled, then notable power events will be
part of these notifications.

Support
-------

Free and commercial support for Rockstor are available. See :ref:`support` for
more information.
