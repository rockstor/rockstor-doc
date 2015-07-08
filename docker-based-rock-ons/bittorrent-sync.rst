.. _btsync_rockon:

BTSync Rock-on
==============

Please be aware of the common prerequisites for all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirement.

What is BTSync
--------------

`BitTorrent Sync <https://www.getsync.com/>`_ is a
`cross platform <https://www.getsync.com/platforms/desktop>`_ Closed Source
pier to pier file synchronization system know for it's advanced
`feature <https://www.getsync.com/features>`_ set.  Please note however that
the full feature set has recently been reserved for paid subscription members;
the paid and free versions
`differ <http://help.getsync.com/customer/portal/articles/1901266-sync-free-vs-sync-pro>`_
significantly.  Its synchronization function works by evaluating files in 4 MB
*chunks*; transferring only the *changed chunks* of files between clients.  If
files are less than 4 MB in size and have changed then they are transferred
to all participating clients in their entirety.
The Web based :ref:`WebUI <btsync_ui>` making it a good fit with Rockstor.

.. _btsync_doc:

BitTorrent Sync Documentation
-----------------------------

The BitTorrent Sync `Help Center <http://help.getsync.com/>`_ is the best place to start and their
`Sync 2.0 Overview <http://help.getsync.com/customer/portal/articles/1902649-sync-2-0-overview>`_
is a good introduction to the technology.
Please note the`supported platforms <http://help.getsync.com/customer/portal/articles/1909016-supported-platforms?b_id=3895>`_
and their `FAQ <http://help.getsync.com/customer/portal/articles/1916920-faqs>`_.


.. _btsync_install:

Installing BitTorrent Sync Rock-on
-------------------------------
First please consider the pre-requisites for any Rockstor Rock-on; these
are linked to at the :ref:`top <btsync_rockon>` of this document. Note also
that the BitTorrent Sync Rock-on will require a Share to sync/store it's
associated folders. Note that this is in addition to the :ref:`rockons_root`
that may well already have been made.

.. image:: btsync_install.png
   :scale: 80%
   :align: center

Click the **Install** button next to the BitTorrent Sync listing on the Rock-ons page.

.. _btsync_share:

BTSync Share
^^^^^^^^^^^^

Next we select the **Storage area** for the BitTorrent Sync files.  Here we are
using the **recommended Share name**.

* **btsync-data** - room enough for your data and snapshots.

.. image:: btsync_share.png
   :scale: 80%
   :align: center

N.B. to create this storage area please see our :ref:`createshare`.

.. _btsync_port:

BTSync Ports
^^^^^^^^^^^^

These are the **Default Ports** and it is unlikely you will have to alter them.

.. image:: btsync_ports.png
   :scale: 80%
   :align: center

Next configure the Transmission **User** and **Password** for the
:ref:`btsync_ui`

.. image:: btsync_user.png
   :scale: 80%
   :align: center

Note that these are examples only, you can use whatever username and password
you like but don't use spaces.

.. image:: btsync_verify.png
   :scale: 80%
   :align: center

Check that the entered details are correct before clicking **Submit**.

Closing the resulting simple *Installation is in progress* dialog and we have:-

**The BitTorrent Sync Rock-on is ON**

.. image:: btsync_on.png
   :scale: 80%
   :align: center

N.B. Notice the **BitTorrent Sync UI** button and the **spanner** to see the
Rock-on settings and add additional Shares.

From the information dialog **i icon** on the BTSync Rock-on listing we get:-

.. image:: btsync_info.png
   :scale: 80%
   :align: center

Reproduced here for clarity:-

***Additional information about BTSync Rock-on***::

   Authentication

   Default username for your BTSync UI is **admin** and password is **password**

   Storage

   You can also assign additional Shares for custom organization of your data.

.. _btsync_ui:

BTSync UI
---------

We now have the **Default BitTorrent Sync UI**.

.. image:: btsync_ui.png
   :scale: 80%
   :align: center

You can now Sync other BitTorrent Sync sources with a Rockstor BitTorrent Sync Rock-on Share; see :ref:`transmission_doc`.