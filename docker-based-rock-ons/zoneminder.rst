.. _zoneminder_rockon:

ZoneMinder Rock-on
==================

Please be aware of the common prerequisites for all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirement.

Our `ZoneMinder Rock-on forum <https://forum.rockstor.com/t/zoneminder-rock-on/1899>`_ area.

.. _zoneminder_whatis:

What is ZoneMinder
------------------

`ZoneMinder <https://zoneminder.com/>`_ is a full-featured and open source video
surveillance software system. Licenced as GPLv2 or later. Capabilities include
the use of pretty much any camera, either directly connected or IP-enabled, and
the capability to run on general purpose hardware. The source code can be found
on their `GitHub page <https://github.com/ZoneMinder/ZoneMinder/>`_.
The web interface is mobile capable but there are also Android and IOS apps
available that interface with the open third-party friendly APIs. The
`zmNinja app <https://pliablepixels.github.io/>`_ is one such example and is
featured on the ZoneMinder main page; this app is also
`open source and on GitHub <https://github.com/pliablepixels/zmNinja>`_
with a `dual licenced <https://github.com/pliablepixels/zmNinja/blob/master/LICENSE>`_
source code (CC BY-NC-SA/4.0 and commercial). This app is written with the aid
of the ionic framework and so should mimic native behaviour.

.. _zoneminder_doc:

ZoneMinder Documentation
------------------------

Zoneminders `own documentation <https://zoneminder.readthedocs.io/en/latest/index.html>`_
is extensive and well presented. A good place to start from a Rockstor
Zoneminder Rock-on perspective would be the
`Getting Started <https://zoneminder.readthedocs.io/en/latest/userguide/gettingstarted.html>`_
section of the `User Guide <https://zoneminder.readthedocs.io/en/latest/userguide/index.html>`_
as the Installation Guide is redundant given that the below instructions guide
you though the Rock-on install which effectively install a docker based version
of ZoneMinder for you.


.. _zoneminder_install:

Installing ZoneMinder Rock-on
-----------------------------

First please consider the pre-requisites for any Rockstor Rock-on; these
are linked to at the :ref:`top <zoneminder_rockon>` of this document. Note also
that the ZoneMinder Rock-on will require two shares. One for the main storage of
configuration and event recording data, and another for the database used by
ZoneMinder to tie everything together. As databases can present a special work
load to btrfs (the underliying filesystem used by Rockstor) this share has been
kept separate. This then affords the possibility of differing filesystem
maintenance schedules for the two shares and for additional performance tunning
if that becomes necessary. Note that this does not include the pre-required
share to enable Rock-ons in the first place ie the previously referenced
:ref:`rockons_root`.

.. image:: zoneminder_install.png
   :scale: 80%
   :align: center

Click the **Install** button next to the ZoneMinder listing on the Rock-ons page.

.. _zoneminder_shares:

ZoneMinder Shares
^^^^^^^^^^^^^^^^^

Next we select the **Storage areas** for the ZoneMinder Rock-on's
**Config Storage** and **MySQL Storage** files. Note that the order of these
items may vary.

* **Config Storage** - room for all video events and configuration - minimum 50 GB
* **MySQL Storage** - sufficient to house the MySQL database - minimum 5GB

If you find that these values are insufficient then please discus this on the
`Rockstor forum <https://forum.rockstor.com/t/zoneminder-rock-on/1899>`_
so that this document might be updated and improved.

In the following image we are using the **recommended names** for all the
pre-configured shares.
