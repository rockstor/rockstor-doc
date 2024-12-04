..  _pools:

Pools
=====

A Pool in Rockstor is a set of drives combined and represented as a single
volume. Pools have attributes such as redundancy profile and compression to
safeguard and store data efficiently. Pools can be expanded or shrunk by adding
or removing drives. In other words, a Pool is a single or multi device
BTRFS filesystem.

Pool related operations can be managed from the **Pools** screen listed under
the **Storage** tab of the Web-UI.

.. _createpool:

Creating a Pool
---------------

Whole (un-partitioned) drives are very much preferred as Rockstor Pool members.

See :ref:`import_data` to re-establish a prior Rockstor installs Pool.
It may also be possible to import similarly structured btrfs volumes, single or multi member.

Click on **Create Pool** button and submit the create pool form to create a pool.
There is a tooltip for each input field to help you choose appropriate parameters.


.. _redundancyprofiles:

Redundancy profiles
^^^^^^^^^^^^^^^^^^^

A broad abstraction of BTRFS raid profiles are available when creating a pool.

- Rockstor 4.1.0-0 and earlier supported btrfs raid single, 0, 1, 10, 5, and 6; with no mixed profile awareness.
- 4.6.0-0's Web-UI supports: single, single-dup, 0, 1, 10, 5, 6, raid1c3, raid1c4, raid1-1c3, raid1-1c4,
  raid10-1c3, raid10-1c4, raid5-1, raid5-1c3, raid6-1c3, raid6-1c4.

.. warning::
    Please see :ref:`btrfsnature` to avoid some surprises regarding the way btrfs does raid.

.. note::
    No btrfs raid profile requires that its member drives be matched in size.
    But in the case of btrfs raid0 particularly,
    the available space is maximised if they are similar, or ideally the same.

.. _mixed_raid_levels:

Btrfs mixed raid levels
~~~~~~~~~~~~~~~~~~~~~~~

Btrfs, somewhat uniquely, can have one raid level for data and another for metadata.
One alternative to using btrfs parity raid levels for metadata, known to be slow, is to use:

- **data** - btrfs raid5 or preferably raid6
- **metadata** - btrfs raid1c3 or preferably raid1c4

I.e. a btrfs raid6-1c4 or raid6-1c3 pool will have a 2 disk failure capability.
This is of particular interest to those running pools with a higher device count.

.. note::
    Rockstor from 4.6.0-0 onwards is required for Web-UI awareness of mixed profiles.
    The naming convention adopted within the Web-UI is essentially comprised of:
    "data-metadata" where the metadata profile is an abridged version, e.g. :ref:`raid5`-:ref:`1 <raid1>`.
    I.e. short-hand for :ref:`raid5` data, with :ref:`raid1` metadata.

.. _single:

single
......

**No redundancy.**
A single disk failure will result in the entire Pool being lost.
Valid option for creating a Pool with a single drive.
It is also recommended if you have multiple drives of very different sizes,
yielding higher total capacity compared to :ref:`raid0` in this setting.

.. _single_dup:

single-dup
..........

**Minimal redundancy for metadata only.**
A single drive failure will result in the entire Pool being lost.
Valid option for creating a Pool with a single drive.
Uses :ref:`single` for data, with duplication of metadata.
Metadata duplication does NOT span devices, providing only a second metadata copy,
possibly on the same device. Enabling a fail-through & repair for metadata read checksum failures.

.. _raid0:

raid0
.....

**No redundancy.**
A single drive failure will result in the entire Pool being lost.
Two or more drives are required for this profile.
It is recommended only when there is no need for redundancy,
and offers better performance than the :ref:`single` profile.
Both data and metadata are striped across the drives.
It is recommended for same/similar size drives.
If you have very differently sized drives and no need for redundancy,
the :ref:`single` profiles provide higher capacity.

.. _raid1:

raid1
.....

Can sustain **a maximum of one drive failure**.
Two or more drives are required.
Data and metadata are replicated on two independent devices,
irrespective of the total pool member count.

.. _raid5:

