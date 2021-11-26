
Product FAQ
===========


What is Rockstor?
-----------------

Rockstor is a **free and open source NAS (Network Attached Storage) operating
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

Rockstor runs on 64-bit commodity hardware, both x86_64 and ARM64 (i.e. Pi4).
You can install it on bare metal or a hypervisor. See :ref:`quickstartguide` for more information.

Can I run Rockstor from a USB flash drive?
------------------------------------------

Yes.
Rockstor is optimized to do less writes if it detects the system drive to be non-rotational.
*Older USB 2.0 ports and devices are not recommended.*
So **we recommend USB 3.0 devices** even if your motherboard doesn't support USB 3.0.
Ideally use the combination of a new fast USB 3.0 device **in a USB 3.0 port**.
See :ref:`minsysreqs` subsection :ref:`usbwarning` for more context and better options.

Are there faster alternatives to running from USB?
--------------------------------------------------

Yes.
SATA or pci-e attached devices are generally a far better option;
with non-rotational media such as SSD via for example mSATA or m.2 preferred.

How much does Rockstor cost?
----------------------------

Little to nothing, depending on how you choose to receive Rockstor package updates.
You can install Rockstor using our x86_64 and ARM64 installers free of cost.
These installers include the last major stable version, or the latest stable Release Candidates.
Depending on if the testing channel has been recently restarted or is in Release Candidate state.
The Testing channel is free, but access to the Stable channel interim updates requires a small subscription fee.
Stable channel interim updates are limited to small "hot fixes" to existing features only.

See :ref:`update_channels` for more information.

**N.B. There are no feature difference between the channels bar those in pre-stable status.**


How can I share files using Rockstor?
-------------------------------------

Rockstor supports popular file sharing protocols like Samba/CIFS, NFS, and
SFTP. See :ref:`services` & :ref:`filesharing` for details on how to setup and
configure these. Linux, Apple, and Windows clients can easily share files using
Rockstor (see :ref:`accessshares`). Rockstor also supports apps like OwnCloud,
Nextcloud, Syncthing, Seafile, and others in the form of :ref:`rockons_intro`
that provide more advanced and/or easier ways to share and access your files.


Do you have any hardware recommendations?
-----------------------------------------

For home or small business use, we've seen Rockstor install flawlessly on
HP, DELL and Supermicro servers and desktops. The developers of Rockstor
have used HP Micro servers and Pi4's for personal use.

Rockstor also installs easily on the latest generation of servers from
vendors like HP and Supermicro and more recently Traverse Technologies' Ten64 platform.

For hobby and small home installs the Pi4 / RPi400 are also supported.

See the `downloads page <https://rockstor.com/dls.html>`_ for both x86_64 and ARM64 installers.


I have Rockstor installed. How do I get software updates?
---------------------------------------------------------

Rockstor can be updated directly from the Web-UI when it indicates that an
update is available. It's a simple, non-disruptive process and takes only a
couple of mouse clicks. Note however that you must select an
:ref:`Update Channel <update_channels>` before you will receive any 'rockstor'
package updates. All upstream OS updates are offered by default.


How frequent are the software updates?
--------------------------------------

Rockstor development depends on the number of contributors and Stable Channel subscribers.
Testing channel releases are always more frequent.
See the :ref:`Update Channel <update_channels>` documentation for more information.

Why is Rockstor updated so frequently?
--------------------------------------

While we make major releases that require complete OS re-installs, i.e. such as
when moving from Rockstor 3 to 4, we try to make these releases as infrequent
as possible. Generally we push small tested updates as often as we can, and
base our Stable Updates channel releases on the field testing carried out by
our community in the Testing Channel.

.. _faq_license:

How is Rockstor licensed?
-------------------------

Rockstor is free software licenced under the terms of GNU General Public
License version 2. See `here <https://www.gnu.org/licenses>`_ for more details.


What Linux flavor is Rockstor based on?
---------------------------------------

