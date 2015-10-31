
.. _quickstartguide:

Quick start
===========

.. _minsysreqs:

Minimum system requirements
---------------------------

Rockstor is a complete Linux distribution (iso) to be installed directly on
hardware or as a VM with the following minimum system requirements and
recommendations.

* 64-bit Intel or AMD processor
* 2GB RAM or more. (recommended)
* 8GB hard disk space for the OS
* One or more additional hard drives for data (recommended)
* Ethernet interface (with internet access -- for updates)
* a UPS (if desired) that is supported by `nut <http://www.networkupstools.org/>`_
* CD/DVD drive or USB port for installation

Download Rockstor
-----------------

Rockstor `download options <http://rockstor.com/download.html>`_. Create a
bootable CD or USB drive from the downloaded iso and proceed to the
:ref:`installation` section.

.. raw:: html

   <div class="alert alert-info">
   For convenience, you can also purchase a USB install disk from <a href="http://shop.rockstor.com/collections/diy-accessories/products/rockstor-usb-install-disk" target="_blank">our shop</a>.
   Thanks for your support!
   </div>

.. _makeusbinstalldisk:

Making a Rockstor USB install disk
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To create a USB install disk on Linux or Mac one can use the dd command. For
example if your USB device is /dev/sdc then from within the directory
containing your downloaded Rockstor iso file the command would be:-

  dd if=Rockstor-3.8-9.iso of=/dev/sdc

Note that the .iso file name will vary depending on the Rockstor version.

If you are on Windows, you can use `dd for Windows <http://www.chrysocome.net/dd>`_ or `Rawrite32 <http://www.netbsd.org/~martin/rawrite32/>`_.

**Please note** the following USB image writing programs have been found to
produce **NON working USB install disks** when used with the Rockstor iso file.

* Unetbootin
* Rufus

.. _osinstall:

Installation
------------

Installing Rockstor is quick and straight forward as shown in `this install
video <https://www.youtube.com/watch?v=yEL8xMhMctw>`_. Since Rockstor is based
on CentOS and uses the same anaconda installer the installation looks similar
to that of CentOS or Fedora. You can also read
:ref:`vmmrockstorinstall` section of our :ref:`kvmsetup` for more information
about installation.

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
