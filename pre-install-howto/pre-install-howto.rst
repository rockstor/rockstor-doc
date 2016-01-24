.. _pre_install:

Pre-Install Best Practice (PBP)
===============================

Not really specific to Rockstor but noteworthy all the same :). This howto sets
out to establish **Best Practice** prior to a Rockstor install. It has grown out
of a number of suggestions on the Rockstor forum where problems have been
encountered that might otherwise have been avoided. The basic premise is to
first ensure that the hardware you are to install Rockstor on is fit for
purpose and tested reasonably with the readily available tools.

.. _memory_test:

Memory test
-----------

Built into the Rockstor installer (inherited from the upstream CentOS installer)
is the famous `memtest86+ <http://www.memtest.org/>`_ boot option. This program
is actually derived from the linux kernel itself, the core of the operating
system that Rockstor is built on.

.. _check_md5sum:

Check Integrity of Downloaded ISO File
--------------------------------------

If the original download is corrupt then all else that follows is likely to have
problems. ISO is computer slang short for ISO9660 and is the
`International Organization for Standardization
<http://www.iso.org/iso/home.html>`_ official definition of the structure of
data on a CD/DVD. If this structure is wrong or the data contained within it is
corrupt then problems are bound to follow. To avoid this there is a simple
command that can be executed once the download of the Rockstor iso file is
complete: that of checking it's checksum. A checksum is a mathematical
abstraction of a dataset, in this case our file, that is unique (near enough
anyway). As a result of this it is possible to establish file corruption by
comparing the published checksum of the official file with that calculated from
the downloaded file. This in effect verifies the downloaded file as legitimate /
free from corruption. Note however though that if you used the BitTorrent
download option to acquire your install image then this check has already been done by
way of the internal workings of the BitTorrent system. No harm in double
checking though. If however you acquired your image by any other means then it
is highly recommended that you check it's md5sum. In the following we assume you
have opened a terminal in the *Downloads* and that this is where you downloaded
the iso file.

.. _check_md5sum_linux:

On a Linux system
^^^^^^^^^^^^^^^^^

The following built-in command is how to get the md5sum of your downloaded file
and any linux system.

::

    md5sum ~/Downloads/Rockstor-3.8-11.iso

example output:

::

    fbb65344b31c7715807750e58e99f788  Rockstor-3.8-11.iso

.. _check_md5sum_osx:

On an OSX system
^^^^^^^^^^^^^^^^

Here we see the built-in command to use on an OSX system as used on modern Apple
computers.

::

    md5 ~/Downloads/Rockstor-3.8-11.iso

example output:

::

    MD5 (Rockstor-3.8-11.iso) = fbb65344b31c7715807750e58e99f788

.. _check_md5sum_win:

On an MS Windows system
^^^^^^^^^^^^^^^^^^^^^^^

Using the built-in tool available on MS Windows.

::

    CertUtil -hashfile %userprofile%\Downloads\Rockstor-3.8-11.iso MD5

example output:

::

    MD5 hash of file C:\Users\username\Downloads\Rockstor-3.8-11.iso:
    fb b6 53 44 b3 1c 77 15 80 77 50 e5 8e 99 f7 88
    CertUtil: -hashfile command completed successfully.

Checking the Install media
--------------------------

Once you have created the USB or in deed the CD / DVD by your chosen method
method