.. _tasks:

Scheduled tasks
===============

Rockstor allows a user to set up scheduled tasks that start at a particular time
and are run at a specified frequency. Two types of tasks are supported currently

* Pool scrub
* Share Snapshot 

On the Web-UI **System** page select **Scheduled Tasks** and **Enable** the **Task
Scheduler**. To create a new task click the **Add Scheduled Task** button.

Create a scrub task
-------------------

To create a pool scrub task select the task type as **scrub**. Select the pool
to scrub from the drop-down list of pools, enter a start date and start time,
enter the task frequency in seconds, and submit the task as shown below.

.. image:: scrub_task.png
   :scale: 100 %
   :align: center

.. _snapshottask:

Create a snapshot task
----------------------

To create a snapshot task enter enter the following:-

* **Task name** and **Task type** ie *snapshot*
* **Share** to snapshot
* **Snapshot prefix** the file name will be *prefix_YYYYMMDDHHMMSS*
* **Maximum count** keep only this number of the most recent snapshots
* **Start Date**, **Start time**, and **Task frequency** in minutes

.. image:: snapshot_task.gif
   :scale: 75 %
   :align: center

Enable / Disable a task
-----------------------

In the Web-UI, click on *System* tab to go to the *System* view. Now click on
*Scheduled Tasks* in the left sidebar to go to the *Scheduled Tasks* view.

In the list of scheduled tasks, the **enabled** checkbox shows whether the task
is currently enabled or not. To disable a currently enabled task, click the
**disable** icon in the corresponding row in the list of tasks, and similarly to
enable a disabled task, click the **enable** icon.

.. image:: enable_disable_task.gif
   :scale: 75 %
   :align: center

Delete a task
-------------

In the Web-UI, click on *System* tab to go to the *System* view. Now click on
*Scheduled Tasks* in the left sidebar to go to the *Scheduled Tasks* view.

To delete a task, click the **Delete** icon in the corresponding row in the list
of tasks.

.. image:: delete_task.gif
   :scale: 75 %
   :align: center

