
Product FAQ
===========


What is Rockstor?
-----------------

RockStor is a **free and open source NAS (Network Attached Storage) operating
system**. It's a software solution and can be installed on commodity hardware
or a hypervisor satisfying :ref:`minsysreqs`


What is a quick way to evaluate Rockstor?
-----------------------------------------

For quick evaluation, install Rockstor on Virtual Box, Virtual Machine Manager
or VMWare. See :ref:`quickeval` for more information.


How can I get started with Rockstor?
------------------------------------

Installation of Rockstor is a very easy and short process. See
:ref:`quickstartguide` to get started.

What kind of hardware do I need to install Rockstor?
----------------------------------------------------

Rockstor runs on 64-bit commodity hardware. You can install it on bare metal or
a hypervisor. See :ref:`quickstartguide` for more information.

Can I run Rockstor from a USB flash drive?
------------------------------------------

Yes. Rockstor is optimized to do less writes if it detects the root
drive to be USB flash drive or SSD. As expected, USB 2.0 can be pretty
slow. So we recommend a USB 3.0 drive even if your motherboard doesn't support
USB 3.0 as it'll still be faster. You can also purchase a 16 GB USB 3.0
drive from our `shop
<http://shop.rockstor.com/collections/diy-accessories/products/usb-stick>`_ and
support our effort!

Are the faster alternatives to running from USB?
------------------------------------------------

Yes. If your motherboard has a spare PCI-Express slot you can get a SSD boot
drive from our `shop <http://shop.rockstor.com/collections/diy-accessories/products/pcie-msata-boot-drive>`_.
This is a cheap yet much faster alternative. Here's a short
`blog post <http://rockstor.com/blog/diy-nas/ssd-boot-drive-for-diy-rockstor-systems>`_ with more information.

How much does Rockstor cost?
----------------------------

Zero USD. You can use the product in it's entirety free of charge and seek
support from `the community forum <http://forum.rockstor.com>`_. `Commercial
support <http://rockstor.com/commercial_support.html>`_ is also
available. Additionally, you can hire us if you need custom integration with
Rockstor.


How can I share files using Rockstor?
-------------------------------------

Rockstor supports popular file sharing protocols like Samba/CIFS, NFS, SFTP and
AFP. Linux, Apple and Windows clients can easily share files using
Rockstor. Rockstor also supports apps like OwnCloud, Syncthing and others in
the form of :ref:`rockons_intro` that provide more advanced and easier ways to
share and access your files.


Do you have any hardware recommendations?
-----------------------------------------

For home or small business use, we've seen Rockstor install flawlessly on
HP, DELL and Supermicro servers and desktops. The developers of Rockstor
use HP Micro servers for individual use.

Rockstor also installs smoothly on the latest generation of servers from vendors like
HP and Supermicro.


I have Rockstor installed. How do I get software updates?
---------------------------------------------------------

Rockstor should be updated directly from the web-ui when it indicates that an
update is available. It's a simple, non-disruptive process and takes only a
couple of mouse clicks and a few minutes.


How frequent are the software updates?
--------------------------------------

Rockstor development happens at a reasonably fast pace. We create test releases
almost every other day. Once we are satisfied with a batch of changes, we
release a stable update. This happens roughly once or twice a month.


Why is Rockstor updated so frequently?
--------------------------------------

While we make major releases that require complete OS install, we try to make
these releases as infrequent as possible. However, we constantly improve
Rockstor and push tested updates in small batches which can be updated online
right from the web-ui. We do this because we want our users to get the best of
Rockstor without any unnecessary disruption or delay.


How is Rockstor licensed?
-------------------------

Rockstor is free software licenced under the terms of GNU General Public
License version 2. See `here <http://www.gnu.org/licenses>`_ for more details.


What Linux flavor is rockstor based on?
---------------------------------------

Rockstor 3.x is based on `CentOS 7 <http://www.centos.org/>`_. We rebrand CentOS, add Rockstor software in
the form of additional rpms and change the installer to make it a bit more
straight forward and specific.


What Filesystems are supported by Rockstor?
-------------------------------------------

BTRFS all the way! Though there's a lot more to Rockstor than the filesystem, at
the core Rockstor productizes neat features of the BTRFS.


How do I prevent data loss with Rockstor?
-----------------------------------------

