Feature Overview
================

User friendly Web-UI
--------------------

Rockstor Web-UI is designed to efficiently manage large and complex storage
infrastructure. It is also designed for intuitive user experience, which
eliminates the need to read extensive documentation and learning to be able to
use it. Below are the feature highlights. See :ref:`webui` for a more detailed
explanation.

* Secure access via HTTPS.

* Efficiently perform storage management including pool and share
  creation, snapshots, nfs exports, etc..

* Efficiently perform necessary system management including
  directory services, user management etc..

* Customize dashboard per admin user by choosing relevant widgets and their
  layout.

* Visualize smart probe data for deeper insights.

* Manage other Rockstor appliances by quick switching.

* Extend functionality using Docker-based plugins called *Rock-ons*

* Contact Rockstor support

Online Disk Management
----------------------

* Rescan the system for any new disks and make them available instantly for
  pools. (Hardware support may be necessary)

* Visualize top disks based on activity

* Act on disk alerts, repair and remove disks from the system if necessary
  without unnecessary disruption.

Online Pool Management
----------------------

* Create pools instantly using the Web-UI or CLI.

* Resize pools online by adding or removing whole disk drives.

* Schedule scrub operations for periodic maintenance

Online Share and Snapshot Management
------------------------------------

* Create shares instantly using the Web-UI or CLI.

* Resize pools online, thin provision or over provision according to your
  needs.

* Export shares via NFS, SMB, and SFTP protocols.

* Create snapshots for shares instantly or schedule snapshots to be created
  periodically.

* Create unlimited number of snapshots for a given share.

* Toggle snapshot visibility to the end user via NFS or Windows :ref:`Shadow Copy <windowsshadowcopy>`.

* Rollback a share to one of it's snapshots.

Share Replication
-----------------

* Replicate shares from one Rockstor appliance to others.

Directory Services
------------------

* LDAP

* NIS

* AD

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

See :ref:`analytics` for more details.

A Docker based Plugin system
----------------------------

Used to extend Rockstors features; we call these :ref:`rockons_intro`

Email notifications
-------------------

Rockstor includes an easy to use Postfix configuration facility to enable
:ref:`email_notifications` on system events and drive health status.

S.M.A.R.T drive monitoring
--------------------------

The S.M.A.R.T technology in most modern drives is integrated
into Rockstor so that many aspect of a drive's status can be examined. It is
possible, thanks to smartmontools, to receive emails via Rockstor's notification
system when drives have heath issues or when they reach a warning or critical
temperature; or even is their temperature varies by more than a configured
value over time.

UPS managed Shutdown
--------------------

By integrating the well established `NUT <https://networkupstools.org/>`_
software package and providing a Web-UI, :ref:`rockstor_nut_config` aims to
make UPS setup easy and straight forward. Defaulting to graceful system
Shutdown in the event of power outage and a UPS battery low state. If
:ref:`email_notifications` have been enabled then power events of note will
be part of these notifications.

Support
-------

Free and commercial support is available for Rockstor. See :ref:`support` for
more information.
