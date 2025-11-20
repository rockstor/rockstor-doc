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

In simple terms: with **OpenTelemetry** you *receive* metrics (CPU temperature, memory usage...) from different *sources* (HTTP endpoints, operating system...), you can *process* the metrics (batching, sampling...), and *export* (pull, push, HTTP, gRPC...) them. **VictoriaMetrics** is the database, where the metrics are exported to and stored in. **Grafana** displays your metrics as charts for easy monitoring.

This rock-on was inspired by the similar
`Grafana LGTM <https://grafana.com/docs/opentelemetry/docker-lgtm/>`_
docker project. 
Key differences:
  
- The number of components was kept to a minimum: only metrics can be monitored with this rock-on
- VictoriaMetrics was used instead of Prometheus, due do its resource-efficient implementation

When I was choosing the components for this rock-on, I tried to strike a balance between resource-efficiency, 
ease-of-use and flexibility. The most important aspect was 100% open-sourced and without compulsory cloud 
account creation.

.. _osk_pre:

Pre-install requirements
------------------------

Ensure SSH access to the Rockstor server: default for 'root' user.
Some steps require root SSH access.
During more recent Rockstor TW/SR based installer, there is a recommended :ref:`ssh_key_enrollment` process.

#. Login to your Rockstor instance via web-UI.
#. Under the *SYSTEM* menu, select the *Groups* menu item.
#. Add two groups: osk-grafana and osk-opentelemetry
#. Under the *SYSTEM* menu, select the *Users* menu item.
#. Add two users: osk-grafana and osk-opentelemetry. Assign the group with the same name to each of them.
#. Under the *STORAGE* menu, select the *Shares* menu item.
#. Add three shares: osk-opentelemetry-collector, osk-victoria-metrics, osk-grafana
#. Login to you Rockstor instance via SSH as root.
#. Create a :code:`config.yaml` file with the `initial content <https://gist.github.com/kanecko/cfaaf349c26e4602878e4a5b82bd9730>`_ in :code:`/mnt2/osk-opentelemetry-collector`.
#. Set the owner of the shares osk-grafana and osk-opentelemetry-collector to their corresponding UID/GID.
#. Example*: :code:`chown -R 472:472 /mnt2/osk-grafana`
#. Example*: :code:`chown -R 10001:10001 /mnt2/osk-opentelemetry-collector`

.. note::
    \*Change the UID/GID from the example to the actual values that you have used in steps 2-5.


.. _osk_install:

Installing the OSK rock-on
------------------------------

Install the rock-on as you would any other.

Make sure that the three shares will correspond to their expected components.


.. _osk_after:

The Visualisation Dashboard
------------------------------

After a successful install, click on the **Observability Starter Kit** button on the Rock-ons page to open the Grafana web-UI.

.. note::
    The initial bootstrapping of Grafana takes a few minutes. 
    If the web-UI doesn't load, then try again after 3 minutes.

At the login screen, input "admin" as both username and password.

.. image:: /images/interface/docker-based-rock-ons/grafana_login.png
   :width: 50%
   :align: center

.. warning::
    It is highly recommended to change the default password.

#. Once logged-in, click on **Data sources**. You can find it on the left-side menu, below *Connections*.
#. Click on the big **Add data source** button.
#. Find and select "VictoriaMetrics" in the list.
#. In the HTTP **URL** field, input "http://osk-victoria-metrics:8428".
#. Scroll down and click the **Save & test** button.
#. Click on **Dashboards** from the left-side menu.
#. Click on the big **Create dashboard** button.
#. Click on the **Import visualization** button.
#. Paste the `dashboard configuration <https://gist.github.com/kanecko/42c696f9a07b557696be2d86430e2f31>`_ into the field "Import via dashboard JSON model".
#. Click on the **Load** button.
#. Select the just-added "VictoriaMetrics" datasource in the field "victoriametrics-metrics-datasource".
#. Click on the **Import** button.

Now you should see something like this:

.. image:: /images/interface/docker-based-rock-ons/grafana_starter_dashboard.png
   :width: 100%
   :align: center

.. _osk_add_chart:

Adding a new chart
------------------------------

In the starter dashboard we don't see any disk metrics. 
Let's add a I/O usage chart now.

#. Enter edit mode by clicking on the **Edit** button on the top-right side.
#. Click on the **Add** menu button, then on **Visualization**.
#. Select the metric "system.disk.io" on the bottom side, in the *Metric* field.

In the
`documentation <https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/receiver/hostmetricsreceiver/internal/scraper/diskscraper/documentation.md#systemdiskio>`_
we can see that this metric:

