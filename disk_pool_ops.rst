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

Create a Pool
-------------

Pool related operations including creating a pool can be done from the *Pools*
view. In the web-ui, click on the *Storage* tab to enter the main Storage
view. Now click on **Pools** in the left sidebar to enter the *Pools* view.
If there are any pools in the system, they are displayed in a table.

If there are a large number of pools, the table will be paginated and the
current page number will be displayed below the table along with **Prev** and
**Next** buttons.

The display can be sorted by individual columns by clicking the small
up/down arrows displayed in each column header.

.. image:: pools_view.gif
   :scale: 65 %
   :align: center

Click on **Create Pool** button and the create pool form will be
displayed. Submit this form to create a new pool as shown below.

.. image:: create_pool.gif
   :scale: 65 %
   :align: center

When creating a new pool, choose the appropriate redundancy from the *Raid
configuration* drop down menu.

Redundancy options
^^^^^^^^^^^^^^^^^^

All standard BTRFS redundancy options are available when creating a pool.

* **Single**: One or more disks can be used. Data is neither mirrored nor
  striped. But metadata is mirrored across drives. Drives of different
  capacities can be used with this configuration.
* **Raid0**: Two or more disks of same size can be used. Both metadata and data
  are striped across the disks.
* **Raid1**: Two or more disks of same size can be used and the configuration applies
  to both data and metadata.
* **Raid10**: This is a Raid0 of Raid1 mirrors. Four or more disks of same size
  can be used and the configuration applies to both data and metadata.

Resize a Pool
-------------

A pool can be resized by adding more disks to it. Go to the Storage tab of the
web-ui and click on *Pools* in the left sidebar to enter the *Pools* view. In
the displayed table of pools, click the pool to be resized to enter the pool
detail view. Now, click on the **Resize** button and a popup form is
displayed. Select disks to be added and submit the form. Upon success, pool's
detail view is dispalyed which lists the new disk(s) added and the resulting
new size of the pool as shown below.

.. image:: resize_pool.gif
   :scale: 65%
   :align: center

Delete a Pool
-------------

A *pool* can be deleted as long as it is empty, i.e., there are no *shares*
remaining in it.

Go to the Storage tab of the web-ui and click on *Pools* in the left sidebar to
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
start a scrub, go to the pool's detail view and click on the **Start scrub**
button. The button will be disabled during the scrub process and enabled again
once the scrub finishes.


