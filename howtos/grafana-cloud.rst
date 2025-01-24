.. _grafana_cloud:

Grafana Cloud
=============

How to remote monitor a Rockstor instance using `Grafana Cloud <https://grafana.com/products/cloud/>`_.

The Free Tier is assumed, with the proviso that there exists telemetry and log space limitations.

Required installs on Rockstor:

- The Prometheus -`node_exporter <https://github.com/prometheus/node_exporter>`_- component.
- `Grafana Alloy <https://grafana.com/docs/alloy/latest/>`_, an `Open Telemetry <https://opentelemetry.io/>`_ (OTel) collector.

.. _prometheus_node_exporter:

Prometheus node_exporter
------------------------

A component of Prometheus used by Grafana Alloy to source operating system telemetry.

.. _node_exporter_install:

Node_exporter install
^^^^^^^^^^^^^^^^^^^^^

The following installs and starts the node_exporter service.

.. code-block:: console

    zypper in golang-github-prometheus-node_exporter
    systemctl enable --now prometheus-node_exporter.service

Test by confirming telemetry type output from the following:

.. code-block:: console

    curl http://localhost:9100/metrics
    # or by visiting
    http://your-rockstor-ip:9100/metrics

.. _grafana_alloy:

Grafana Alloy
-------------

Grafana Alloy (licensed Apache-2.0) supersedes its now deprecated predecessor `Grafana Agent <https://grafana.com/docs/agent/latest/>`_.
Alloy also supersedes `Grafana Promtail <https://grafana.com/docs/loki/latest/send-data/promtail/>`_ re future developments.
This OTel collector filters & translates operating system (OS) telemetry and log data into Open Telemetry compatible streams.
These streams can then be received by, for example, the following **hosted** services of a Grafana Cloud account:

- a `Prometheus <https://prometheus.io/>`_ metric & alerting server: licensed Apache-2.0.
- a `Grafana Loki <https://grafana.com/oss/loki/>`_ Log aggregation server/system: licensed AGPLv3.

or any other Open Telemetry compatible receivers.

.. _alloy_install:

Alloy install
^^^^^^^^^^^^^

These instructions are derived from the `Alloy install documentation <https://grafana.com/docs/alloy/latest/set-up/install/linux/>`_.
Be sure to select the openSUSE tab, given Rockstor's "Built on openSUSE" status.

.. code-block:: console

    wget -q -O gpg.key https://rpm.grafana.com/gpg.key
    rpm --import gpg.key
    zypper addrepo https://rpm.grafana.com grafana
    zypper refresh
    zypper install alloy

The following config files are installed as part of the rpm package when installed on an openSUSE base:

- /etc/alloy/config.alloy - Default alloy config file - overwritten by Grafana Cloud initialisation script.
- /etc/sysconfig/alloy - User defined environment variables, e.g. CUSTOM_ARGS, and default config file via CONFIG_FILE.
- /usr/lib/systemd/system/alloy.service - Systemd service file, modified by Grafana Cloud initialisation script.

For examples of CUSTOM_ARGS use, e.g. enabling Alloy's debug/info Web-UI,
see: https://grafana.com/docs/alloy/latest/configure/linux/

.. _alloy_remote_config:

Alloy remote config
^^^^^^^^^^^^^^^^^^^

.. note::

    A key Alloy feature, presumed by many elements of Grafana Cloud, is Alloy remote configuration.
    This capability, as of Alloy v1.5.1-1, requires the `--stability.level=public-preview` switch on starting the Alloy service.
    Grafana Cloud initialisation arranges this by editing the systemd service file.
    The following environment variables are also added to this same file: GCLOUD_RW_API_KEY, GCLOUD_FM_COLLECTOR_ID.

.. warning::
    GCLOUD_FM_COLLECTOR_ID defaults to the hostname. When modifying any configuration,
    or inputting hostname within Grafana Cloud forms/intergrations, ensure consistency.
    I.e. **hostname** must match the output of `uname -n`, used by the Cloud initialisation script.



.. _linux_server_integration:

Linux server integration
^^^^^^^^^^^^^^^^^^^^^^^^

An Alloy remote configuration is offered by Grafana Cloud.
Visit your Grafana Cloud account and select:

1. Connections -> Add new connection -> Linux Server (Configuration details tab).
2. Under `Select platform` choose **RedHat** (it uses the same rpm package & repository as installed above),
   assuming no openSUSE option is yet available. Also select the appropriate `Architecture`.
3. Click the "Run Grafana Alloy" button and follow the instructions in the pop-up dialog.
   Ensure **Enable Remote Configuration** is ticked/enabled.
   This step remotely installs an Alloy self_monitoring configuration for metrics & logs.

.. note::

    If Alloy was previously running, you will need to restart it via: `systemctl restart alloy.service`.

4. Once the provided test has passed, proceed with the rest of the instructions.
5. Use `nano /etc/alloy/config.alloy` to add the example configuration snippets as suggested.

