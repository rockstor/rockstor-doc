.. _special_install_scenarios:

Special Installation Scenarios
==============================

Since Rockstor can accommodate a wide range of hardware configurations, as well
as virtual machine set ups, there have been instances reported over the years that
required some specific actions to enable setting up Rockstor on a new system.
While the friendly `Rockstor forum <https://forum.rockstor.com>`_ contains many more
scenarios and resolutions that can be searched for, some recurring themes are
documented below:

Assign static IP address after installation but before WebUI setup
------------------------------------------------------------------

If during setup the network architecture requires a static IP address on the Rockstor appliance's
network interface :code:`Network Manager` can be used to force a static IP address on the network interface.

Check Network connection using the command line:

.. code-block:: console

    Rockstorsys:~$ nmcli connection show
    NAME     UUID                                  TYPE      DEVICE
    enp0s3   aa44c29f-33e8-358f-879b-e0b8efae27f3  ethernet  enp0s3

In order to make this a static connection, here is an example on how this can be set up using `nmcli`:

.. code-block:: console

   nmcli connection modify 'enp0s3' \
      connection.autoconnect  yes \
      ipv4.method manual \
      ipv4.address 192.168.22.199/24 \
      ipv4.gateway 192.168.22.1 \
      ipv4.dns 8.8.8.8, 8.8.4.4.

Upon successful completion of the command the connection will receive a static IP address:

* automatically (i.e. whenever the network management is started)
* static address with
* IP address of 192.168.22.199 and
* Gateway of 192.168.22.1 and
* DNS1 and DNS2 server 8.8.8.8 and 8.8.4.4 respectively.

To move the connection back to `DHCP` mode, the above settings need to be reverted:

.. code-block:: console

   nmcli con mod "enp0s3" \
     ipv4.method "auto"
     ipv4.addresses "" \
     ipv4.gateway "" \
     ipv4.dns ""

For either of these changes to take effect run

.. code-block:: console

   nmcli connection up "enp0s3"

or reboot the system.

.. note::
   The above is meant for setting up a specific connection **before** the installation/configuration is completed using Rockstor's WebUI.
   Once the Rockstor installation is complete, a static IP can be assigned from the WebUI. Under most circumstances neither should be necessary, as most routers today offer IP address reservation that will effectively result in a static IP address assigned to the Rockstor appliance (which by default uses `dhcp` to automatically obtain an IP address from the gateway).

Proxy for private network
-------------------------

In some network architectures, a proxy is required to be able to manage updates from external sources
like OpenSUSE upstream packages, or to check for and update to a new version of the `rockstor` package.

This `KB 7006845 <https://www.suse.com/support/kb/doc/?id=000017441>`_ provides some insights into how
to set up a Proxy using the command line.

VMWare guest tools installation
-------------------------------

As VMWare is a commmon virtualization package that is used by the Rockstor (alongside with others VirtualBox, Proxmox, etc.), there is a useful toolset available that helps with various aspects of the integration between
the host and guest among other tools (similar guest extensions exist under VirtualBox as well): **open-vm-tools**.

There is the option to build this package into the custom installer, so it becomes part of the initial installation routine.
When building a customer installer to include it, using the `Rockstor installer <https://github.com/rockstor/rockstor-installer>`_
the package is already contained in the **rockstor.kiwi** file, albeit commented out.

.. note::

   This is intended for more advanced users that are comfortable creating their own installers with custom content.

To install the package after Rockstor has already been installed on a VMWare Guest instance, go to the command line and run:

.. code:: console

   zypper install open-vm-tools

Subsequent updates to the package will be automatically considered during Rockstor's upstream package checks.
