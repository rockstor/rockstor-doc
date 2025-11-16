.. _osk_rockon:

Observability Starter Kit Rock-on
==========================

Before you install the Observability Starter Kit rock-on, you should understand the
prerequisites and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirements.


.. _osk_whatis:

What is Observability Starter Kit (OSK)
---------------------------------------

The OSK rock-on was created to allow advanced Rockstor users to start creating their
own custom monitoring solution via a so-called "observability stack".
  
An observability stack is an umbrella project, leveraging multiple monitoring components
that come together into a whole monitoring solution. 
`More information <https://observability-stack.io/>`_.

This rock-on consists of the following components:

- `OpenTelemetry Collector (contrib) <https://opentelemetry.io/docs/collector/>`_: a vendor-agnostic way to receive, process and export telemetry data
- `VictoriaMetrics Community Edition <https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/>`_: an efficient time-series database
- `Grafana OSS <https://grafana.com/docs/grafana/latest/>`_: a visualization frontend

This rock-on was inspired by the similar
`Grafana LGTM <https://grafana.com/docs/opentelemetry/docker-lgtm/>`_
docker project. 
Key differences:
  
- The number of components was kept to a minimum: only metrics can be monitored with this rock-on
- VictoriaMetrics was used instead of Prometheus, due do its resource-efficient implementation

When I was choosing the components for this rock-on, I tried to strike a balance between resource-efficiency, 
ease-of-use and flexibility. And the most important aspect was 100% open-sourced and without compulsory cloud 
account creation.

.. _osk_pre:

Pre-install requirements
------------------------

Ensure SSH access to the Rockstor server: default for 'root' user.
Some steps require root SSH access.
During more recent Rockstor TW/SR based installer, there is a recommended :ref:`ssh_key_enrollment` process.

Login to your Rockstor instance.

Under the *SYSTEM* menu, select the *Groups* menuitem.

Click on the **Add group** button.
  
**Groupname**: grafana

**Put this group under Rockstor management?**: checked

**GID**: 472

Click on the **Submit** button.

Under the *SYSTEM* menu, select the *Users* menuitem.

Click on the **Add user** button.
  
**Username**: grafana

**UID**: 472

**Group**: select "grafana"

Click on the **Submit** button.

.. note::
    This is needed because the Grafana component expects exactly this username and UID and assigned GID.
    Without this configuration, you will get file permission errors.

Click on the **Add user** button again.
  
**Username**: opentelemetry

**UID**: 10001

**Group**: select "docker"

Click on the **Submit** button.  

.. note::
    This is needed because the OpenTelemetry component expects exactly this username and UID and assigned GID.
    Without this configuration, you will get file and docker permission errors.
  
create three shares: osk-grafana, osk-victoria-metrics, osk-opentelemetry-collector
create config.yaml with the following contents in /mnt2/osk-opentelemetry-collector: https://gist.github.com/kanecko/cfaaf349c26e4602878e4a5b82bd9730
chown -R 472:472 /mnt2/osk-grafana
chown -R 10001:[docker GID] /mnt2/osk-opentelemetry-collector



.. _osk_install:

Installing the OSK rock-on
------------------------------
This rock-on does not require additional shares to be set. The only
pre-install requirement is to identify the **group ID (GID)** of the **docker**
group. This allows Netdata to identify by name the various rock-ons currently
running and thus report their own resource usage accurately. The **docker
group GID** can be easily identified using the Rockstor web-UI.

First, navigate to *System* > *Groups*, and search for the **docker** group in
the bottom table (*Other system groups*). In the example below, the **docker**
group has a :code:`GID` of :code:`476`.

.. image:: /images/interface/docker-based-rock-ons/netdata_docker_group.png
   :width: 100%
   :align: center

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
