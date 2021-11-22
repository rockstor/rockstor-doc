
.. _windowsshadowcopy:

Accessing Snapshots from Windows
================================

One of the main features of Rockstor, by the way of BTRFS, is the ability to
take Snapshots of Shares. Snapshots can be taken on demand or can be scheduled
to be taken periodically. But say, we have a Share exported out to clients via
Samba. How does a client, in this case a Windows user, access not only the
contents of the Share but also the contents(individual files) of it's
Snapshots? It can be very useful to retrieve previous versions of a file, for
example.

In the Windows world, this feature is called `Shadow Copy
<https://en.wikipedia.org/wiki/Shadow_Copy>`_. The server side of this feature
is what Rockstor supports by using Samba's `vfs_shadow_copy2
<https://www.samba.org/samba/docs/current/man-html/vfs_shadow_copy2.8.html>`_
which understands BTRFS Snapshots and exposes them to Windows clients as shadow
copies.

Step 1: Add a Samba export
--------------------------

Just like adding any other Samba export, go to the *Samba* screen under the
*Storage* tab of the Web-UI and click on **Add Samba Export** button. Select
*Enable Shadow Copy* checkbox and fill out the *Snapshot prefix* field. You
should choose the *Snapshot prefix* field to be unique enough that it will not
clash with directory or filenames. Eg: SNAPSHOT. The rest of the input in the
form is same as it would be for any other Samba export.

Step 2: Schedule Snapshots
--------------------------

We need to schedule Snapshots for the Share exported in the above step. We can
do this by going to the *Scheduled Tasks* screen under the *System* tab and
clicking the *Schedule a Task* button. The important input parameter here is
the *Snapshot prefix*. It must be the same string from the previous step. Eg:
SNAPSHOT. Choose rest of the input according to your needs.


Step 3: Access Snapshots from Windows
-------------------------------------

The previous step results in periodic Snapshots for the Share that is exported
via Samba in Step 1. The binding factor between Steps 1 and 2 is the *Snapshot
prefix* input variable. All that is left now is to access the Share from
Windows.

As the time goes by, files are added, edited and deleted from the
Share by the client. Meanwhile, Snapshots are taken on Rockstor periodically
and result in *Previous versions* or *Shadow copies* for files. To access
previous versions of a file from Windows, go to it's *Properties* window and
click on *Previous Versions* tab.
