
Snapshots and Clones
============================

Snapshot
^^^^^^^^

A snapshot is read-only point in time copy of a share. Since BTRFS is a CoW filesystem, snapshots are created instantly and take up no extra space when created.

Create a Snapshot
-----------------

A snapshot can be created in two ways, 1. By clicking **Create** under *Storage->Snapshots* tab to create a snapshot of a share 2. By clicking **Schedule** under *Storage->Snapshots* tab. This leads to *Schedule a Task* page where you can set up a snapshot schedule based on your parameters like hourly, daily, monthly freqeuncy etc. Also, refer **Create a Snapshot Task** under `Scheduled Task <http://rockstor.com/docs/tasks.html` _ documentation.      

.. youtube:: https://www.youtube.com/watch?v=QTQePwrYMS0
   

.. youtube:: https://www.youtube.com/watch?v=PA0hneCq-AE
   
.. _cloneasnapshot:

Clone a Snapshot
----------------

A Clone can be created from a Snapshot of a Share. This is useful if you wish
to create a new Share that is an exact copy of the Snapshot.

In the Web-UI, click on the *Storage* tab to enter the main Storage view. Now
click on *Shares* in the left sidebar to enter the *Shares* view. In the
displayed table of shares, click on the desired share to enter the share detail
view, and click on the *Snapshot* tab to view the list of snapshots of the
share. Click the **Clone** button to display the form to create a clone. Submit
it after entering the new name for the newly created share as shown below.

.. youtube:: https://www.youtube.com/watch?v=aySlQCx65GM
   
.. _rollbackashare:


Rollback a Share to a specific Snapshot
---------------------------------------

A Share can be rolled back to any of its snapshots. This is useful if you wish
to restore a Share to it's previous state represented by its snapshots

In the web-ui, click on the *Storage* tab to enter the main Storage view. Now
click on *Shares* in the left sidebar to enter the *Shares* view. In the
displayed table of shares, click on the desired share to enter the share detail
view. Click the **Rollback** button to display the form to select a snapshot to
rollback to, and submit the form as shown below.

*Note:* Shares that are exported through NFS or Samba cannot be rolled back. The
NFS or Samba shares should be deleted before the share can be rolled back.

.. youtube:: https://www.youtube.com/watch?v=r0SbCZ_kEBg

 