Rockstor 4 is "Built on openSUSE" and resembles most closely the upstream JeOS
variants.
Our `rockstor-installer <https://github.com/rockstor/rockstor-installer>`_ uses
openSUSE's own `kiwi-ng <https://github.com/OSInside/kiwi>`_ installer builder.
We host a bare minimum of re-branding apps on the
`Open Build Service <https://build.opensuse.org/project/subprojects/home:
rockstor>`_ (see also Overview) courtesy of openSUSE/SuSE/AMD. Otherwise we
favour openSUSE's own \*-branding-upstream options.


Our now legacy Rockstor 3.x was based on `CentOS 7 <https://www.centos.org/>`_.
We re-branded CentOS, added Rockstor software in the form of additional rpms and
changed the installer to make it a bit more straightforward and specific.


.. _faq_rockstor4_repos:

What Repositories does Rockstor 4 use?
--------------------------------------

Optional Rockstor package :ref:`Update Channel <update_channels>` selection exclusively adds one of either:

The :ref:`testing_channel` or :ref:`stable_channel` repositories.

The following repositories are included and enabled in :ref:`installer_howto`:

* `OSS <https://en.opensuse.org/Package_repositories#OSS>`_ (open source software only)

* `Update <https://en.opensuse.org/Package_repositories#Update>`_ (security and bugfix updates for OSS packages)

Aliased as per the installer profile: e.g. "Leap_15_3" & "Leap_15_3_Updates" respectively.

**Leap 15.2 profiles** have the following additional repositories:-

* `shells <https://build.opensuse.org/project/show/shells>`_
  An OBS repo for shellinabox - used by our Web-UI shell function.

* `home_rockstor_branches_Base_System <https://build.opensuse.org/project/subprojects/home:rockstor>`_
  Rockstor's OBS repo for branding packages.

We are required to de/re-brand packages that have no
"...branding-upstream" equivalent". See: `Making_an_openSUSE_based_distribution
<https://en.opensuse.org/Archive:Making_an_openSUSE_based_distribution>`_


**Leap 15.3 profiles** and newer - shells is replaced with Rockstor's OBS
home_rockstor; there was no Leap 15.3 ARM64 shellinabox package available otherwise:-

* `home_rockstor <https://build.opensuse.org/project/show/home:rockstor>`_
  Multi-arch Shellinabox with no changes from upstream:

* `home_rockstor_branches_Base_System <https://build.opensuse.org/project/subprojects/home:rockstor>`_
  As for Leap 15.2 Profiles.

The following are new in upstream openSUSE Leap 15.3: see
`Upstream release notes <https://doc.opensuse.org/release-notes/x86_64/openSUSE/Leap/15.3/#installation-new-update-repos>`_
They are included but no persisted by our installer build process.
However they are identical to those added by a regular openSUSE Leap 15.3 update.
And so are also auto included in the resulting install.

* `repo-backports-update <http://download.opensuse.org/update/leap/15.3/backports/>`_
  Update repository of openSUSE Backports

* `repo-sle-update <http://download.opensuse.org/update/leap/15.3/sle/>`_
  Update repository with updates from SUSE Linux Enterprise 15

Debug-info counterparts "repo-backports-debug-update" & "repo-sle-debug-update" are also added but are not enabled.
These are not used during the installer build.

What Filesystems are supported by Rockstor?
-------------------------------------------

BTRFS all the way! Though there's a lot more to Rockstor than the filesystem,
at the core Rockstor productizes neat features of the BTRFS.


How do I prevent data loss with Rockstor?
-----------------------------------------

This is a very important question and a lot of our work with Rockstor revolves
around minimizing data loss. There are a few measures you can take to prevent
dataloss and have disaster recovery strategy for different possibilities. See
:ref:`dataloss`. Also note that the btrfs raid5/6 profiles are not currently
recommended for production use.


Does Rockstor provide Block or Object storage?
----------------------------------------------

While Rockstor does not currently offer native object storage, it is possible
to leverage one of our :ref:`rockons_intro`, `MinIO <https://min.io>`_,
which provides high-performance object storage. See our :ref:`minio_rockon`
write-up for additional details.

In addition, since Rockstor is open source, anyone in our community can work
with us to get new features added in the future.


Does Rockstor support plugins?
-----------------------------------

