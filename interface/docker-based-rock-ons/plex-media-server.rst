.. _plex_rockon:

Plex Server Rock-on
===================

Please be aware of the common prerequisites for all Rockstor
:ref:`rockons_intro`; specifically the :ref:`rockons_preinstall` and
:ref:`rockons_root` requirement.

Our `Plex Media Server Rock-on forum <https://forum.rockstor.com/t/plex-media-server-rock-on/179>`_ area.

.. _plex_whatis:

What is Plex
------------

`Plex <https://www.plex.tv/>`_ is a
`centralized <https://support.plex.tv/articles/200288286-what-is-plex/>`_
domestic media distribution system that acts
both as a `DLNA <https://en.wikipedia.org/wiki/Digital_Living_Network_Alliance>`_
server and as its own more `flexible <https://www.plex.tv/>`_ type of
media server and client system.
`Plex client apps <https://www.plex.tv/media-server-downloads/>`_ are available
on
nearly
every platform.  But in order to manage your media with the
Plex system it is first necessary to have a
**Plex Media Server**. This **Rock-on** is **exactly that**; and aims to make
the install and media provisioning of a Plex server as simple as possible.

.. _plex_doc:

Plex Documentation
------------------

Plex's `own documentation <https://support.plex.tv/articles/>`_ is extensive and
well presented and a good kicking off point might well be their `Getting
Started <https://support.plex.tv/articles/200288286-what-is-plex/>`_ guide
that has a thorough
`Step by Step <https://support.plex.tv/articles/200264746-quick-start-step-by-step-guides/>`_
introductions to the Plex system.  Also note that the Plex Media Server
requires your media to be
`organized <https://support.plex.tv/articles/naming-and-organizing-your-movie-media-files/>`_
in a certain way.


.. _plex_install:

Installing Plex Rock-on
-----------------------
First please consider the pre-requisites for any Rockstor Rock-on; these
are linked to at the :ref:`top <plex_rockon>` of this document. Note also
that the Plex Rock-on will require a Share for your media and optionally
(but recommended) another two more Shares, one to store its configuration files
and one used internally as a temporary working during transcoding.
This makes a total of 4 shares, one for the Rock-on system itself ie
:ref:`rockons_root` that may well already have been made and an additional 1 to
3 shares depending on whether you wish to split your Plex config, data, and
transcoding working area. It is highly recommended that all 3 Plex Rock-on
shares be created as their use and size varies greatly and will help to
simplify upgrades and maintenance in the future; as well as helping to open up
further possibilities for performance tuning, ie ssd for transcoding Share and
varying scrub or de-fragmentation task schedules.

It is also recommended that this Rock-on be run by a dedicated user and that
the above shares be owned by that user. The following :ref:`plex_shares`
section and the later :ref:`plex_uidgidver` section detail the relevant
aspects. If you do not already have a *non-admin non-root* user under which
you would like to run Plex then please first create a **plex** user, see our
:ref:`users` section for instructions.

.. image:: /images/interface/docker-based-rock-ons/plex_install.png
   :width: 100%
   :align: center

Click the **Install** button next to the Plex listing on the Rock-ons page.

.. _plex_shares:

Plex Shares
^^^^^^^^^^^

Next we select the **Storage areas** for the Plex Rock-on's **data** and
**configuration** files. Note that the order of these items may vary.

Please note that it is best practice to have all these shares owned by a
non-admin non-root user ie *plex*.

* **Config Storage** - minimum 20 GB
* **Data Storage** - room enough for your data and snapshots - minimum 100GB

If you find that these values are insufficient then please discus this on the
`Rockstor forum <https://forum.rockstor.com/t/plex-media-server-rock-on/179>`_
so that this document might be updated and improved.

In the following image we are using the **recommended names** for all the
pre-configured shares, the suggested names are provided by the mouse over
*i* icons.

.. image:: /images/interface/docker-based-rock-ons/plex_shares.png
   :width: 100%
   :align: center

N.B. to create these Shares or 'Storage areas' please see our
:ref:`createshare`.

The following image illustrates an example *Access Control* setting for the
*plex-data* share; the *plex-config* and *plex-transcode* can be configured
similarly.

.. image:: /images/interface/docker-based-rock-ons/plex_share_owner.png
   :width: 100%
   :align: center

Note that the plex user does not exist by default but can be created easily
by following the :ref:`users` part of our documentation.
**Please take a note of the created user's UID and GID** as they will be
required in a later step.

By visiting the **System - Users** page one can see the **UID** and **GID** of
any user.

.. image:: /images/interface/docker-based-rock-ons/plex_user_info.png
   :width: 100%
   :align: center

In the above example we see our created **plex** user has UID and GID of 1001,
if you have previously created any other users then your *plex* user may have a
different UID and GID.

.. _plex_port:

Plex Port
^^^^^^^^^

This is the **Default Port** and it is unlikely that you will have to alter it.

* **WebUI port** - This is the port you will use to access the :ref:`plex_ui`.

.. image:: /images/interface/docker-based-rock-ons/plex_port.png
   :width: 100%
   :align: center

In the above we see the default port number is automatically entered.

.. _plex_uidgidver:

Plex User, Group, and Version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In this section we select the **UID (User ID)** and the **GID (Group ID)**
under which the Plex server will run. Note that these must be the same as the
user who owns the shares configured in the :ref:`plex_shares` section above.
We also get a chance to stipulate the version of Plex we want to use.

* **VERSION** ie **latest** for latest version or a specific version if
  desired.
* **UID** User ID (number) to run Plex as.
* **GID** Group ID (number) to run Plex as.

Note the order of these options may change.

