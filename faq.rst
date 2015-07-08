
Product FAQ
===========


What is Rockstor?
-----------------

RockStor is a **free and open source NAS (Network Attached Storage)
operating system**. It's a software solution and can be installed on commodity hardware or a
hypervisor satisfying :ref:`minsysreqs`


How can I share files using Rockstor?
-------------------------------------

Rockstor supports popular file sharing protocols like Samba/CIFS, NFS, SFTP and
AFP. Linux, Apple and Windows clients can easily share files using
Rockstor. Rockstor also supports apps like OwnCloud, Syncthing and others that
provide more advanced and easier ways to share and access your files.


How much does Rockstor cost?
----------------------------

Zero USD. You can use the product in it's entirety free of charge and seek
support from `community forum. <http://forum.rockstor.com>`_
options. `Commercial support <http://rockstor.com/commercial_support.html>`_ is
also available. Additionally, you can hire us if you need custom integration
with Rockstor.


How can I get started with Rockstor?
------------------------------------

Installation of Rockstor is a very easy and short process. You can even install
it on a spare server. See :ref:`quickstartguide` to get started.


What kind of hardware do I need to install Rockstor?
----------------------------------------------------

Rockstor runs on 64-bit commodity hardware. You can install it on bare metal or
a hypervisor. See :ref:`quickstartguide` for more information.


What is a quick way to evaluate Rockstor?
-----------------------------------------

For quick evaluation, install Rockstor on Virtual Box, Virtual Machine Manager
or VMWare. See :ref:`quickeval` for more information.


Do you have any hardware recommendations?
-----------------------------------------

For home or small business use, we've seen Rockstor install flawlessly on
HP, DELL and Supermicro servers and desktops. The developers of Rockstor
use HP Micro servers for individual use.

Rockstor also installs smoothly on the latest generation of servers from vendors like
HP and Supermicro.


I have Rockstor installed. How do I get software updates?
---------------------------------------------------------

Rockstor development happens at a reasonably fast pace. However, we are aware
that your data is important and that you don't like to lose it. So, we create
and test staging releases more frequently, but production/public updates are
made available once a month or so. Rockstor should be updated directly from the
web-ui when it indicates that an update is available. It's a simple,
non-disruptive process and takes only a couple of mouse clicks and a few minutes.


How is Rockstor licensed?
-------------------------

Rockstor is free software licenced under the terms of GNU General Public
License version 2. See `here <http://www.gnu.org/licenses>`_ for more details.


What Linux flavor is rockstor based on?
---------------------------------------

Rockstor 3.x is based on CentOS 7. We rebrand CentOS, add Rockstor software in
the form of additional rpms and change the installer to make it a bit more
straight forward and specific.


What Filesystems are supported by Rockstor?
-------------------------------------------

BTRFS all the way! Though there's a lot more to Rockstor than the filesystem, at
the core Rockstor productizes neat features of the BTRFS filesystem.


How do I prevent data loss with Rockstor?
-----------------------------------------

This is a very important question and a lot of our work with Rockstor revolves
around minimizing data loss. There are a few measures you can take to prevent
dataloss and have disaster recovery strategy for different possibilities. See
:ref:`dataloss`


How frequently is Rockstor updated?
-----------------------------------

We make a major release requiring a OS reinstall ONLY when necessary. Almost
all updates are pushed online and we like to push small batches at a regular
frequency. Depending on the update, it could be once a week or once a month. We
almost never wait too long to push updates unless there is a compelling reason
to do so.


Why is Rockstor updated so frequently?
--------------------------------------

While we make major releases that require complete OS install, we try to make
these releases as infrequent as possible. However, we constantly improve
Rockstor and push tested updates in small batches which can be updated online
right from the web-ui. We do this because we want our users to get the best of
Rockstor without any unnecessary disruption or delay.


Does Rockstor provide Block or Object storage?
----------------------------------------------

Not currently. But since Rockstor is open source, anyone in our community can
work with us to get new features added in the future.


What plugins does Rockstor support?
-----------------------------------

Rockstor has a built-in engine that supports Docker based applications called
Rock-ons. For a complete list see :ref:`rockons_available`


How do I backup to Rockstor using Apple Time Machine?
-----------------------------------------------------

Please refer to this blog post on instructions for backup to Apple Time Machine. See `here <http://rockstor.com/blog/uncategorized/time-machine-backups-with-rockstor/>`_ for details.


Do you have examples on how to build complete NAS solutions for different storage capacities?
---------------------------------------------------------------------------------------------

Rockstor is hardware agnostic, so you can build a complete Linux, BTRFS powered NAS solution
using Rockstor NAS OS and hardware of your choice. If you are a home-user/prosumer, read `8TB DIY NAS using Rockstor <http://rockstor.com/blog/uncategorized/8tb-rockstor-diy-nas/>`_. For bigger storage footprint, read `240TB DIY NAS using Rockstor <http://rockstor.com/blog/diy-nas/rockstor-on-45-drives-aka-the-rockinator/>`_ .


I run a small organization with 10TB and growing data needs. How can Rockstor help me?
-----------------------------------------------------------------------------------------------

With Rockstor, you can scale your infrastructure with low incremental cost to support your growing
data needs. You can have very large storage capacity, limited only by system resources like CPU, RAM etc.


How do I build a small home personal cloud using Rockstor?
-----------------------------------------------

Rockstor can be installed on many small computeres like ASUS xyz and Intel NUC. Please refer to this blog post on instructions on building a personal cloud using Rockstor and Intel NUC. See `here <http://rockstor.com/blog/tutorials/rockstor-on-the-intel-nuc/>`_ for details.


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
hitting deep intricate bugs. The fact that bugs being reported lately are
only triggered by very special scenarios is an encouraging sign.


Why does Rockstor support only BTRFS and not other Linux filesystems?
---------------------------------------------------------------------

Rockstor intends to focus its development efforts only on BTRFS filesystem and
not any other filesystem.  While we understand that BTRFS, especially RAID5/6 are
not yet considered enterprise ready, we believe that it is a matter of time before BTRFS
matures and becomes enterprise ready and the default filesystem for Fedora, eventually
replacing EXT4 and XFS.


How can I stay in touch with the latest Rockstor news?
------------------------------------------------------

We recommend you join the community forum, follow the `rockstor-core project
<https://github.com/rockstor/rockstor-core>`_ on github, and follow us on `twitter <https://twitter.com/rockstorinc>`_.


How can I contribute to Rockstor?
---------------------------------

Thanks for asking and welcome to the Rockstor community. Depending on your
needs and interests, there are a few ways to participate. See
:ref:`contributetorockstor` for more details.


How can I report bugs and request features?
-------------------------------------------

Create a new issue on `github
<https://github.com/rockstor/rockstor-core>`_. You can also join the
`development mailing list
<https://lists.sourceforge.net/lists/listinfo/rockstor-devel>`_ and report bugs
and request features.

-------------------------------------------
