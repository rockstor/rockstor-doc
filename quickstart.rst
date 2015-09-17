
.. _quickstartguide:

Quick start
===========

.. _minsysreqs:

Minimum system requirements
---------------------------

Rockstor is a complete Linux distribution (iso) to be installed
directly on hardware or on a VM with the following minimum system requirements.

* 64-bit Intel or AMD processor
* 2GB RAM
* 8GB hard disk space for the OS
* One or more additional hard drives
* 1Gbps Ethernet interface (with internet access -- for updates)
* CD/DVD drive or USB port for installation

Download Rockstor
-----------------

Rockstor `download options <http://rockstor.com/download.html>`_. Create a
bootable CD or USB drive from the downloaded iso and proceed to the next
section for installation.

.. raw:: html

   <div class="alert alert-info">
   For convenience, you can also purchase a USB install disk from <a href="http://shop.rockstor.com/collections/diy-accessories/products/rockstor-usb-install-disk" target="_blank">our shop</a>.
   Thanks for your support!
   </div>

To create a USB install disk, you can use the dd command on Linux or Mac. For
example, if your USB drive is /dev/sdb, the command would be::

  dd if=Rockstor-3.8-0.iso of=/dev/sdb

If you are on Windows, you can use `dd for Windows <http://www.chrysocome.net/dd>`_ or `Rawrite32 <http://www.netbsd.org/~martin/rawrite32/>`_.

.. _osinstall:

Installation
------------

Installing Rockstor is quick and straight forward. Since Rockstor is based on
CentOS and uses the same anaconda installer the installation looks similar to
that of CentOS, Redhat, or Fedora.

To find out what the installation process looks like, watch a 5 minute video of
`a Rockstor VirtualBox install <http://youtu.be/00k_RwwC5Ms>`_, or see
:ref:`vmmrockstorinstall` section of our :ref:`kvmsetup`.

.. raw:: html

   <div class="alert alert-warning">
   <strong>Important!</strong> Installing RockStor deletes existing data on the system
   drive(s) selected as installation destination.
   </div>

   <div class="alert alert-info">
   If you need further assistance during or post install, you
   can post a topic on our <a href="http://forum.rockstor.com">Forum</a> or send an e-mail to support@rockstor.com
   </div>

1. Boot your machine with the Rockstor CD and the splash screen will
   appear. Press enter and the graphical installer will start momentarily
   and display the **Installation Summary screen**

2. **Installation Summary screen**

   On this screen, multiple parameters can be configured together.

   a. Click on the **Date & Time** to change the default timezone.

   b. A network connection is required and the installation will not proceed
      otherwise. The default is DHCP which the installer automatically picks
      up. You can configure the network manually, but make sure your system has
      a working ip address for the installation to proceed.

   c. Under the **Installation Destination** there may be further action
      required if there are partitions on sda. By default the sda hard drive is
      selected and set to be auto partitioned but only if blank. If not then an
      exclamation icon indicates the need for attention. Please see our
      :ref:`wiping_disk` for more details.

      For the default automatic partitioning, just click **DONE**.

      If you are an advanced user, you can go with a custom partitioning
      scheme. However, note that Rockstor only supports **BTRFS** for its root
      filesystem.

    .. raw:: html

        <div class="alert alert-warning">
        <strong>Important!</strong> Installing RockStor deletes existing data on the system
        drive(s) selected as installation destination.
        </div>

   d. Once the installation configuration is complete and there are no amber
      icons, click on **Begin Installation** button to start the package
      installation.

3. **Package Installation**

   On the next screen, package installation begins in the background and you
   must set the root password. You can **optionally** create an additional
   user.

4. **Boot into Rockstor**

   Package installation takes a few minutes and once it's complete you can
   reboot, remove the install cd and boot into Rockstor. Once the system boots
   up, the url for web-ui is displayed above the login prompt. The url is
   simply https://<IP_ADDRESS_OF_THE_SYSTEM>

5. **Setup Rockstor**

   Go to Rockstor's web-ui from your web browser and complete the initial setup.
