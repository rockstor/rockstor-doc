.. _rustfs_rockon:

RustFS Rock-on
==============

Before you install the RustFS Rock-on, you should understand the 
prerequisites and configurations common to all Rockstor 
:ref:`rockons_intro`, specifically the :ref:`rockons_preinstall` 
and :ref:`rockons_root` requirements.


.. _rustfs_whatis:

What is RustFS?
---------------

`RustFS <https://rustfs.com>`_ is an open-source, high-performance 
S3-compatible object storage system. 
RustFS can scale from a single server with a single object store 
all the way to a fault-tolerant commercial-grade distributed infrastructure. 
This RustFS Rock-on targets the low end, creating a
single RustFS server using a single Rockstor share as its object store. 
This configuration should be perfect for catching and storing backups on a home 
server, for example.

This RustFS Rock-on does not implement encryption. 
If connections between the client and the RustFS server traverse a network 
lacking physical security, consider either using a VPN or putting RustFS 
behind a reverse proxy for encryption. 
Implementing native encryption in the RustFS Rock-on, although
possible, would require post-installation configuration and on-going
certificate management in addition to the RustFS Rock-on installation. 
This would violate the '"all-in-one" user experience' guideline in
:ref:`contributerockons`.

Once installation is complete you can point your S3-compatible client at
the URL for your server (``http://rockstor-server-address:9001``) and use 
the Access Key and Secret Key that you specified during installation.


.. _rustfs_migration:

Migration from Other S3-compatible Object Stores
------------------------------------------------

If you are switching from another S3-compatible object server 
(MinIO, for example), be aware that there presently is no 
direct migration tool.  Specifically, you cannot simply reuse 
a share full of MinIO objects by specifying it as the share for 
RustFS.  The only migration option for now is to use an S3 
client software package such as `MinIO Client <https://github.com/minio/mc>`_ 
to copy the objects from MinIO to RustFS.


.. _rustfs_documentation:

RustFS Documentation
--------------------
Official documentation for the RustFS project can be found at 
<https://docs.rustfs.com/>.


.. _rustfs_install:

Installing the RustFS Rock-on
-----------------------------
The RustFS Rock-on requires a Rockstor share to use as the object store.
You should create this share in a pool with sufficient space for your needs
before beginning the RustFS Rock-on installation.

The RustFS Docker container runs as user ID (UID) 10001, group ID (GID) 10001.  
Before starting the installation process, create a user with UID 10001 and a 
group with GID 10001, then assign ownership of the RustFS share to that user 
and group.  
See :ref:`users` for details on creating users and groups, and 
:ref:`accesscontrol` for setting share access controls.

Once your share is ready, click the "Install" button next to the RustFS listing
on the Rock-ons page.

.. image:: /images/interface/docker-based-rock-ons/rustfs_install.png
   :width: 100%
   :align: center


.. _rustfs_share:

Create the RustFS Share
-----------------------
Specify the share you created for RustFS.

.. image:: /images/interface/docker-based-rock-ons/rustfs_share.png
   :width: 100%
   :align: center

.. _rustfs_ports:

RustFS Ports
------------

RustFS needs to know what TCP ports you would like to assign to the 
S3 Application Programming Interface (API) and to the Web management 
interface. The standard ports for S3-compatible servers are 9000 (API) 
and 9001 (Web UI).  Specify those standard ports unless you have an 
application that requires non-standard ports, or you have another 
Rock-on already using those ports.

.. image:: /images/interface/docker-based-rock-ons/rustfs_ports.png
   :width: 100%
   :align: center


.. _rustfs_environment:

Set the RustFS Environment Variables
------------------------------------
RustFS needs values for three environment variables.  
"Access Key" (3 to 128 alphanumerics), 
"Secret Key" (8 to 128 alphanumerics), and 
"Enable Console".  
"Access Key" and "Secret Key" are the username and password you 
will use on the Web management interface and in your S3-compatible 
client software.
"Enable Console" should be set to "true" unless 
you have some reason for disabling the Web management interface.

.. image:: /images/interface/docker-based-rock-ons/rustfs_environment.png
   :width: 100%
   :align: center


.. _rustfs_verify:

RustFS Configuration Verify and Submit
--------------------------------------
Verify the information you've provided is correct, then click "Submit".

.. image:: /images/interface/docker-based-rock-ons/rustfs_submit.png
   :width: 100%
   :align: center

You'll see a screen indicating the Rock-on is being installed.  Click "Close".

.. image:: /images/interface/docker-based-rock-ons/rustfs_installing.png
   :width: 100%
   :align: center


.. _rustfs_success:

RustFS Installation Successful
------------------------------
Congratulations!  Your installation is complete.

.. image:: /images/interface/docker-based-rock-ons/rustfs_finished.png
   :width: 100%
   :align: center


.. _rustfs_console:

RustFS Web Console Interface
----------------------------
You can use the "RustFS UI" button to go to the 
RustFS Web management interface.  
There you can view and create storage objects.  
Point your S3-compatible application at your new server and you are 
up and running with RustFS block storage. 

.. image:: /images/interface/docker-based-rock-ons/rustfs_console.png
   :width: 100%
   :align: center
