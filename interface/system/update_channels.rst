.. _update_channels:

Software update
================

.. _rockstor_license:

Licensed: FSF Free/Libre & OSI approved
---------------------------------------

The Rockstor package code, as distributed, is developed under two main repositories:

* Source0: `rockstor-core <https://github.com/rockstor/rockstor-core>`_ is
  `GPL-3.0-or-later <https://www.gnu.org/licenses/gpl-3.0-standalone.html>`_ licensed.

* Source1: `rockstor-jslibs <https://github.com/rockstor/rockstor-jslibs>`_ is
  (`MIT <https://opensource.org/license/mit-0>`_ AND
  `Apache-2.0 <https://opensource.org/license/apache-2-0>`_ AND
  `GPL-3.0-or-later <https://www.gnu.org/licenses/gpl-3.0-standalone.html>`_ AND
  `LGPL-3.0-or-later <https://www.gnu.org/licenses/lgpl-3.0-standalone.html>`_ AND
  `ISC <https://spdx.org/licenses/ISC.html>`_) licensed.
  Indicating the combined works in this jslibs repository.

Making the package license, as per the `Fedora Project Wiki (Packaging:LicensingGuidelines)
<https://fedoraproject.org/wiki/Packaging:LicensingGuidelines#Mixed_Source_Licensing_Scenario>`_:

* *"GPL-3.0-or-later AND (MIT AND Apache-2.0 AND GPL-3.0-or-later AND LGPL-3.0-or-later AND ISC)"*

See the `SPDX License List <https://spdx.org/licenses/>`_ for details on the above assertions.

As such, the 'rockstor' package is fully Open Source; there is no contributor agreement, and
everyone is encouraged to help in whatever way they can. It is very much
developed in the open with key decisions made by the community and their
interaction with Rockstor contributors and maintainers.
See: `About US <https://rockstor.com/about-us.html>`_.
This flow of ideas and open development is held as a founding principal and is
instantiated in the `Rockstor forum <https://forum.rockstor.com/>`_ and within
the code issues currently `on GitHub <https://github.com/rockstor>`_.

In 2023 `The Rockstor Project <https://opencollective.com/the-rockstor-project>`_
became a non-profit fiscally hosted by
`Open Source Europe (OSE) <https://opencollective.com/europe>`_
with the aim to establish sustainable Open Source project development and maintenance.
Sustaining the required resources necessary; human included.

Released in 2013, around 2 years later the sustainable nature was approached, and redressed on our
`community forum <https://forum.rockstor.com/t/would-you-pay-a-one-time-charge-for-stable-updates/448/21>`_.
The consensus was to adopt a two-tiered updates model; Testing and Stable.
Around 11 years later, during the 5.5.*-* testing phase, an addition third tier was added: Edge.

..  image:: /images/interface/system/update-channels//update_channel_options.png
    :width: 100%
    :align: center

The 'rockstor' package **Update Tiers**.

.. _edge_channel:

Edge Channel
------------

.. note::
    **Untested** - Edge updates are definitely not intended for production use.

Edge tier updates are intended primarily for **developers**,
i.e. those who wish to **actively test and develop Rockstor**,
and who are entirely happy on the developmental edge.
We have around three hundred unit tests that every 'rockstor' package passes prior to its release,
but ultimately any production system needs wider field testing,
which is why packages in Edge, if found to be basically functional,
are promoted to the :ref:`testing_channel` for far wider community testing, evaluation, and feedback.

*As a transient scratch-pad for pre-testing channel packages,
the associated repo will be aggressively pruned.
Do not depend on any specific pkg version persisting within the Rockstor-Edge repo.*

**No charge**

..  image:: /images/interface/system/update-channels//activate_edge_channel.png
    :width: 100%
    :align: center

In Web-UI info/confirmation dialog.

.. _testing_channel:

Testing Channel
---------------

.. note::
    **In testing** - Be advised that production use of Testing updates is discouraged.

All reasonable efforts are made to avoid obvious breakage in this channel.
But ultimately the Testing channel is intended to find problems by way of
community field-testing and reporting.
Collaboration may involve partially implemented features of an experiment nature,
likely published to Edge first, with the intention to provide a
feature/fix testing platform that we can gradually stabilise before then releasing
to the curated :ref:`stable_channel`.
I.e. we cyclically restart testing phases to periodically release end phase testing package to the Stable channel.

Participation in the Edge & Testing channels along with considered bug,
code, or documentation contributions is the heart of Rockstor development.
Note: patience and understanding can only benefit all those involved.

There is no better testing alternative than thousands of willing folk putting a proposed product to real-world use,
and actively involving themselves in finding and/or fixing/reporting for the greater good.
It's the classic *Bazaar* model described in `CatB <https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar>`_.

**No charge**

..  image:: /images/interface/system/update-channels//activate_testing_channel.png
    :width: 100%
    :align: center

In Web-UI info/confirmation dialog.

.. _stable_channel:

Stable Channel
--------------

.. note::
    **Tested** - Stable updates are intended for **Production use**.

Here there is the reassurance that updates have been field tested first in the Testing channel.
The Stable channel will receive the highest attention with regard to bug fixes,
whereas the Edge & Testing channels are focused on developing those fixes ready for production.
Attention is also paid to avoiding regressions from one Stable update to the next.

N.B. When re-installing on a different motherboard, or where the boards
product_uuid is non unique, a different Appliance ID will result. This means
the prior install's activation code will no longer work against the new Appliance ID.
For these scenarios simply edit the Appliance ID on the relevant 'Computer' entry within
`Appman (Appliance ID manager) <https://appman.rockstor.com/>`_.

Participation in the Stable channel is key to the sustainability of Rockstor's development.
The ability to continue to improve and provide advanced file system facilities made easy,
is dependant on a financial component.
The Stable channel's associated non-profit subscription is that financial component.
See also the qualifying but as-yet pending `Paid Support <https://rockstor.com/paid_support.html>`_ option.

For the current cost of a **Stable Updates subscription membership**,
see our `Open Collective non-profit <https://opencollective.com/the-rockstor-project>`_.

..  image:: /images/interface/system/update-channels//activate_stable_channel.png
    :width: 100%
    :align: center

In Web-UI dialog indicating the steps to activating Stable Updates.

.. _free_stable:

`Rockstor project repositories <https://github.com/rockstor>`_ contributors
qualify for up to 3 personal use activation codes.

.. _auto_updates:

Auto Updates
------------

Rockstor's current Web-UI does not include auto updates configuration.
Although such a facility is planned.
Pull requests, as always, are welcome; see: :ref:`contributetorockstor`.

In the interim the well proven YaST2 can server this purpose.
See `Automatic online update <https://doc.opensuse.org/documentation/leap/startup/html/book-startup/cha-onlineupdate-you.html#sec-onlineupdate-you-automatically>`_.
A minimum (60 MB) console only YaST2 can be installed via:

.. code-block:: console

    zypper install --no-recommends yast2-online-update-configuration

and the resulting online update module invoked there-after via:

.. code-block:: console

    yast2 online_update_configuration

..  image:: /images/interface/system/update-channels/enable_auto_updates.png
    :width: 100%
    :align: center

The above shows the default settings once **Automatic Online Update** is selected (**Alt+m**).
Use the onscreen instructions to make any required changes.

When enabled, all qualifying updates are auto installed at the chosen interval.
This is only **recommended** when on the :ref:`stable_channel`.
The :ref:`testing_channel` and :ref:`edge_channel`, due to their developmental nature,
are likely to break.

**N.B. Rockstor is not necessarily compatible with other YaST modules.**
Although again, pull requests are welcome in this regard.
