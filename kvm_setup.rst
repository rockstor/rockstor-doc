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

Using the same procedure we can add additional drives for use by Rockstor as it's data drives.  The following illustrates the result of adding another two data drives each of 2GB.

.. image:: VMM_drives_created.png
    :scale: 100%
    :align: center

Close the above dialog and return to main window of Virtual Machine Manager to creating the virtual machine that will use the storage / drives we have now defined.

Creating the Virtual Machine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Starting the "Create a new virtual machine" wizard either from the File menu or the icon bar should show the first of 5 configuration dialogs.

Step 1 - Method of install ie via **iso**

.. image:: VMM_iso_step1.png
    :scale: 100%
    :align: center

Step 2 - Select our install media; in this case the **Rockstor-#.#-#.iso**

.. image:: VMM_iso_os_step2.png
    :scale: 100%
    :align: center
N.B. In the above dialog we must also select OS type **Linux** and Version **Red Hat Enterprise Linux 7 (or later)**

Step 3 - Set the RAM / memory (minimum **2048MB**) and **CPU count** eg 1 or 2 on a quad core host

.. image:: VMM_ram_step3.png
    :scale: 100%
    :align: center

Step 4 - Set the **system drive** to install Rockstor on.
As we have already created our named volumes tick **Select managed or other existing storage**

.. image:: VMM_system_disk_step4.png
    :scale: 100%
    :align: center
We should then be presented with the following dialog where we can select our pre-prepared **system-drive**

.. image:: VMM_system_disk_step4_choose.png
    :scale: 100%
    :align: center

Step 5 - Set our VM's **Name** and **tick "Customise configuration before install"**

.. image:: VMM_customise_tick_step5.png
    :scale: 100%
    :align: center
As we ticked customize we get the chance to modify our VM prior to its fist launch

.. image:: VMM_system_disk_sata.png
    :scale: 100%
    :align: center
N.B. in the above we have changed what was **Disk 1** to the required **SATA Disk 1** by changing its "Disk bus" in **Advanced options** to **SATA**.
This is necessary as otherwise the Red Had Kickstarter semi automated installer process can fail to identify the default kvm drive type of vda.

If you receive a "Specified nonexistent disk sda in ignoredisk command" then look to this last setting.

VM Creation Summary
^^^^^^^^^^^^^^^^^^^
So in the above example we have added a single system drive/disk to our virtual machine; the system-drive.
This is good practice and can simplify the install; as well as removing the possibility of accidentally installing onto existing data drives.

The Rockstor Install
^^^^^^^^^^^^^^^^^^^^
It only remains for you to boot the above configured Virtual Machine via the **Begin Installation** button in the top left of the last dialog.

.. image:: VMM_iso_boot.png
    :scale: 100%
    :align: center

Selecting the **Install Rockstor 3** option via the **Return Key** should result in

.. image:: VMM_Installation_summary_screen.png
    :scale: 100%
    :align: center

N.B. If you do not see the whole of the graphical install screen like in the above image you can select **View** and then **Resize to VM**

Following the graphical installers prompts should result in a problem free install and once complete the virtual system should rebooted and the initial minimal configuration can be done.

Initial first boot configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The rest of Rockstor's configuration is done via it's Web GUI interface; simply point you browser as the indicated ip address. The result should be similar to:


















