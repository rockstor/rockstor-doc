..  _disksandpools:

Disks and Pools
===============

..  _disksoverview:

Disks Overview
--------------

The WebUI **Disks** subsection of the **Storage** page gives
an overview of disks **currently or previously known** to the Rockstor system.

*Table links from left to right:-*

* **Drive Name** - see that drives **SMART data** / status
* **Bulb Icon** - to flash the drive's activity light ie to **identify its location**
* **Pool Name** - that pools specific **details** page
* **S.M.A.R.T** - enable or disable for each device

*Buttons:-*

* **Rescan** - the hardware for any supported drives, see :ref:`scandisks` below
* **S.M.A.R.T** - system wide **custom configuration** (advanced)

.. image:: disks_overview.png
   :scale: 80%
   :align: center

The disks table can be sorted by individual columns by clicking the small
up/down arrows displayed in each column header.

With a large numbers of disks the table will be paginated and the current page
number will be displayed below the table along with **Prev** and **Next**
buttons.

..  _scandisks:

Scan for new disks
^^^^^^^^^^^^^^^^^^

In the :ref:`disksoverview` (above) clicking the **Rescan** button starts a scan for any
new disks added to the system since the last scan. This is particularly useful
if a drive has been added to the system since Rockstor was power-on ie
*hot plugged*.

..  _btrfsdisk:

Existing whole disk BTRFS
^^^^^^^^^^^^^^^^^^^^^^^^^

If after scanning or after a Rockstor reinstall the system finds an
**existing whole disk BTRFS filesystems** a small **down arrow icon** next to
the drive name will indicate this. This down arrow can be used to import the
discovered btrfs filesystem. In this situation there are two
options:

* **import** the exiting **whole disk btrfs** filesystem - see :ref:`reinstall_import_data` in our :ref:`reinstall` HowTo

*or*

* **wipe the disk** and re-use as if new - see :ref:`wipedisk` below


..  _partitioneddisks:

Partitioned disks
^^^^^^^^^^^^^^^^^

Rockstor works only with whole disk drives that do not contain a partition table.
If a disk has a partition table, it is suspected to have data and
Rockstor doesn't allow it's usage until the partition table is explicitly
wiped. Such disks are displayed with a little **eraser icon** next to their
name. Relevant help text is displayed upon mousing over this icon indicating
the above restriction. See the next section :ref:`wipedisk` for the procedure.

.. image:: partitioned_disk.png
   :scale: 65 %
   :align: center

..  _wipedisk:

Wiping a Partitioned Disk
^^^^^^^^^^^^^^^^^^^^^^^^^

Before a partitioned or previously used disk can be deployed it's partition
table or existing whole disk filesystem needs to be wiped, as
indicated by the help text above. Click on the **eraser icon** and a popup confirmation
dialog will be displayed. Upon confirmation, the entire disk will be wiped and
ready for use as shown below.

**Please note that whole disk btrfs filesystems can also be imported, see:**
:ref:`btrfsdisk`

.. image:: disk_wipe_partition.png
   :scale: 65 %
   :align: center

Broken or removed disks
^^^^^^^^^^^^^^^^^^^^^^^

Rockstor detects when a disk drive goes offline (damaged or removed from the
system) and marks it as such. This is indicated by a **little trash icon** next
to the disk name and relevant help text is displayed upon mousing over this icon.

.. image:: disk_offline.png
   :scale: 65 %
   :align: center

In order to remove the disk from Rockstor click on the trash icon and a popup
confirmation dialog is displayed. Upon confirmation, the disk will be removed
as shown below.

.. image:: disk_remove.png
   :scale: 65 %
   :align: center

|
Pools overview
--------------

A Pool in Rockstor is a set of disk drives combined and represented as a single
volume. Pools have attributes such as redundancy profile and compression to
safeguard and store data efficiently. Pools can be expanded or shrunk by adding
or removing disk drives. In other words, a Pool is a single or multi device
BTRFS filesystem.

Pool related operations can be managed from the **Pools** screen listed under
the **Storage** tab of the Web-UI.


Creating a Pool
^^^^^^^^^^^^^^^

Only whole disk drives can be used to create Pools. But they don't have to be
of the same size, which is a great feature of BTRFS. Disks that are partitioned
with other filesystems including BTRFS won't be touched. Whole disks with BTRFS
created outside of Rockstor or from a previous install, can however be
imported. For more information, see :ref:`reinstall_import_data`.

Click on **Create Pool** button and submit the create pool form to create a
pool. There is a tooltip for each input field to help you choose appropriate
parameters. Here's a video showing this operation.

.. youtube:: https://www.youtube.com/watch?v=T5sg8xSoH1E

Redundancy profiles
^^^^^^^^^^^^^^^^^^^

.. _redundancyprofiles:

All standard BTRFS redundancy profiles are available when creating a pool.

* **Single**: This profile offers no redundancy, and is the only valid option
  for creating a Pool with a single disk drive. It is also recommened if you
  have multiple disks of different sizes, yielding higher total capacity
  compared to **Raid0**. Data is neither mirrored nor striped, so if a disk
  fails, the entire data of the Pool will be lost.

