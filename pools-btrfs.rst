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

.. _createpool:

Creating a Pool
---------------

Only whole disk drives can be used to create Pools. But they don't have to be
of the same size, which is a great feature of BTRFS. Disks that are partitioned
with other filesystems including BTRFS won't be touched. Whole disks with BTRFS
created outside of Rockstor or from a previous install, can however be
imported. For more information, see :ref:`reinstall_import_data`.

Click on **Create Pool** button and submit the create pool form to create a
pool. There is a tooltip for each input field to help you choose appropriate
parameters. Here's a video showing this operation.

.. youtube:: https://www.youtube.com/watch?v=T5sg8xSoH1E


.. _redundancyprofiles:

Redundancy profiles
^^^^^^^^^^^^^^^^^^^



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

* **zlib**: Provides slower but higher compression ratio. You can find out
  more from `zlib.net <http://www.zlib.net/manual.html>`_.
* **lzo**: A faster compression algorithm but provides lower ratio compared to
  **zlib**. You can find out more from `oberhumer.com
  <http://www.oberhumer.com/opensource/lzo/>`_.


Mount Options
^^^^^^^^^^^^^

These are optional and meant for more advanced users to provide BTRFS specific
mount options. Since a Pool is a filesystem, it is mounted with default options
which can be altered by providing one or more of the following. You can find
out more about each option from the `btrfs wiki mount options section
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

.. _poolresize:

Pool resizing
-------------

A really cool feature in Pool management(powered by BTRFS) is the ability to
add or remove disks and change redundancy profile online without access
disruption. You can resize a Pool easily from the Web-UI for one of the
following reasons

1. To change it's redundancy profile. For example, to go from a RAID10 to
   RAID1. See :ref:`poolraidchange`.

2. To add more disks and increase it's capacity. See :ref:`pooladddisks`.

3. To remove disks and decrease capacity. Removed disks can be reused for other
   Pools. See :ref:`poolremovedisks`.

Pool resize is an online operation that does not cause access
disruption. However, depending on size of the Pool, it could take a long time
to finish.

.. _poolraidchange:

Redundancy profile changes
^^^^^^^^^^^^^^^^^^^^^^^^^^

You can change :ref:`redundancyprofiles` online with very few
restrictions. This video shows how to change a Pool from RAID1 to RAID10.

.. youtube:: https://www.youtube.com/watch?v=DouOx8gX5yE

.. _pooladddisks:

Adding Disks
^^^^^^^^^^^^

Disks can be added to a Pool online and expand capacity.  This video shows how
to expand a RAID1 Pool by adding three disks.

.. youtube:: https://www.youtube.com/watch?v=E37rzWcwGu0

.. _poolremovedisks:

Removing Disks
^^^^^^^^^^^^^^

Disks can be removed from a Pool online similar to adding Disks. However, since
it results in reduced capacity, this operation can succeed only if the
resulting capacity after removal is greater than the current usage. This video
shows how to remove two disks from a RAID1 Pool made up of four disks.

.. youtube:: https://www.youtube.com/watch?v=535pxsF16Pk


Pool deletion
-------------

A *Pool* can be deleted as long as it is empty, i.e., there are no *Shares*
remaining in it. So, if you need to delete a Pool, first delete every Share in
it. Then, click on the corresponding **trash** icon for it in the *Pools*
screen under the *Storage* tab of the Web-UI.


.. image:: images/delete_pool.png
   :scale: 65%
   :align: center

A Pool can also be deleted using the **Delete** button inside it's detail
screen.

Scrubbing a Pool
----------------

The scrub operation initiates a BTRFS scrub process in the background. It reads
all data from all disks of the Pool, verifies checksums and fixes corruptions
if detected and possible. To find out more, see the `btrfs wiki scrub section
<https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-scrub>`_.

To start a scrub, go to the Pool's detail page and click on the **Start a new
scrub** button in the Scrubs tab. The button will be disabled during the scrub
process and enabled again once the scrub finishes. The progress of a running
scrub operation is displayed in a table. Refresh the page to update the
information.

A periodic scrub is a proactive strategy to fix errors before too many
accumulate. You can schedule it using the **Scheduled Tasks** screen under
**System** tab of the Web-UI.


Balance a pool
--------------

The balance operation initiates a BTRFS balance process in the background. It
spreads data more evenly across multiple disks of the Pool. It is automatically
triggered after a :ref:`poolresize` operation, which is the main purpose of
this feature. A standalone balance operation is intended for advanced users who
can judge for themselves if it is necessary. To find out more, see the `btrfs
wiki balance section
<https://btrfs.wiki.kernel.org/index.php/FAQ#What_does_.22balance.22_do.3F>`_.

To start a balance, go to the Pool's detail page and click on the **Start a new
balance** button in the **Balances** tab.