- represents the disk bytes transferred,
- its unit is *bytes* (`"By" <https://opentelemetry.io/docs/specs/semconv/general/metrics/#instrument-units>`_),
- its underlying data type is *integer* ("Int"),
- it is monotonic, which means that its value can only ever increase,
- and has two attributes:
    - *device*: name of the disk or device,
    - *direction*: direction of flow, either *read* or *write*.

Let's see how it looks like by clicking on the "Run queries" button

.. image:: /images/interface/docker-based-rock-ons/grafana_run_queries.png
   :width: 30%
   :align: center

You should see something like this:

.. image:: /images/interface/docker-based-rock-ons/grafana_diskio_initial_chart.png
   :width: 50%
   :align: center

The chart is pretty confusing in this state. 
We see some huge numbers on the left.
Some very straight lines flowing to the right.
And in the bottom, the legend is full of items.

Let's start by fixing the display of units:

#. Scroll down to the section "Standard options" on the right-side menu,
#. Select "Data / bytes (IEC)" from the list in the field "Unit"
#. Scroll down to the section "Thresholds" and remove the red "80" item.
#. Click on the "Run queries" button to update the dashboard, if it hasn't automatically already.

At this point the chart should update, and you should see units with prefixes like GiB, TiB, PiB...

Now let's change those straight lines into something more meaningful.
As mentioned before, the metric "system.disk.io" is monotonic.
This basically means in its current state you will only ever get the *total* transferred bytes per device.

In order to get the *current* transferred bytes value, you need to make a modification to our metric.

#. Select the "Code" option. You will find it at the bottom, next to the "Run queries" button.
#. Replace the current metric with the following expression: ``rate(system.disk.io[$__interval])``
#. Change the unit from "Data / bytes (IEC)" to "Data rate / bytes/sec(IEC)"
#. Scroll up to the "Tooltip" section, and select the "All" option, and then the "Descending" option.

Now the lines will not be straight anymore because thanks to the
`rate() function <https://docs.victoriametrics.com/victoriametrics/metricsql/#rate>`_
it will calculate the average per-second increase rate over the given time window for us.

The time window in this case is denoted by ``[$__interval]`` which is bound to the time range
that you can select above the chart (next to the "Refresh" button).

The changed tooltip mode has enabled us to mouse-over the chart to see a list of current values of all devices.

.. note::
    If you have an NVMe OS disk, then you will see multiple ``nvme0n1*`` entries in the legend.
    Let's fix this now by grouping them together.

As mentioned before, the metric "system.disk.io" has two attributes: device and direction.
The legend will be filled with a small combinatorial bomb of all your devices and their read/write directions.

The device attribute basically represents the disks and partitions devices under ``/dev/``. 
You can run ``fdisk -l`` via SSH to see your disk configuration.

In case of NVMe OS disks, you will probably want to group them together, so that the chart won't be cluttered.

Here's how:

#. Replace the current metric expression with ``sum(rate(system.disk.io{device=~"nvme0n1.*",direction="read"}[$__interval]))``
    - ``device=~"nvme0n1.*"`` performs a regex filter. It will select the ``nvme0n1`` disk as well as its partitions/namespaces.
    - ``direction="read"`` selects the "read" operation.
    - ``sum()`` sums all the values together.
#. Under the "Options" section, click on the "Legend" combobox and select "Custom"
#. Input something like "nvme read"
#. Click on the **Add query** button below
#. Select the "Code" option
#. Input the following expression: ``sum(rate(system.disk.io{device=~"nvme0n1.*",direction="write"}[$__interval]))``
    - performs the same kind of selection as above, but this time for the "write" operation.
#. Input something like "nvme write" for the legend
#. Add a new query with the following expression: ``rate(system.disk.io{device!~"nvme0n1.*"}[$__interval])``
    - ``device!~"nvme0n1.*"`` performs a negated regex filter. It will select anything but ``nvme0n1``. In my case this will select ``sda``, ``sdb`` and ``sdc``.
    - because we didn't include any ``direction`` selection, it will return values for both "read" and "write" operations, for each of the three aforementioned devices.
#. Input "{{device}} {{direction}}" for the legend
#. Click on a "Run queries" button to update the chart

You should now see something more meaningful:

.. image:: /images/interface/docker-based-rock-ons/grafana_diskio_fixed_chart.png
   :width: 50%
   :align: center

Now try picking a different visualization:

#. Click on the "Visualization" combobox
#. Select Stat
#. Select Gauge

Pick which suits you the most!

.. _osk_under_the_hood:

Under the hood and next steps
-------------------------------

...also known as digging into documentation, searching for information on the internet and experimenting.

Before you go off and explore the possibilities of this observability stack, let me briefly explain 
the configuration of the three components and how they interact, so that you will understand what
is happening under the hood.

