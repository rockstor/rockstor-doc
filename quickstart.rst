
Quick start
===========

Minimum system requirements
---------------------------

RockStor is available as a complete Linux distribution (iso) to be installed
directly on hardware or as a VM with the following minimum system requirements.

* 64-bit processor
* 1GB RAM
* 6GB hard disk space for the OS
* One or more additional hard drives
* 1Gbps Ethernet interface with internet access
* CD/DVD drive or USB port for installation

Download Rockstor
-----------------

Download RockStor by clicking `here
<http://rockstor.com/download-form.html>`_. Create a bootable CD from the
downloaded iso and proceed to the next section for installation.

Installation
------------

Installing RockStor is straight forward and only takes a few minutes. You can
watch the `installation video <https://www.youtube.com/watch?v=p3izPNhsqA4>`_
or proceed to read further.

1. Boot your machine with the RockStor CD and the splash screen will
appear. Hit Enter to proceed. Anaconda installer starts, which looks identical
to installing a CentOS system.

2. In the first screen, you can skip the media test to proceed to the welcome
banner in the next screen. Hit enter to proceed to the language selection
screen. Proceed with the default english language to the keyboard selection
screen. Again, proceed with the default us keyboard selection.

3. Select your time zone in the next screen and proceed to the Root Password
screen. Type in your desired root password and proceed to the next screen.

4. The next screen is for disk partitioning on which only the first drive(sda)
is shown and selected by default. Select "Use entire drive" and press OK to
proceed. A warning screen appears next. Press "Write changes to disk" and the
installer will proceed for a few minutes without any prompting.

5. The Package Installation screen appears for a few minutes showing the
progress of 255 packages being installed. After the package installation is
complete, hit enter to reboot on the next screen. You may need to pop out the
installation CD for the machine to boot from the hard drive.

Some configuration steps are necessary before proceeding to use RockStor NAS, as detailed in the next section

Configuration
-------------

Rockstor's webUI and CLI are designed to be very user friendly. All of the
storage provisioning tasks be done via WebUI or CLI. But before proceeding to
provisioning storage, a few steps are necessary

1. Make sure that RockStor is assigned an ip address. No additional steps are
necessary for dhcp configuration, but static ip can be assigned during
installation or manually during post install. After initial ip address
assignment, all further configuration changes can be done easily via webUI
and CLI.

2. There is a good chance that RockStor RPMs have been updated. Before
proceeding further, update the installation::

    [root@localhost ~]# yum update rockstor

3. On the first boot, login as root and turn off
iptables.::

    [root@localhost ~]# service iptables stop
    iptables: Flushing firewall rules:                         [  OK  ]
    iptables: Setting chains to policy ACCEPT: filter          [  OK  ]
    iptables: Unloading modules:                               [  OK  ]
    [root@localhost ~]# chkconfig iptables off
    [root@localhost ~]#

4. Nginx service should already be running. Ensure that it
is.::

    [root@localhost ~]# service nginx status
    nginx (pid  1251) is running...
    [root@localhost ~]#

5. Besides Nginx, execute the following two commands in order to start using
the WebUI or CLI.::

    [root@localhost ~]# /opt/rockstor/bin/supervisord -c /opt/rockstor/etc/supervisord.conf
    [root@localhost ~]# /opt/rockstor/bin/supervisorctl start all
    gunicorn: started
    smart_manager: started
    rd: started
    [root@localhost ~]# /opt/rockstor/bin/supervisorctl status
    gunicorn                         RUNNING    pid 1540, uptime 0:00:35
    smart_manager                    RUNNING    pid 1544, uptime 0:00:30
    rd                               RUNNING    pid 1546, uptime 0:00:40
    [root@localhost ~]#

RockStor WebUI is now ready. Open firefox browser on a laptop or some other
machine and go to https://rockstor_appliance_ip. On the first visit, the
browser shows a SSL certificate security warning. Please add the exception to
proceed. You need to click through the initial setup process after which the
main dashboard appears. Watch the WebUI video for a detailed overview.

