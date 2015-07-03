.. _tasks:

Scheduled tasks
===============

Rockstor allows a user to set up scheduled tasks that start at a particular time
and are run at a specified frequency. The types of tasks currently supported are:-

* Pool scrub
* Share Snapshot 

On the Web-UI **System** page select **Scheduled Tasks** and **Enable** the **Task
Scheduler**. To create a new task click the **Add Scheduled Task** button.


Create a Scrub Task
-------------------

To create a scrub task enter the following:-

* **Task name** and **Task type** ie *scrub*
* **Pool to scrub** from the drop down
* **Start Date**, **Start time**, and **Task frequency** in minutes


.. image:: scrub_task.png
   :scale: 100 %
   :align: center

Then the **Submit** button.

.. _snapshottask:

Create a Snapshot Task
----------------------

To create a snapshot task enter the following:-

* **Task name** and **Task type** ie *snapshot*
* **Share** to snapshot
* **Snapshot prefix** the file name will be *prefix_YYYYMMDDHHMMSS*
* **Maximum count** keep only this number of the most recent snapshots
* **Start Date**, **Start time**, and **Task frequency** in minutes

.. image:: mpsnapshot_daily.png
   :scale: 100 %
   :align: center

Then the **Submit** button.


Enable / Disable one or all Tasks
---------------------------------

On the Web-UI **System** page select **Scheduled Tasks**.
The **Task Scheduler** switch will enable or disable all Tasks at once.

If you wish to Enable / Disable an **individual task** use that task's
respective **tick box** in the *Enabled column*


.. image:: tasks_list.png
   :scale: 100 %
   :align: center


Delete a Task
-------------

To delete a task, click the **Delete / bin** icon in that tasks **Actions**
column in the list of tasks available on the **System** page **Scheduled Tasks**
section.


