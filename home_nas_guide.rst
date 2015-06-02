.. _homenasguide

Home Nas Guide
==============

**A guide to setting up a Fileserver / NAS (Network attached storage) for your home using Rockstor**

What is Network Attached Storage (NAS)?
---------------------------------------
      
A Fileserver or NAS is simply a server that stores all your
media (photos, videos, music, documents, other files) and serves it to all
the other computers in your network (or in this case, your home)

You need to store all movies, music, photos, documents that you create 
every day, and be able to access them from any computer in your home. 

This guide looks at how to build your own NAS using easily available
hardware, and the RockStor storage server.
RockStor is an open-source storage server based on linux, that can be
installed on commodity hardware.

Hardware
--------

hardware components for a home NAS build
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      
**A Server**
          
A server with at least `minimum system requirements <http://rockstor.com/docs/quickstart.html#minimum-system-requirements>`_
          
`HP Proliant Microserver <http://www8.hp.com/us/en/products/proliant-servers/product-detail.html?oid=5379860#!tab=features">`_ (Chosen for its small form factor, 4 easily accessible hard drive slots, and eSata capability to expand storage)

Sample configuration:

1. AMD Turion II Neo 1.5 GHz Dual Core (64 bit) CPU
2. 2 GB Memory
3. 1 Gbps Ethernet interface
          
(Note - The Display port on the microserver is VGA so you need a monitor with a VGA port during installation)

**Hard drives**
          
Hard drives to hold your data. Multiple hard drives are recommended, to create pools for RAID capability.</p> 
`Western Digital Red <http://www.wd.com/en/products/products.aspx?id=810>`_ series or the `Seagate NAS <http://www.seagate.com/internal-hard-drives/nas-drives/nas-hdd/>`_ series.
          
**USB Flash drives**

2 USB flash drives, one for the installation media (at least 1GB), and one that will hold the OS (at least 8GB). If you have a CD drive installed, and blank CDs available, you can use a CD as the installation media.</p>

`SanDisk Cruzer Fit <http://www.sandisk.com/products/usb/drives/cruzer-fit/>`_
      
**Software**
      
Download the RockStor iso at `http://www.rockstor.com/downloads <http://rockstor.com/downloads.html>`_

If you are using a USB drive as the installation media, prepare the USB drive with the RockStor iso, by following the instructions `here <https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB>`_

**Installation and Setup**

Insert both the flash drives into the server. Set the flash drive containing the iso as the boot disk, and during installation, select the other flash drive as the destination to install RockStor.

Install RockStor using the installation instructions provided `here <http://rockstor.com/docs/quickstart.html#quickstartguide>`_

**Using RockStor**
        
1. Accessing a shared folder from a Mac client

   To access a shared folder on RockStor from a Mac, you have to create a pool, create a share in the pool, and export it using Samba. This is explained in the :ref:`createshare` section.

   Once you have exported the Share using Samba on RockStor, it should appear as a folder in the Devices menu on your Mac.

2. Accessing a shared drive from a Windows client

   To access a shared folder on RockStor from a Mac, you have to create a pool, create a share in the pool, and export it using Samba. This is explained in the :ref:`createshare` section.

   Once you have exported the Share using Samba on RockStor, it should appear as a folder in the Devices menu on your Mac.


