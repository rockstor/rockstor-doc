.. _dataloss:

Data loss Prevention and Recovery in Rockstor
=============================================

There is no single cause of data loss as failures in hardware, software and
user errors can trigger removal or corruption of storage data in different and
sometimes complicated ways.

BTRFS is the underlying filesystem of Rockstor. It is a self correcting
filesystem that prevents data loss from bitrot and provides CoW snapshots and
diffs between them which can be used to efficiently restore files in case of
accidental loss.

BTRFS is also a newer Linux filesystem and is under heavy development. As of
this writing, a lot of functionality has become considerably stable. However,
raid5/6 support is still experimental, more so than all other
features. Overall, BTRFS is still considered experimental even though it's
acceptance increased so much over last few years. In our own experience and in
the context of Rockstor usecases, it has become quite reliable.

We have servers with different types of pools and usecases here at Rockstor
which are constantly put to test. We also rely on Rockstor and BTRFS
communities to report and fix issues and help improve Rockstor.

.. raw:: html

   <div class="alert">
   We strongly recommend that you have a backup of all critical Shares
   on Rockstor to another system.
   </div>

Backup Recommendations
----------------------

If you have critical data on Rockstor, we strongly recommend that you have a
backup. In the near future, BTRFS and hence Rockstor shall become stable enough
to not require this. But as of this writing, we strongly recommend you have
backups. Here are some recommendations.

* Use Rockstor's replication feature to asynchronously and automatically
  replicate important shares on another Rockstor system.
* Use Rockstor's external share backup functionality which rsyncs selected
  shares to an external location on a periodic basis (under development)
* Use your own method to backup important Shares to another external system.

Rockstor Web-UI and Data Loss Monitoring
----------------------------------------

Currently, there is no support for monitoring of drives or pools in
Rockstor. So the web-ui is simply unaware and incapable of notifying potential
problems or failures. It is a high priority for us to improve this aspect of
Rockstor and we are working on it.

At the moment, we suggest that you have your own scripts and methods to detect
any potential failures.

Rockstor also does not support any recovery features at this time. Given the
current state of rapid BTRFS development, we have not added this support as it
may need to fundamentally change again. So wear your Linux ninja hat to
troubleshoot serious data loss problems. Hope this document helps.

Ask Us for Help
---------------

If you are in a data loss scenario, we'd like to help you. Though we cannot
guarantee any recovery, we'll use our expertise to help you as much as
possible. Send an email to support@rockstor.com or ask on our forum.

If you are using Rockstor, you may already know the latest and greatest in
BTRFS in which case you can also seek help on btrfs mailing list.


.. _datalossraid0:

Data loss Prevention and Recovery in RAID0 Pools
------------------------------------------------

A raid0 pool consists of two or more drives and offers no data redundancy. All
drives in a raid0 pool are simply combined to present a single large volume and
data is never duplicated.

If a drive in raid0 fails, the pool becomes completely unusable. The recovery
strategy is to simply delete the pool, replace the failed drive with a new one,
create a brand new pool and restore data from the backup. Here's a detailed
step by step example.

0. Suppose three drives sda, sdb and sdc form a raid0 pool called "mypool".

1. Drive sda fails.

2. umount the pool and any shares belonging to that pool::

     # umount /mnt2/<pool_name|share_name>

3. Delete all shares belonging to "mypool" (from the web-ui)

4. Delete "mypool". (from the web-ui)

5. If your hardware supports drive hotswap, replace the failed drive with a new
   one online. Otherwise, shutdown the machine and replace the drive and start
   it back up.

6. In the disks section of the web-ui, click "Rescan" to identify the new drive
   and delete the old one.

7. Create "mypool" again.

8. Restore all shares from backup.

Currently, Rockstor does not support any cleanup such as deleting Shares from
the damaged pool or deleting the pool itself. Until such support is added,
please contact support@rockstor.com and we'll try to help.

.. _datalossraid1:

Data loss Prevention and Recovery in RAID1 Pools
------------------------------------------------

A raid1 pool in Rockstor consists of exactly two drives. A copy of data on one
drive exists on the other one. So a raid1 pool is simply a two drive mirror.

If one of the drives fails in a raid1 pool, the pool will continue to
function. But there is high risk of losing all data in case the second and only
remaining drive also fails while the failed first drive is not yet replaced.

The recovery strategy is to stop any further writes to the pool, replace the
failed drive with a new one and balance the pool before making it available to
end users. Here's a detailed step by step example.

0. Suppose 2 drives sda and sdb form a raid1 pool called "mypool".

1. Prior to any disk failures, make a note of all devids in the pool::

     # btrfs fi show

2. Drive sda(say, devid 4) fails.

3. Depending on the severity of the failure, "btrfs fi show" command may show
   the failed drive or just report that some drives are missing.

4. Mount "mypool" in degraded mode::

     # mount -o degraded /dev/sdb /mnt2/mypool

5. If the above command fails because "mypool" is already mounted, just remount it::

     # mount -o remount,degraded /dev/sdb /mnt2/mypool

