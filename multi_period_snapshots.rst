.. _mpsnapshots:

Multi Period Snapshots
======================

It is common practice to keep progressively less frequent snapshots of Shares as
those snapshots become older.  This might be thought of as a self thinning multi period
snapshot arrangement, ie:-

* 7 days of daily snapshots
* 1 month of weekly snapshots
* 12 months of monthly snapshots
* 2 years of yearly snapshots

This arrangement, or variations of it, can be achieved with Rockstor's
:ref:`tasks` feature; or more specifically with a series of
:ref:`snapshot tasks <snapshottask>` and their respective *Maximum count*
feature.

To create the above multi period snapshot arrangement we need to create 4
independent snapshot tasks each with a progressively longer period and an
appropriate *Maximum count* feature to achieve the self thinning component.


Day Week Month Year Example
---------------------------

One example of how this might be done:-

.. image:: mpsnapshot_all_four.png
   :scale: 100%
   :align: center

In the above example we keep, 7 daily, 5 weekly, 12 monthly, and 2 yearly
snapshots by using the *Maximum count* feature on each snapshot task.

From the *mouse over tooltip* on the WebUI we have *"Older snapshots beyond
this number and created by this task will be deleted"*