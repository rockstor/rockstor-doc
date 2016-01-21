..  _mdraid_bootdrive_howto:

Mirroring Rockstor OS using Linux Raid
======================================

It's a common and recommended practice to setup redundancy for the OS bits
while installing a mission critical Rockstor server. The idea is to combine two
Hard Disk Drives(HDDs) in a mirror configuration to house the OS. If one of the
HDDs fails, it can simply be swapped out with a new drive saving us from a
re-install or downtime.

In this howto, we will use `Linux Raid
<https://raid.wiki.kernel.org/index.php/Linux_Raid>`_ to setup the redundant OS
drive mirror. This can be done easily as part of Rockstor installation. If you
have never installed Rockstor before, we recommend you read our
:ref:`quickstartguide` and watch `this install video
<https://www.youtube.com/watch?v=yEL8xMhMctw>`_ before proceeding with this
howto.

Requirements
------------

You need two HDDs to setup the mirror. We recommend HDDs of same size and brand
for uniformity. The drives can be as small as 16GB, but in practice, they are
usually 100+ GB. In this howto, we demonstrate with 8GB virtual drives using
VirtualBox.

We will create a mirrored setup for each of **/boot, / and swap**
partitions. You should plan the sizing of each partition before proceeding
further. **/boot** can be as little as 1-2GB and will store Kernels. **swap**
can be 2-4GB or twice the amount of RAM in the system. **/** will store most of
the OS bits and should be atleast 8GB, more the better. For demonstration
purposes of this howto, our **/** will be 6GB, **/boot** will be 1GB and
**swap** will also be 1GB.

Step 1: Device Selection
^^^^^^^^^^^^^^^^^^^^^^^^

Start the Rockstor installation process and you'll soon see the **INSTALLATION
SUMMARY** screen. Click on **INSTALLATION DESTINATION** to go to device
selection screen.

.. image:: installation_summary.png
   :scale: 85%
   :align: center

On the next screen, the two HDDs we are about to mirror should be
visible. Click to select them. In the bottom half of the screen,
select *I will configure partitioning* radio button. Finally click **DONE** at
the top.

.. image:: device_selection.png
   :scale: 85%
   :align: center

Step 2: Destroy old data, if any
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The next screen is titled **MANUAL PARTITIONING** as shown below. If there are
any partitions already on the two HDDs selected before, they will appear on the
right under a collapsible menu. If you don't see any, your HDDs are clean and
you can ignore this step. In our demonstration, HDDs are not clean and the
existing partioning is titled **UNKNOWN**

.. image:: manual_partitioning_1.png
   :scale: 85%
   :align: center

Click on the **-** button at the bottom to delete these partitions. Repeat this
process until all of them are deleted.

.. image:: manual_partitioning_2.png
   :scale: 85%
   :align: center

Step 3: Setup **/** partition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Select **Standard Partitioning** from the dropdown menu and click **+** button
at the bottom to create a new partition.

.. image:: manual_partitioning_3.png
   :scale: 85%
   :align: center

A popup window will appear titled **ADD A NEW MOUNT POINT**. Select **/** from
the dropdown, enter the size you planned out eariler(minimum 8GB) and click
*Add mount point* button.

.. image:: root_partition_1.png
   :scale: 85%
   :align: center

On the next screen, select **RAID** under **Device Type**, **RAID 1** under
**RAID Level** and **ext4** under **File System**. Click *Update Settings*
button to finalize **/** partition setup.

.. image:: root_partition_2.png
   :scale: 85%
   :align: center

Step 4: Setup **/boot** partition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Click on **+** button at the bottom left to add the **/boot** partition. The
procedure is just like above but pick **/boot** from the dropdown, enter
appropriate size(1-2GB recommended) and click *Add mount point*

.. image:: boot_partition_1.png
   :scale: 85%
   :align: center

On the next screen, select **RAID** under **Device Type**, **RAID 1** under
**RAID Level** and **ext4** under **File System**. Click *Update Settings*
button to finalize **/boot** partition setup.

.. image:: boot_partition_2.png
   :scale: 85%
   :align: center

