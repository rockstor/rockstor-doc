
.. _rootpwreset:

Reset the root password
=======================

The **root** user is created during the Rockstor installation. During one of the
installation steps the root password was set (and confirmed).
After a while, it's conceivably possible that the password information is
lost and needs to be reset. The Rockstor installation media does not contain
a rescue environment anymore, due to install media size concerns. Therefore,
a separate rescue disk needs to be downloaded (less than 1 GB in size).

The disk image can be obtained from openSUSEs repositories for the different releases:

* `Leap 15.5 <https://download.opensuse.org/distribution/leap/15.5/live/>`_
* `Leap 15.6 <https://download.opensuse.org/distribution/leap/15.6/live/>`_
* `Tumbleweed <https://download.opensuse.org/tumbleweed/iso/>`_ 
  (only available for x86_64 architecture)

In order to quickly narrow down the search, the Search function in the top left can
be used. Entering the terms **Rescue** followed by the architecture **x86_64** or **aarch64**
should narrow this down to the relevant image that can then be downloaded. Unfortunately,
there is no ready image for a Pi architecture:

.. image:: /images/howtos/reset-root-password/pw01_search_rescue_disk.png
   :scale: 100%
   :align: center
   
The downloaded image needs to be used to create bootable media, on a USB stick, 
CD-ROM/DVD disk, or, if using Rockstor on a virtual machine, the downloaded
*iso* file can be mounted directly. For USB one can use the same approach
described for :ref:`makeusbinstalldisk`.

Once that's completed, below are the instructions:


Step 1: Boot up with an OpenSUSE rescue CD
------------------------------------------

To reset the password shut down the Rockstor system and boot it up with
the above created rescue media. Like with the original Rockstor installation,
it might require to adjust the boot device sequence (in the BIOS, or, if
available, during the boot process by pressing Function Keys like **<F12>**,
depending on the motherboard manufacturer).

On the splash screen, select the **Failsafe** option and hit <Enter>. This will
boot the system into the command line. If, by accident, it boots into the first
option with a graphical UI, either reset the machine and try again, or attempt to
open a terminal window on the desktop and proceed from there with the command
line-based process.

.. image:: /images/howtos/reset-root-password/pw01_splash_screen.png
   :scale: 50%
   :align: center


Step 2: Log in and mount relevant devices and partitions
--------------------------------------------------------

After the boot completes the login prompt should appear (the screenshot
is from a virtual machine, hence the *vbox* login). Right above the network
interfaces are listed, though they won't be needed for this activity.

.. image:: /images/howtos/reset-root-password/pw01_rescue_shell.png
   :scale: 80%
   :align: center

To log into the system, just type :code:`root` for the user and hit <Enter>.
Now that the login is complete, a device and a few partitions need to be 
mounted for the password reset to work.

First, identify the device that houses the Rockstor Operating System, using:

.. code-block: console
   lsblk
   
to identify all devices connected to the machine, and then, identify
the one that's the system device (likely the one that has the smallest size).
Here is a sample output, it will look different on every user's machine:

.. image:: /images/howtos/reset-root-password/pw01_lsblk_output.png
   :scale: 80%
   :align: center

In the above example **/dev/sda4** is the system device (largest partition on
*sda*).

Next mount that device:

.. code-block: console
   
   vbox:~# mount -o rw /dev/sda4 /mnt
   
Then create a few bind mounts, change the filesystem root directory for the 
running process and finally mount these, so that the system can use them
for the next step:

.. code-block:: console
   
   vbox:~# mount -o bind /proc /mnt/proc
   vbox:~# mount -o bind /sys /mnt/sys
   vbox:~# mount -o bind /dev /mnt/dev
   vbox:~# chroot /mnt
   vbox:~# mount -a

Step 3: Reset password
----------------------

Now change the password with the *passwd* command:

.. code-block:: console

   vbox:~# passwd

Enter the new password. The system will ask for confirmation
through retyping it. Then the new password is set.

Get out of chroot with the exit command:

.. code-block:: console
   
   vbox:~# exit

Shut down the system and remove the rescue disk.

Boot the system back up and a login using the root password should
once again be possible.
