.. _v3_to_v4:

Migrating from Legacy V3 to V4 "Built on openSUSE"
==================================================

Rockstor v3 was based on CentOS 7 and is no longer supported.
Last updates per channel:

- Stable (3.9.2-57) - April 2020
- Testing (3.9.1-16) - November 2017

Our `downloadable <https://rockstor.com/dls.html>`_ v4 installers have the most Stable channel
release preinstalled. Below is a non-exhaustive list of notes, recommendations and warnings
for user planning on going through the upgrade process.

.. note::

    All v3 (and likely earlier) Pools and :ref:`config_backup` files (**once downloaded**),
    are expected to import and restore respectively as they would in a v3 install.
    It is important to import all pools **before** uploading and applying a config save file.

.. note::

    As of 3.9.2-56, in common with many NAS systems, the :ref:`afp` was dropped.

.. note::

    In v4 we auto label the system pool as "ROOT" in line with our JeOS upstream.
    Previous v3 installs use the label "rockstor_rockstor".
    V4 has also removed the inadvertent (as seen in v3) appearance of the "root"
    share (subvolume).

.. warning::

    As this migration requires an operating system re-install,
    it is imperative that you ensure your backups have been refreshed and verified.
    Greater hardware compatibility is assumed given the years newer kernel.
    But there is always the possibility of regressions.

.. warning::

    It is also possible, although unlikely,
    that once you have imported a pool under a newer kernel,
    it may fail to import rw in the older v3 related kernel.

.. _shares_on_system:

Shares on the v3 system disk
----------------------------

Rockstor's Web-UI discourages, but does not prohibit,
creating and using shares on the system disk.
If your current install has valued data on the system disk,
then copy it to a dedicated data pool share first.
Ideally one with redundancy.
It is always best to avoid creating and using shares on the system disk.
There is currently no redundancy options btrfs vise and it complicates re-install,
or major updates such as we have here with v3 to v4.
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

If at all possible it is highly advisable to install v4 onto a fresh system disk.
This leave open the possibility of re-attaching the old v3 system disk in case of any difficulties.
Do not leave an old v3 system disk attached while installing v4:
unless you are re-using the same system disk (not advised but entirely possible).
A v4 install is significantly faster and simpler than a v3 install,
but will destroy all data on the target disk.
Hence the advise here to preserve the original system disk and to detach it prior to the v4 install.

.. warning::

    If you do end up reverting to your v3 system disk, for whatever reason,
    do not have more than one Rockstor system disk, of any version, attached simultaneously.
    This causes known confusion within the current and past Web-UI.
    We hope to improve this inflexibility in time.

.. _disconnect_data_disks:

Disconnect all Data disks
-------------------------

As a purely precautionary measure,
it is highly advisable that all data disks be detached prior to the v4 install.
Take careful note of their connections to the host system.
This connection concern relates to potential hardware compatibility of these interconnects.
Btrfs, our underlying file system and device manager, is not normally concerned with such changes.
But the existing hardware pairings, assuming prior function, are best noted never-the-less.
Ready for the planned re-connection after v4 is installed, updated, and tested successfully.
Just in case.
After the last shutdown of v3, while attaching the new system disk, be sure to unplug all prior disks.
This is simply to avoid an accidental selection of a data pool member for the fresh install.

.. warning::

    As stated above, the v4 install will wipe all prior data on the target disk selected.
    A simple quick mistake at the initial :ref:`installer_select_disk` step could destroy a pool member's data inadvertently.

.. _v4_installer:

V4 Installer
------------

See our :ref:`installer_howto` for a step-by-step explanation and guide.
And again, take great care on the early :ref:`installer_select_disk` (intended v4 target system disk) choice.
If the above advise is followed, there will only be one newly attached proposed system disk anyway.

Once the new install is in place, it is advisable to apply all upstream updates.
See: :ref:`updaterockstorwebui`.
Take care to ensure these have all been applied prior to rebooting.
The Dashboard can help to indicate this by observing the network and CPU activity.
*We have an outstanding bug where our 'wifi like' busy indicator does not last the duration of the installs.*

Make sure that the system does reboot and return as expected before re-attaching all prior pool members,
connected as before, and doing the pool import and then optionally a config restore.


.. _v4_import_notes:

V4 Pool/s import
----------------

V4 Pool import is as per v3 import, initiated via the :ref:`disks` overview page.
See: :ref:`import_data`.

.. warning::

    V4 btrfs parity raid levels of 5 and 6 are read-only by default.
    This is an upstream decision and not enacted by Rockstor.
    See our :ref:`redundancyprofiles` for more information,
    and our suggested work around if needs must.
    See also :ref:`btrfsunwellimport` in case your pool requires special mount options.

V4 Config restore
-----------------

V4 Config restore is as per v3. See: :ref:`config_backup`.

.. note::

    You must have first downloaded your v3 saved config as they otherwise reside on the system disk.

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
we have found and fixed a large number of bugs, and inherited such things as our
`Rockstor 4 Installer Recipe <https://github.com/rockstor/rockstor-installer>`_
that trivially enables highly customised installer creation.
We also now have ARM64 (e.g. Pi4 / Ten64) compatibility, baring some Rock-ons,
courtesy of openSUSE's extreme heritage in ARM support.

Also note the following, now we are past the `Jump <https://en.opensuse.org/Portal:Jump>`_ initiative:

- In v3 our upstream of CentOS had in turn its upstream of RedHat's RHEL.
- In v4 our upstream of openSUSE has in turn its increasingly binary compatible upstream with SuSE SLES.

So, if your prior v3 install had a customization involving a CentOS/RHEL compatibility,
you should now, in v4, look first for an openSUSE equivalent and then for a SLES equivalent.
This is most likely only going to affect advanced users and is not a concern for mainly Web-UI users.

Users and default group
^^^^^^^^^^^^^^^^^^^^^^^

As we have, between v3 and v4, changes our underlying OS,
there are other more subtle differences that may only come to light in time.
One such difference is the default use of the "users" group in v4 for newly added users.
Our prior CentOS base defaulted to individual user group creation named after the user concerned.
It is thought that the newer default is more suited to a shared resource.
But this difference may come as a surprise to prior v3 administrators.
