
Product FAQ
===========

What is Rockstor?
-----------------

RockStor is a **free and open source NAS(Network Attached Storage)
solution**. It's a software solution and can be installed on any hardware or a
virtual machine satisfying :ref:`minsysreqs`

How can I share files using Rockstor?
-------------------------------------

Rockstor works as a centralized file storage server and supports popular
protocols like Samba/CIFS, NFS and SFTP. Linux, Apple and Windows clients can
store and access files from your Rockstor box.

How is Rockstor different from other software NAS products?
-----------------------------------------------------------

Just like other NAS products, Rockstor supports file storage via popular
protocols(NFS, Samba/CIFS, SFTP). With the exception of that broad similarity,
there are many differences. Rockstor runs on Linux kernel and uses BTRFS as the
underlying filesystem. It makes storage management easy with smart features and
a powerful UI. It exposes a RESTful API to be used as a high performance
storage backend in Cloud infrastructure. These are just a few differences. Give
Rockstor a try and you'll notice the value and differentiation right away.

How is Rockstor different from Dropbox, Google Drive and other Cloud Storage offerings?
---------------------------------------------------------------------------------------

For home/small-office users Rockstor works as personal cloud storage and
unlike public cloud storage services, all of your data resides on your
appliance. In other words, you have complete control and ownership of your data
and you can store lots of it at very low cost. We are working towards
compatibility and interoperability with some Cloud Storage solutions. We have
plans to make Rockstor compatible and interoperable with popular public cloud
storage offerings.

Does Rockstor provide Block or Object storage?
----------------------------------------------

Not currently. But since Rockstor is open source, anyone in our community can
work with us to get new features added in the future.

How much does Rockstor cost?
----------------------------

Zero USD. You can use the product in it's entirety for free of cost and explore
`Free Support <http://rockstor.com/free_support.html>`_ options. `Commercial
support <http://rockstor.com/commercial_support.html>`_ is also
available. Additionally, you can hire us if you need custom integration with
Rockstor.


How can I get started with Rockstor?
------------------------------------

Installation of Rockstor is a very easy and short process. You can even install
it on a spare server or check it out on AWS cloud. See :ref:`quickstartguide` to
get started.

What kind of hardware do I need to install Rockstor?
----------------------------------------------------

Rockstor runs on 64-bit commodity hardware. You can run it as a virtual
machine, or install it on bare metal. See :ref:`quickstartguide` for more
information.


What is a quick way to evaluate Rockstor?
-----------------------------------------

For quick evaluation, install Rockstor on Virtual Box, VMWare or try it out on
Amazon EC2. See :ref:`quickeval` for more information.


Do you have any hardware recommendations?
-----------------------------------------

For home or small business use, we've seen Rockstor install flawlessly on
HP, DELL and supermicro servers and desktops. The developers of Rockstor
use HP Micro servers for individual use.

Rockstor also installs smoothly on latest generation servers from vendors like
HP and Supermicro.


I have Rockstor installed. How do I get software updates?
---------------------------------------------------------

Rockstor development happens at a reasonably fast pace. However, we are aware
that your data is important and that you don't like to lose it. So, we create
and test staging releases more frequently, but production/public updates are
made available once a month or so. Rockstor should be updated directly from the
web-ui when it indicates that an update is available. It's a simple,
non-disruptive process and takes couple of mouse clicks and a few minutes.

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

BTRFS all the way! Though there's lot more to Rockstor than the filesystem, at
the core Rockstor productizes neat features of BTRFS filesystem.

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
Rockstor without any unnecessary disruption.

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


Can I use Rockstor with other Storage products?
-----------------------------------------------

This question is a bit ambiguous. All that Rockstor needs in terms of storage
resources is a set of disk drives. These drives can be physical, virtual,
direct attached or can come from SAN. So you can surely let SAN products
provide volumes for Rockstor.

Rockstor also comes with a backup plugin, making it a suitable backup target to
replicate data from other NAS products.

Can Rockstor support my specific storage usecase?
---------------------------------------------------

You can `contact us <http://rockstor.com/feedback.html>`_ with your requirements
and we will get in touch with you. We do storage services and support
and are happy to enable you to use Rockstor for your storage requirements.


How can I stay in touch with latest Rockstor news?
--------------------------------------------------

You can follow the `rockstor-core project
<https://github.com/rockstor/rockstor-core>`_ on github, join the `mailing list <https://lists.sourceforge.net/lists/listinfo/rockstor-announce>`_,
and follow us on `twitter <https://twitter.com/rockstorinc>`_.

How is Rockstor development funded?
-----------------------------------

Until recently, there was no external funding for Rockstor. We bootstrapped it
for over a year. Currently, our own funding is augmented with customer revenue.

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
