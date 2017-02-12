..  _disks:

Disks
=====

Disks can be Hard Disk Drives(HDDs), Solid State Drives(SSDs), USB drives,
virtual disks from a hypervisor or open LUKS mount, or even sdcards. Rockstor
supports and recommends whole disk btrfs (ie no partitions or partition table),
but can also recognise and configure btrfs pool members in partitions; but
this is not encourages. The recommendation to use whole disk btrfs pool members
arises from the simplification afforded by removing the partition 'layer' all
together. This way partition types, partition table types, sizes relative to
whole disk etc are all made irrelevant as each disk is simply and wholly a pool
member and only a pool member. I.e. Keep it Simple and Straightforward (KISS).

Disk related operations such as S.M.A.R.T monitoring, data importing etc. can
be managed from the **Disks** page listed under the **Storage** tab of the
Web-UI. This page is an overview of disks **currently or previously known** to
the system and is essentially a table where each row is an entry for a single
real or virtual drive. **Previously attached drives** that are no longer found
to be attached are re-named to **detached-<random-string>**. Attached devices
are named according to their boot to boot stable udev assigned by-id names (ie
/dev/disk/**by-id** entries). All devices require and are tracked by their
unique **serial number** which allows for consistent settings even when a disk
is moved from one pool to another (via sequential pool resize operations).

*Table links from left to right:-*

* **Drive 'by-id' Name** - see drive's **SMART data** / status.
* **Bulb Icon** - flash drive's activity light to **identify it's physical location**.
* **Pool Name** - :ref:`pools` specific **details** page.
* **Pause Drive** - immediate **spin down** (suspend mode).
* **Hour glass** - configure **auto spin down timer** given no activity.
* **S.M.A.R.T Pen Icon** - configure **custom smart options**.
* **S.M.A.R.T Switch** - enable or disable for each device.

*Buttons:-*

* **Rescan** - the hardware for any supported drives, see :ref:`scandisks` below.
* **S.M.A.R.T** - system wide **custom configuration** (advanced).

.. image:: images/disks_overview.png
   :width: 100%
   :align: center

The disks table can be sorted by individual columns by clicking the small
up/down arrows displayed in each column header.

With a large numbers of disks the table will be paginated and the current page
number will be displayed below the table along with **Prev** and **Next**
buttons.

..  _scandisks:

Scan for Disk Changes
---------------------

Clicking the **Rescan** button forces an update of the Disk table. This is
particularly useful if a drive has been added or removed since Rockstor was
power-on ie *hot plugged/unplugged*. It is recommended that this action be
taken just prior to *removing detached devices* to ensure the table contents
is freshly updated.

..  _btrfsdisk:

Existing whole disk BTRFS
-------------------------

If after scanning or after a Rockstor reinstall the system finds an
**existing whole disk BTRFS filesystem** a small **down arrow icon** next to
the drive name will indicate this. This down arrow can be used to import the
discovered btrfs filesystem. In this situation there are two
options:

* **import** the exiting **whole disk btrfs** filesystem - see :ref:`reinstall_import_data` in our :ref:`reinstall` HowTo

*or*

* **wipe the disk** and re-use as if new - see :ref:`wipedisk` below


..  _partitioneddisks:

Partitioned disks
-----------------

Rockstor works only with whole disk drives that do not contain a partition table.
If a disk has a partition table, it is suspected to have data and
Rockstor doesn't allow it's usage until the partition table is explicitly
wiped. Such disks are displayed with a little **gear icon** next to their
name. Relevant help text is displayed upon mousing over this icon indicating
the above restriction. See the next section :ref:`wipedisk` for the procedure.

.. image:: images/partitioned_disk.png
   :scale: 65 %
   :align: center

..  _wipedisk:

Wiping a Partitioned Disk
-------------------------

Before a partitioned or previously used disk can be deployed it's partition
table or existing whole disk filesystem needs to be wiped, as
indicated by the help text above. Click on the **gear icon** and a popup confirmation
dialog will be displayed. Upon confirmation, the entire disk will be wiped and
ready for use as shown below.

**Please note that whole disk btrfs filesystems can also be imported, see:**
:ref:`btrfsdisk`

.. image:: images/disk_wipe_partition.png
   :scale: 65 %
   :align: center

Broken or removed disks
-----------------------

Rockstor detects when a disk drive goes offline (damaged or removed from the
system) and marks it as such. This is indicated by a **little trash icon** next
to the disk name and relevant help text is displayed upon mousing over this icon.

.. image:: images/disk_offline.png
   :scale: 65 %
   :align: center

In order to remove the disk from Rockstor click on the trash icon and a popup
confirmation dialog is displayed. Upon confirmation, the disk will be removed
as shown below.

.. image:: images/disk_remove.png
   :scale: 65 %
   :align: center
