.. _snapshots:

Snapshots
=========

Snapshots are point in time representations of :ref:`shares`. Here are some
benefits of Snapshots.

* They can be created and deleted instantly.
* They take up very little extra space when created.
* They can be read-only or read-write
* Files present in a Share when a Snapshot is taken are preserved in it even if
  they are deleted in the original Share afterwards.
* A Snapshot takes up extra space only to store files deleted in its Share
  over time.
* A Share can be rolled back in time to one of it's Snapshots
* A Snapshot can be cloned to become a brand new Share
* Many Snapshots can be taken overtime

At the time of creation, a Snapshot does not take up extra space as it merely
point to the same contents of the Share. But if a file is later deleted from
the Share, it still persists in the Snapshot. This feature makes it possible to
retrieve certain deleted files of a Share from it's Snapshots.

Snapshots can be created read-only or read-write. Since Snapshots are
predominantly used to retrieve deleted files, read-only Snapshots are suggested
for this purpose.

Internally, Snapshots are BTRFS Snapshots. To find out more about internal
implementation, go `here
<https://forum.rockstor.com/t/internal-implementation-of-pools-shares-snapshots-and-clones/453>`_.

Snapshot related operations can be managed from the **Snapshots** screen listed
under the **Storage** tab of the Web-UI.

.. _createsnapshot:

Creating a Snapshot
-------------------

To create a Snapshot, use the **Create Snapshot** button and submit the form
with your chosen input values. There is a tooltip for each input field with
more help.


.. _schedulesnapshot:

Scheduling Snapshots
--------------------

Using Rockstor's :ref:`tasks` system it is also possible to schedule Snapshot
creation automatically at a predefined time and frequency similar to cronjobs
in Linux. To find out more, see :ref:`snapshottask`.

You can also schedule Snapshots such that the frequency decreases over
time. For example, you can schedule 12 hourly Snapshots during the day, 4
weekly, 12 monthly and 2 yearly and so on. To find out more, see
:ref:`mpsnapshots`.

Deleting a snapshot
-------------------

Snapshots can be easily deleted from the Web-UI. To delete a single Snapshot,
use the corresponding **trash** icon for it in the **Snapshots** screen under
the **Storage** tab. To delete multiple Snapshots, select them and use the
**Delete** button at the bottom.

.. image:: /images/interface/storage/delete_snapshot.png
   :width: 100%
   :align: center


.. _clonesnapshot:

Cloning a Snapshot
------------------

A Snapshot can be cloned to create a brand new Share. This is useful if you
wish to create a new Share that is an exact copy of the Snapshot.

To clone a Snapshot, click on the clone icon in the **Actions** column of the
Snapshot table.

To clone a Share, see :ref:`cloneshare`.

.. _rollingbackshare:

Rolling back a Share
--------------------

A Share can be rolled back to any of its snapshots. This is useful if you wish
to restore a Share to it's previous state represented by its snapshots

Click on the **Rollback** button in the Share's detail screen.

.. note::
  Shares that are exported through NFS or Samba cannot be rolled back. The NFS
  or Samba exports must be deleted before the Share can be rolled back.
