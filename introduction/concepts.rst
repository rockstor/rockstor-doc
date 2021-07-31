..  _Concepts:


Basic Concepts
==============

Disk
----

A disk is a block device that is usable by Rockstor. Disks can be locally
attached SCSI or SATA drives or can be SAN backed block devices, there is also
increasing support for some virtual block devices for when Rockstor is
installed in a virtual machine.

N.B. Rockstor only works with whole drives and not partitions. If a disk has
partitions it is displayed in the list of available disks but is
unusable. However the UI does provide a facility to remove any existing
partition tables so that those disks might become usable.

Disks can be added online as long as it is supported by the underlying
hardware. Rockstor can rescan to detect new disks and make them available.  
See our :ref:`disks` section for a more detailed explanation.

Pool
----

A pool is a collection of disks with predefined redundancy strategy.  Available
redundancy options include RAID0, RAID1 and RAID10. Redundancy strategy must be
chosen during pool creation but cannot be changed afterwards.

A pool can be resized at anytime by adding or removing drives. Obviously,
success of these operations depends on the state of the pool including current
usage.  See our :ref:`pools` section for a more detailed explanation.

Share
-----

A share is created by carving out a chunk from a pool. Shares can be resized
at a later time as well as exported via NFS, SMB, or SFTP protocols.
See our :ref:`shares` section for a more detailed explanation.

Snapshot
--------

A snapshot is a read-only point in time copy of a share. Since BTRFS is a CoW
filesystem, snapshots are created instantly and take up no extra space when
created.  See our :ref:`snapshots` section for a more detailed explanation.

Web UI
------

The easiest way to manage your storage with Rockstor is via it's web-ui. It can
be accessed by visiting the appliance's management IP over https using the
Firefox browser. Note that other browsers are not supported.  
See our :ref:`webui` section for a more detailed explanation.

Secure Shell
------------

Console access to Rockstor is possible by logging in as one of the admin users
using SSH.  During normal operations this should not be required but is
provided for advanced configurations and development purposes.

Smart Manager
-------------

Smart Manager includes the dashboard of WebUI, smart probes, analytics and
other features that increase operational efficiency of the storage
infrastructure.


Rock-ons
--------

This is our made-up term to reference the built-in
`docker <https://www.docker.com/>`_ based plugin system.
See our :ref:`rockons_intro` section for a more detailed explanation.
