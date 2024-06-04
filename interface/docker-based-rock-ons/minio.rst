.. _minio_rockon:

MinIO Rock-on
=============

Before you install MinIO, you should understand the prerequisites
and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirement.


.. _minio_whatis:

What is MinIO
-----------------

`MinIO <https://min.io/product/overview>`_ is an open-source, high-performance, distributed
S3-compatible object storage system. MinIO can scale from a single server with
a single object store all the way to a fault-tolerant commercial-grade
distributed infrastructure. This MinIO Rock-on targets the low end, creating a
single MinIO server using a single Rockstor share as its object store. This
configuration should be perfect for catching backups on a home server, for
example.

This MinIO Rock-on does not implement encryption. If connections between the
client and the MinIO server traverse a network lacking physical security,
consider either using a VPN or putting MinIO behind a reverse proxy for
encryption. Implementing native encryption in the MinIO Rock-on, although
possible, would require post-installation configuration and on-going
certificate management in addition to the MinIO Rock-on installation. This
would violate the '"all-in-one" user experience' guideline in
:ref:`contributerockons`.

Simply point your MinIO-enabled client at
the URL for your server (``http://domain-name:port``) and use the Access Key
(username) and Secret Key (password) that you specified during installation.


.. _minio_install:

Installing MinIO Rock-on
----------------------------
The MinIO Rock-on requires a Rockstor share to use as the object store.
You should create this share in a pool with sufficient space for your needs
before beginning the MinIO Rock-on installation.

Once your share is ready, click the "Install" button next to the MinIO listing
on the Rock-ons page.

.. image:: /images/interface/docker-based-rock-ons/minio_install.png
   :width: 100%
   :align: center


.. _minio_share:

MinIO Share
^^^^^^^^^^^^^^^^
Specify the share you created for MinIO.

.. image:: /images/interface/docker-based-rock-ons/minio_share.png
   :width: 100%
   :align: center


.. _minio_port:

MinIO Ports
^^^^^^^^^^^^^^^
The default "MinIO Admin Portal Port" is 9001; the default "MinIO API Port"  
is 9000.  You can choose different ports if you are already using 9000/9001 
for another application, but it is wise to stick with the standard ports, 
if possible.

.. image:: /images/interface/docker-based-rock-ons/minio_ports.png
   :width: 100%
   :align: center


.. _minio_environment:

MinIO Environment
^^^^^^^^^^^^^^^^^^^^^^
MinIO needs values for three environment variables.  "MinIO Admin User" 
(3 to 128 alphanumeric characters) and 
"MinIO Admin Password" (8 to 128 alphanumeric characters) 
are the username and password you will use on the Web 
interface and in your S3-compatible client software.  "MinIO Console Address" 
must be set to the same port you chose in the previous dialog for 
"MinIO Admin Portal Port", but with a colon in front.  (":9001", for 
example.)

.. image:: /images/interface/docker-based-rock-ons/minio_environment.png
   :width: 100%
   :align: center


.. _minio_verify:

MinIO Verify and Submit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Verify the information you've provided is correct, then click "Submit".

.. image:: /images/interface/docker-based-rock-ons/minio_submit.png
   :width: 100%
   :align: center

You'll see a screen indicating the Rock-on is being installed.  Click "Close".

.. image:: /images/interface/docker-based-rock-ons/minio_installing.png
   :width: 100%
   :align: center

MinIO Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Congratulations!  You can use the "MinIO UI" button to go to the Web
management interface to view and create storage objects, and you can point
your S3-compatible application at your new server. 

.. image:: /images/interface/docker-based-rock-ons/minio_finished.png
   :width: 100%
   :align: center
