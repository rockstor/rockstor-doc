.. _rpm_install:

Install on Vanilla openSUSE/SuSE SLES
=====================================

Our installer profiles (`<https://github.com/rockstor/rockstor-installer>`_),
and consequently our pre-built installers,
deviate only a little from openSUSE’s JeOS / Minimal appliance profiles.
As a result,
one can manually configure a Vanilla openSUSE/SuSE SLES install to be the host OS to a `rockstor` rpm customisation.

.. warning::

    **For advanced users only**

    This install method is predominantly for developers or advanced users and will likely require additional maintenance.
    It may also serve as an option where a SLES base is required.
    Please note our undesirable disabling of apparmor,
    we hope to resolve this shortfall in due time.
    Pull requests welcome.

This procedure, not recommended or supported,
constitutes adding the relevant Rockstor repositories to a dedicated vanilla openSUSE / SuSE SLES non transactional server install.
The base OS version is assumed to be within our current profiles at:
`Installer Recipes <https://github.com/rockstor/rockstor-installer>`_.
For recommended openSUSE versions of the host OS, see our `downloads page <https://rockstor.com/dls.html>`_.

.. _rpm_install_procedure:

Procedure
---------

The relevant commands are as follows:

First, disable :code:`apparmor`.

.. code-block:: console

    systemctl disable apparmor

Then, ensure :code:`NetworkManager` is installed and running.

.. code-block:: console

    zypper install --no-recommends NetworkManager
    systemctl disable wicked
    systemctl enable --now NetworkManager

Instantiate the package repositories required by Rockstor (all are multi-arch).

.. note::

    In the following replace all `15.X` instances to match your installed OS version.

.. code-block:: console

    zypper --non-interactive addrepo --refresh -p105 https://download.opensuse.org/repositories/home:/rockstor/15.X/ home_rockstor
    zypper --non-interactive addrepo --refresh -p97 https://download.opensuse.org/repositories/home:/rockstor:/branches:/Base:/System/15.X/ home_rockstor_branches_Base_System
    rpm --import https://rockstor.com/ROCKSTOR-GPG-KEY
    zypper addrepo -f http://updates.rockstor.com:8999/rockstor-testing/leap/15.X/ Rockstor-Testing
    zypper --non-interactive --gpg-auto-import-keys refresh

Finally, install and enable/start Rockstor via it's systemd services.

.. note::

    In the following replace `X.X.X-X` with your preferred rockstor package version.
    For available `rockstor` package versions see our `downloads page <https://rockstor.com/dls.html>`_.
    The initial Stable rpm release, in each development phase, appears first at the end of the prior testing channel phase.
    :ref:`Update channel <update_channels>` selection can be modified, if required, via the Web-UI.

.. code-block:: console

    zypper in --no-recommends rockstor-X.X.X-X
    systemctl enable --now rockstor-bootstrap

.. warning::

    Please note that Rockstor is not yet Multi-path controller compatible.

.. note::
    Visit our `friendly forum <https://forum.rockstor.com/>`_ for questions, and suggestions for improving these instructions.
    As always, Pull requests are welcome: `<https://github.com/rockstor/rockstor-doc>`_.
