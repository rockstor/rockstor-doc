.. _scrutiny_rockon:

Scrutiny Rock-on
==========================

Before you install the Scrutiny rock-on, you should understand the
prerequisites and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirements.


.. _scrutiny_whatis:

What is Scrutiny
----------------

`Scrutiny <https://github.com/AnalogJ/scrutiny>`_ is a Hard Drive
Health Dashboard & Monitoring solution, merging manufacturer provided
S.M.A.R.T metrics with real-world failure rates.

.. _scrutiny_intro:

Introduction from Scrutiny documentation
----------------------------------------

If you run a server with more than a couple of hard drives, you're probably
already familiar with S.M.A.R.T and the :code:`smartd` daemon. If not, it's an
incredible open source project described as the following:

   smartd is a daemon that monitors the Self-Monitoring, Analysis and Reporting
   Technology (SMART) system built into many ATA, IDE and SCSI-3 hard drives.
   The purpose of SMART is to monitor the reliability of the hard drive and
   predict drive failures, and to carry out different types of drive
   self-tests.


Theses S.M.A.R.T hard drive self-tests can help you detect and replace failing
hard drives before they cause permanent data loss. However, there's a couple
issues with :code:`smartd`:

- There are more than a hundred S.M.A.R.T attributes, however :code:`smartd`
  does not differentiate between critical and informational metrics

- :code:`smartd` does not record S.M.A.R.T attribute history, so it can be
  hard to determine if an attribute is degrading slowly over time.

- S.M.A.R.T attribute thresholds are set by the manufacturer. In some cases
  these thresholds are unset, or are so high that they can only be used to
  confirm a failed drive, rather than detecting a drive about to fail.

- :code:`smartd` is a command line only tool. For head-less servers a web UI
  would be more valuable.


.. _scrutiny_doc:

Scrutiny Configuration
----------------------

By default Scrutiny looks for its YAML configurations files located in the
share:

:code:`/mnt2/Scrutiny-Config-Share/scrutiny.yaml`
There are two configuration files available:

- Webapp/API config via :code:`scrutiny.yaml` - `example.scrutiny.yaml <https://github.com/AnalogJ/scrutiny/blob/master/example.scrutiny.yaml>`_.

- Collector config via :code:`collector.yaml` - `example.collector.yaml <https://github.com/AnalogJ/scrutiny/blob/master/example.collector.yaml>`_.

Neither file is required, however if provided, it allows you to configure how
Scrutiny functions.

Notifications
^^^^^^^^^^^^^
Scrutiny supports sending SMART device failure notifications via the following
services:
- Custom Script (data provided via environmental variables)
- Email
- Webhooks
- Discord
- Gotify
- Hangouts
- IFTTT
- Join
- Mattermost
- Pushbullet
- Pushover
- Slack
- Teams
- Telegram
- Tulip

Check the :code:`notify.urls` section of `example.scrutiny.yaml
<https://github.com/AnalogJ/scrutiny/blob/master/example.scrutiny.yaml>`_
for more information and documentation for service specific setup.

Here is a basic example for email notifications:

.. code-block:: yaml

   notify:
      level: 'warn' # 'warn' or 'error'
      urls:
         - "smtp://mail@address.org:password@smtp.server.org:465/?fromAddress=mail@address.org&toAddresses=mail2@address.org"


More information can be found on `Scrutiny GitHub <https://github
.com/AnalogJ/scrutiny#user-content-configuration>`_

.. _scrutiny_install:

Installing the Scrutiny rock-on
-------------------------------
This Rock-on requires a share to store the config files, a **group ID (GID)**
and **user ID (UID)** of the owner for that share. In this case, we will create
a specific **share** and a **user**.

Pre-installation requirements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
First, navigate to *System* > *Users*, and create a new user:

.. image:: /images/interface/docker-based-rock-ons/scrutiny_create_uid.png
   :width: 100%
   :align: center


Take note of the new **user ID (UID)**, you will need this during the
installation of the Rock-on.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_get_uid.png
   :width: 100%
   :align: center


Then navigate to *Storage* > *Shares*, and create a new share:

.. image:: /images/interface/docker-based-rock-ons/scrutiny_config_share.png
   :width: 100%
   :align: center


Select the newly created share and navigate to the *Access control* tab then
click *Edit* and select "scrutiny" user as owner.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_config_share_permissions.png
   :width: 100%
   :align: center

Scrutiny rock-on installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now, navigate to *Rock-ons* and click the *Update* button, once the refresh is
done, you will be in the tab with all Rock-ons. Search for "Scrutiny" Rock-on
and click *Install* button.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_install.png
   :width: 100%
   :align: center


First step of the wizzard, select the "Scrutiny-Config-Share" earlier created:

.. image:: /images/interface/docker-based-rock-ons/scrutiny_install_step1.png
   :width: 100%
   :align: center


Step 2, enter a port number that is not in use by another rock-on (Default
8088).

.. image:: /images/interface/docker-based-rock-ons/scrutiny_install_step2.png
   :width: 100%
   :align: center


Step 3, enter the **user ID (UID)** and **group ID (GID)** for "scrutiny" user.

- API endpoint of the scrutiny UI should be :code:`http://localhost:8080`. Do
  not change unless using as a remote collector.

- Run the web service, this should remain :code:`true`.

- Run the metrics collector, this should remain :code:`true`.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_install_step3.png
   :width: 100%
   :align: center


Step 4, review your configuration, then click **Submit** to start the Rock-on
installation.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_install_step4.png
   :width: 100%
   :align: center


Step 5, installation in progress, you can close the wizzard.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_install_step5.png
   :width: 100%
   :align: center


Once the installation done, you can use the **Scrutiny UI** button to go to the
web interface to view and monitor all the metrics collected from your server
disks.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_installed.png
   :width: 100%
   :align: center

Scrutiny initial configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**No Devices detected!**

First time you install and access the Scrutiny UI, the dashboard will be empty.

.. image:: /images/interface/docker-based-rock-ons/scrutiny_no_devices.png
   :width: 100%
   :align: center

Why? Because the container is using cron to refresh all data, and by default
it's scheduled at midnight. You can wait for the next scheduled refresh, or you
can do it manually.


Manual refresh
^^^^^^^^^^^^^^
In order to refresh the dashboad manually, you must connect to your Rockstor
server via SSH  and type the following command:

:code:`docker exec -it scrutiny sh -c "scrutiny-collector-metrics run"`

.. image:: /images/interface/docker-based-rock-ons/scrutiny_shell_metrics_run.png
   :width: 100%
   :align: center


Scrutiny Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Congratulations! You successfully installed and configured **Scrutiny**, your
dashboard should now be filled with valuable information about all your disks:

.. image:: /images/interface/docker-based-rock-ons/scrutiny_dashboard.png
   :width: 100%
   :align: center


More detailed information is available for each disks as well:

.. image:: /images/interface/docker-based-rock-ons/scrutiny_hdd_details.png
   :width: 100%
   :align: center


More options and configurations
-------------------------------

A fully commented example configuration yaml file can be found in the original
project repository `here <https://github.com/AnalogJ/scrutiny/blob/master/example.scrutiny.yaml>`_.
You can modify the file `scrutiny.yaml` located in the share
"Scrutiny-Config-Share".

**Warning!**

If :code:`smartd` is not working or doesn't list any device, (like in a VM) the
dashboard will remain empty!
