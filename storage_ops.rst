
Storage operations
==================

Various storage operations including creating pools, shares etc.. are possible
with few clicks on the webui. Click on the Storage tab of the webui to enter
the main screen for all storage operations. Below is a collection of most
common operations.

Scan disks
----------

Inside the Storage screen, Disks view is selected by default. In this view,
already existing disks in the system are displayed in a table. The table
consists of one row per disk and each row has three columns. The first column
displays the disk's name. The second column displays it's capacity and the
third column displays the name of the pool the disk belongs to.

.. image:: disks_rescan.png
   :height: 75pt
   :width: 100pt
   :align: center

Click the **Rescan** button to scan for any new disks added to the system.

If there are large number of disks in the system, the table is paginated and
the current page number is displayed below the table along with **Prev** and
**Next** buttons.

The display can be sorted by disk names, capacity or pool by clicking small
up/down arrows displayed in each column header.

Partitioned disks
^^^^^^^^^^^^^^^^^
Rockstor only works with whole disks that do not contain a partition table. If
a disk has a partition table, it is suspected to have data. Such disk is
displayed in the table with a little sprocket icon next to it. If you mouse
over the sprocket icon, relevant help text is displayed.

.. image:: partitioned_disk.png
   :height: 75pt
   :width: 100pt
   :align: center

Inorder to use the disk, the partition table needs to be wiped as indicated by
the help text. Simply click on the sprocket icon and a popup confirmation
dialog is displayed.

.. image:: disk_wipe_partition.png
   :height: 75pt
   :width: 100pt
   :align: center

Click OK to confirm. The partition table is wiped and the disk will be shown in
the table, ready to be used.

Broken or removed disks
^^^^^^^^^^^^^^^^^^^^^^^
Rockstor detects when a disk drive goes offline(broken or removed from the system) and
marks it as such. This is indicated by the little trash icon next to the
disk. If you mouse over the trash icon, relevant help text is displayed.

.. image:: disk_offline.png
   :height: 75pt
   :width: 100pt
   :align: center

Inorder to remove the disk from Rockstor, click on the trash icon and a popup
confirmation dialog is displayed.

.. image:: disk_remove.png
   :height: 75pt
   :width: 100pt
   :align: center

Click OK to confirm. The disk will be removed and no longer shown in the table.

Create pool
-----------



Disk operations
---------------

managing disks, adding new ones, removing bad ones

Pool operations
---------------

pool management, resizing etc..

Share operations
----------------

NFS exports
-----------
