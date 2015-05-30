Rockstor in a GNU/Linux Kernel Virtual Machine (KVM)
====================================================
A quick and easy way to evaluate Rockstor is by using a virtual machine. A virtual machine instance of Rockstor is also invaluable as part of a build environment.

If you are using a Linux desktop you have the option to use the GNU/Linux KVM and its associated GUI Virtual Machine Manager.  This can be more efficient than the more well know Oracle VirtualBox.

Can I run the Linux KVM?
-----------------------
This depends on you CPU having the appropriate capabilities; to find out on an ubuntu desktop you can install the cpu-checker program with the following command::

    sudo apt-get install cpu-checker

Once this program is installed you can execute in a terminal the following command::

    kvm-ok

The response should indicate if KVM is possible. Another less friendly but more portable way to establish KVM capability is::

    egrep -c '(svm|vmx)' /proc/cpuinfo

A non zero response from the above command should indicate KVM possibility.

Installing KVM and its GUI
--------------------------
This is Ubuntu specific but may well work on other debian derivatives::

    sudo apt-get install qemu-kvm libvirt-bin bridge-utils virt-manager

N.B. it is required that one logs out and then back in again after the above installs as then your linux user is able to acquire their new group privileges.

Setting up a KVM for Rockstor
-----------------------------
The easiest way to do this is by using the KVM GUI "Virtual Machine Manager" or virt-manager via command line.

.. image:: VMM.png
    :scale: 100%
    :align: center

This graphical assistant is fairly intuitive and can get a VM up and running by just following the built in "Create a new virtual machine" however if you like to be able to name your drives/volumes then creating them first will be necessary.

Adding the virtual drives / disks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Double click on the localhost (QEMU) and select the storage tab

.. image:: VMM_add_volumes.png
    :scale: 100%
    :align: center

Click on the New Volume button and create the system drive eg

.. image:: VMM_system_drive.png
    :scale: 100%
    :align: center

In the above we used the provided defaults but named our volume system-drive. The 8GB size coincides with the suggested minimum for Rockstor's install drive.

Using the same procedure we can add additional drives for use by Rockstor as it's data drives.  The following illustrates the result of adding another 2 data drives each of 2GB.

.. image:: VMM_drives_created.png
    :scale: 100%
    :align: center










