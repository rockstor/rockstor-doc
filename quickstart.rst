
.. _quickstartguide:

Quick start
===========

.. _minsysreqs:

Minimum system requirements
---------------------------

RockStor is available as a complete Linux distribution (iso) to be installed
directly on hardware or as a VM with the following minimum system requirements.

* 64-bit processor
* 2GB RAM
* 8GB hard disk space for the OS
* One or more additional hard drives
* 1Gbps Ethernet interface with internet access
* CD/DVD drive or USB port for installation

Download Rockstor
-----------------

Download RockStor by clicking `here
<http://rockstor.com/download-form.html>`_. Create a bootable CD or USB drive
from the downloaded iso and proceed to the next section for installation.

Installation
------------

Installing RockStor is straight forward and is similar to installing
Fedora. RockStor is provided as a network install image and requires an
internet connection. Total installation time varies based on internet speeds.

**Important note: Installing RockStor deletes existing data on the system
drive(s) selected as installation destination.**

**Important note: If you need further assistance during or post install, you
can contact us by sending an email to support@rockstor.com**

1. Boot your machine with the RockStor CD and the splash screen will
appear. Select **Install RockStor 2.0** option. The graphical installer should
start momentarily. If you run into graphics problem at this stage, you can
select **Troubleshooting** from the splash screen and then select "Install
RockStor 2.0 in basic graphics mode".

2. The language selection window appears as the first screen soon as the
graphical installer starts. Go with the default -- English(United States),
which is the only supported language and optionally select the "Set keyboard to
default layout for selected language" checkbox at the bottom of the screen and
click the **Continue** button to proceed.

3. On the next(Installation Summary) screen, multiple parameters can be
configured together.

    a. Click on the **Date & Time** to change the default timezone
    .

    b. The network configuration can also be changed from the default dchp
    configuration. Make sure your system has network connection for the
    installation to proceed.

    c. Under the **Storage** section, click on **Installation Destination**. On
    the next screen, all local drives are displayed. You have several options
    here, but for the minimalist setup pick the first drive(it must be atleast
    8GB). If your system can boot from a USB drive, you can dedicate one as the
    root drive and this will free up an extra Hard drive for data. Click **Done**
    at the top after selecting a disk and a popup will appear. Select **BTRFS**
    for the partition scheme. If the disk is free, you'll see the **Continue**
    button. If not, click on **Reclaim space** to wipe the drive clean(this will
    erase all data on the drive) in the next screen.

    d. If there are any errors in the **Storage** or **Software** sections, the
    installation will not proceed and you'll have the opportunity to correct
    them. Soon as all installation requirements are satisfied, click on **Begin
    Installation** button to start the package installation.

4. On the next screen, package installation begins in the background while you
can set the root password. You can also create an additional user, but it's not
necessary.

5. Package installation takes varying time based on your hardware configuration
and internet speed. Please be patient, eventually the installer will finish and
you can reboot into RockStor! Upon reboot, remove the install cd from the
system and boot into RockStor from the install destination(Hard drive or USB)
as selected earlier.

Some configuration steps are necessary before proceeding to use RockStor NAS,
as detailed in the next section

Configuration
-------------

Rockstor's web-ui and CLI are designed to be very user friendly. All of the
storage provisioning tasks must be done via WebUI or CLI. But before proceeding
to provisioning storage, a few steps are necessary

1. Once the system boots, login as the root user
.

2. RockStor is rapidly evolving and software updates are released almost
daily. Update your system::

    [root@localhost ~]# yum update

3. Turn off iptables
::

    [root@localhost ~]# systemctl disable firewalld
    rm '/etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service'
    rm '/etc/systemd/system/basic.target.wants/firewalld.service'
    [root@localhost ~]# systemctl stop firewalld
    [root@localhost ~]#

5. Execute the following two commands in order to start using
the WebUI or CLI.::

    [root@localhost ~]# /opt/rockstor/bin/supervisord -c /opt/rockstor/etc/supervisord.conf
    [root@localhost ~]# /opt/rockstor/bin/supervisorctl start all
    rd: started
    smart_manager: started
    nginx: started
    gunicorn: started
    [root@localhost ~]# /opt/rockstor/bin/supervisorctl status
    gunicorn                         RUNNING    pid 2695, uptime 0:00:17
    nginx                            RUNNING    pid 2694, uptime 0:00:17
    rd                               RUNNING    pid 2699, uptime 0:00:16
    smart_manager                    RUNNING    pid 2701, uptime 0:00:15
    [root@localhost ~]#

6. RockStor WebUI is now ready. Open Firefox browser on a laptop or some other
machine and go to https://rockstor_appliance_ip. **On the first visit, the
browser shows a SSL certificate security warning. Please add the exception to
proceed**.

7. Click through the initial setup process as shown
in :ref:`setup`.

