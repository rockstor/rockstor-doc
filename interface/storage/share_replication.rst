
.. _sharereplication:

Replication
===========

Redundancy options of a pool operate at the single appliance level. While this
reduces the risk of data loss from bad disks, it does no good if the entire
appliance fails. To mitigate and distribute this risk, Shares can be replicated
to other Rockstor appliances.

Replicate shares to other Rockstor appliances
---------------------------------------------

Shares from one Rockstor appliance can be replicated to others at scheduled
frequencies. Replication frequency is in seconds and can be as little as 60
seconds. The appliance that hosts the replica is called a target
appliance. At least one target appliance must be added before setting up
replication for shares. See :ref:`add_appliance` for more details.

In the webui, click on the *Storage* tab to enter the main Storage view. Now
click on *Replication* in the left sidebar to enter *Replication* view. Click
on **Add Replication Task** button and a form will be displayed. Submit the
form as shown below.

.. image:: /images/interface/storage/add_replica.gif
   :width: 100%
   :align: center

Note that a pool must already exist on the target appliance to host the
replica of the share.

Disable or enable a replication task
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the webui, click on the *Storage* tab to enter the main Storage view. Now
click on *Replication* in the left sidebar to enter *Replication* view. In the
displayed table of replication tasks, click on the **disable** icon of the
corresponding task to disable it as shown below.

.. image:: /images/interface/storage/disable_replica.gif
   :width: 100%
   :align: center

Follow the same procedure to enable a replication task back again.
