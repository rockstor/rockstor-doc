
.. _rootpwreset:

Resetting root password
=======================

root user is created during Rockstor OS install. You may remember setting root
password in one of the install screens. After a while, it's possible that you
forgot the password and would like to reset it. To do that is a straight
forward process as described in this howto.


Step 1: Boot up with install CD/DVD/USB-drive
---------------------------------------------

Resetting password requires shutting down the system and booting it up with
Rockstor install CD/DVD or USB-drive as you have done it during install. If you
are unsure, see :ref:`osinstall`.

On the splash screen, scroll down to **Troubleshooting** and hit enter to go to
the Troubleshooting screen.

.. image:: /images/howtos/reset-root-password/splash_screen.png
   :scale: 80%
   :align: center

Step 2: Go to Rescue Shell
--------------------------

In the **Troubleshooting** screen, scroll down to **Rescue and Rockstor
System** and hit enter to go to the **Rescue** screen.

.. image:: /images/howtos/reset-root-password/troubleshooting_screen.png
   :scale: 80%
   :align: center

In the **Rescue** screen, use the Tab key to highlight the **Continue** button
and hit enter.

.. image:: /images/howtos/reset-root-password/rescue_screen.png
   :scale: 80%
   :align: center

Hit Enter key again on the next two screens to be dropped into the Shell.

.. image:: /images/howtos/reset-root-password/rescue_shell.png
   :scale: 80%
   :align: center

Step 3: Reset password
----------------------

Once you are in the rescue shell, change the filesystem root ::

  sh-4.2# chroot /mnt/sysimage

Now change the password with the *passwd* command ::

  bash-4.2# passwd

Remove autorelabel file ::

  bash-4.2# rm -f /.autorelabel

Get out of chroot with the exit command ::

  bash-4.2# exit

Here's an example image showing execution of above commands.

.. image:: /images/howtos/reset-root-password/reset_pw_commands.png
   :scale: 80%
   :align: center

Enter *exit* command again and the system will reboot ::

  sh-4.2# exit

Remove the install CD/DVD or USB-drive and let the system boot up
completely. You can now login at the terminal and SSH as root using the new
password.
