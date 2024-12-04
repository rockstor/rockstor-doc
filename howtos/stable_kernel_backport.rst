.. _stable_kernel_backport:

Installing the Stable Kernel Backport
=====================================

.. warning::

    This How-to is intended for advanced users only.
    Its contents are likely irrelevant unless you require capabilities beyond our default openSUSE base.
    We include these instructions with the proviso that they will significantly modify your system from our upstream base.
    As such you will be running a far less tested system, and consequently may face more system stability/reliability risks.
    N.B. Pools created with this newer kernel have the newer free space tree i.e. (space_cache=v2).
    As do Pools created using "Built on openSUSE" Leap 15.6 and newer instances.
    Future imports require kernels which are equally new/capable (at least ideally).

If you are reporting issues on our `Community Forum <https://forum.rockstor.com/>`_
or in any of our `GitHub <https://github.com/rockstor>`_ repositories,
please indicate if you have applied these changes.

Install all updates before following these instructions.
And test your system again after a reboot to ensure that this procedure is still necessary.

As of writing, the Leap version used in our "Built on openSUSE" comes with many openSUSE/SuSE organised patches.
Almost all of these patches are backports from newer kernels,
applied to a designated 'base' kernel version.
As such the running kernel is newer than its 'base' version indicates.

Rockstor "Built on openSUSE" does not install newer kernels than its upstream OS,
as it once did when based on CentOS 7 (Rockstor v3 and earlier).
That is primarily because it is no longer necessary,
our new upstream actively maintains btrfs and employs some of the key btrfs contributors.
As a result many relevant btrfs backports are already in our upstream default kernel.
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

OpenSUSE's Leap 15.3/15.4/15.5 default kernels restrict the parity raid levels of 5 & 6 to read-only.
This decision was taken as the parity raid profiles are far younger than the non parity profiles of 0, 1, and 10.

From openSUSE Leap 15.6 this is no longer the case as a far newer kernel base was chosen.
As such our "Built on openSUSE" Leap 15.6 variant and newer have read-write parity btrfs raid out-of-the-box.

See :ref:`redundancyprofiles` for supported btrfs profiles per Rockstor version.

Pre "Built on openSUSE" Leap 15.6,
when creating a parity raid pool (volume in btrfs parlance), the following message appears in the system journal:

.. code-block:: console

    kernel: btrfs: RAID56 is supported read-only, load module with allow_unsupported=1

Rather than just *allowing unsupported* it was proposed that instead one took advantage of a newer kernel.
In this case the upstream-of-openSUSE latest stable kernel version back-ported to openSUSE.

.. warning::

    As of Leap 15.6 there are far-fewer btrfs reasons to use the Stable_kernel_Backport approach.
    Consider instead installing a later version of Rockstor,
    or following the appropriate in-place "Distribution update from 15.* to 15.*` howto.

.. _newer_kernel_repos:

Adding the repositories
-----------------------

Here we add not only the Stable_kernel_Backport repository but also it's filesystems counterpart.
That is because we are concerned primarily with the entire btrfs software stack: kernel and userland.
Keeping both in sync is very important, especially in the context of Rockstor's NAS functions.

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

.. warning::

    NOTE: Correct the filesystems repository line in the following for your Leap version.

.. code-block:: text

    zypper --non-interactive addrepo --refresh https://download.opensuse.org/repositories/Kernel:/stable:/Backport/standard/ Kernel_stable_Backport
    zypper --non-interactive addrepo --refresh https://download.opensuse.org/repositories/filesystems/15.X/ filesystems
    zypper --non-interactive --gpg-auto-import-keys refresh

.. _newer_kernel_install:

Installing the updates
----------------------

Once both repositories are in-place we must instruct the system to update from these newer repositories.

.. code-block:: console

    zypper up --no-recommends --allow-vendor-change

The above command will install packages requiring around 300 MB more space on the ROOT pool.
Rockstor's package selection is JeOS (Just enough Operating System) themed.
Hence the "--no-recommends" option above.
It may well be that your particular hardware requires additional firmware as well as the kernel update.
In which case omit the "--no-recommends" option to also install these firmware

.. note::

    A system reboot will be required for the above changes to take effect.
