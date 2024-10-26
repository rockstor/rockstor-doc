.. _centos_to_opensuse:

Migrating from Legacy V3 on CentOS to "Built on openSUSE" versions
==================================================================

Rockstor v3 was based on CentOS 7 and is no longer supported.
Last updates per channel:

- Stable (3.9.2-57) - April 2020
- Testing (3.9.1-16) - November 2017

Starting with v4, openSUSE has become the basis for the Rockstor appliance.
Our `downloadable <https://rockstor.com/dls.html>`_ installers aim to have the most
recent Stable channel release pre-installed.
Below is a non-exhaustive list of notes, recommendations and warnings for those planning on
going through the upgrade process.

.. note::

    All v3 (and likely earlier) Pools and :ref:`config_backup` files (**once downloaded**),
    are expected to import and restore respectively as they would in a v3 install.
    It is important to import all pools **before** uploading and applying a config save file.

.. note::

    As of 3.9.2-56, in common with many NAS systems, the :ref:`afp` was dropped.

.. note::

    In the openSUSE versions the system pool is auto-labeled as "ROOT" in line with the JeOS upstream.
    Prior to v4, installs use the label "rockstor_rockstor".
    Starting with v4 the inadvertent (as seen in v3) appearance of the "root"
    share (subvolume) has also been removed .

.. warning::

    As this migration requires an operating system re-install,
    it is imperative to ensure that backups have been created/refreshed and verified.
    Greater hardware compatibility is assumed given the years newer kernel.
    But there is always the possibility of regressions.

.. warning::

    It is also possible, although unlikely,
    that once a pool is imported under a newer kernel,
    it may fail to import as read-write (rw) in the older v3 related kernel.

.. _shares_on_system:

Shares on the v3 system disk
----------------------------

Rockstor's Web-UI discourages, but does not prohibit,
creating and using shares on the system disk.
If the current install has valued data on the system disk,
then copy it to a dedicated data pool share first.
Ideally one with redundancy.
It is always best to avoid creating and using shares on the system disk.
There is currently no redundancy options btrfs-wise and it complicates re-install,
or major updates such as this one with moving from CentOS to openSUSE versions.
Try to avoid this in the future.

.. _rockons_root_on_system:

Rock-ons 'root' on system disk
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

One common pragmatic setup in small to medium-sized Rockstor installs
is the use of the system pool for the :ref:`rockons_root` share.
However the contents of this share, if used exclusively for the indicated purpose,
are freely downloadable again via the respective setup of the associated Rock-ons.
This compromise is common in small setups as the system disk, often an SSD,
makes for a low power store for the docker images that back Rock-ons.
Since the Rock-ons root is separate from associated data or configuration shares
that would be stored on shares of the non-system pool(s), they will not be affected by
recreating the Rock-ons root share after upgrade.


.. _use_new_system_disk:

Use a new system disk
---------------------

If at all possible it is highly advisable to install the new openSUSE-based version onto
a fresh system disk.
This leaves open the possibility of re-attaching the old v3 system disk in case of any difficulties.
Do not leave an old v3 system disk attached while installing a new openSUSE version, unless of course,
the same system disk is reused (not advised but entirely possible).
An openSUSE version install is significantly faster and simpler than a v3 install,
but will destroy all data on the target disk.
Hence the advise here to preserve the original system disk and to detach it prior to the new install.

.. warning::

    If, for whatever reason, there is a need to revert to the v3 system disk,
    avoid having more than one Rockstor system disk, of **any** version, attached simultaneously.
    This causes known confusion within the current and past versions of the Web-UI.
    This inflexibility will be improved in time.

.. _disconnect_data_disks:

Disconnect all Data disks
-------------------------