Step 5: Setup **swap** partition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Just like in **/boot** above, click on **+** button and pick **swap** from the
dropdown. Leave the size field blank and all of the remaining space will be
used. As we planned the sizes ahead of time, this will come out to be same
without having to enter the exact number.

.. image:: swap_partition_1.png
   :scale: 85%
   :align: center

On the next screen, select **RAID** under **Device Type** and **RAID 1** under
**RAID Level**. Click *Update Settings* button to finalize **swap** partition
setup. We really don't need redundancy for swap partition, and it also results
in a performance overhead. So alternatively, you can keep the default **Standard
Partitioning** selection.

.. image:: swap_partition_2.png
   :scale: 85%
   :align: center


Step 6: Accept Changes and proceed
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Click **DONE** at the top left of the screen and then click on **Accept
Changes** to finalize the manual partition scheme.

.. image:: accept_changes.png
   :scale: 85%
   :align: center

The installer will then display the **INSTALLATION SUMMARY** screen. Click on
*Begin Installation* button at the bottom right to start the install. In this
demonstration, we did not show other configuration such as selecting Time Zone
and making sure there's network connectivity. If you need assistance with them,
refer to :ref:`quickstartguide`.

.. image:: begin_installation.png
   :scale: 85%
   :align: center

Verification of the mirror
--------------------------

It's a good idea to verify the setup once the installation is finished. You can
do that simply with the following command ::

  # cat /proc/mdstat
  Personalities : [raid1]
  md125 : active raid1 sdb2[1] sda2[0]
        976832 blocks super 1.0 [2/2] [UU]
        bitmap: 0/1 pages [0KB], 65536KB chunk

  md126 : active raid1 sda1[0] sdb1[1]
        5859328 blocks super 1.2 [2/2] [UU]
        bitmap: 1/1 pages [4KB], 65536KB chunk

  md127 : active raid1 sda3[0] sdb3[1]
        1546240 blocks super 1.2 [2/2] [UU]

The three md* devices correspond to the mirror configuration we setup earlier
during the install. Note that each partition is mirrored(raid1) where the
counter parts of the mirror are from different drives(**sda** and **sdb** in
our example). We can also verify that **/** and **/boot** are mounted and are
the right size with the following command ::

  # df -h | grep md
  /dev/md126      5.4G  1.4G  3.8G  28% /
  /dev/md125      923M  100M  761M  12% /boot

Disaster Recovery
-----------------

Up to this point, we have setup the mirror and verified that everything looks
good. Over time, usually after a long time, one of the HDDs may start throwing
errors indicating that it's time to replace it. Following steps will guide you
through that process.

Step 1: Remove failing HDD
^^^^^^^^^^^^^^^^^^^^^^^^^^

If your hardware supports hotswapping HDDs, you can pull out the failing drive
and leave the system running while you replace it with a new HDD. After
removing the failing drive, the System continues to run normally, but the
mirror is no longer redundant as shown in the below output(note sdb parts are
missing) ::

  # cat /proc/mdstat
  Personalities : [raid1]
  md125 : active raid1 sda2[0]
        976832 blocks super 1.0 [2/1] [U_]
        bitmap: 0/1 pages [0KB], 65536KB chunk

  md126 : active raid1 sda1[0]
        5859328 blocks super 1.2 [2/1] [U_]
        bitmap: 1/1 pages [4KB], 65536KB chunk

  md127 : active raid1 sda3[0]
        1546240 blocks super 1.2 [2/1] [U_]

Step 2: Add a replacement HDD
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Next step is to replace the failing HDD with a new HDD. Same size and brand is
recommended, to keep things uniform. In our demonstration here, I've added a
new 8GB virtual drive(similar to the failed HDD) and it appeared as **sdb** to
the system.

Step 3: Partition the replacement HDD
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The replacement HDD must be partitioned, much like during OS install. But this
time we'll use command line tools to do so. The advantage of using the same
size HDD is that we can just copy the partition scheme from the functioning
HDD. In our demonstration, **sda** is the still functioning HDD and it's
partition table looks as follows ::

  # sfdisk -d /dev/sda
  # partition table of /dev/sda
  unit: sectors

  /dev/sda1 : start=     2048, size= 11726848, Id=fd
  /dev/sda2 : start= 11728896, size=  1953792, Id=fd, bootable
  /dev/sda3 : start= 13682688, size=  3094528, Id=fd
  /dev/sda4 : start=        0, size=        0, Id= 0

