.. _Spoolman_rockon:

Spoolman Rock-on
================

Before you install Spoolman, you should understand the prerequisites
and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirement.


.. _Spoolman_whatis:

What is Spoolman
-----------------

From the author's repository description: "Spoolman is a self-hosted web service
designed to help you efficiently manage your 3D printer filament spools and monitor their usage. 
It acts as a centralized database that seamlessly integrates with 
popular 3D printing software like OctoPrint and Klipper/Moonraker.  
When connected, it automatically updates spool weights as printing progresses,
giving you real-time insights into filament usage."  

For more information go to https://github.com/Donkie/Spoolman.
Be sure to check for compatibility with your print system.


.. _Spoolman_install:

Installing Spoolman Rock-on
----------------------------
The Spoolman Rock-on requires a Rockstor share to use as the object store.
You should create this share in a pool with sufficient space for your needs
before beginning the Spoolman Rock-on installation.

Once your share is ready, click the "Install" button next to the Spoolman listing
on the Rock-ons page.

.. image:: /images/interface/docker-based-rock-ons/Spoolman_rockons.png
   :width: 100%
   :align: center


.. _Spoolman_share:

Spoolman Share
^^^^^^^^^^^^^^^^
Specify the share you created for Spoolman.

.. image:: /images/interface/docker-based-rock-ons/Spoolman_share.png
   :width: 100%
   :align: center

The Spoolman docker app does not run as root, so you must change the 
ownership of the share so that the user is the same as the user you 
created when installing Rockstor (the "admin" user) and the group is 
"users".  Give group full permissions, as well.

.. image:: /images/interface/docker-based-rock-ons/Spoolman_shareowner.png
   :width: 100%
   :align: center

.. _Spoolman_environment:

Spoolman Environment
^^^^^^^^^^^^^^^^^^^^
Spoolman does not need any environment variable defined.


.. _Spoolman_port:

Spoolman Port
^^^^^^^^^^^^^
Spoolman needs to know what TCP port you would like to assign to the Web admin interface. 
Select a port that is not currently in use on your RockStor server.

.. image:: /images/interface/docker-based-rock-ons/Spoolman_port.png
   :width: 100%
   :align: center


.. _Spoolman_verify:

Spoolman Verify and Submit
^^^^^^^^^^^^^^^^^^^^^^^^^^
Verify the information you've provided is correct, then click "Submit".

.. image:: /images/interface/docker-based-rock-ons/Spoolman_submit.png
   :width: 100%
   :align: center

You'll see screens indicating the Rock-on is being installed.  Click "Close".

.. image:: /images/interface/docker-based-rock-ons/Spoolman_installing.png
   :width: 100%
   :align: center

.. image:: /images/interface/docker-based-rock-ons/Spoolman_inprogress.png
   :width: 100%
   :align: center


.. _Spoolman_success:

Spoolman Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Congratulations!  You can click the red "Spoolman UI" button or open a Web browser 
and navigate to `http://ROCKSTOR-IP:PORT-NUMBER` to go to the Spoolman Web management interface. 
There you can begin to create and manage your filament library. 

.. image:: /images/interface/docker-based-rock-ons/Spoolman_success.png
   :width: 100%
   :align: center

.. image:: /images/interface/docker-based-rock-ons/Spoolman_homepage.png
   :width: 100%
   :align: center
