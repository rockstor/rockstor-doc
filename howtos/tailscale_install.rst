.. _install_tailscale:

Tailscale install
=================

This How-to covers only the installation of the `Tailscale <https://tailscale.com/>`_ cloud service program.

.. note::

    Once installed, see our :ref:`Tailscale service <configure_tailscale>`
    documentation for configuration and use.

.. _install_tailscale_upstream:

Upstream instructions
---------------------

This How-to is derived from, and secondary to,
the canonical upstream instructions as provided by Tailscale themselves.
It is intended only to assist in providing relevant links and light guidance.

.. note::

    Rockstor is "Built on openSUSE", specifically **openSUSE Leap** or **Tumbleweed**:
    depending on the `downloadable installer <https://rockstor.com/dls.html>`_ used.
    *Our Tailscale service integration requires only that a relevant Tailscale repo and package be installed.*
    The Tailscale `Stable` variant is advised but not assumed.


.. _install_tailscale_upstream_openSUSE:

Install Tailscale repo and package
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

From the `Tailscale <https://tailscale.com/>`_ website select:

- `Downloads` -> `Linux`
- Scroll down to the **Manually install on** selector and choose your "Build on **openSUSE**" version.

.. note::

    Only steps 1 and 2 are required, Rockstor's Web-UI can do the rest.

E.g. for "Build on **openSUSE**" **Leap 15.6** you need only do the following at the command line interface:

.. code-block:: console

    sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.6/repo.gpg
    sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.6/tailscale.repo
    sudo zypper ref
    sudo zypper in tailscale

**Continue service enablement & configuration via our Web-UI** :ref:`Tailscale service <configure_tailscale>` integration.


