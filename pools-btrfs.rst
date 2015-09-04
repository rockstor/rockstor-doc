..  _pools:

Pools
=====

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
---------------

You can resize a Pool for one of the following reasons

1. To change it's redundancy profile. For example, to go from a RAID10 to RAID1.

2. To add more disks and increase it's capacity.

3. To remove disks and decrease capacity. Removed disks can be reused for other Pools.

Pool resize is an online operation that does not cause any access
disruption. However, depending on size of the Pool, it could take a long time
to finish. Resizing is simple and can be done using the Web-UI.

This video shows changing the redundancy profile

.. youtube:: https://www.youtube.com/watch?v=T5sg8xSoH1E

This video shows adding disks to a Pool

.. youtube:: https://www.youtube.com/watch?v=T5sg8xSoH1E

This video shows removing disks from a Pool

.. youtube:: https://www.youtube.com/watch?v=T5sg8xSoH1E


Deleting a Pool
---------------

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

Scrubbing a Pool
----------------

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
