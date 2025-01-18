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

Now we need to add the *macvlan-network* for the Rock-on.
Using the WebUI's System Shell, execute the command below, after adjusting it according to your local network settings. Since this requires an elevated command prompt, have the `root` user password ready:

.. code:: bash 

   sudo docker network create -d macvlan --subnet=192.168.178.0/24 --ip-range=192.168.178.58/32 --gateway=192.168.178.1 -o parent=eth0 adguard-home


In this example, the *--ip-range* value is the single IP address: *192.168.178.58*.
Please select an unused IP address in your local *--ip-range*. If you use a DHCP server
either reserve this address permanently or choose an address outside the DHCP server range.

The value for *-gateway* must be set to the IP address of the gateway of your local network.

The value for *-parent* must be set to the name of your network. This can be found under *System* > *Network*.
The default and expected value is *eth0*. 

The last entry of the *adguard-home* command must be kept the same.
This network name is set in the Rock-on configuration.

We are now ready to start the installation of the AdGuard Home Rock-on.
Click on the *Install* button next to the **AdGuard Home** listing on the *Rock-ons* page.

.. _adguard_home_shares:

Set Shares
^^^^^^^^^^^

We just need to set up the shares for the installation. Set them in the web interface.
Use the shares we set up earlier.

.. image:: /images/interface/docker-based-rock-ons/adguard_share_installation.png
   :width: 100%
   :align: center


.. _adguard_home_port:

Web-UI port
^^^^^^^^^^^
This is the port used to access the AdGuard Home web interface. Note that
port *3000* is the port for the initial configuration.
After configuration, the Web UI will be accessible on port *80* or *443*.
These ports are set without any user interaction.

Verify and Submit
^^^^^^^^^^^^^^^^^
Verify that the information you've entered is correct, then click **Submit**.
You'll see a screen indicating that the Rock-on is being installed.  Click Close.


AdGuard Home Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Congratulations! You can see the **AdGuard Home** entry in the list of installed rock-ons.
To access the web interface, you need to use the configured value of *--ip-range* and port *3000*.
Using the example values, the UI can be reached at *http://192.168.178.58:3000*.
After configuration, the web interface can be reached at *http://192.168.178.58:80*.

For recommendations of DNS blocklists see : `hagezi dns-blocklists <https://github.com/hagezi/dns-blocklists>`_.

