.. _netdata_official_rockon:

Netdata (official) Rock-on
==========================

Before you install the Netdata (official) rock-on, you should understand the
prerequisites and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirements.


.. _netdata_official_whatis:

What is Netdata
---------------

`Netdata <https://www.netdata.cloud/product/>`_ Agent is a free an open-source
tool to monitor and analyze the performance of your system in real time. It
gathers a wealth of metrics from the operating system, hardware, as well as
applications (including rock-ons), and display them in a modern and descriptive
interface. Netdata also allows you to set different alerts to get notified when
a specific metric reaches a designated threshold.
For further details and up-to-date description of Netdata, please visit the
`project's documentation <https://learn.netdata
.cloud/docs/overview/what-is-netdata>`_.

.. _netdata_doc:

Netdata Documentation
---------------------

Netdata's features and possibilities can be greatly expanded and customized to
better fit your needs, hardware, and preferences. Fortunately, Netdata provides
`extensive documentation <https://learn.netdata.cloud/>`_ to learn how to do
so. Note that out-of-the-box, Netdata (and thus this rock-on) already gathers a
very large number of metrics suitable for most users; further customization is
thus optional.

.. _netdata_install:

Installing the Netdata rock-on
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
   :align: center

We are now ready to start the installation of the Netdata rock-on. Click the
*Install* button next to the **Netdata (official)** listing on the *Rock-ons*
page.

.. image:: /images/interface/docker-based-rock-ons/netdata_install.png
   :align: center


.. _netdata_port:

Web-UI port
^^^^^^^^^^^
This corresponds to the port used to reach Netdata's web-UI. Note that
this port **must** be set to **19999**.

.. image:: /images/interface/docker-based-rock-ons/netdata_webUI_port.png
   :align: center


.. _netdata_pgid:

PGID
^^^^
This corresponds to the **docker group GID** that was identified above (see
:ref:`netdata_install` above).

.. image:: /images/interface/docker-based-rock-ons/netdata_PGID.png
   :align: center


.. _netdata_verify:

Verify and Submit
^^^^^^^^^^^^^^^^^
Verify the information you've provided is correct, then click **Submit**.

.. image:: /images/interface/docker-based-rock-ons/netdata_verify.png
   :align: center

You'll see a screen indicating the Rock-on is being installed.  Click "Close".

.. image:: /images/interface/docker-based-rock-ons/netdata_final.png
   :align: center


Netdata Installation Successful
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Congratulations! You can use the **Netdata (official) UI** button to go to the
web interface to view and monitor all the metrics collected by Netdata.

.. image:: /images/interface/docker-based-rock-ons/netdata_UI.png
   :align: center
