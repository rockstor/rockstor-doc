.. _oemguide:

OEM Guide
=========

This Guide is intended for Original Equipment Manufacturers/NAS hardware sellers, Value-added resellers (VARs),
who are interested in bundling Rockstor "Built on openSUSE" with their hardware products.

For our software license, please see FAQ entry: ":ref:`faq_license`".
Compliance with the stated licenses under which our code is released,
and their necessarily associated Copyright notices,
and that of our trivially modified linux distro base; the "Built on openSUSE" bit,
is a legal requirement.

.. note::

    Note however; this requirement does not differ from any other predominantly GPL-3.0-or-later licensed software bundling.
    I.e. one is free to redistribute, as-is, so long as no modifications are made.
    Modified versions, once re-distributed,
    entail further legal responsibilities regard availability of the modified version.
    Continuing the freedoms originally granted, for folks to know what code their systems are running.

Note that `The GPL Is a License, not a Contract <https://lwn.net/Articles/61292/>`_.

`The Rockstor Project <https://opencollective.com/the-rockstor-project>`_
is an `Open Collective <https://opencollective.com/>`_
Non-Profit/Non-Business Open Source community endeavour.

- All Rockstor distributed code is FSF Free/Libre & OSI approved and available on our
  `GitHub Organisation <https://github.com/rockstor>`_ site.

- All 'rockstor' rpm packages are source (--format sdist) in nature: i.e. non-binary.

- All released packages are built directly from publicly tagged GitHub releases,
  for details see: `rockstor-rpmbuild <https://github.com/rockstor/rockstor-rpmbuild>`_.

- All installers are built using an open source project and configuration,
  for details see: `rockstor-installer <https://github.com/rockstor/rockstor-installer>`_.

Our continued existence, i.e. ongoing-development & distribution services,
depend entirely upon good-will and active community participation in our Open Collective membership Tiers.
As such, circumvention of these service orientated tiers (curated release channels/support/membership/etc),
in any way, would result in no future communication or service to the offending agent.
We protect, by way of our licensing choices, and consequent code availability, the end-users freedoms.
That does not oblige any member of The Rockstor Project's team, in any way, regardless of Tier membership.

**Given the above freedoms, all-around, we can only request the following:**

1. OEM hardware distributors/redistributors resellers honour our existing sustainability model,
i.e. they have an appropriate number, given anticipated development team contacts per-year,
of 'OEM Pre-installer subscription' memberships.
Rockstor's continued development, and existence,
depends entirely on interested parties appreciating both past and ongoing development team efforts and associated costs.

The Rockstor Project development team, in-turn,
will endeavour to prioritise OEM/reseller technical enquiries/requests as resources allow.
I.e. a pre-installer's enquiries/concerns are assumed to relate to more than one install,
whereas our non-OEM contribution tiers relate to specific installs; i.e:

- a. Stable Updates subscription €24/year.
- b. Incident-based Support subscription (`Planned <https://rockstor.com/paid_support.html>`_) €240/incident/year.
- c. OEM Pre-installer subscription (proposed) €960/year.

.. note::

    Each of the above Tiers is independent,
    (a.) no implied support,
    (b.) superset of (a.) including a single support incident.
    (c.) OEM/pre-installer/for-profit entity membership: no implied end-user support.

2. Any pre-install arrangement must honour our default of neither :ref:`update_channels` channel being enabled.
All non 'rockstor' package upstream updates are available regardless of this selection.
See: :ref:`updaterockstorwebui`.
We stand-by the end-users choice to subscribe to either of our update channels, or neither.
Support requests of any sort related to pre-installed instances,
where this choice was made by the distributor/re-distributor,
will be ignored.

3. All pre-installs/re-distributions will involve only our
`downloadable <https://rockstor.com/dls.html>`_ installer images.
And then only when said installers include Stable Release Candidate 10 or later status 'rockstor' packages.
With Stable release status (non RC) strongly preferred, if available.

.. warning::

    Apparent Rockstor installs not conforming to all of (1), (2), and (3) above,
    will be deemed modified:
    with all the consequent licensing ramifications regarding redistribution of modified code.
    We digitally sign all released rpm packages,
    and all distribution repositories that host them.
    We can only reasonably respond to support/development requests/enquiries for software that we distribute.

Practical considerations
------------------------

Our installer is end-user orientated, but, with caveats, OEM compatible.
During the very first boot of our installers: the systems `root` user password is configured.
As such the end user, not a pre-installer, is the intended client.
See: :ref:`installer_howto` for all the steps involved.
In brief:

- Select Installation Disk
- Select Locale
- Select Keyboard Layout
- Rockstor “Built on openSUSE” installer License Agreement
- Select Time Zone
- Enter Desired root User Password (with a confirmation step thereafter)

.. warning::

    Only once the `Rockstor bootstrapping tasks` has completed,
    can the system then be safely shutdown/halted.
    Enabling the remainder of the install to be completed on the intended final hardware.

.. note::

    The Web-UI setup stage, until it is completed, will remain 'pending',
    irrespective of reboots.
    Enabling target drive transfer to the intended final system & network.

**In summary**: before the initial Web-UI setup,
but after confirmation of the `OK Rockstor bootstrapping tasks`,
the installation disk can be safely transferred (assuming a clean shutdown) to final hardware.
Only during the :ref:`webui_setup` stage do we establish the intended system-unique **Appliance ID**.
See :ref:`aboutapplianceid` for details.

Pre-installers are strongly requested to ensure their distributed systems do not result in fake/non-unique Appliance IDs.
Repeat Appliance ID installs will be refused support by The Rockstor Project.

.. note::
    If hardware preferred by a pre-installer results in fake/non-unique Appliance IDs,
    please consider enabling our accommodation by informing support.
    The Rockstor Project development team can then extend our list of known non-unique product_uuids.

Given all of the above, and our end-user accessible installer,
we recommend that Rockstor bundling takes the form of supplying/bundling an installation medium:
i.e. a USB key pre-loaded with our installer, with BIOS settings adjusted accordingly.
This will empower the designated end-user with bare-metal re-install capability, assisted or otherwise.