This is a very important question and a lot of our work with Rockstor revolves
around minimizing data loss. There are a few measures you can take to prevent
dataloss and have disaster recovery strategy for different possibilities. See
:ref:`dataloss`


Does Rockstor provide Block or Object storage?
----------------------------------------------

Not currently. But since Rockstor is open source, anyone in our community can
work with us to get new features added in the future.


Does Rockstor support plugins?
-----------------------------------

Yes. Rockstor has a built-in engine that supports Docker based
applications. See :ref:`rockons_intro`.


What is the current list of supported Rock-ons?
-----------------------------------------------

For the current list see :ref:`rockons_available`. Note that new ones are added
regularly and can be requested on the `Forum <http://forum.rockstor.com>`_.


How do I backup to Rockstor using Apple Time Machine?
-----------------------------------------------------

See `Time Machine backups with Rockstor
<http://rockstor.com/blog/uncategorized/time-machine-backups-with-rockstor/>`_
for details.


Do you have examples on how to build complete NAS solutions for different storage capacities?
---------------------------------------------------------------------------------------------

Rockstor is hardware agnostic, so you can build a complete Linux, BTRFS powered
NAS solution using Rockstor NAS OS and hardware of your choice. If you are a
home-user/prosumer, read `8TB DIY NAS using Rockstor
<http://rockstor.com/blog/uncategorized/8tb-rockstor-diy-nas/>`_. For bigger
storage footprint, read `240TB DIY NAS using Rockstor
<http://rockstor.com/blog/diy-nas/rockstor-on-45-drives-aka-the-rockinator/>`_
.


I run a small organization with 10TB and growing data needs. How can Rockstor help me?
--------------------------------------------------------------------------------------

With Rockstor, you can scale your infrastructure with low incremental cost to
support your growing data needs. You can have very large storage capacity,
limited only by system resources like CPU, RAM etc. Feel free to `contact us
<http://rockstor.com/about-us.html#contact>`_ with your questions.


Can I run a small home personal cloud using Rockstor?
-----------------------------------------------------

Yes. Rockstor can be installed on many small computeres like ASUS VivoPC or Intel
NUC. Here's a blog post describing `Rockstor on Intel NUC
<http://rockstor.com/blog/tutorials/rockstor-on-the-intel-nuc/>`_.


Can Rockstor support my specific storage use case?
--------------------------------------------------

You can `contact us <http://rockstor.com/about-us.html#contact>`_ with your requirements
and we will get in touch with you. We do storage services and support
and are happy to enable you to use Rockstor for your storage requirements.


Is BTRFS filesystem reliable?
-----------------------------

BTRFS is a newer Linux filesystem and is under heavy development. Some
commercial Linux distribution vendors are supporting it to various levels and
others will follow very soon given that the stability has improved quite a
bit. So for now, you have to answer that question yourself based on data and
your risk. In our experience, BTRFS has become very reliable. Also, Rockstor
confines users from using BTRFS more freely, thus reducing the chances of
hitting deep intricate bugs. The fact that BTRFS bugs being reported lately are
only triggered by very special scenarios is an encouraging sign.


Why does Rockstor support only BTRFS and not other Linux filesystems?
---------------------------------------------------------------------

BTRFS is in it's own league among Linux filesystems and we see tremendous value
in building over it and making it's advanced feature set easily accessible to
users. While there are other excellent filesystems, we plan to focus on
providing the best solution based on BTRFS.


How can I stay in touch with the latest Rockstor news?
------------------------------------------------------

We recommend you join our `community forum <http://forum.rockstor.com>`_,
follow the `rockstor-core project <https://github.com/rockstor/rockstor-core>`_
on github, and follow us on `twitter <https://twitter.com/rockstorinc>`_.


How can I contribute to Rockstor?
---------------------------------

Thanks for asking and welcome to the Rockstor community. Depending on your
needs and interests, there are a few ways to participate. See
:ref:`contributetorockstor` for more details. Don't feel shy and e-mail any of
the developers if you like to discuss more before jumping in!


How can I report bugs and request features?
-------------------------------------------

You can create issues or add comments to existing ones on our `github issue
tracker <https://github.com/rockstor/rockstor-core>`_. The `forum
<http://forum.rockstor.com>`_ is also a good place to start.
