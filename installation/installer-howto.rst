.. _installer_howto:

Rockstor’s “Built on openSUSE” installer
========================================

.. _installer_thanks:

Thanks
------

Rockstor’s developers would like to thank the entire OSS community for making
any of this possible. Specifically with our recent move / rebase on openSUSE
Leap, our thanks go to the openSUSE/SuSE organisations and the larger
community for the extreme generosity we all benefit from in a myriad of seen
and unseen ways.

**Please note: Rockstor is in no way affiliated with openSUSE / SuSE and does
not wish, under any circumstances, to misrepresent these organisations.**
*Any errors you encounter are most likely our fault and we try, on a current
volunteer basis, to support our users via our*
`friendly forum <https://forum.rockstor.com/>`_.

It is hoped that Rockstor’s ongoing small contribution back to the larger
community is of value, and if this is so for you please consider either
subscribing to our Stable Channel updates or taking part in our developer
orientated Testing Channel. Details of these Rockstor package update services
are available in our subsection on :ref:`update_channels`. Rockstor’s ongoing
development is wholly dependent on community support via either of these
channels and by positively participating in our forum, linked above. It is
hoped that in time we can contribute back more significantly, and possibly
financially, as our own community and Stable Channel subscriptions grow. Also
note that irrespective of Rockstor update channel selection or otherwise,
upstream updates are available by normal command line means and via our Web-UI.
See :ref:`dash_and_updates` later in this guide for the details.

.. _our_kiwi_ng_installer:

Our "Built on openSUSE" Kiwi-ng created installer
-------------------------------------------------

The existence of this installer, and those of many Linux distributions, is down
in a major part to the Kiwi installer creation tool. I would specifically like
to thank `Marcus Schafer <https://github.com/schaefi>`_ and David
`Cassany Viladomat <https://github.com/davidcassany>`_ of openSUSE/SuSE for
their timely and rapid oem, partition, swap, and btrfs related fixes that were
required for our initial version of this installer. Please contribute to this
important multi-distribution upstream project if you have the means and/or
talent `KIWI - Next Generation <https://github.com/OSInside/kiwi>`_.

Initial Selection Screen
^^^^^^^^^^^^^^^^^^^^^^^^

Select the "Install Rockstor- ..." option.
The default is "Boot from Hard Disk".

.. image:: /images/installation/installer-howto/initial_screen.png
   :width: 100%
   :align: center

Use cursor keys to highlight, then the "Enter" key to select.
Only use Failsafe if the 'Install ...' option fails, i.e. the screen goes blank
and does not return.

.. _installer_select_disk:

Select Installation Disk
^^^^^^^^^^^^^^^^^^^^^^^^

This will usually be your smallest disk: dedicated to system only use.
If unsure do not proceed and select <Cancel> via Tab key and then Enter.

.. image:: /images/installation/installer-howto/select_installation_disk.png
   :width: 100%
   :align: center

Use cursor keys to highlight, then the "Enter" key to select.
Only devices less than 5000 GB (5 TB) are shown. Larger disks are assumed to be data
disks.

Destroying ALL data on ..., continue ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Do not proceed if at all unsure. This will wipe the entire contents of the
indicated drive.

.. image:: /images/installation/installer-howto/destroy-all-data.png
   :width: 100%
   :align: center

There will be a short period of scrolling text after this screen.

Loading Rockstor ...
^^^^^^^^^^^^^^^^^^^^

This step may take a while, please be patient.

.. image:: /images/installation/installer-howto/loading-rockstor.png
   :width: 100%
   :align: center

After 100% there will be more scrolling text that may pause for a few minutes
depending on computer and selected drive speed.

Select Locale
^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/select_locale.png
   :align: center

Use cursor keys to highlight, then the "Enter" key to select.

Select Keyboard Layout
^^^^^^^^^^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/select_keyboard.png
   :align: center

Use cursor keys to highlight, then the "Enter" key to select.

.. _installer_license:

Rockstor "Built on openSUSE" installer License Agreement
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Rockstor installer is "Built on openSUSE" and so the consequent
installs are considered modified copies of the indicated openSUSE variant.

The included **rockstor** package is :ref:`rockstor_license`

.. image:: /images/installation/installer-howto/gplv2_license_agreement.png
   :width: 100%
   :align: center

Use cursor keys or Page-up / Page-down (space bar) to view the entire
agreement. There are about 3 pages: Enter key to 'Exit' & 'Agree', or cursor
keys to select 'No' in pop up.

Select Time Zone
^^^^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/select_time_zone.png
   :align: center

Use cursor keys to highlight, then the "Enter" key to select.

Enter Desired root User Password
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/enter_root_password.png
   :align: center

Confirm root User Password
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/confirm_root_password.png
   :align: center

Wait for the "Rockstor bootstrapping tasks"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Rockstor bootstrapping task may take around 3-4 minutes to appear,
depending on computer, drive, and internet speed.
This same delay occurs during every `rockstor` package update,
as rockstor-build downloads and builds from `PyPi <https://pypi.org/>`_.