* **Raid0**: Two or more disks can be used with this profile when there is no
  need for redundancy. Both metadata and data are striped across the disks. It
  is recommended for same size disks. If you have different size disks and no
  need for redundancy, **Single** profile provides higher capacity. If a disk
  fails, the entire data of the Pool will be lost.

* **Raid1**: Two or more disks can be used with this profile. And both metadata
  and data are replicated on 2 devices. So a Pool with this profile can sustain
  a single disk failure.

* **Raid5**: Two or more disks can be used with this profile, which supports
  striping + parity. Like **Raid1**, this profile can sustain a single disk
  failure. The BTRFS community consensus is that **Raid5** support is not yet
  fully stable.

* **Raid6**: Three or more disks can be used with this profile, which supports
  striping + dual-parity. Because of dual-parity, a **Raid6** Pool can sustain
  upto two disk failures at the same time.  The BTRFS community consensus is
  that **Raid6** support is not yet fully stable.

* **Raid10**: This is a Raid0 of Raid1 mirrors, with a minimum requirement of
  four disk drives. It offers most redundancy at the cost of capacity where a
  Pool can sustain multiple disk failures at the same time as long as they part
  of different Raid1 groups.


Compression Options
^^^^^^^^^^^^^^^^^^^

Compression can optionally be chosen during Pool creation or it can be set on a
previously created Pool. In the latter scenario, compression is applied only to
data written after it's set.

Compression can also be set at the Share level. If you don't want to enable
compression for all Shares under a Pool, don't enable it at the Pool
level. Instead, selectively enable it on Shares.

Besides not enabling compression at all, there are two additional choices

* **zlib**: Provies slower but higher compression ratio. You can find out more `here <http://www.zlib.net/manual.html>`_.
* **lzo**: A faster compression algorithm but provides lower ratio compared to
  **zlib**. You can find out more `here <http://www.oberhumer.com/opensource/lzo/>`_.


Mount Options
^^^^^^^^^^^^^

These are optional and meant for more advanced users to provide BTRFS specific
mount options. Since a Pool is a filesystem, it is mounted with default options
which can be altered by providing one or more of the following. You can find
out more about each option `here
<https://btrfs.wiki.kernel.org/index.php/Mount_options>`_.

* **alloc_start**
* **autodefrag**
* **clear_cache**
* **commit**
* **compress-force**
* **discard**
* **fatal_errors**
* **inode_cache**
* **max_inline**
* **metadata_ratio**
* **noacl**
* **noatime**
* **nodatacow**
* **nodatasum**
* **nospace_cache**
* **space_cache**
* **ssd**
* **ssd_spread**
* **thread_pool**

|
Resizing a Pool
-------------

You can resize a Pool for one of the following reasons

1. To change it's redundancy profile. For example, to go from a RAID10 to RAID1.

2. To add more disks and increase it's capacity.

3. To remove disks and decrease capacity. Removed disks can be reused for other Pools.

Pool resize is an online operation that does not cause any access
disruption. However, depending on the size of the Pool, it took take a long
time to finish.

A pool can be resized by adding more disks, removing disks or by modifying RAID level. Click on the pool (under 'Name' tab) that you want to resize from the displayed table of pools to enter the detail view. In the detail view, go to the *Overview* tab of the Web-UI that gives the details such as Usage, Compression and Mount Options, Disks in the pool. Now, click on the **Resize** button and a popup form with three options 1) Modify RAID level 2) Add Disks 3) Remove Disks is displayed. Select any one of the options and submit the form.
Upon success, 1) If *Modify RAID level* is selected, then the message *Resize is initiated. A balance process is kicked off to redistribute data. It could take a while. You can check the status in the Balances tab. Its finish marks the success of resize.* is displayed.

	      2) If *Add Disks* is selected, and if disks are available to be added to the pool, then upon success, the added disks are displayed.
	      3) If *Remove Disks* is selected, and if disks are successfully removed, then the correct message is displayed.  [NOTE : Suman to complete]

.. image:: resize_pool.gif
   :scale: 65%
   :align: center

Delete a Pool
-------------

A *pool* can be deleted as long as it is empty, i.e., there are no *shares*
remaining in it.

Go to the Storage tab of the Web-UI and click on *Pools* in the left sidebar to
enter the *Pools* view. In the displayed table of pools, click on the **trash**
icon corresponding to the pool to delete it as shown below.

.. image:: delete_pool1.gif
   :scale: 65%
   :align: center

A pool can also be deleted by clicking the **Delete** button inside it's detail
view.

Scrub a Pool
------------

Over time, a pool could accumulate low level errors relating to
redundancy. Scrubbing is a background process that finds and fixes these errors
and ensures the long life of a pool.

The *pool* scrub operation can take a while depending on the size of the pool. To
start a scrub, go to the pool's detail view and click on the **Start a new scrub** button under the scrub tab.
The button will be disabled during the scrub process and enabled again
once the scrub finishes.

Balance a pool
--------------

click on **Start a new balance**.  [NOTE : Suman to complete the documentation for balances]

Add Share
---------

From a detail view of a pool, you can click **Add Share** button, to create and add a share to the pool you selected.
`
