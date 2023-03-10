.. _rpm_install:

Install on Vanilla openSUSE/SuSE SLES
=====================================

Our installer profiles (`<https://github.com/rockstor/rockstor-installer>`_), and consequently our pre-built installers, deviate only a little from openSUSE’s JeOS appliance profiles.
As a result, it is possible to manually configure a Vanilla openSUSE/SuSE SLES based install to then install Rockstor's rpm.

.. warning::

    **For advanced users only**

    This install method is predominantly for developers or advanced users and will likely require additional maintenance.
    It may also serve as an option where a SLES base is required. Please note our undesirable disabling of apparmor.
    We hope to resolve this partial failure in due time.

The procedure, not recommended or supported, consists in adding the relevant Rockstor repositories to a dedicated vanilla openSUSE / SuSE SLES non transactional server install.
The base OS version is assumed to be already found within our Rockstor 4 `Installer Recipes <https://github.com/rockstor/rockstor-installer>`_, and in the case of SLES, to be at least version 15.4--when the upstream binary compatibility between openSUSE Leap & SuSE SLES matured.

.. _rpm_install_procedure:

Procedure
---------

The relevant commands (assuming a 15.4 base version) are as follows:

First, disable :code:`apparmor`.

.. code-block:: console

    systemctl disable apparmor

Then, ensure :code:`NetworkManager` is installed and running.

.. code-block:: console

    zypper install --no-recommends NetworkManager
    systemctl disable wicked
    systemctl enable NetworkManager
    systemctl start NetworkManager

Define and instantiate the rpm repositories required by Rockstor (all are multiarch).

.. code-block:: console

    zypper --non-interactive addrepo --refresh -p105 https://download.opensuse.org/repositories/home:/rockstor/15.4/ home_rockstor
    zypper --non-interactive addrepo --refresh -p97 https://download.opensuse.org/repositories/home:/rockstor:/branches:/Base:/System/15.4/ home_rockstor_branches_Base_System
    rpm --import https://raw.githubusercontent.com/rockstor/rockstor-core/master/conf/ROCKSTOR-GPG-KEY
    zypper addrepo -f http://updates.rockstor.com:8999/rockstor-testing/leap/15.4/ Rockstor-Testing
    zypper --non-interactive --gpg-auto-import-keys refresh

Finally, install and start Rockstor.

.. code-block:: console

    zypper in --no-recommends rockstor-4.5.8-0
    systemctl enable --now rockstor-bootstrap

.. warning::

    Please note that Rockstor is not yet Multi-path controller compatible.

.. note::
    Please visit our `friendly forum <https://forum.rockstor.com/>`_ for questions and suggestions for improving these instructions.
    As always, GitHub pull requests are welcome: `<https://github.com/rockstor/rockstor-doc>`_.
