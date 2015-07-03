.. _mpsnapshots:

Multi Period Snapshots
======================

It is common practice to keep progressively less frequent snapshots of Shares as
they become older.  This might be thought of as a self thinning multi period
snapshot arrangement, ie:-

* 7 days of daily snapshots
* 1 month of weekly snapshots
* 12 months of monthly snapshots
* 2 years of yearly snapshots

This arrangement, or variations of it, can be achieved with Rockstor's :ref:`tasks`
and it *Maximum count* feature as follows:-