6. Any mounted Shares of "mypool" will automatically show as mounted in degraded mode.

7. If your hardware supports drive hotswap, replace the failed drive with a new
   one online. Otherwise, shutdown the machine and replace the drive and start
   it back up.

8. The new drive could have the same name(sda) as the failed one. Let's assume that's the case.

9. Make sure the new drive is clean of any old data::

     # wipefs -a /dev/sda

10. Make sure that "mypool" is mounted (necessary if you rebooted the system)

11. Replace the failed drive with the new drive::

      # btrfs replace start <devid_of_the_failed_drive> /dev/sdb /mnt2/mypool

12. If drive names are different, then we can use /dev/sd<failed> instead of devid.

13. The replace process may take a while depending on the usage of the pool.

12. periodically check status::

      # btrfs replace status /mnt2/mypool

13. Once the replace is finished, the status command output will say finished
    along with a little more information.

14. Unmount the pool and mount it again so it's no longer in degraded mode.

If both drives in a raid1 pool simultaneously fail, the scenario becomes
catastrophic similar to a raid0 pool. In such case follow the recovery strategy
described in :ref:`datalossraid0`

.. _datalossraid10:

Data loss Prevention and Recovery in RAID10 Pools
-------------------------------------------------

A raid10 pool in Rockstor consists of stripes of raid1 mirrors and requires at least 4
drives. So, just like a raid0 consists of stripes of individual drives, raid10
consists of stripes of raid1 mirrors.

A raid10 pool can tolerate multiple simultaneous drive failures as long as each
failed drive is in a separate raid1 mirror.

If a drive fails, the recovery process is same as the one described in
:ref:`datalossraid1`

If multiple drives fail simultaneously but each of them belong to a different
mirror, the recovery process is again the same and it must be repeated for
each failed drive.

If multiple drives fail simultaneously but two of them belong to the same raid1
mirror, then the scenario becomes catastrophic similar to a raid0 pool. In such
case, follow the recovery strategy described in :ref:`datalossraid0`

.. _datalossraid5:

Data loss Prevention and Recovery in RAID5 Pools
------------------------------------------------

A raid5 pool in Rockstor requires at least 3 drives. Parity information is
distributed among the drives so the pool stays functional even when a single
drive fails.

Currently, raid5 is experimental and we suggest that you don't create a pool
with the minimum configuration of 3 drives. It's very error prone to replace a
failed drive of a 3 drive raid5 pool.

If your raid5 pool has 4 or more drives and a single drive fails, you can
follow these steps to replace it with a new drive and balance(rebuild) the
pool.

.. raw:: html

   <div class="alert">
   <strong>Important!</strong> These steps only apply to raid5 pools with 4+
   drives or raid6 pools with 5+ drives
   <br>
   These steps are tested, but we cannot guarantee the accuracy given the
   current state of raid5/6 in BTRFS
   </div>

0. Suppose there is a raid5 pool called "mypool" with drives: sda, sdb, sdc,
   sdd. Say, sdd failed.

1. mount the pool if it's not already::

     # mount /dev/sda /mnt2/mypool

2. if "btrfs fi show" command output doesn't list sdd, or if it says "some
   devices missing", skip to step 5. Else, go to the next step

3. remove the drive from the pool::

     # btrfs device delete /dev/sdd /mnt2/mypool

4. Go to step 7

5. Remove the first "missing" drive which should be sdd::

     # btrfs device delete missing /mnt2/mypool

6. Now btrfs fi show output should neither show the missing drive nor show that
   drives are missing. As if sdd was never part of this pool.

7. Hotswap a new drive in place of the failed one if your hardware supports hotswapping

9. Otherwise, power down the machine, take the bad drive out, insert the new
   drive and power it up.

10. Let's assume that the new drive also appears as sdd (it doesn't matter, but just for simplicity)

11. Make sure the new drive is clean of any old data::

      # wipefs -a /dev/sdd

12. Make sure the pool is mounted, if not, mount it::

      # mount /dev/sda /mnt2/mypool

13. Add the new drive to the pool::

      # btrfs device add /dev/sdd /mnt2/mypool

14. balance the pool (could take a while)::

      # btrfs balance start /mnt2/mypool

If multiple drives fail simultaneously, then the scenrio becomes catastrophic
similar to a raid0 pool. In such case, follow the recovery strategy described
in :ref:`datalossraid0`

.. _datalossraid6:

Data loss Prevention and Recovery in RAID6 Pools
------------------------------------------------

A raid6 pool is very similar to raid5. Unlike raid5, two copies of parity
information is distributed among the drives, so the pool will be functional
even when two drives simultaneously fail.

Like raid5, raid6 is also experimental and we suggest that you don't create a
pool with minimum configuration of 4 drives, but instead with at least 5
drives.

If your raid5 has 5 or more drives and one of them fails, you can follow the
same steps laid out in :ref:`datalossraid5` to replace it with a new drive
and balance(rebuild) the pool.

If more than two drives fail simultaneously, then the scenario becomes
catastrophic similar to a raid0 pool. In such case, follow the recovery
strategy described in :ref:`datalossraid0`
