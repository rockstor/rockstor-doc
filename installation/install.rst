
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

See YouTube `VirtualBox Rockstor install demo <https://www.youtube.com/watch?v=00k_RwwC5Ms>`_.

Before proceeding with a serious installation that may require hardware
procurement, you can evaluate Rockstor on Amazon AWS.

See YouTube `Rockstor on ec2 <https://www.youtube.com/watch?v=ys_8FLVov2U>`_.

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
   intended via our newer Rockstor 4 "Build on openSUSE" variant. N.B. RPi 400
   requires at least a 15.3 profile for the internal keyboard to work.

Upgrading Rockstor
------------------
Rockstor is under continuous development and we generally release updates in
small batches. These updates are easy to install. But we do roll-out major
releases that require a complete re-installs. Upgrading from Rockstor 3 (CentOS
based) to Rockstor 4 "Built on openSUSE" is one such update.
But such updates are very rare.

Non re-install Rockstor updates can be installed in two ways :

1. Install updates from the Web-UI (recommended):
On the Rockstor Web-UI, far top-right, you will see an upward facing arrow if
any Rockstor package updates are available. All upstream packages except the
'rockstor' package can similarly be installed by clicking on a flashing
wifi-like icon. Again this is not shown if no updates are available. But it
does show, as per the up-arrow, if there is a rockstor package update
available.
But only the up-arrow will actually update the main rockstor package.
These disparate but related mechanisms allows folks to choose to only update
all packages bar the rockstor package (wifi-like icon).

See the following section for details on upgrading the Rockstor package plus
all pending upstream updates :ref:`update_channels`.

2. Alternatively, for advanced users only, one can updated from the Command
Line Interface (CLI).

Just the main rockstor package::

    [root@localhost ~]# zypper update rockstor

The entire Rockstor 4 system including all upstream updates. Our login message
has a reminder of these commands::

    [root@localhost ~]# zypper refresh
    [root@localhost ~]# zypper up --no-recommends

- And Rockstor 3 similarly via::

    [root@localhost ~]# yum update rockstor

and::

    [root@localhost ~]# yum update

On both OS bases a reboot is recommended, but only after the update has
completed. This can take some time, depending on how many updates have to be
downloaded and established.

If an update is disruptive, the update process prompts for user action and
provides the necessary information to choose to update or not. You can safely
decide not to update if that makes sense for your environment.
