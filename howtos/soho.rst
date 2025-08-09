.. _sohoguide:

Small Office Fileserver with Rockstor
=====================================

In a small office or home office like environment, a centralized storage server
is needed to store documents, photos, videos and other files including backups
and virtual machines and access them from other computers on the network. Here
are some simple but important uses of such a server.

1. Backup data from workstations, laptops and other computers

2. Share data easily with other users and from any computer.

3. Create and organize a central repository of all data.

There are more complex usecases which are covered in their own separate
documents. In this document, We'll describe how to setup Rockstor as your
centralized storage server, also called a Fileserver or NAS.

.. _serverreqs:

Server requirements and suggestions
-------------------------------------

The first step in building the Rockstor Fileserver is to procure
hardware. Since Rockstor is a `Free software
<https://en.wikipedia.org/wiki/Free_software>`_ product based on Linux, there is
a lot of flexibility. You can purchase hardware that fits your budget and
performance requirements. See :ref:`minsysreqs` for general guidance. You can
easily convert an old PC into a Fileserver with Rockstor as long
as it meets these requirements. You can also purchase small office servers from
various places like newegg, ebay and Dell.

.. note::
   Disclaimer: Rockstor is a software product only. We don't recommend or
   certify any particular hardware. Feel free to peruse the `Rockstor Forum
   <https://forum.rockstor.com>`_ for recommendations or ask
   for insights on hardware they have used for their deployments.

.. _hdds:

Hard disk drives
----------------

Disk drives are critical in a fileserver. While Rockstor offers slick
management and access to your data, all of it is ultimately stored inside the
Hard disk drives of the system. Most servers including the ones mentioned in
:ref:`serverreqs` are compatible with standard SATA HDDs. Once you choose the
right server based on your needs, choose appropriate HDDs for that server.

**Note about hardware raid**: Rockstor provides BTRFS based software RAID
capabilities. However, advanced servers offer hardware RAID functionality
providing additional redundancy. Evaluate your risks and choose appropriately.

Rockstor needs one entire HDD for the operating system. So at least two HDDs
are required in the system. Alternatively, you can put the operating system on
a USB disk and use all of the system's HDDs for data. See :ref:`usboverhdd`
for more information about this approach.

.. _servermemory:

Server Memory
-------------

At least 2 GB of RAM is required for Rockstor to function reasonably. This
should deliver decent performance for about 1 TB of data. If your capacity
needs are larger, a simple rule of thumb is to add 1 GB
RAM per 1 TB of extra capacity.

Pre-install checklist
---------------------

Here's what you need before proceeding with installation

1. Right server for your needs. See :ref:`serverreqs` for help.
2. At least two HDDs installed in the system. See :ref:`hdds` for more details.
3. At least 2 GB of RAM. See :ref:`servermemory` for more information.
4. (Optional) 8 GB USB drive if you choose to run Rockstor entirely from a USB
   flash drive. See :ref:`usboverhdd` for more information.
5. Network cable to connect the server to your router. Rockstor install needs
   connection to the internet.
6. CD/DVD ROM drive. If your server does not have an internal CD/DVD ROM, an
   external usb based one should work.
7. (Optional) 1 GB USB drive if you choose to install from the USB instead of
   CD/DVD ROM.
8. The Rockstor ISO file, downloadable from
   `https://rockstor.com/download. <https://rockstor.com/download.html>`_
9. A blank CD-R/RW to burn the ISO file to. This is not necessary if installing
   from a USB flash drive as mentioned in step 7.
10. A monitor, keyboard and a mouse to drive the install process.

.. _cdinstall:

Install Rockstor from CD/DVD drive
----------------------------------

**Skip this section and go to** :ref:`usbinstall` **instead, if you plan to
install Rockstor from a USB flash drive.**

Installing Rockstor from a CD-R/RW is straight forward on most system that
come with a CD/DVD drive and if there is no built in drive then Rockstor
should also install just fine using an external USB CD/DVD drive.

Burn the downloaded Rockstor ISO file onto a blank CD or DVD disk as a bootable
image. On Linux, you can use programs like K3b. On Windows, you can use Windows
Disc Image Burner(Windows 7 only) or an open source program like
`Infra Recorder <http://infrarecorder.org/>`_. On macOS, use the **Disk Utility**
program.

