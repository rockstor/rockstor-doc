.. _stable_kernel_backport:

Installing the Stable Kernel Backport
=====================================

.. warning::

    This How-to is intended for advanced users only.
    It's contents are likely irrelevant unless you require capabilities beyond our default openSUSE base.
    We include these instructions with the proviso that they will significantly modify your system from our upstream base.
    As such you will be running a far less tested system, and consequently may face more system stability/reliability risks.
    N.B. Pools created with this newer kernel have the newer free space tree i.e. (space_cache=v2).
    Future imports require kernels which are equally new/capable (at least ideally).

If you are reporting issues on our `Community Forum <https://forum.rockstor.com/>`_
or in any of our `GitHub <https://github.com/rockstor>`_ repositories,
please indicate if you have applied these changes.

Install all updates before following these instructions.
And test your system again after a reboot to ensure that this procedure is still necessary.

As of writing, the Leap 15.3 used in our v4 "Built on openSUSE" comes with many openSUSE/SuSE organised patches.
Almost all of these patches are backports from newer kernels,
applied to a designated 'base' kernel version of, in the case of Leap 15.3, **5.3.18**.

Rockstor no longer installs newer kernels than it's openSUSE/SuSE upstream, as it once did when based on CentOS 7 (Rockstor v3).
That is primarily because it is no longer necessary to do so,
our new upstream actively maintains btrfs and employs some of the key btrfs contributors.
As a result all relevant btrfs backports are already in our upstream default kernel.
But in some situations it may be desirable to enable a newer base kernel version.

.. _why_newer_kernel:

Why install a newer kernel
--------------------------

There are two main reasons:

1. **Newer Hardware support** - newer hardware often requires newer kernels to work as intended.
2. **Newer BTRFS support** - newer kernels contain more recent btrfs technologies.

.. _parity_raid_readonly:

Btrfs raid 5/6 read-only
------------------------

OpenSUSE Leap 15.3's default kernel restricts the parity raid levels of 5 & 6 to read-only.
This decision was taken as the parity raid levels are far younger than the non parity levels of 0, 1, and 10.
Rockstor's Web-UI supports btrfs raid 0, 1, 10, 5, and 6.
See the following links for how other newer raid levels such as :ref:`raid1c3_raid1c4` and :ref:`mixed_raid_levels` are treated.

When creating a parity raid pool (volume in btrfs parlance) we see the following message in the system journal:

.. code-block:: console

    Dec 12 18:57:55 rleap15-3 kernel: btrfs: RAID56 is supported read-only, load module with allow_unsupported=1

Rather than just *allowing unsupported* it is proposed that instead we take advantage of a newer kernel.
In this case the upstream-of-openSUSE latest stable kernel version back-ported to openSUSE.
And in turn Rockstor.

.. _newer_kernel_repos:

Adding the repositories
-----------------------

Here we add not only the Stable_kernel_Backport repository but also it's filesystems counterpart.
That is because we are concerned primarily with the entire btrfs software stack: kernel and userland.
Keeping both in sync is important, especially in the context of Rockstor's NAS functions.

.. code-block:: console

    zypper --non-interactive addrepo --refresh https://download.opensuse.org/repositories/Kernel:/stable:/Backport/standard/ Kernel_stable_Backport
    zypper --non-interactive addrepo --refresh https://download.opensuse.org/repositories/filesystems/15.3/ filesystems
    zypper --non-interactive --gpg-auto-import-keys refresh

.. _kernel_stable_repo:

Kernel Stable Backport repo
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This repo is cross architecture so will work for both x86_64 and ARM64 installs (i.e Pi4).

See the OBS page: `Kernel_stable_Backport <https://build.opensuse.org/project/show/Kernel:stable:Backport>`_.

.. _filesystems_repo:

Filesystems repo
^^^^^^^^^^^^^^^^

This repo is also cross architecture and so provides for both x86_64 and ARM64 architectures.

See the OBS page: `filesystems <https://build.opensuse.org/project/show/filesystems>`_.

.. _newer_kernel_install:

Installing the updates
----------------------

Once both repositories are in-place we must instruct the system to update from these newer repositories.

.. code-block:: console

    zypper up --no-recommends --allow-vendor-change

The above command will install packages requiring around 250 MB more space on the ROOT pool.
Rockstor's package selection is JeOS (Just enought Operating System) themed.
Hence the "--no-recommends" option above.
It may well be that your particular hardware requires additional firmware as well as the kernel update.
In which case omit the "--no-recommends" option to also install these firmware

.. note::

    A system reboot will be required for the above changes to take effect.

.. _raid1c3_raid1c4:

Btrfs raid1c3 raid1c4
---------------------

These raid levels are currently the newest available in btrfs.
As they are based on the far more mature btrfs raid1 they may be considered more mature than the parity raid levels.
They simply 'amplify' the number of copies stored across the same number of independent devices.

- **raid1c3** - 3 copies across 3 independent drives.
- **raid1c4** - 4 copies across 4 independent drives.

The :ref:`stable_kernel_backport` above procedure also enables the use of these even newer btrfs raid levels.
At least in the underlying operating system.

.. note::

    Rockstor 'allows' these raid levels but is currently un-aware of them.
    As such if any Pool modifications are enacted via the Web-UI,
    e.g :ref:`poolbalance` or :ref:`poolresize` the Rockstor defaults will be reasserted.
    See :ref:`dlbalance_re_raid` to reassert a custom raid profile.

.. _mixed_raid_levels:

Btrfs mixed raid levels
-----------------------

Btrfs, somewhat uniquely, can have one raid level for data and another for metadata.
One approach to alleviate the currently know issues, design wise, in the btrfs parity raid levels,
is to use:

- **data** - btrfs raid5 or preferred raid6
- **metadata** - btrfs raid1c3 or preferred raid1c4

Note that with the preferred options above btrfs can have a 2 disk failure capability per pool.
This is of particular interest to those running pools consisting of many devices.

.. note::

    As per the :ref:`raid1c3_raid1c4` note, Rockstor is unaware of some non standard data/metadata mixes.
    And likewise the Web-UI Pool operations of :ref:`poolbalance` or :ref:`poolresize`
    will undo any custom pool data/metadata mixed raid setup and revert to Rockstor defaults.
    See :ref:`dlbalance_re_raid` to re-assert a custom mixed raid arrangement.
    All other operations however should function as normal.