raid5
.....

Can sustain **a maximum of one drive failure**.
Two or more drives are required.
Uses parity and striping.
The BTRFS community consensus is that btrfs raid5 is ***not recommended for production/metadata use***.

.. _raid6:

raid6
.....

Can sustain **a maximum of two drive failures**.
Three or more drives are required.
Uses dual-parity and striping.
The BTRFS community consensus is that btrfs raid6 is ***not recommended for production/metadata use***.

.. _raid10:

raid10
......

Can sustain **a practical maximum of one drive failures**.
Four or more drives are required.
Uses a Raid0 (strip) of Raid1 mirrors.
Btrfs raid 10 offers the best overall performance with single drive redundancy.

.. _raid1c3_raid1c4:

raid1c3 & raid1c4
.................

Can sustain **two or three drive failures respectively**.
Three or four drives are respectively required.
These raid profiles are a more recent addition to btrfs.
Based on the far more mature btrfs :ref:`raid1`,
they may be considered more mature than the parity raid levels of :ref:`raid5` and :ref:`raid6`.
They essentially 'amplify' the number of copies stored across the same number of independent devices:

- **raid1c3** - 3 copies across 3 independent drives.
- **raid1c4** - 4 copies across 4 independent drives.

Please see the `btrfs docs <https://btrfs.readthedocs.io/en/latest/Introduction.html>`_
for up to date information on all btrfs matters.

For a BTRFS features stability status overview
see: `btrfs docs Status <https://btrfs.readthedocs.io/en/latest/Status.html>`_.

.. warning::

    Rockstor "Built on openSUSE" before Leap 15.6 defaulted to read-only for :ref:`raid5` & :ref:`raid6`.
    Write access can be enabled on older installs via :ref:`stable_kernel_backport`: **advanced users only**.
    Preferably consider an in-place OS update via the appropriate "Distribution update from 15.* to 15.*" how-to.

Compression Options
^^^^^^^^^^^^^^^^^^^

Compression can optionally be chosen during Pool creation or it can be set on a
previously created Pool. In the latter scenario, compression is applied only to
data written after it's set.

Compression can also be set at the Share level. If you don't want to enable
compression for all Shares under a Pool, don't enable it at the Pool
level. Instead, selectively enable it on Shares.

Besides not enabling compression at all, there are three additional choices.
For more info see:  `btrfs.readthedocs compression <https://btrfs.readthedocs.io/en/latest/Compression.html>`_

* **zlib**: Provides slower but higher compression ratio. Levels as yet unsupported.
* **lzo**: A faster compression algorithm but provides lower ratio compared to **zlib**.
* **zstd** Comparable compression to **zlib** but faster. Levels as yet unsupported.
  Requires Rockstor 5.0.2-0 "Build on openSUSE" Leap 15.4 or newer.

.. _poolmountoptions:

Mount Options
^^^^^^^^^^^^^

These are optional and meant for more advanced users to provide BTRFS specific
mount options. Since a Pool is a filesystem, it is mounted with default options
which can be altered by providing one or more of the following. You can find
out more about each option from the `BTRFS documentation mount options section
<https://btrfs.readthedocs.io/en/latest/btrfs-man5.html#mount-options>`_.

* **alloc_start**
* **autodefrag**
* **clear_cache**
* **commit**
* **compress-force**
* **degraded**
* **discard**
* **fatal_errors**
* **inode_cache**
* **max_inline**
* **metadata_ratio**
* **noacl**
* **noatime**
* **nodatacow**
* **nodatasum**
* **nospace_cache**
* **nossd**
* **ro**
* **rw**
* **skip_balance**
* **space_cache**
* **ssd**
* **ssd_spread**
* **thread_pool**

.. _poolresize:

Pool Resize/ReRaid
------------------

A convenience feature of btrfs Pool management is the ability to add or remove drives,
and change redundancy profiles, while still using the Pool.
The persistence of a pool's accessibility is otherwise known as it's 'online' state.
And so these changes are referenced as it's online capabilities.

