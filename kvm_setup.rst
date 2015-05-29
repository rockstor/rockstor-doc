Rockstor in a GNU/Linux Kernel Virtual Machine (KVM)
====================================================
A quick and easy way to evaluate Rockstor is by using a virtual machine. A virtual machine instance of Rockstor is also invaluable as part of a build environment.

If you are using a Linux desktop you have the option to use the GNU/linux KVM and its associated GUI Virtual Machine Manager.  This can be more efficient than the more well know Oracle VirtualBox.

Can I run the Linux KVM
-----------------------
This depends on weather you CPU has the appropriate capabilities; to find out on an ubuntu desktop you can install the cpu-checker program with the following command::

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

N.B. it is required that one logout and then back in again after the above installs as then your linux user is able to acquire their new group privileges.

Setting up a KVM for Rockstor
-----------------------------






