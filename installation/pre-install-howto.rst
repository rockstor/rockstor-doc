.. _pre_install:

Pre-Install Best Practice (PBP)
===============================

This how-to sets out to establish **Best Practice** prior to a **Rockstor install**.
It has grown out of a number of suggestions on the
`Rockstor forum <https://forum.rockstor.com/>`_
where problems have been encountered that might otherwise have been avoided.
The basic premise is to first ensure that the hardware you are to install Rockstor on
is fit for purpose and tested with readily available tools.

.. _memory_test:

Memory testing
--------------

Accurately working memory is key to an appliance like Rockstor. Regardless of what memory type
will be used, it is important to ensure that it is functioning error-free, otherwise it could
cause inconsistencies in the data stored, moved or changed. There are a few tools available,
some closed-source, some open source. While not endorsing one or the other, below is the
open-source tool that is frequently being used.

Memtest86+
^^^^^^^^^^

The `memtest86+ <https://www.memtest.org/>`_ program is derived from the linux kernel itself,
the core of the operating system that Rockstor is built on.
The current version of Memtest86+ is licensed under the GPL v2.
Technical reference: `GitHub memtest86plus <https://github.com/memtest86plus/memtest86plus/>`_.

Memtest86+ cautionary note
^^^^^^^^^^^^^^^^^^^^^^^^^^

Memtest86+ can place a very intense load on your system, especially if run in the
new multi-threaded mode (via F2 on initial start) but a sufficiently cooled
system should be able to execute this test indefinitely.

.. warning::
    If your system has cooling issues then it may lock up or even sustain damage.
    Please take care to monitor your system's temperatures during this test,
    for example using the CPU temperature monitor available in memtest86+.

.. note::
    This memory test will **continue indefinitely** until you either:
        1. turn off the system (which is safe to do)
        2. press the **ESC Key**

It is **recommended that two full test cycles** be completed.
But a single full pass of all available tests is better than no memory testing at all!
Depending on the size of memory to be tested and the other hardware involved, a single
test cycle may well take several hours.

Additional features can be activated/deactivated at startup of the memtest86+ image.
For more details see the `Operations section <https://memtest.org/readme#operation>`_
of the `Readme <https://memtest.org/readme>`_.


Memtest86+ download
^^^^^^^^^^^^^^^^^^^

The official website offers `bootable images and installers <https://www.memtest.org>`_.
There is also advice on how to install memtest86+ onto removable media in the FAQs of the
homepage.

.. _wiping_disks:

Wiping disks
------------

There are limited instances where Rockstors Web-UI may falter, or be confused by a pre-used disks format.
Rendering the capability to first wipe these disks via the Web-UI's :ref:`wipedisk` inaccessible.
On these rare occasions one can simply resource the linux command line tool "wipefs" to achieve the same.
Behind the scenes Rockstor's partition and/or disk wipe procedure executes a "wipefs -a dev-name-here".
Pre-used mdraid members may require additional mdraid configuration removal.

.. warning::
    As with all mass delete functions, be extremely certain that you are doing the right thing.
    This requirement has not now been reported for some time.
    So do first consider/research carefully if such a command line approach is in fact required.

.. note::
    Past instances of this command line approach to removing pre-use partitioning and formatting
    has been associated with prior mdraid use and some LVM configurations.
    Neither of which are supported by Rockstor's Web-UI.

.. _nwipe:

ShredOS/nwipe
^^^^^^^^^^^^^

`ShredOS <https://github.com/PartialVolume/shredos.x86_64>`_
is an Open Source tool to securely erase HDDs prior to their deployment or disposal. It is very
similar to the popular (Darik's Boot and Nuke) tool based on `dwipe`. Unfortunately, DBAN
has not really been updated since 2015. ShredOS is based on a fork of `dwipe`, which created
the `nwipe` functionality which is available in various Linux distributions.
In brief, this tool writes to every part of a disks surface to exercise the entire storage.
Akin to :ref:`memory_test` this will stress the tested parts of the system;
in this case the drives selected for wiping.

ShredOS/nwipe purpose
^^^^^^^^^^^^^^^^^^^^^

1. Securely remove all data on a per drive basis.
2. Test the drive/s ability to write to all its available sectors,

It is often the case that a drive is 'unaware' of an issue with itself,
via the built in SMART system, until an attempts is made to write to a faulty sector.
Writes can trigger a drives own built-in ability to swap-in spare/redundant sectors.
These spare sectors are a very limited resource, and should not be relied upon.

Note that the *Fill with Zeros* option is probably sufficient for testing purposes.
There are however many more exotic and official wiping algorithms available.
All options will take a considerable amount of time to complete,
i.e. in the region of a few hours per drive minimum.

It is **not** strongly recommended that drives be ShredOS tested prior to using them for Rockstor.
But this tool can be a valuable resource, especially if a drive's hardware is suspect.
Keep in mind however that this test procedure will stress the drive concerned,
and likely its associated cooling.

ShredOS/nwipe cautionary note
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. warning::
    The ShredOS/nwipe program / procedure will **Irreversibly Erase/Overwrite all data**.
    Use with extreme caution.
    Be sure to disconnect all drives that you wish not to be affected before booting/running ShredOS/nwipe.

.. note::
    Due to the comparatively limited write cycles of earlier generation SSDs
    further wear consideration should be given prior to running ShredOS/nwipe on these devices.

.. _installer_checksum:

Check integrity of downloaded Rockstor installer
------------------------------------------------

.. note::
    It is highly recommended that you check your downloaded installer's integrity.
    If the original download is corrupt then all else that follows is likely to have problems.

ISO is computer-slang/short for ISO9660 which is the
`International Organization for Standardization <https://www.iso.org/home.html>`_
official definition of the structure of data on a CD/DVD.
If this structure is wrong, or the data contained within is corrupt, then problems will follow.
The same is true for our non ISO type installers.

The `Rockstor Downloads <https://rockstor.com/dls.html>`_ page has image specific instruction
on how to check each type of installer offered via a single simple linux/OSX command line instruction.
The test is a checksum validation; made against a tiny matching additional download ending in "sha256".

A checksum is a mathematical abstraction of a data set, in this case our file,
that is unique (near enough anyway).
As a result it is possible to establish file corruption by comparing the published checksum
with that calculated directly from the downloaded file.
This in effect verifies the integrity of the downloaded file and confirms it as free from corruption.
