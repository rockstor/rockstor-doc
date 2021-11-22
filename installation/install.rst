
.. _installation:

Installation
============

Installation of Rockstor is a short and straight forward process. For all types
of installations, see :ref:`quickstartguide` to get started. Please also note
that we have a :ref:`pre_install`.

.. toctree::
   :caption: Further details are in the following sections:
   :maxdepth: 2

   quickstart
   pre-install-howto
   installer-howto

.. _quickeval:

Quick evaluation using a virtual environment
--------------------------------------------

Rockstor can also be evaluated quickly using a virtual machine, see our
:ref:`kvmsetup`.

Hardware recommendations
-------------------------

There is nothing about Rockstor that requires special hardware. It's Linux, and
specifically Rockstor 4 is "Built on openSUSE" while v3 used CentOS, so it can
be installed on a wide range of commodity hardware, with 4 gaining ARM64
compatibility.
See :ref:`minsysreqs` for basic requirements.

Over time, the Rockstor developers and community at large share hardware specs
that are known to work with Rockstor. Below is a list of these recommendations.
Please note, however, that the following examples are to be taken as
illustrations of possible builds at the time of writing and will likely be
rapidly outpaced by the rapidly evolving hardware market. We always recommend
visiting our `Forum <https://forum.rockstor.com>`_ for user stories, example
builds, and request advice on hardware choice or recommendations.

Complete Builds for Home and small organizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can find user stories and example builds on our
`Forum <https://forum.rockstor.com>`_, but some excerpts are listed below:

1. A build used by Rockstor developers and at least some known
   community members uses `ASRock C2550D4I
   <https://www.asrockrack.com/general/productdetail.asp?Model=C2550D4I>`_
   with `this memory
   <https://www.kingston.com/unitedstates/us/memory/search/discontinuedmodels?partId=kvr16le11%2F8>`_. The
   motherboard provides 12 SATA ports, so `this
   <https://www.silverstonetek.com/product.php?pid=452>`_ is a recommended tower
   case to hold up to 12 hard drives.

2. Yet another recommendation used by some community members is HP Proliant
   Microserver Gen8.

3. Raspberry Pi4 and RPi 400 have also both been reported as working as
   intended via our newer Rockstor 4 "Built on openSUSE" variant. *N.B.* RPi
   400 requires at least a 15.3 profile for the internal keyboard to work.

.. _updating_rockstor:

Updating Rockstor
------------------
Rockstor is under continuous development and we generally release updates in
small batches. These updates are easy to install and distributed in two
distinct *update channels* described in our :ref:`update_channels` section. On
rare occasions, we roll-out major releases that require a complete re-install;
upgrading from Rockstor 3 (CentOS-based) to Rockstor 4 "Built on openSUSE" is
one such update.

.. note::
   Would you like to see a specific feature added or updated? Come share your
   idea on our `friendly forum <https://forum.rockstor.com/>`_ or see how you
   can contribute to Rockstor in our :ref:`contributetorockstor` section.


Non re-install Rockstor updates can be installed in two ways:

1. from the :ref:`Web-UI<updaterockstorwebui>` (**recommended**):
2. from the :ref:`command line<updaterockstorcli>`

.. _updaterockstorwebui:

Install updates from the Web-UI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Rockstor distinguishes between two types of software updates:

* updates of the Rockstor package itself
* updates to the base OS (system updates)

The presence of both these updates is signaled on the Rockstor Web-UI, in the
top-right corner:

.. image:: /images/installation/install/update-arrow.png
   :align: center

As you can see in the screenshot above, we have:

* an upward facing arrow next to the Rockstor version number: this indicates an
  update to the Rockstor package itself is available.
* a flashing WiFi-like icon: this indicates updates for the base OS are
  available.

To update, simply click on either one of these icons to see details about the
update(s) and proceed with their installation.

.. note::
   While an update to the Rocsktor package itself will also be listed among
   system updates, only clicking the upward facing arrow next to Rockstor's
   version will actually update the Rockstor package.

This allows you to choose to only update what you want:

* all system updates bar the Rockstor package: WiFi-like icon
* only the Rockstor package: upward facing arrow next to Rockstor's version

.. _updaterockstorcli:

Install updates from the command line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Alternatively, for advanced users only, one can update from the Command
Line Interface (CLI). In Rockstor 4 "Built on openSUSE", the procedure is as
follows:

To update the Rockstor package *only*:

.. code-block:: bash

   [root@localhost ~]# zypper update rockstor

To update the entire Rockstor 4 system including all upstream updates (note
that our shell login message has a reminder of these commands):

.. code-block:: bash

   [root@localhost ~]# zypper refresh
   [root@localhost ~]# zypper up --no-recommends


Similarly, in our legacy Rockstor 3 version, run :code:`yum update rockstor` or
:code:`yum update` to update the Rockstor package itself or the entire system,
respectively.

.. warning::

   On both OS bases a reboot is recommended, but only after the update has
   completed. This can take some time, depending on how many updates have to be
   downloaded and established.

If an update is disruptive, the update process prompts for user action and
provides the necessary information to choose to update or not. You can safely
decide not to update if that makes sense for your environment.