A performance reduction is expected during any changes of this sort,
but depending on your hardware overhead, this can be unnoticeable.

**Note that increases in; drive count, percent usage, snapshots count, and Pool size can all impact on the memory and CPU required,
and the time for any changes to be enacted.**

Pool Resize / ReRaid may be done for the following reasons.

1. Change redundancy profiles. E.g. from btrfs RAID10 to btrfs RAID1. See :ref:`poolraidchange`.
2. Add disks and increase capacity. See :ref:`pooladddisks`.
3. Remove disks and decrease capacity. See :ref:`poolremovedisks`.

The following is the **first page of the Resize/ReRaid wizard**:

.. image:: /images/interface/storage/pool-resize-reraid-wizard-1.png
   :width: 100%
   :align: center

.. _poolraidchange:

Redundancy profile changes
^^^^^^^^^^^^^^^^^^^^^^^^^^

You can change :ref:`redundancyprofiles` online with only a few restrictions.

1. The resulting pool must have sufficient space for the existing data.
2. The target drive count will be sufficient for the target btrfs raid profile.
3. Rockstor can simultaneously change btrfs raid levels while :ref:`pooladddisks`, but NOT while :ref:`poolremovedisks`.

Because of (3.) above, when removing for example a drive from a pool which is already at the minimum drive count,
attached or detached, we have to first change the raid level of that pool.
A better approach is to instead add a disk, then remove the problem/detached/missing one.
But this is not always an option and the following example serves to show both raid level change and detached disk removal.


.. _poolbelowminimummembers:

Pool has below minimum members
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This situation is most common in non industrial DIY setups where a pool will often have only the minimum number of disks.

In the following example we have a btrfs raid1 Pool (minimum 2 disks) that has a detached/missing member.
We have already refreshed our backups via the suggested ro,degraded mount;
from the Pool details maintenance section that appeared.
And we have then switched to a rw,degraded mount to allow for the Pool changes.

A degraded mount option is required when there is a detached/missing disk; irrespective of drive count and btrfs raid level.
Otherwise any mount operation is refused.
The intention of the obligatory 'degraded' option is to ensure conscious intervention during an enhanced data loss state.
And a Pool may well go read only on it's own, by design, shortly after loosing access to one of it's members.
Again this is a data loss prevention tactic.
Continuing to write new data to a degraded pool incurs a progressively increasing risk of data loss.

Following on from the last image of the first page of the Resize/ReRaid wizard, if we selected **Remove disks**.

We would receive the following error:

.. image:: /images/interface/storage/pool-resize-reraid-below-min-disk-count.png
   :width: 100%
   :align: center

So we must first change this Pool's btrfs raid level to one that can sustain our examples target single disk count.
This leaves only btrfs raid single.
Note that we would not need this additional risky step if we were not running our raid 1 with it's minimum disk count.
Then if/when the first disk died/became unusable,
we could simply select the Remove disk wizard option and still be within the 2 disk minimum for our raid level.
Extra steps are considered risky as it stresses the remaining disks when on of their kin has recently died.
Often drives are of a similar age and wear level so this may not bode well for the remaining pool members.

So we must, in this example case, select **Modify RAID level only**.
And then select "Single" from the dropdown.

.. image:: /images/interface/storage/pool-resize-reraid-single.png
   :width: 100%
   :align: center

We are then presented with the proposed actions to be taken:

.. image:: /images/interface/storage/pool-resize-reraid-single-summary.png
   :width: 100%
   :align: center


And if all looks to be as intended, and we **Resize** (which also means ReRaid),
We are presented with the wizard complete dialog:

.. image:: /images/interface/storage/pool-resize-reraid-wizard-complete.png
   :width: 100%
   :align: center

Which warns of the expected potential performance hit during the operation,
and that the operation, depending on many factors, can last many hours to complete.

Once this re-raid operation is complete,
indicated by the new **Raid configuration:** entry in the pool details page,
we can :ref:`remove our detached disk <poolremovedisks>`.
As we are now no longer restricted by our prior raid level and it's associated 2 disk count minimum.
Again this raid level change would not have been required if we had not run our Pool at it's minim disk count for it's raid level.

