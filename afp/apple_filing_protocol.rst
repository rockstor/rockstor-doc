..  _afp:

Apple Filing Protocol (AFP)
===========================

An Apple / OSX native network sharing system akin to SMB/CIFS from
MS Windows and NFS from Unix. However as of OSX 10.9 Mavericks and 10.10
Yosemite the default network sharing protocol in OSX is SMB/CIFS
(`apple reference <https://support.apple.com/en-gb/HT204445>`_). However AFP
is still enabled by default and if SMB is not available then AFP is used.

..  _time_machine:

Time Machine
------------

Time Machine is the built in backup system in Apple's OSX (Operating System
10). It is a `requirement <https://support.apple.com/en-us/HT202784>`_ of Time
Machine that network volumes be over AFP. By way of example this document steps
through the configuration of a Time Machine compatible network volume.

..  _create_afp_share:

Creating an AFP share
---------------------

In order to establish an AFP share it is first necessary to have a
pre-configured storage pool, a Share of this pool, and a Rockstor user to
authenticate against this Share. Finally the Share must be exported via the AFP
method. The following list details a suggested order and links to
documentation on each of these steps.

* To create a storage pool see :ref:`createpool` in the :ref:`pools` section.
* :ref:`Add a Rockstor user <adduser>` to match the OSX user, see the :ref:`users` section.
* A :ref:`Share <shares>` of this storage pool is then required, see :ref:`createshare` in the :ref:`pools` section.
* Finally this share is exported via the AFP system.

The Time Machine Pool
^^^^^^^^^^^^^^^^^^^^^

In the following example a dedicated **time_machine_pool** has been created.

..  image:: time_machine_pool.png
    :scale: 80%
    :align: center

*A 3 disk Raid1 pool of drives*

The "Backup" Share
^^^^^^^^^^^^^^^^^^

Here a :ref:`Share <shares>` named **Backups** has been created; note that it
is strongly advised that any Share to be used by Time Machine be at least 3
to 5 times the size of a single full backup. A typical OSX install
before any data is 6-20 GB depending on upgrades applied etc. This makes it
advisable to allocate around 30-100 GB per client machine.

In this example we have changed the owner and group of our share to that of an
existing Rockstor user and removed *Other* users access as it is not required.
Note that the Rockstor user name doesn't have to match that of the OSX user
but it is easier if it does as it will then be auto populated on the client
machine.

..  image:: tm_backups_single_user.png
    :scale: 80%
    :align: center

**If multiple users are required to share this Network Volume then create an
appropriate group eg macuser and ensure all you Mac user belong to
that group. You can then select this group and enable group write.**

Please note that if practical it is best to create one share per machine for
Time Machine backups as this prevents single client machines monopolizing the
available space as Time Machine defaults to using all the available space and
will only remove it's own old backups when space is short; and not another
machines backups. This results in frequently used machines backups dominating
the available space and can prevent occasionally used machines from having
space to do their backups.

The Access Control section of a Share also allows for setting up read only
shares on the network if this is desired.

Our Example Share:

..  image:: tm_backups_share.png
    :scale: 80%
    :align: center

*A 100 GB share of the time_machine_pool*

Add AFP Export
^^^^^^^^^^^^^^

Finally **export** the **Share** via the **AFP** entry in **File Sharing**.
This menu entry is available in the Storage section. Note that the **AFP
Service** will first have to be **switched ON** before these options are
available.

..  image:: add_afp_export_tm.png
    :scale: 80%
    :align: center

**Note the Time Machine option** this default to off and is not required for
normal AFP file sharing.

Client OSX configuration
------------------------

Having now setup an AFP share as :ref:`above <create_afp_share>` we can now
configure the client Mac machines to use this share as the Network Time Machine
Volume.