We can copy the partition table of **sda** to **sdb** with the following
composite command ::

  # sfdisk -d /dev/sda > /tmp/sda.pt; sfdisk /dev/sdb < /tmp/sda.pt; rm -f /tmp/sda.pt
  Checking that no-one is using this disk right now ...
  OK

  Disk /dev/sdb: 1044 cylinders, 255 heads, 63 sectors/track
  Old situation:
  Units: cylinders of 8225280 bytes, blocks of 1024 bytes, counting from 0

     Device Boot Start     End   #cyls    #blocks   Id  System
  /dev/sdb1          0       -       0          0    0  Empty
  /dev/sdb2          0       -       0          0    0  Empty
  /dev/sdb3          0       -       0          0    0  Empty
  /dev/sdb4          0       -       0          0    0  Empty
  New situation:
  Units: sectors of 512 bytes, counting from 0

     Device Boot    Start       End   #sectors  Id  System
  /dev/sdb1          2048  11728895   11726848  fd  Linux raid autodetect
  /dev/sdb2   *  11728896  13682687    1953792  fd  Linux raid autodetect
  /dev/sdb3      13682688  16777215    3094528  fd  Linux raid autodetect
  /dev/sdb4             0         -          0   0  Empty
  Warning: partition 1 does not end at a cylinder boundary
  Warning: partition 2 does not start at a cylinder boundary
  Warning: partition 2 does not end at a cylinder boundary
  Warning: partition 3 does not start at a cylinder boundary
  Warning: partition 3 does not end at a cylinder boundary
  Successfully wrote the new partition table

  Re-reading the partition table ...

  If you created or changed a DOS partition, /dev/foo7, say, then use dd(1)
  to zero the first 512 bytes:  dd if=/dev/zero of=/dev/foo7 bs=512 count=1
  (See fdisk(8).)

Step 4: Rebuild the mirror
^^^^^^^^^^^^^^^^^^^^^^^^^^

This is the final and crucial step. We'll resync the partitions of the
replacement HDD with their counter parts in the mirror. This can be done with
the following composite command ::

  # mdadm --manage /dev/md125 --add /dev/sdb2; mdadm --manage /dev/md126 --add /dev/sdb1; mdadm --manage /dev/md127 --add /dev/sdb3
  mdadm: added /dev/sdb2
  mdadm: added /dev/sdb1
  mdadm: added /dev/sdb3

After the above step, the mirror is re-synchronized. It will take some time
proportional to your HDD size. You can monitor the progress and confirm the
finish by looking at the contents of /proc/mdstat file as shown here ::

  # cat /proc/mdstat
  Personalities : [raid1]
  md125 : active raid1 sdb2[2] sda2[0]
	976832 blocks super 1.0 [2/2] [UU]
	bitmap: 0/1 pages [0KB], 65536KB chunk

  md126 : active raid1 sdb1[2] sda1[0]
	5859328 blocks super 1.2 [2/1] [U_]
	[=============>.......]  recovery = 68.0% (3985280/5859328) finish=2.0min speed=15366K/sec
	bitmap: 1/1 pages [4KB], 65536KB chunk

  md127 : active raid1 sdb3[2] sda3[0]
	1546240 blocks super 1.2 [2/1] [U_]
	  resync=DELAYED

  unused devices: <none>

Above output indicates that md125 and md127 have finished recovery(re-sync),
but md126 is at 68%. It is completed after a few more seconds as shown again here. ::

  # cat /proc/mdstat
  Personalities : [raid1]
  md125 : active raid1 sdb2[2] sda2[0]
	976832 blocks super 1.0 [2/2] [UU]
	bitmap: 0/1 pages [0KB], 65536KB chunk

  md126 : active raid1 sdb1[2] sda1[0]
	5859328 blocks super 1.2 [2/2] [UU]
	bitmap: 0/1 pages [0KB], 65536KB chunk

  md127 : active raid1 sdb3[2] sda3[0]
	1546240 blocks super 1.2 [2/2] [UU]

  unused devices: <none>

That completes the disaster recovery section and the howto!