Yes. Rockstor has a built-in engine that supports Docker based
applications. See :ref:`rockons_intro`.


What is the current list of supported Rock-ons?
-----------------------------------------------

For the current list see :ref:`rockons_available`. Note that new ones are added
regularly and can be requested on the `Forum <https://forum.rockstor.com>`_.


How do I backup to Rockstor using Apple Time Machine?
-----------------------------------------------------

Samba exports can be used for Time Machine backups as of Rockstor-3.9.2-56, as
a replacement for the now-deprecated AFP exports. The following forum post can
be of interest for instructions on how to create a compatible Samba export:
`Time Machine backups with Rockstor <https://forum.rockstor
.com/t/3-9-2-stable-channel-changelog/5741/22>`_.


Do you have examples on how to build complete NAS solutions for different storage capacities?
---------------------------------------------------------------------------------------------

Rockstor is hardware agnostic, so you can build a complete Linux, BTRFS-powered
NAS solution using the Rockstor NAS OS and hardware of your choice. The only
requirement is that the system be of a 64bit Intel or compatible architecture.
Don't hesitate to visit our `Forum <https://forum.rockstor.com>`_ to find user
stories, example builds, or ask for advice from our community!


I run a small organization with 10TB and growing data needs. How can Rockstor help me?
--------------------------------------------------------------------------------------

With Rockstor, you can scale your infrastructure with low incremental cost to
support your growing data needs. You can have very large storage capacity,
limited only by system resources like CPU, RAM etc. Feel free to `contact us
<https://rockstor.com/about-us.html#contact>`_ with your questions.


Can I run a small home personal cloud using Rockstor?
-----------------------------------------------------

Yes. Rockstor can be installed on many small computers like ASUS VivoPC or
Intel NUC. We recommend visiting our `Forum <https://forum.rockstor.com>`_ for
user stories, examples builds, and request advice or recommendation from the
community.


Can Rockstor support my specific storage use case?
--------------------------------------------------

You can `contact us <https://rockstor.com/about-us.html#contact>`_ with your
requirements and we will get in touch with you. We do storage services and
support and are happy to enable you to use Rockstor for your storage
requirements.


Is the BTRFS filesystem reliable?
---------------------------------

BTRFS is a newer Linux filesystem and is under heavy development. Some
commercial Linux distribution vendors are supporting it to various levels and
others will follow very soon given that the stability has improved quite a
bit. So for now, you have to answer that question yourself based on data and
your risk. In our experience, BTRFS has become very reliable. Also, Rockstor
confines users from using BTRFS more freely, thus reducing the chances of
hitting deep intricate bugs. The fact that BTRFS bugs being reported lately are
only triggered by very special scenarios is an encouraging sign.

However a proviso here is that The BTRFS community consensus is that **raid5
and raid6** levels of btrfs support are not yet fully stable and so are ***not
recommended for production use***. Please see the `btrfs wiki
<https://btrfs.wiki.kernel.org/index.php/Main_Page>`_ for up to date
information on all btrfs matters.



Why does Rockstor support only BTRFS and not other Linux filesystems?
---------------------------------------------------------------------

BTRFS is in it's own league among Linux filesystems and we see tremendous value
in building over it and making it's advanced feature set easily accessible to
users. While there are other excellent filesystems, we plan to focus on
providing the best solution based on BTRFS.


How can I stay in touch with the latest Rockstor news?
------------------------------------------------------

We recommend you join our `community forum <https://forum.rockstor.com>`_,
follow the `rockstor-core project <https://github.com/rockstor/rockstor-core>`_
on github, and follow us on `twitter <https://twitter.com/rockstorinc>`_.


How can I contribute to Rockstor?
---------------------------------

Thanks for asking and welcome to the Rockstor community. Depending on your
needs and interests, there are a few ways to participate. See
:ref:`contributetorockstor` for more details. Don't feel shy and email any of
the developers if you like to discuss more before jumping in!


How can I report bugs and request features?
-------------------------------------------

You can create issues or add comments to existing ones on our `github issue
tracker <https://github.com/rockstor/rockstor-core>`_. The `forum
<https://forum.rockstor.com>`_ is also a good place to start.