.. image:: /images/installation/installer-howto/wait_for_rockstor_tasks.png
   :align: center

Press the Enter key to show the login prompt again.

Login as the 'root' user
^^^^^^^^^^^^^^^^^^^^^^^^

This one-off login is required to find the Web-UI's address for use in your
browser.

.. image:: /images/installation/installer-howto/root_login_myip.png
   :align: center

Enter your systems' :code:`https://...` address into your browser,
Chrome/Firefox/.., for the Web-UI.

Visit Rockstor's Web-UI
^^^^^^^^^^^^^^^^^^^^^^^

Rockstor defaults to a self signed https certificate.

Although more secure than 'http' (no 's') your browser will still present a
warning:

.. image:: /images/installation/installer-howto/self_signed_certificate_advanced.png
   :width: 100%
   :align: center

As your Rockstor is on your Local Area Network (LAN) you can add an exception
for this address.
Click Advanced:

.. image:: /images/installation/installer-howto/self_signed_certificate_accept.png
   :width: 100%
   :align: center

Then "Accept the Risk and Continue".
*Do not do this for any site on the internet.*
You can use a 'real' domain certificate with Rockstor but this is an advanced
topic beyond the scope of this installer guide.

.. _webui_setup:

Rockstor Setup and EULA
^^^^^^^^^^^^^^^^^^^^^^^
The following shows example entries for this initial Web-UI setup screen, they
are blank by default.

.. note:: An unprivileged linux user will also be created by this step (UID=1000 GID=100).

.. image:: /images/installation/installer-howto/initial_rockstor_setup_screen.png
   :width: 100%
   :align: center

Note the required "license agreement".
This link opens an additional tab shown below:

.. image:: /images/installation/installer-howto/eula-page.png
   :width: 100%
   :align: center

Welcome banner
^^^^^^^^^^^^^^

Directly after the initial Rockstor setup the following welcome banner
introduces the Rockstor package Update Channels. A link to our documentation
explaining these channels is included:

.. image:: /images/installation/installer-howto/initial_welcome_banner.png
   :align: center

.. _dash_and_updates:


Dashboard and System updates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As the entirety of this installer stands on the shoulders of numerous
OSS giants, it is possible to update all upstream, read openSUSE/SuSE,
provided/curated packages via the flashing icon to the left of the "Uses
openSUSE ..." text in the top right of the Web-UI:

.. image:: /images/installation/installer-howto/dashboard.png
   :width: 100%
   :align: center

Your Rockstor installation is now up and running and ready to be configured.

Update Channel reminder banner
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Until an :ref:`Update Channel <update_channels>` selection has been made,
a reminder banner appears whenever the dashboard is visited:

.. image:: /images/installation/installer-howto/update_channel_reminder_banner.png
   :align: center

Enjoy your Rockstor DIY NAS 'Built on openSUSE'
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All upstream (openSUSE) updates, at time of installer creation, are
pre-applied and their respective repositories enabled by default.
See our FAQ entry: :ref:`faq_rockstor4_repos`

**NOTE: No Rockstor package update repository is configured until an
Update Channel is selected.**


.. _special_install_scenarios:

Special Installation Scenarios
-------------------------------
There a some specific installation use cases that have been reported over the
years, that are documented here:

Assign static IP address after installation but before WebUI setup
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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
* IP address of 192.168.1.199 and
* Gateway of 192.168.22.1 and
* DNS1 and DNS2 server 8.8.8.8 and 8.8.4.4 respectively.

To move the connection back to to `dhcp` mode, the above settings need to be reverted:

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
   Once the Rockstor installation is complete, a static IP can be assigned from the WebUI. Under most circumstances neither
   should be necessary, as most routers today offer IP address reservation that will effectively result in a static IP address
   assigned to the Rockstor appliance (which by default uses `dhcp` to automatically obtain an IP address from the gateway).

Proxy for private network
^^^^^^^^^^^^^^^^^^^^^^^^^

In some network architectures, a proxy is required to be able to manage updates from external sources
like OpenSUSE upstream packages, or check for and update a new version of the Rockstor software.

This `KB 7006845 <https://www.suse.com/support/kb/doc/?id=000017441>`_ provides some insights into how
to set up a Proxy using the command line.

VMWare guest tools installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As VMWare is a commmon virtualization package that is used by the Rockstor (alongside with others VirtualBox, Proxmox, etc.),
there is a useful toolset available that helps with various aspects of the integration between the host and guest among other tools
(similar guest extensions exist under VirtualBox as well): **open-vm-tools**

There is the option to build this package into the custom installer, so it becomes part of the initial installation routine.
When building a customer installer to include it, using the `Rockstor installer <https://github.com/rockstor/rockstor-installer>`_
the package is already contained in the **rockstor.kiwi** file, albeit commented out.

.. note::

   This is intended for more advanced users that are comfortable creating their own installers with custom content.

To install the package after Rockstor has already been installed on a VMWare Guest instance, go to the command line and run:

.. code:: console

   zypper install open-vm-tools

Subsequent updates to the package will be automatically considered during Rockstor's upstream package checks.
