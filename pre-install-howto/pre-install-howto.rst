.. _pre_install:

Pre-Install Best Practice (PBP)
===============================

Not really specific to Rockstor but noteworthy all the same :). This howto sets
out to establish **Best Practice** prior to a Rockstor install. It has grown out
of a number of suggestions on the Rockstor forum where problems have been
encountered that might otherwise have been avoided. The basic premise is to
first ensure that the hardware you are to install Rockstor on is fit for
purpose and tested reasonably with the readily available tools.

Memory test
-----------

Built into the Rockstor installer (inherited from the upstream CentOS installer)
is the famous `memtest86+ <http://www.memtest.org/>`_ boot option. This program
is actually derived from the linux kernel itself, the core of the operating
system that Rockstor is built on.


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
the downloaded file. This in effect verifies the downloaded file as legit / free
from corruption. Note however though that if you used the BitTorrent option to
acquire your install image then this check has already been done by way of the
internal workings of the BitTorrent system. No harm in double checking though.

The following image shows how to get the md5sum of your downloaded file.

..  image:: md5sum_list.png
