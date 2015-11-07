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

Time Machine is the built in backup system in OSX (Operating System 10).
It is a `requirement <https://support.apple.com/en-us/HT202784>`_ of Time
Machine that network volumes be over AFP. By way of example this document steps
through the configuration of a Time Machine compatible network volume.

..  _create_afp_share:

Creating an AFP share
---------------------

In order to establish an AFP share it is first necessary to have a
pre-configured storage pool, this pool will then be used in the AFP Share.

* To create a storage pool see :ref:`createpool` in the :ref:`pools` section.
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

Here a :ref:`Share <shares>` named **Backups** has been created; note that is
it strongly advised that any Share to be used by Time Machine be at least 3
to 5 times the size of the data on the client machine. A typical OSX install
before any data is 6-9 GB. This makes it advisable to allocate around 30-50 GB
per client machine.

..  image:: tm_backups_share.png
    :scale: 80%
    :align: center

*A 100 GB share of the time_machine_pool*

A note of