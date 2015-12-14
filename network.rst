.. _network_config:

Network configuration
=====================

Rockstor supports basic network configuration from the Web-UI. Network
interfaces can be configured with DHCP or Static IP
configuration. Configuration using the Web-UI is intuitive and self guided with
helpful tooltips for each input field.

To view or configure network, navigate to **Network Interfaces** screen under
the **System** tab. Rockstor fetches the current state and lists all ethernet
devices and connection information on this screen.

.. image:: images/network_interfaces.png
   :scale: 80%
   :align: center


.. _network_reconfig:

Re-configuring the Network
--------------------------

To **alter** the network configuration **click** on the **pen icon** in the
**Actions column**. Please be aware though that altering the network
configuration of the interface over which you are currently communicating with
Rockstor can be problematic as once submitted you will have to manually change
the IP you use to access Rockstor's Web-UI.


.. _network_dhcp:

Auto (DHCP)
^^^^^^^^^^^

DHCP is a very common and easy way to configure a network interface. This is
the default/recommended method for home-office/small-office type
deployments. Just select *Auto (DHCP)* in the **Config Method** dropdown and
submit. An example of this default configuration is shown below.

.. image:: images/network_dhcp.png
   :scale: 80%
   :align: center


.. _static_ip:

Manual (Static IP)
^^^^^^^^^^^^^^^^^^

It is more common to use Static IP configuration in commercial
installations. Select *Manual* in the **Config Method** dropdown and provide
appropriate input. The following is an example of a Static IP configuration.

.. image:: images/network_static.png
   :scale: 80%
   :align: center


Network Bonding and Teaming
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Network bonding and teaming are currently not supported from the Web-UI. There
are plans to add the support, but in the meantime, they can be configured from
the command line.


Implementation details
^^^^^^^^^^^^^^^^^^^^^^

NetworkManager is used to configure and manage connections. For more
information see `implementation details
<http://forum.rockstor.com/t/network-management-implementation-details/441>`_.
