.. _adguard_home_rockon:

AdGuard Home Rock-on
==========================

Before you install the Adguard Home rock-on, you should understand the
prerequisites and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirements.


.. _adguard_home_whatis:

What is AdGuard Home
---------------------

`AdGuard Home <https://adguard.com/en/adguard-home/overview.html>`_ AdGuard Home is a 
network-wide software for blocking ads and tracking. After you set it up, it'll
cover all your home devices, and you won't need any client-side software for that.
AdGuard Home is available for amd64 and arm64 architecture.

.. _adguard_doc:

AdGuard Home Documentation
---------------------------

AdGuard Home features and documentation can be found here: `documentation <https://github.com/AdguardTeam/AdGuardHome>`_.
Note that there is some preparation required to get this rock-on to work.

.. _adguard_install:

Installing the Adguard Home Rock-on
-------------------------------------
This rock-on requires two additional shares to be set. 
E.g. **adguard_config** and **adguard_data**. These shares must be 
setup up before the installation. 


We will also change the share permissions for **adguard_data**.
Navigate to *Storage* > *Shares* and select the data share you created. Navigate to 
to *Access Control* and click on *Edit*. Change the settings as shown in
the picture. 

.. image:: /images/interface/docker-based-rock-ons/adguard_share_permission.png
   :width: 100%
   :align: center

Now we need to add the *macvlan-network* for the rock-on. To do this, we need to 
with a command that needs to be changed to match your local network. 

.. code:: bash 

   docker network create -d macvlan --subnet=192.168.178.0/24 --ip-range=192.168.178.58/32 --gateway=192.168.178.1 -o parent=eth0 adguard-home

The value for *--subnet* must be changed to the ip range of your local network.
Values like these are examples: 192.168.1.0/24, 192.168.100.0/24, etc.

In this example the *--ip-range* value is the to the single IP-Adress: *192.168.178.58*.
Please select a unused ip address in your local *--ip-range*. If your using a DHCP-Server
either reserve this address permantly or choose an address outside of the DHCP-Server range.

The value for *--gateway* has to be set to the IP-Adress of your gateway of your local network.

The value for *parent* has to be set to the name of your network. Found under *System* > *Network*.
The default and expected value is *eth0*. 

The last entry of the command *adguard-home* has to be kept the same. This is fixed in 
the Rock-on configuration.

We are now ready to start the installation of the AdGuard Home rock-on. Click the
*Install* button next to the **AdGuard Home** listing on the *Rock-ons*
page.

.. _adguard_home_shares:

Set Shares
^^^^^^^^^^^

We need to only need to set the shares for the installation. Set them in the Web-UI.
Use the shares we configured before.

.. image:: /images/interface/docker-based-rock-ons/adguard_share_installation.png
   :width: 100%
   :align: center


.. _adguard_home_port:

Web-UI port
^^^^^^^^^^^
This corresponds to the port used to reach AdGuard Home web-UI. Note that
the Port *3000* is the port for the initial configuration.
After the configuration is done, the Web-UI is reachable under port *80* or *443*.
These are set without any User Interaction.

Verify and Submit
^^^^^^^^^^^^^^^^^
Verify the information you've provided is correct, then click **Submit**.
You'll see a screen indicating the Rock-on is being installed.  Click "Close".


AdGuard Home Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Congratulations! You can see the **AdGuard Home** entry in in the list of installed Rock-ons.
To reach the Webinterface you have to use the configured value of *--ip-range* and the port *3000*.
Using the example values the UI is reachable under *http://192.168.178.58:3000*

