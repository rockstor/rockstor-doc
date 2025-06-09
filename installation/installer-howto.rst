.. _installer_howto:

Rockstor’s “Built on openSUSE” installer
========================================

.. _installer_thanks:

Thanks
------

Rockstor’s developers would like to thank the entire OSS community for making
any of this possible.
Specifically with our recent move / rebase on openSUSE Leap, our thanks go to
the openSUSE/SuSE organisations and the larger community for the extreme
generosity we all benefit from in a myriad of seen and unseen ways.

**Please note: Rockstor is in no way affiliated with openSUSE/SuSE and does
not wish, under any circumstances, to misrepresent these organisations.**
*Any errors you encounter are most likely our fault and we try, on a current
volunteer basis, to support our users via our*
`friendly forum <https://forum.rockstor.com/>`_.

It is hoped that Rockstor’s ongoing small contribution back to the larger
community is of value, and if this is so for you please consider either
subscribing to our Stable Channel updates or taking part in our developer
orientated Testing Channel.
Details of these Rockstor package update services are available in our
subsection on :ref:`update_channels`. Rockstor’s ongoing development is wholly
dependent on community support via either of these channels and by positively
participating in our forum, linked above.
It is hoped that in time we can contribute back more significantly, and possibly
financially, as our own community and Stable Channel subscriptions grow.
Also note that irrespective of Rockstor update channel selection or otherwise,
upstream updates are available by normal command line means and via our Web-UI.
See :ref:`dash_and_updates` later in this guide for the details.

.. _our_kiwi_ng_installer:

Our "Built on openSUSE" Kiwi-ng created installer
-------------------------------------------------

The existence of this installer, and those of many Linux distributions, is down
in a major part to the Kiwi installer creation tool.
I would specifically like to thank `Marcus Schafer <https://github.com/schaefi>`_
and David `Cassany Viladomat <https://github.com/davidcassany>`_ of openSUSE/SuSE for
their timely and rapid oem, partition, swap, and btrfs related fixes that were
required for our initial version of this installer.
Please contribute to this important multi-distribution upstream project if you have
the means and/or talent `KIWI - Next Generation <https://github.com/OSInside/kiwi>`_.

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
Only devices less than 5000 GB (5 TB) are shown.
Larger disks are assumed to be data disks.

Destroying ALL data on ..., continue ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Do not proceed if at all unsure.
This will wipe the entire contents of the indicated drive.

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
agreement.
There are about 3 pages: Enter key to 'Exit' & 'Agree', or cursor
keys to select 'No' in pop up.

Select Time Zone
^^^^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/select_time_zone.png
   :align: center

Use cursor keys to highlight, then the "Enter" key to select.

Set the 'root' User's Password
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /images/installation/installer-howto/enter_root_password.png
   :align: center

----

.. image:: /images/installation/installer-howto/confirm_root_password.png
   :align: center

.. _ssh_key_enrollment:

SSH key Enrollment (TW/SR)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Tumbleweed/Slowroll **(TW/SR)** only.
Recommended: password SSH is disabled by default on these variants.

.. image:: /images/installation/installer-howto/ssh_key_enrollment_1.png
   :align: center

Client SSH instructions
~~~~~~~~~~~~~~~~~~~~~~~

.. image:: /images/installation/installer-howto/ssh_key_enrollment_2.png
   :align: center

All details, e.g. IP address, will vary from one install to another.

Client SSH login
~~~~~~~~~~~~~~~~

.. code-block:: console

    ssh root@192.168.2.105

    The authenticity of host '192.168.2.105 (192.168.2.105)' can't be established.
    ED25519 key fingerprint is SHA256:MJWWw94HSmgPkrVE3SHf2WlPkHRON8Q6y7oTLoSQEhs.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added '192.168.2.105' (ED25519) to the list of known hosts.
    ssh-pairing: Received 1 public keys
    Received disconnect from 192.168.2.105 port 22:11: Bye Bye
    Disconnected from 192.168.2.105 port 22

Enrollment Confirmation
~~~~~~~~~~~~~~~~~~~~~~~

.. image:: /images/installation/installer-howto/ssh_key_enrollment_3.png
   :align: center

----

.. image:: /images/installation/installer-howto/ssh_key_enrollment_4.png
   :align: center

----


.. image:: /images/installation/installer-howto/ssh_key_enrollment_5.png
   :align: center

**The enrolled key based SSH login may require a reboot to become active.**
**Finish the install before enacting any reboot.**

.. _installer_user_creation:

User Creation - Cockpit Web-UI  (TW/SR)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Skip advised**: Rockstor's Web-UI has :ref:`User Management<users>` built-in.
If the above :ref:`SSH key Enrollment<ssh_key_enrollment>` was skipped, consider creating a dedicated user at this point.

`Cockpit <https://cockpit-project.org/>`_ is not `installed <https://cockpit-project.org/running.html#tumbleweed>`_ and
**Rockstor compatibility is unknown.**
**Experienced user testing feedback is welcome - but there is no assurance of future compatibility.**

.. image:: /images/installation/installer-howto/user_creation_dialog.png
   :align: center

Wait for the "Rockstor bootstrapping tasks"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Rockstor bootstrapping task may take **around 3-4 minutes** to appear,
depending on computer, drive, and internet speed.
This same delay occurs during every `rockstor` package update,
as rockstor-build.service downloads and builds from `PyPi <https://pypi.org/>`_.

.. image:: /images/installation/installer-howto/wait_for_rockstor_tasks.png
   :align: center

Press the Enter key to show the login prompt again.

Login as the 'root' user
^^^^^^^^^^^^^^^^^^^^^^^^

This one-off login is required to find the Web-UI's address for use in your
browser.

.. image:: /images/installation/installer-howto/root_login_myip.png
   :align: center

- Optional: consider running :code:`zypper refresh` and awaiting its completion.
  This can help avoid delays in the Web-UI offering upstream OS updates.

Enter your systems' displayed :code:`https://...` address into your browser's URL bar.

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
introduces the Rockstor package Update Channels.
A link to our documentation explaining these channels is included:

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


.. note::

   For advanced installation scenarios see: :ref:`special_install_scenarios`.
