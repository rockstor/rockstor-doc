.. _snapshots:

Snapshots
=========

A Snapshot of a Share represents the Share from a particular point in time, the
time when Snapshot is created. At the time of creation, it does not take up
extra space as it merely point to the same contents of the Share. But if a file
is later deleted from the Share, it still persists in the Snapshot. This
feature makes it possible to retrieve certain deleted files of a Share from
it's Snapshots.

Snapshots can be created read-only or read-write. Since Snapshots are
predominantly used to retrieve deleted files, read-only Snapshots are suggested
for this purpose.

Internally, Snapshots are BTRFS Snapshots. To find out more about internal
implementation, go `here
<http://forum.rockstor.com/t/internal-implementation-of-pools-shares-snapshots-and-clones/453>`_.

Snapshot related operations can be managed from the **Snapshots** screen listed
under the **Storage** tab of the Web-UI.

.. _createsnapshot:

Creating a Snapshot
-------------------

A snapshot can be created on demand or on a schedule. Click on **Create** button and submit the Snapshot creation form to create one as shown in this video.

.. youtube:: https://www.youtube.com/watch?v=QTQePwrYMS0

There is also a **Schedule** button next to **Create** using which you can
schedule periodic Snapshots as shown in this video.

.. youtube:: https://www.youtube.com/watch?v=PA0hneCq-AE

You can also refer to :ref:`snapshottask` for more information.


.. _clonesnapshot:

Cloning a Snapshot
------------------

A Snapshot can be cloned to create a brand new Share. This is useful if you
wish to create a new Share that is an exact copy of the Snapshot.

To clone a Snapshot, click on the clone icon in the **Actions** column of the
Snapshot table as shown in this video.

.. youtube:: https://www.youtube.com/watch?v=aySlQCx65GM

To clone a Share, see :ref:`cloneshare`.

Rolling back a Share
--------------------

A Share can be rolled back to any of its snapshots. This is useful if you wish
to restore a Share to it's previous state represented by its snapshots

Click on the **Rollback** button in the Share's detail screen as shown in this video.

.. youtube:: https://www.youtube.com/watch?v=r0SbCZ_kEBg

*Note:* Shares that are exported through NFS or Samba cannot be rolled back. The
NFS or Samba shares should be deleted before the share can be rolled back.
