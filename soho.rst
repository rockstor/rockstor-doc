
Small Office Fileserver with RockStor
=====================================

In a small office or home office like environment, a centralized storage server
is needed to store documents, photos, videos and other files including backups
and virtual machines and access them from other computers on the network. Here
are some simple but important uses of such server.

1. Backup data from workstations, laptops and other computers

2. Share data easily with other users and from any computer.

3. Create and orgnize a central repository of all data.

There are more complex usecases which are covered in their own separate documents.

RockStor can be setup as this centralized storage server, also called a
Fileserver or NAS following the steps described in this document.

.. _serverreqs:

Server requirements and suggestions
-------------------------------------

The first step in building a RockStor Fileserver is to procure hardware. Since
RockStor is Free software based on Linux, there is a lot of flexibility. You
can purchase hardware that fits your budget and performance requirements. See
:ref:`minsysreqs` for general guidance. As long as it meets these requirements,
you can easily convert an old PC into a powerful Fileserver with RockStor. You
can also purchase small office servers from various vendors.

In our community, RockStor is humming on different hardware. Here are some
examples:

**Disclaimer: RockStor is a software only product. We don't recommend or certify any particular hardware. These are mere suggestions based on deployments in our community**

* `HP Proliant Microserver <http://www8.hp.com/us/en/products/proliant-servers/product-detail.html?oid=5379860#!tab=features">`_ is chosen for its small form factor, 4 easily accessible hard drive slots, and eSata capability to expand storage. This is ideal for a simple setup with a small footprint that meets most file storage needs of a small or home office.

* `Dell Poweredge T300 <http://www.dell.com/us/dfb/p/poweredge-t300/pd>`_ is a powerful server tower with Intel Xeon processor that can have upto 24GB Memory and 4 hard drives. This model is officially discontinued by Dell and newer more powerful options are available in it's place.

* `IBM System x3400 <http://www-947.ibm.com/support/entry/portal/docdisplay?lndocid=migr-64905>`_ is a powerful server tower similar to the Dell mentioned above. It can have upto 32GB Memory and 8 hard drives.

Hard disk drives
----------------

Disk drives are critical in a fileserver. While RockStor offers slick
management and access to your data, all of it is ultimately stored inside the
Hard disk drives of the system. Most servers including the ones mentioned in
:ref:`serverreqs` are compatible with standard SATA HDDs. Once you choose the
right server based on your needs, choose appropriate HDDs for that server.

**Note about hardware raid**: RockStor provides BTRFS based software RAID
capabilities. However, advanced servers offer hardware RAID functionality
providing additional redundancy. Evaluate your risks and choose appropriately.


Pre-install checklist
---------------------