.. image:: /images/interface/docker-based-rock-ons/plex_uid_gid_version.png
   :width: 100%
   :align: center

The next screen is to confirm the details entered so far.

.. image:: /images/interface/docker-based-rock-ons/plex_verify.png
   :width: 100%
   :align: center

Now check that the entered details are correct before clicking **Submit**.

Closing the resulting simple *Installation is in progress* dialog and we have:-

.. image:: /images/interface/docker-based-rock-ons/plex_installing.png
   :width: 100%
   :align: center

and a few minutes later depending on internet and machine speed:-

**The Plex Media Server Rock-on is ON**

.. image:: /images/interface/docker-based-rock-ons/plex_on.png
   :width: 100%
   :align: center

N.B. Notice the **Plex UI** button to visit the installed Plex Web interface
and the **spanner** icon to view the Rock-on settings and add additional
Rockstor Shares.

.. _plex_addshares:

Adding Shares to Plex
---------------------
This facility is only required if you wish to have the Plex Rock-on access more
than one Rockstor Share.  However it is not uncommon for all of a Plex Media
Server's data to reside on a single Share.  N.B. the Shares are not the same as
the Libraries within Plex, ie one can have multiple Plex libraries on a single
Rockstor Share by using different directories within that Share. Plex Libraries
are configured from within the :ref:`plex_ui` and represent how the Plex Server
organizes and shares your media. When configuring a Plex Library one can either
choose and existing directory or configure a non-existing one, all from within
Plex itself. An example of requiring more than one Rockstor Share to
be mapped into the Plex Rock-on is if you already have all your Movies in one
Share and all you Music in another Share, or wish for this to be the case.

From the information dialog **i icon** on the Plex Rock-on listing we get:-

.. image:: /images/interface/docker-based-rock-ons/plex_info.png
   :width: 100%
   :align: center

Reproduced here for clarity:-

**Additional information about Plex Rock-on**::

   Adding more media to Plex.

   You can add more Shares (with media) to Plex from the settings wizard of
   this Rock-on. Then, from Plex WebUI, you can update and re-index your library.

The **settings wizard** is accessed via the **spanner** icon on the Plex
entry on the Rock-ons page.

.. image:: /images/interface/docker-based-rock-ons/plex_spanner.png
   :width: 100%
   :align: center

As can be seen here there is an **Add Storage** button on the spanner dialog.

.. _plex_ui:

Plex UI
-------
On first accessing the Plex UI via the **Plex UI** button on the Rock-ons page
you should be greeted with a **Plex Terms of Service** screen:

.. image:: /images/interface/docker-based-rock-ons/plex_tos.png
   :width: 100%
   :align: center

It is required that you *AGREE* in order to proceed with the server setup.

Once you have agreed to the Plex Terms of Service you should be presented with
the following screen which give you a chance to name this server. This defaults
to the Rockstor's host name.

.. image:: /images/interface/docker-based-rock-ons/plex_server_setup.png
   :width: 100%
   :align: center

After setting the plex name we are given an option to add a library:

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library.png
   :width: 100%
   :align: center

Selecting the type of media in this library is important as it defines how Plex
will process and present the files found there in.

* **Movies** These files will be treated as commercial films and will be
  subject to meta data lookups.
* **TV Shows** Same as movies with regard to lookups but are expected to be
  multi part.
* **Music** Again these files have meta data lookup executed as well as local
  analysis (linux only).
* **Photos** Treated as not having publicly available meta data.
* **Home Videos** Again treated as not having meta data available on the
  internet so no lookups.

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_type.png
   :width: 100%
   :align: center

On selecting Movies we are presented with a default name **Movies** and a
language option.

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_movies.png
   :width: 100%
   :align: center

Once the Name has been confirmed we have the option to setup our directory
options. Plex Libraries can consist of multiple directories or folders as they
reference them:

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_folders.png
   :width: 100%
   :align: center

From the previous summary screen or via the **Plex Settings** panel opened via
the **spanner icon** we have that our *plex-data* share was mapped to the
**data** directory. Which we now select as there is as yet no other sub
directories created or other shares mapped within our Plex Rock-on.

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_data.png
   :width: 100%
   :align: center

In this case we have chosen to add **Movies** to the end of our selection

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_data_movies.png
   :width: 100%
   :align: center

More plex libraries of various types and their associated directories can be
setup and when done we are presented with the following options:

.. image:: /images/interface/docker-based-rock-ons/plex_ss_outside_stream.png
   :width: 100%
   :align: center

As in this example our Library directories are empty, so is our Plex Dashboard.

.. image:: /images/interface/docker-based-rock-ons/plex_dashboard.png
   :width: 100%
   :align: center

If you wish to register this server with an existing Plex account, please see
the settings - server section within the Plex WebUI. This will enables the
various remote and sync features co-ordinated by the Plex backend service.
The facilities available will vary according to your Plex web account status.
If you do not already have a Plex account you can create one from within the
PlexUI.

Please see `Sign in to Your Plex Account
<https://support.plex.tv/articles/200878643-sign-in-to-your-plex-account/>`_
for details.

**Sign In** (with an existing Plex account) or **Sign Up** to remotely
administer, sync, or share your various libraries, all co-ordinated via this
Plex Web ID.

Remember that our **Movies** library is expecting a directory called
**Movies**. Make sure to create this Directory when uploading your Movies.
Simply Export the plex-data share by your chosen means in order to be able to
upload directly into your Plex Media Server over your local lan from any
machine. The :ref:`shares` section contains links to methods by which this can
be accomplished. The most common and compatible of these being via the
:ref:`samba` protocol.

You can now configure and populate your Plex Media Server Rock-on;
:ref:`plex_doc`