OpenTelemetry
^^^^^^^^^^^^^

For a quick introduction, first watch the short video about 
`OpenTelemetry <https://opentelemetry.io/docs/what-is-opentelemetry/>`_.

`OpenTelemetry Collector's <https://opentelemetry.io/docs/collector/>`_
`configuration <https://opentelemetry.io/docs/collector/configuration/>`_
is basically configured with receivers, processors and exporters.
We have placed our 
`config.yaml` <https://gist.github.com/kanecko/cfaaf349c26e4602878e4a5b82bd9730>`_ 
file in :code:`/mnt2/osk-opentelemetry-collector` to be available to the Collector.

We have defined the
`"hostmetrics" <https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/receiver/hostmetricsreceiver>`_
receiver which generates metrics about the host system scraped from various sources.
All of the data being currently shown on your dashboard, is being collected by this receiver every 15 seconds.

In addition to that, we have also defined two endpoints (gRPC and HTTP).
They listen for metric data on the configured ports. 
You can push any kind of external metrics via these ports, and they become available to be
visualized on your dashboard in Grafana.

We have defined the
`"batch" <https://github.com/open-telemetry/opentelemetry-collector/tree/main/processor/batchprocessor>`_
processor which batches all the different metric data together efficiently.

We also have defined the
`"deltatocumulative" <https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/processor/deltatocumulativeprocessor>`_
processor, because our VictoriaMetrics database can only understand metrics with 
`cumulative temporality <https://docs.victoriametrics.com/guides/getting-started-with-opentelemetry/>`_.

One of your next steps should be adding the "memory_limiter" processor.
You can read more about 
`recommended processors <https://github.com/open-telemetry/opentelemetry-collector/tree/main/processor#recommended-processors>`_.

We have defined a
`"otlphttp" <https://github.com/open-telemetry/opentelemetry-collector/tree/main/exporter/otlphttpexporter>`_
exporter which is configured to send metric data to VictoriaMetrics database.
If you would like to add the VictoriaLogs database to the mix, you will need to add the "logs_endpoint" field.

We have defined and enabled the
`internal telemetry for the OpenTelemetry Collector <https://opentelemetry.io/docs/collector/internal-telemetry/>`_
service which is configured to send metric data to VictoriaMetrics database every 15 seconds.
You can visualize these metrics in Grafana. They start with "otelcol_" in their name.

All components (except the internal telemetry service), need to be added into the pipeline, 
in order to be enabled. The pipeline components are executed in the order they were defined in.

You can 
`explore <https://opentelemetry.io/ecosystem/registry/?language=collector>`_
all available collector receivers, processors, exporters and more.

Check out their 
`community <https://opentelemetry.io/community/>`_
for any kind of configuration problems you might encounter.

Grafana
^^^^^^^

Here are the relevant Grafana documentation parts for beginners:

- `Dashboard <https://grafana.com/docs/grafana/latest/visualizations/dashboards/use-dashboards/>`_.
- `Panels <https://grafana.com/docs/grafana/latest/visualizations/panels-visualizations/>`_.

Also check out their published 
`Plugins <https://grafana.com/grafana/plugins/>`_.
and 
`Dashboards <https://grafana.com/grafana/dashboards/>`_.
that you can browse through and use.

In case of issues with your Grafana configuration, don't hesitate to ask them in their
`community forum <https://community.grafana.com/>`_.

VictoriaMetrics
^^^^^^^^^^^^^^^

You will spend the least time fiddling around with this component. 

You should note that the configured data 
`retention time <https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#retention>`_.
is set to 1 month. After that the metrics are being deleted. 
This means you will only ever see the maximum of 1 month of history on your dashboard charts.

It is very important to learn the differences between the 
`rate() and increase() <https://signoz.io/guides/understanding-prometheus-rate-vs-increase-functions-correctly/>`_.
functions. 
You will use them a lot with those monotonic counters.

Another very useful tool is the *vmui*. 
It is a web-UI for query troubleshooting and exploration.

Open your browser at ``http://<Rockstor IP>:18428/vmui`` and enable the "Autocomplete" option.
Start typing a name of the metric in the "Query" field (e.g. "sys") and select a metric.

If something won't work on your Grafana charts, you will be able to get a raw view into metrics via this web-UI.
You will be able to seek answers to the following questions:

- is there any metric data present (within the configured time window)?
- is my metric monotonic (use ``rate()``/``increase()``) or not (use values directly)?
- which attributes are available?

After you have completed your monitoring project, I suggest you check out the **Explore** menu on the top.
These tools give you an insight into the performance of your active queries and time series cardinality.