.. _pooladddisks:

Adding Disks
^^^^^^^^^^^^

Disks of any size can be added, online, to an existing Pool.
The same Resize/ReRaid operation can also change the current btrfs raid level.
Combining both operations can result in a reduction of available storage, but this is usually the exception.

.. _poolremovedisks:

Removing Disks
^^^^^^^^^^^^^^

Disks can be removed from a Pool, online, similar to adding Disks.
But unlike when adding disks, Rockstor cannot change raid levels in the same Resize/ReRaid operation.
Given the above removing a disk always results in a reduced Pool capacity.
As such this operation can succeed only if the resulting capacity is greater than the current usage.
And if the resulting member count is not taken below the minimum for the btrfs raid level and mount options.

In the following we have a btrfs single raid level pool with a detached disk we wish to remove.
This is a convenient follow-on from the example used in the earlier :ref:`poolraidchange`.

From the **first page of the Resize/ReRaid wizard** indicated in the earlier :ref:`poolresize` section,
we select (this second go around) the **Remove disks** option.
This gives the following disk member selection dialog; in this example we have selected our detached member:

.. image:: /images/interface/storage/pool-resize-reraid-wizard-remove-selection.png
   :width: 100%
   :align: center

And it's consequent summary page:

.. image:: /images/interface/storage/pool-resize-reraid-wizard-remove-summary.png
   :width: 100%
   :align: center

And finally after committing via the Resize button,
we have the same Resize ReRaid wizard complete dialog shown at the end of the earlier :ref:`poolraidchange` example.

Our example degraded pool, post disk removal, has now been returned to a non degraded state.
And consequently the Web-UI header warning about this 'emergency' state is no longer displayed.
But note that a page refresh in the Pool Details page is required as unlike the leader it does not yet auto refresh.

**Be very sure, after having used a degraded mount option,
that it is removed from the custom mount options after a Pool has been returned to a non degraded state.**
*A reboot may be necessary to effectively remove this option from actively applying.*

.. _pooldelete:

Pool deletion
-------------

A *Pool* can be deleted by click on the corresponding **trash** icon for it in the *Pools*
screen under the *Storage* tab of the Web-UI.


.. image:: /images/interface/storage/delete_pool.png
   :width: 100%
   :align: center

A Pool can also be deleted using the **Delete** button inside it's detail
screen.

.. warning::

    **ALL ASSOCIATED DATA AND SHARES (BTRFS SUBVOLUMES) WILL BE DESTROYED.**

.. _poolscrub:

Scrubbing a Pool
----------------

The scrub operation initiates a BTRFS scrub process in the background. It reads
all data from all disks of the Pool, verifies checksums and fixes corruptions
if detected and possible. To find out more, see the `btrfs-scrub manual entry
<https://btrfs.readthedocs.io/en/latest/btrfs-scrub.html>`_.

To start a scrub, go to the Pool's detail page and click on the **Start a new
scrub** button in the Scrubs tab. The button will be disabled during the scrub
process and enabled again once the scrub finishes. The progress of a running
scrub operation is displayed in a table. Refresh the page to update the
information.

.. _poolautomatedscrubs:

Automated Scrubs
^^^^^^^^^^^^^^^^

A periodic scrub is a proactive strategy to fix errors before too many
accumulate. You can :ref:`scrubtask` on the :ref:`tasks` page under the
:ref:`system` menu item.

.. _poolbalance:

Balance a pool
--------------

The balance operation initiates a BTRFS balance process in the background. It
spreads data more evenly across multiple disks of the Pool. It is automatically
triggered after a :ref:`poolresize` operation, which is the main purpose of
this feature. A standalone balance operation is intended for advanced users who
can judge for themselves if it is necessary. To find out more, see
`btrfs docs balance <https://btrfs.readthedocs.io/en/latest/Balance.html>`_.

To start a balance, go to the Pool's detail page and click on the **Start a new
balance** button in the **Balances** tab.