Missing receivers
.................

The given configuration, at the time of this how-to's last edit, remains incomplete.
The integration is still missing the following:

- prometheus.remote_write.metrics_service.receiver - A Prometheus server Storage backend:
  Visit Connections - Data sources - grafanacloud-!!!!!!-prom for Connection **<url>** and Auth **username**.
- loki.write.grafana_cloud_loki.receiver
  Visit Connections - Data sources - grafanacloud-!!!!!!-logs for Connection **<url>** and Auth **username**.

Apply the following to config.alloy with the **<url>** & **username** `#######` elements replace by your values.

.. code-block:: console

    // Write metrics to your Grafana Cloud Prometheus instance.
    // Home - Connections - Data sources - grafanacloud-******-prom
    prometheus.remote_write "metrics_service" {
        endpoint {
            url = "<url>/push"

            basic_auth {
                username = "#######"
                password = sys.env("GCLOUD_RW_API_KEY")
            }
        }
    }

    // Write logs to your Grafana Cloud Loki instance.
    // Home - Connections - Data sources - grafanacloud-******-logs
    loki.write "grafana_cloud_loki" {
        endpoint {
            url = "<url>/loki/api/v1/push"

            basic_auth {
                username = "#######"
                password = sys.env("GCLOUD_RW_API_KEY")
            }
        }
    }

.. _rockstor_logs:

Rockstor logs
.............

To add Rockstor specific logs to the above :ref:`linux_server_integration`,
copy-in the following Alloy components to `/etc/alloy/config.alloy`.
An Alloy service reload via `systemctl reload alloy` is then required.

.. code-block:: console

    // Note: 'instance' and 'job' intentionally match integrations_node_exporter
    // enabling default dashboard inclusion.
    local.file_match "logs_rockstor_direct_scrape" {
      path_targets = [{
        __address__ = "localhost",
        __path__    = "/opt/rockstor/var/log/*.log",
        instance    = constants.hostname,
        job         = "integrations/node_exporter",
      }]
    }

    loki.source.file "logs_rockstor_direct_scrape" {
      targets    = local.file_match.logs_rockstor_direct_scrape.targets
      forward_to = [loki.write.grafana_cloud_loki.receiver]
    }

The above establishes a
`local.file_match <https://grafana.com/docs/alloy/latest/reference/components/local/local.file_match/>`_
to discover all `*.log` files in `/opt/rockstor/var/log/` and exports what it finds as `targets`.
These targets are then consumed (via targets =) by
`loki.source.file <https://grafana.com/docs/alloy/latest/reference/components/loki/loki.source.file/>`_
and forwarded to our loki receiver.

.. _alloy_log_customisation:

Alloy log customisation
^^^^^^^^^^^^^^^^^^^^^^^

.. note::

    To read systemd's journal, the `alloy` user is required to be a member of `systemd-journal`.
    This is established by the rpm package and can be confirmed via: `groups alloy`.

Alloy's `loki.source.journal <https://grafana.com/docs/alloy/latest/reference/components/loki/loki.source.journal/>`_ component is a systemd journal interface.
It can label log entries using `systemd.journal-fields <https://www.freedesktop.org/software/systemd/man/latest/systemd.journal-fields.html>`_.
On a linux system with man pages installed, labels can also be researched via `man systemd.journal-fields`


.. _live_debug_enable:

Alloy Web-UI live debug
^^^^^^^^^^^^^^^^^^^^^^^

.. note::

    This capability, as of Alloy v1.5.1-1, requires the `--stability.level=experimental` switch on starting the Alloy service.

To enable live debug the following is required within config.alloy:

.. code-block:: console

    livedebugging {
      enabled = true
    }

.. _advanced_alloy_install_notes:

Advanced Alloy install notes
----------------------------

The cut'n'paste script based initialisation provided by Grafana Cloud,
will not appeal to some users: i.e. those who prefer to avoid `root` user execution of unknown 3rd party scripts.

The following is a run-down of the initialisation scripts actions.

- Set GCLOUD_FM_URL, GCLOUD_FM_POLL_FREQUENCY, ARCH, GCLOUD_FM_HOSTED_ID, and GCLOUD_RW_API_KEY within the immediate environment.
- Retrieve and run: https://storage.googleapis.com/cloud-onboarding/alloy/scripts/install-linux.sh
- The install-linux.sh script, in-turn: retrieves and installs an alloy rpm.
  Retrieving a config.alloy template file from: https://storage.googleapis.com/cloud-onboarding/alloy/config/config-fm.alloy
  and substituting the variables within using the above 5 environmental variables.
- The existing alloy config is overwritten as a result of the above steps.
- GCLOUD_FM_HOSTED_ID, GCLOUD_RW_API_KEY, and GCLOUD_FM_COLLECTOR_ID (set to HOSTNAME using `uname -n`);
  are added as definitions to /usr/lib/systemd/system/alloy.service file.
- The Alloy systemd service is enabled and started.
