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
the canonical upstream instructions as provided by `Tailscale <https://tailscale.com/>`_ themselves.
It is intended only to assist in providing relevant links and light guidance.

.. note::

    Rockstor is "Built on openSUSE", specifically **openSUSE Leap** or **Tumbleweed**: depending on the installer used.
    Our Tailscale service integration requires only that a recent Tailscale instance be installed.
    The Tailscale `Stable` variant is advised but not assumed.


.. _install_tailscale_upstream_leap:

Built on openSUSE Leap
^^^^^^^^^^^^^^^^^^^^^^
Installs derived from our Leap based `downloadable installers <https://rockstor.com/dls.html>`_.

.. warning::

    As of this How-to's publication, tailscale does not yet provide Leap 15.6 repositories.
    Until Tailscale resolves this situation, consider using their 15.5 repository in the interim period.
    Also note that their `Downloads` -> `Linux` -> `Manually install on ...` **dropdown** is
    now years **out-of-date**. **Reference instead the following more maintained instructions.**

- `Setting up Tailscale on openSUSE Leap <https://tailscale.com/kb/1303/install-opensuse-leap>`_

.. note::

    Replace $VERSION in the above instructions with your base OS Leap version.

E.g. for Leap 15.6 (using the 15.5 repo instead):

.. code-block:: console

    sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.5/repo.gpg
    sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.5/tailscale.repo
    sudo zypper ref
    sudo zypper in tailscale

**Continue service enablement & configuration via our Web-UI** :ref:`Tailscale service <configure_tailscale>` intergration.

.. _install_tailscale_upstream_tumbleweed:

Built on openSUSE Tumbleweed
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Installs derived from our Tumbleweed based `downloadable installers <https://rockstor.com/dls.html>`_.

- `Setting up Tailscale on openSUSE Tumbleweed <https://tailscale.com/kb/1047/install-opensuse-tumbleweed>`_

E.g.

.. code-block:: console

    sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/tumbleweed/repo.gpg
    sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/tumbleweed/tailscale.repo
    sudo zypper ref
    sudo zypper in tailscale

**Continue service enablement & configuration via our Web-UI** :ref:`Tailscale service <configure_tailscale>` intergration.