Once the disk is ready to be booted, insert it in your soon to be Rockstor
Fileserver and power cycle the machine. Please see :ref:`bootorderchanges`
to boot the install media.

.. _usbinstall:

Install Rockstor from USB flash drive
-------------------------------------

**Skip this section and go to** :ref:`cdinstall` **instead, if you plan to
install Rockstor from a CD-R/RW**

A USB flash drive of at least 1 GB in size is required. **All data on the USB
drive will be erased**. So backup your data as needed before proceeding
further.

On Windows, macOS, or Fedora linux systems,
the Fedora Media Writer program can be used to prepare your USB flash drive with the Rockstor ISO installer variant.
If you are using Windows or macOS then Fedora Media Writer can be downloaded & installed from
`GitHub MediaWriter Releases <https://github.com/FedoraQt/MediaWriter/releases>`_.
On Fedora linux, you need only run the following command::

    # sudo dnf install mediawriter

On macOS or any Linux system, you can also use the **dd** program to prepare the USB
flash drive by running the following command::

    # dd if=path_to_rockstor_iso of=/dev/<usb_flash_drive>

Plug the USB flash drive into your soon to be Rockstor Fileserver and power
cycle the machine. Please see :ref:`bootorderchanges` to boot the install
media.

..  _bootorderchanges:

Boot order changes
------------------

When installing Rockstor from a USB boot disk or a CD-R/DVD it may well be
necessary to change the system's device boot order so that the install disk is
booted first. Often this can be accomplished by pressing the **F12 key**
shortly after system power on (note the on screen instructions). If this option
is not available or doesn't work then try changing the boot options within the
systems BIOS settings. Take careful note of what you change though so that
the original setting can be restored if need be. Also note that some systems
require the USB key to be inserted prior to power on before offering it as an
option within the BIOS boot section screens.

To get to a systems BIOS (Basic Input / Output System) take note of early
on screen messages during system power on. Many systems use the **F2 key** or
the **Del key** and some Compaqs use the **F10** key. Note that changes in the
system BIOS may have to be un-done post install to prevent accidental booting
of future install media on subsequent reboots.

.. _installsetup:

Installation and Setup
----------------------

If you wish to install Rockstor on to one of the Hard Drives / SSD's or mSATA
devices in the system see our :ref:`quickstartguide` guide and specifically
the :ref:`osinstall` section. But if you want to install it on to a USB flash
drive, just plug in a USB flash drive with at least 8 GB capacity and select it
as the installation destination as described in :ref:`quickstartguide`. For the
pros and cons of this approach see :ref:`usboverhdd`

**Note: This USB flash drive is separate and not to be confused with the one
mentioned earlier in the document. The earlier one can be as little as 1 GB and
contains the Rockstor installer. After the installation, you'll unplug it and
use it again only for another install. This separate drive needs to be at least
8 GB and will hold the Rockstor operating system and must stay plugged
permanently.**

**Note: All data will be completely erased from this USB flash drive. So backup
your data as needed before proceeding further.**

.. _usboverhdd:

Rockstor on USB flash drive
---------------------------

The Rockstor operating system requires a whole Hard disk drive for
itself. However, it only needs about 8 GB of space to function. This is
terribly inefficient since the drive capacity is usually in hundreds of
gigabytes. So, we made it possible to run Rockstor completely off a USB flash
drive as an alternate approach. But as with anything else, there are
trade-offs.

Here are some advantages of running Rockstor completely off a USB flash drive.

1. You save a whole Hard disk drive for data, that would otherwise be claimed
   exclusively by the operating system.

2. This is especially beneficial in small servers with 2-4 bays.

Here are some disadvantages of this approach

1. HDDs are more reliable and faster than USB flash drives.
2. The USB drive must be permanently plugged in and must not be disturbed.
3. More advanced servers support hardware raid and the operating system can
   live on a raid mirror ensuring high availability. This is not possible with
   USB flash drives.

Using Rockstor
--------------

After the installation and initial setup proceses are complete as described in
:ref:`quickstartguide` and :ref:`setup`, Rockstor is ready to be
used for all your Fileserver needs.

In order to start storing and accessing your data see :ref:`accessshares`

For any questions about installation and other matters, or to get commercial
support, see :ref:`support` for more information.