As a purely precautionary measure, it is highly advisable that all data disks be detached
prior to the new install.
Take careful note of their connections to the host system.
This connection concern relates to potential hardware compatibility of these interconnects.
Btrfs, our underlying file system and device manager, is not normally concerned with such changes,
but the existing hardware pairings, assuming prior function, are best noted nevertheless.
Just in case, after the last shutdown of v3, while attaching the new system disk,
be sure to unplug all prior disks.
This is simply to avoid an accidental selection of a data pool member for the fresh install.

.. warning::

    As stated above, the new openSUSE install will wipe all prior data on the target disk selected.
    A simple quick mistake at the initial :ref:`installer_select_disk` step could inadvertently
    destroy a pool member's data.

.. _openSUSE_installer:

OpenSUSE Installer
------------------

See :ref:`installer_howto` for a step-by-step explanation and guide.
And again, great care should be taken on the early :ref:`installer_select_disk` (intended target system disk)
choice.
If the above advise is followed, there will only be one newly attached proposed system disk anyway.

Once the new install is in place, it is advisable to apply all upstream updates.
See: :ref:`updaterockstorwebui`.
Take care to ensure these have all been applied prior to rebooting.
The Dashboard can help to determine this by observing the network and CPU activity.
*There is an outstanding bug where our 'wifi-like' busy indicator does not last the duration of the installs.*

Ensure that the system does reboot and return as expected before re-attaching all prior pool members,
connected as before, perform the pool import and then optionally a config restore.


.. _openSUSE_import_notes:

OpenSUSE versions Pool/s import
-------------------------------

Under the OpenSUSE version, the Pool import is performed the same as under v3, initiated via the :ref:`disks` overview page.
See: :ref:`import_data`.

.. warning::

    This is an upstream decision and **not** enacted by Rockstor.
    See our :ref:`redundancyprofiles` for more information,
    and a suggested workaround if needed.
    See also :ref:`btrfsunwellimport` in case a pool requires special mount options.

OpenSUSE versions config restore
--------------------------------

Under openSUSE versions, the config restore is as per v3. See: :ref:`config_backup`.

.. note::

    Ensure to first download the v3 saved config as they otherwise reside on the system disk.

.. warning::

    Although older config save files are compatible,
    there has been much work done on extending this features capability.
    Earlier config saves cover less elements of the system than later ones.
    E.g., Rock-ons installed and their associated share settings
    are not included in config saves before 3.9.2-52.
    Note that Rock-ons restore capability depends upon a non-system disk
    :ref:`rockons_root` share location.

Other differences
-----------------

Many bug fixes
^^^^^^^^^^^^^^

In the process of moving from a CentOS base to a "Built on openSUSE" one,
the developers have found and fixed a large number of bugs, and inherited such things as our
`Rockstor 4 Installer Recipe <https://github.com/rockstor/rockstor-installer>`_
that trivially enables highly customised installer creation.
Also, there is now ARM64 (e.g. Pi4/Ten64) compatibility, baring some Rock-ons,
courtesy of openSUSE's extreme heritage in ARM support.

Also note the following, Rockstor has moved past the `Jump <https://en.opensuse.org/Portal:Jump>`_
initiative:

- In v3 the upstream of CentOS had in turn its upstream of RedHat's RHEL.
- openSUSE has in turn its binary compatible upstream of SuSE SLES.

So, if the prior v3 install has a customization involving a CentOS/RHEL compatibility, that should
also be used on the openSUSE based version, check first for an openSUSE equivalent and then
for a SLES equivalent (note that sometimes packages are not named exactly the same, so it might
require some detective work to find the matching package to install).
This most likely only affects advanced users and should not be a concern when using Rocksto's
built-in capabilities.


.. _Users_default_groups:

Users and default group
^^^^^^^^^^^^^^^^^^^^^^^

Since the underlying OS has changed between v3 and v4 onwards, there are other more subtle
differences that may only come to light in time.
One such difference is the default use of the "users" group in openSUSE for newly added users.
Our prior CentOS base defaulted to individual user group creation named after the user concerned.
It is thought that the newer default is more suited to a shared resource, though this difference
may come as a surprise to prior v3 administrators.
