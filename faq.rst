
Product FAQ
===========

What is Rockstor?
-----------------

Rockstor is a **free enterprise class file storage platform**. At the
foundation, it is a Fedora flavored Linux operating system tailored for
storage usecases. The primary supported usecase is NAS via protocols including
NFS, Samba/CIFS and SFTP. Rockstor brings together technologies including the
Linux kernel, BTRFS filesystem, SystemTap and our own free software stack to
deliver a compelling solution.

Does Rockstor provide Block or Object storage?
----------------------------------------------

Not currently. **File storage is the only supported usecase**. Block storage
support can be added and we shall consider it based on demand, but Object
storage is not on the idea board. However, Rockstor is Free Software and anyone
in the community is welcome to add these features.

How is Rockstor different from other software NAS products?
-----------------------------------------------------------

Just like other NAS products, Rockstor supports file storage via popular
protocols(NFS, Samba/CIFS, SFTP). With the exception of that broad similarity,
there are many differences. Rockstor runs on Linux kernel and uses BTRFS as the
underlying filesystem. It makes storage management easy with smart features and
a powerful UI. It exposes a RESTful API to be used as a high performance storage
backend in Cloud infrastructures. These are just a few differences. Give
Rockstor a try and you'll notice the value and differentiation right away.

How is Rockstor different from Dropbox, Google Drive and other Cloud Storage offerings?
---------------------------------------------------------------------------------------

Rockstor is your personal cloud storage and unlike public cloud storage
services, all of your data resides on your appliance. In other words, you have
complete control and ownership of your data and you can store lot's of it at
very low cost. We are working towards compatibility and interoperability with
some Cloud Storage solutions. However, Rockstor is not a simple replacement and
doesn't come with comparable user interfaces.

Who can download and use Rockstor?
----------------------------------

Anybody. Rockstor is an open source project with the primary goal of ensuring
free availability for anyone to use and providing value and quality to all of
it's users. A lot of effort goes into developing Rockstor and we'd love for it
to be widely used and distributed.

How much does Rockstor cost?
----------------------------

Zero USD. It is completely Free and Open Source and is here to stay that
way. You can use the product in it's entirety for free of cost and explore
`Free Support <http://rockstor.com/free_support.html>`_ options. `Commercial
support <http://rockstor.com/commercial_support.html>`_ is also available and
if you so choose, you can even hire us to build stuff with Rockstor.


How can I get started with Rockstor?
------------------------------------

Installation of Rockstor is a very easy and short process. You can even install
it on a old server or check it out on AWS cloud. See :ref:`quickstartguide` to
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

For individual or small business use, we've seen Rockstor install flawlessly on
HP, DELL and supermicro servers and desktops. The developers of Rockstor
use HP Micro servers for individual use.

Rockstor also installs smoothly on latest generation servers from vendors like
HP and Supermicro.


Is rockstor ready for production use?
-------------------------------------

While some features of Rockstor are ready for primetime, as a whole, it is
currently in Beta. However, the product has been downloaded by many and we have
direct knowledge of a handful of deployments. The developers of Rockstor use it
heavily and continue to test all layers of Rockstor software.

Who is using Rockstor?
----------------------

We see regular downloads, but it's hard to say who is actively using the
product as we don't collect that information. It is suitable for small and
midsize businesses, and of course for advanced individual users. We are
familiar with deployments storing up to 200 GB of data on Rockstor.

I have Rockstor installed. How do I get software updates?
---------------------------------------------------------

Rockstor development happens at a reasonably fast pace. However, we are aware
of criticality given that users store data and don't want to lose it. We create
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

Rockstor is based on Fedora 19. Our plan is to fully support Rockstor on latest
CentOS out of the box. However, that is not possible until a more recent Linux
kernel is supported on CentOS.


What Filesystems are supported by Rockstor?
-------------------------------------------

Rockstor only supports BTRFS filesystem. See `here
<https://btrfs.wiki.kernel.org/index.php/Main_Page>`_ for more details about
BTRFS, a rich and disruptive filesystem.

How do I protect data loss with Rockstor?
-----------------------------------------

Disk level redundancy is provided by builtin software raid of BTRFS including
raid1, raid10, raid5 and raid6. Beyond that, Rockstor also supports replication
of Shares across two or more Rockstor appliances. See :ref:`sharereplication`
for more details.

Can I use Rockstor with other Storage products?
-----------------------------------------------

This question is a bit ambiguous. All that Rockstor needs in terms of storage
resources is a set of disk drives. These drives can be physical, virtual,
direct attached or can come from SAN. So you can surely let SAN products
provide volumes for Rockstor.

Rockstor also comes with a backup plugin, making it a suitable backup target to
replicate data from other, perhaps expensive NAS products.

Can Rockstor support my specific storage usecase?
---------------------------------------------------

You can `contact us <http://rockstor.com/feedback.html>`_ with your requirements
and we will get in touch with you. We do storage services and support
and are happy to enable you to use Rockstor for your storage requirements.


How can I stay in touch with latest Rockstor news?
--------------------------------------------------

You can follow the `rockstor-core project
<https://github.com/rockstor/rockstor-core>`_ on github, join the `development
mailing list <https://lists.sourceforge.net/lists/listinfo/rockstor-devel>`_,
and follow us on `twitter <https://twitter.com/rockstorinc>`_.

How is Rockstor development funded?
-----------------------------------

Until recently, there was no external funding for Rockstor. We bootstrapped it
for over a year. Currently, our own funding is augmented with customer revenue.

How can I contribute to Rockstor?
---------------------------------

Thanks for asking and welcome to the Rockstor community. Depending on your needs and interests, there are a few ways to participate. See :ref:`contributetorockstor` for more details.

How can I report bugs and request features?
-------------------------------------------

Create a new issue on `github
<https://github.com/rockstor/rockstor-core>`_. You can also join the
`development mailing list
<https://lists.sourceforge.net/lists/listinfo/rockstor-devel>`_ and report bugs
and request features.
