.. _adguard_home_rockon:

AdGuard Home Rock-on
==========================

Before you install the Adguard Home rock-on, you should understand the
prerequisites and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirements.


.. _adguard_home_whatis:

What is AdGuard Home
---------------

`AdGuard Home <https://adguard.com/en/adguard-home/overview.html>`_ AdGuard Home is a 
network-wide software for blocking ads and tracking. After you set it up, it'll
cover all your home devices, and you won't need any client-side software for that.
AdGuard Home is available for amd64 and arm64 architecture.

.. _adguard_doc:

AdGuard Home Documentation
---------------------

AdGuard Home features and documentation can be found at `documentation <https://github.com/AdguardTeam/AdGuardHome>`_.
Note that there is some preparation necassary to get this rock-on to work.

.. _adguard_install:

Installing the Adguard Home rock-on
------------------------------
This rock-on does require two additional shares to be set. 
E.g. **adguard_Config** and **adguard_data**. These shares have 
to be setup up before installation. 

Additional we are changing the share permissions for the **adguard_data**.
Navigate to *Storage* > *Shares* then select the created data share. Navigate 
to *Access Control* and the click on *Edit*. Change the settings like shown in
the picture. 

.. image:: /images/interface/docker-based-rock-ons/adguard_share_permission.png
   :width: 100%
   :align: center

We now have to add the *macvlan-network* for the Rock-on. For that we have to 
use a command with has to be changed to confirm with your local network. 

.. code:: bash 

   docker network create -d macvlan --subnet=192.168.178.0/24 --ip-range=192.168.178.58/32 --gateway=192.168.178.1 -o parent=eth0 adguard-home

The value for the *--subnet* has to be change to the ip range of your local network.
Values like these are examples: 192.168.1.0/24, 192.168.100.0/24, etc.

In this example the *--ip-range* value is the to the single IP-Adress: *192.168.178.58*.
Please select a unused ip address in your local *--ip-range*. If your using a DHCP-Server
either reserve this address permantly or choose an address outside of the DHCP-Server range.

The value for *--gateway* has to be set to the IP-Adress of your gateway of your local network.

The value for *parent* has to be set to the name of your network. Found under *System* > *Network*.
The default and expected value is *eth0*. 

The last entry of the command *adguard-home* has to be kept the same. This is fixed in 
the Rock-on configuration.

With the shares and the network created the Rock-on can be installed.







We are now ready to start the installation of the Netdata rock-on. Click the
*Install* button next to the **Netdata (official)** listing on the *Rock-ons*
page.

.. image:: /images/interface/docker-based-rock-ons/netdata_install.png
   :width: 100%
   :align: center


.. _netdata_port:

Web-UI port
^^^^^^^^^^^
This corresponds to the port used to reach Netdata's web-UI. Note that
this port **must** be set to **19999**.

.. image:: /images/interface/docker-based-rock-ons/netdata_webUI_port.png
   :width: 100%
   :align: center


.. _netdata_pgid:

PGID
^^^^
This corresponds to the **docker group GID** that was identified above (see
:ref:`netdata_install` above).

.. image:: /images/interface/docker-based-rock-ons/netdata_PGID.png
   :width: 100%
   :align: center


.. _netdata_verify:

Verify and Submit
^^^^^^^^^^^^^^^^^
Verify the information you've provided is correct, then click **Submit**.

.. image:: /images/interface/docker-based-rock-ons/netdata_verify.png
   :width: 100%
   :align: center

You'll see a screen indicating the Rock-on is being installed.  Click "Close".

.. image:: /images/interface/docker-based-rock-ons/netdata_final.png
   :width: 100%
   :align: center


Netdata Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Congratulations! You can use the **Netdata (official) UI** button to go to the
web interface to view and monitor all the metrics collected by Netdata.

.. image:: /images/interface/docker-based-rock-ons/netdata_UI.png
   :width: 100%
   :align: center
