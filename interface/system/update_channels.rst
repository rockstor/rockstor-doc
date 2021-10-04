.. _update_channels:

Software update
================

.. _rockstor_licence:

GNU GPLv2 Licenced
------------------

The code that makes Rockstor possible is developed under the
`GNU GPLv2 <https://www.gnu.org/licenses/old-licenses/gpl-2.0.html>`_ licence
and is therefore fully Open Source, there is no contributor agreement and
everyone is encouraged to help in what ever way they can. It is very much
developed in the open with key decisions made by the community and their
interaction with Rockstor contributors and maintainers `Our Mission <https://rockstor.com/about-us.html>`_.
This flow of ideas and open development is held as a founding principal and is
instantiated in the `Rockstor forum <https://forum.rockstor.com/>`_ and within
the code itself `on GitHub <https://github.com/rockstor>`_.

`Rockstor <https://rockstor.com/>`_ the project embodies an identifiable
software distributor and coordinator of the Open Source product that is the
scheduled Rockstor releases. It also forms an identifiable entity necessary
for the support of the releases (where needed) and infrastructure necessary to
maintain the open development that is essential in modern non trivial software
appliances that have any hope of qualifying as **future-proof**.

After an initial development of 2.5 years the sustainable nature of this
endeavour was approached and redressed in `a thread on the community forum <https://forum.rockstor.com/t/would-you-pay-a-one-time-charge-for-stable-updates/448/21>`_.
The consensus was to adopt a two-tiered updates model; testing and stable.

..  image:: /images/interface/system/update-channels//update_channel_options.png
    :width: 100%
    :align: center

The **update alternatives** offered in Rockstor.

.. _testing_channel:

Testing Channel
---------------

The testing channel for updates is intended primarily for **developers** or
for those who wish to **actively test Rockstor** and who are entirely happy on
the developmental edge of releases. There is growing unit test coverage that
all releases are expected to pass prior to their release, but, given the rapid
nature of these releases **weekly or shorter**, it is not recommended to put
production systems on this update channel. The flip side is that a rapid
release cycle affords fast development and widespread field testing of what
ultimately becomes the :ref:`stable_channel` at curated points.

However, it must be understood that appliance development is a complicated
business and it is inevitable that along the way fixing one thing will break
another. All reasonable efforts will be made to avoid obvious breakage. But
ultimately this testing channel is intended to find problems by way of
tester/developer reports and collaboration and will involve partially
implemented features of an experiment nature. The intention is to provide a
feature testing platform that we can gradually stabilise before then releasing
it's stable channel spin offs at known good points.

Participation in the testing channel along with considered bug, code, or
documentation contributions is the heart of Rockstor development and along
with patience and understanding can only benefit all those involved.
Please see :ref:`additional benefits <free_stable>`.

*N.B. due to recent resource shortages we have had to temporarily suspend the
testing channel in favour of serving our Stable channel subscribers. But all
efforts are under way to re-establish this valuable and previously popular
development facility. Our pending and long planned move to openSUSE is
intended to mark the re-birth of this developer favoured channel.*

**No charge**

..  image:: /images/interface/system/update-channels//activate_testing_channel.png
    :width: 100%
    :align: center

There is really no better testing alternative than thousands of willing testers
putting a proposed product to uses that were never envisaged by its developers;
and when those testers/developers see rapid iteration in the problems they
find/fix and report, everybody wins. It's the classic *Bazaar* model described
in `CatB <https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar>`_.

.. _stable_channel:

Stable Channel
--------------

This is the recommended channel for **Production Rockstor use**.
The frequency of releases is much lower (**monthy or longer**) than those in
the :ref:`testing_channel` and there is the reassurance that updates in the
stable channel have been field tested first in the testing channel. This
channel will receive the highest attention with regard to bug fixes, whereas
the testing channel is more focused on development rather than refinement.
There will also be greater attention paid to avoiding regressions from one
stable channel release to the next.

Below we see the process involved in setting up the stable channel updates.
A link is provided to the Rockstor shop showing the **Stable Updates
subscription** option. On selection and purchase the activation code will be
emailed to the address given. This code is intended for the dialog shown
below. Also note our :ref:`email_test` section where the Appliance ID, a UUID
generated during install, is contained within the test email. The appliance ID
is used to identify an individual install and when paired with an activation
code configures stable channel access.

N.B. When re-installing on a different motherboard, or where the boards
product_uuid is non unique, a different appliance id will result. This means
the prior installs activation code will no longer work against the new
appliance id. For this circumstance we have our *in public beta test*
`Appliance ID manager (appman) <https://appman.rockstor.com/>`_. Please be
patient as we work our the teething problems expected with newly release
systems. Specific documentation will follow once we have established the less
self explanatory elements.

Participation in the stable channel is key to the future of Rockstor
development. The ability to continue to improve and provide future-proof
services, by way of advanced file system facilities made easy, is dependant on
a financial component. The stable channel is that financial component.
Currently a one-year subscription costs £20.00 (GBP).

Please keep an eye on our `friendly forum <https://forum.rockstor.com/>`_ as
discount / promotional codes are occasionally issued.

**Yearly subscription managed by appman**

..  image:: /images/interface/system/update-channels//activate_stable_channel.png
    :width: 100%
    :align: center

.. _free_stable:

`Rockstor project repositories <https://github.com/rockstor>`_: contributors
qualify for up to 10 personal use activation codes.

.. _auto_updates:

Auto Updates
------------

When enabled, **auto update** checks for all system updates and installs them
automatically on a daily basis. This is the **recommended** setting when on the
:ref:`stable_channel` only. If you are on the :ref:`testing_channel` it is not
recommended to enable auto updates but instead to evaluate all updates prior to
applying them; this advice is down to the more unstable nature of
the testing channel and its inevitably greater chance of breakage or bugs.

..  image:: /images/interface/system/update-channels//enable_auto_updates.png
    :width: 100%
    :align: center

**N.B. Auto updates are only recommended when on the stable updates channel**
