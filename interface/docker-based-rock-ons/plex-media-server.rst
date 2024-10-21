.. _plex_rockon:

Plex Server Rock-on
===================

Please be aware of the common prerequisites for all Rockstor
:ref:`rockons_intro`; specifically the :ref:`rockons_preinstall` and
:ref:`rockons_root` requirement.

The `Plex Media Server Rock-on forum <https://forum.rockstor.com/t/plex-media-server-rock-on/179>`_ area.

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
on nearly every platform. But in order to manage media with the
Plex system it is first necessary to have a **Plex Media Server**. This **Rock-on** is
**exactly that**; and aims to make the install and media provisioning of a Plex server as simple as possible.

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
are linked to at the :ref:`top <plex_rockon>` of this document. The Plex Rock-on 
requires a share for the media it is going to manage and a share to store its configuration
files.

.. note::
    Plex optionally offers the configuration to use hardware-based transcoding capabilities. This Rock-on supports
    Intel's Quick Sync capabilities. To determine whether the (Intel) CPU used in the Rockstor installation
    supports Quick Sync, refer to `Intel's Product Specifications <https://ark.intel.com/>`_
    If this is desired, another share needs to be created for temporary storage while transcoding takes place.
    The transcoding share should be housed on the fastest Pool or disk that is managed by Rockstor to minimize
    performance bottlenecks.
    Alternatively, using the command line can be used to determine whether Quick Sync is available
    (essentially by checking for the Kernel module **i915**)
    being used. Using the command below

.. code:: bash

    lsmod | grep i915


should return some results containing **i915** indicating that the system/CPU supports Quick Sync transcoding.


This makes a total of up to 3 shares to split the Plex config, data, and
optional transcoding working area. As with every Rockon, the shares should be created prior
to starting the installation.


.. note::
    It is also recommended that this Rock-on be run by a dedicated user and that
    the above shares be owned by that user. This Rockon allows for selecting a non-root user.
    The following :ref:`plex_shares` section and the later :ref:`plex_uidgidver` section detail the relevant
    aspects. If there is not already a *non-admin non-root* user under which
    Plex could be run, consider first creating for example a **plex** user (and group). See
    :ref:`users` section for instructions.

.. image:: /images/interface/docker-based-rock-ons/plex_install.png
   :width: 100%
   :align: center

Click the **Install** button next to the Plex listing on the Rock-ons page.

.. _plex_shares:

Plex Shares
^^^^^^^^^^^

Next, select the **Storage areas** for the Plex Rock-on's **data** and
**configuration** files.

Some general size recommendations:

* **Config Storage**: should be a minimum 20 GB for larger libraries
* **Data Storage**: enough space for data and snapshots - minimum 100GB


.. note::
    Additional information for each field can be found by hovering the mouse over the *i* icons.

.. image:: /images/interface/docker-based-rock-ons/plex_shares.png
   :width: 100%
   :align: center

.. note::
    To create these Shares or 'Storage areas' please see :ref:`createshare`.


The following image illustrates an example *Access Control* setting for the
*plex-data* share; the *plex-config* and *plex-transcode* can be configured
similarly.

.. image:: /images/interface/docker-based-rock-ons/plex_share_owner.png
   :width: 100%
   :align: center


.. note::
    Note that the plex user does not exist by default but can easily be created
    by following the :ref:`users` part of the documentation.
    **Please take a note of the created user's UID and GID** as they will be
    required in a later step.

By visiting the **System - Users** page one can see the **UID** and **GID** of
any user.

.. image:: /images/interface/docker-based-rock-ons/plex_user_info.png
   :width: 100%
   :align: center

In the above example one can see our created **plex** user has UID and GID of 1001.
Depending on whether other users and groups have been have created previously, a new *plex* user
may have a different UID and GID.

.. _plex_port:

Plex Port
^^^^^^^^^

This is the **Default Port** and it is unlikely that you will have to alter it.

* **WebUI port** - This is the port you will use to access the :ref:`plex_ui`.

.. image:: /images/interface/docker-based-rock-ons/plex_ports.png
   :width: 100%
   :align: center

The default port *32400* is automatically populated, but can be changed.

.. _plex_quicksync:

Enable transcoding with Quick Sync
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As mentioned above, CPU based transcoding can be enabled in this Rock-on. If not needed, or
not possible because the CPU does not have the Quick Sync feature, the field should be
left blank and the **Next** button can be selected.
If planning on using the transcoding feature, the Quick Sync device needs to be added. This is 
done by typing

.. code:: bash

    /dev/dri

into the field. Then proceed to the next screen.

.. _plex_uidgidver:

Plex Version, User and Group
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In this section one selects the version of Plex to be used, as well as the **UID (User ID)** and
the **GID (Group ID)** under which the Plex server will run.

.. note::
    The **UID** and **GID** must be the same as the user/group who owns the shares configured
    in the :ref:`plex_shares` section above.


* **VERSION**: e.g., **latest** for the newest version or a specific version if so desired.
* **UID**: User ID (number) to run Plex as.
* **GID** Group ID (number) to run Plex as.


.. image:: /images/interface/docker-based-rock-ons/plex_uid_gid_version.png
   :width: 100%
   :align: center


The next screen is a summary view of all parameters entered in the previous steps.

.. image:: /images/interface/docker-based-rock-ons/plex_verify.png
   :width: 100%
   :align: center

Check that the entered details are correct before selecting **Submit**.

Closing the resulting simple *Installation is in progress* dialog and we the installation progress is shown:

.. image:: /images/interface/docker-based-rock-ons/plex_installing.png
   :width: 100%
   :align: center

and a few minutes later depending on internet and machine speed:

**The Plex Media Server Rock-on is ON**

.. image:: /images/interface/docker-based-rock-ons/plex_on.png
   :width: 100%
   :align: center

.. note::
    Notice the **Plex UI** button to visit the installed Plex Web interface
    and the **spanner** icon to view the Rock-on settings and add additional
    Rockstor Shares.

.. _plex_transcoding:

Add Transcoding Share
^^^^^^^^^^^^^^^^^^^^^
If CPU-based transcoding was configured :ref:`plex_quicksync`, then the transcoding share
created earlier needs to be mapped into the Rockon, so Plex can see and use it.
Adding another share requires the Rockon to be turned off (but not uninstalled).
Select the spanner icon that shows the configuration information in a pop-up, then select **Add Storage**.

Select the *transcode* share created earlier and populate the *Rock-on directory* with
`/transcode` to complete the mapping. Then select the **Next** button.

.. image:: /images/interface/docker-based-rock-ons/plex_add_transcode.png
   :width: 100%
   :align: center

Now the additional share is visible in the configuration data set:

.. image:: /images/interface/docker-based-rock-ons/plex_transcode_summary.png
   :width: 100%
   :align: center

If satisfied with the settings, select **Next** and then **Submit**. This will add the new share and start the
Plex Rock-on.

See the Plex support article on 
`using Hardware-Accelerated Streaming <https://support.plex.tv/articles/115002178853-using-hardware-accelerated-streaming/>`_.

.. _plex_addshares:

Adding Other Shares to Plex
---------------------------
It is also possible to configure additional media shares for the Plex Rock-on to access. For example: if all movies reside in one
share and all recorded TV Shows in another one. However, it is not uncommon for all of a Plex Media Server's data to reside on a single share.

.. note::
    Shares are **not** the same as the libraries within Plex, i.e., there can be multiple
    Plex libraries on a single Rockstor Share by using different directories within that Share.
    The Libraries are configured from within the :ref:`plex_ui` and represent how the Plex Server
    organizes and shares the media.

When configuring a Plex Library one can either choose an existing directory or configure a non-existing one, all
from within Plex itself. 

From the information dialog **i icon** on the Plex Rock-on listing:

.. image:: /images/interface/docker-based-rock-ons/plex_add_storage.png
   :width: 100%
   :align: center


The **settings wizard** is accessed via the **spanner** icon on the Plex
entry on the Rock-ons page.

.. image:: /images/interface/docker-based-rock-ons/plex_spanner.png
   :width: 70%
   :align: center

As can be seen here, there is an **Add Storage** button on the spanner dialog.

.. _plex_ui:

Plex UI
-------
.. warning::
    These instructions follow the screen flow at the time this document was updated. Future Plex releases might change
    that installation procedure again.


On first accessing the Plex UI via the **Plex UI** button on the Rock-ons page
Plex requires to sign into an existing plex account:

.. image:: /images/interface/docker-based-rock-ons/plex_login.png
   :width: 90%
   :align: center

.. note::
    Please see `Sign in to Your Plex Account <https://support.plex.tv/articles/200878643-sign-in-to-your-plex-account/>`_
    for details.

.. warning::
    However, if no account is handy, the login can be skipped by selecting the **What's this?** link.

.. image:: /images/interface/docker-based-rock-ons/plex_whats_this.png
   :width: 90%
   :align: center

.. warning::
   In the subsequent screen there is the option to skip first and accept limited functionality.

.. image:: /images/interface/docker-based-rock-ons/plex_skip_login.png
   :width: 90%
   :align: center

After an information screen is displayed (which one can cancel out of or move on), the first setup screen is displayed for
the server setup.

.. image:: /images/interface/docker-based-rock-ons/plex_server_setup.png
   :width: 90%
   :align: center

After setting the plex server name and decide whether to allow access from outside (this can be changed in detailed configuration later)
the installation routine provides the option to add a library:

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library.png
   :width: 90%
   :align: center

Selecting the type of media in this library is important as it defines how Plex
will process and present the files found therein.

- **Movies**: These files will be treated as commercial films and will be subject to meta data lookups.
- **TV Shows**: Same as movies with regards to lookups but are expected to be multi-part.
- **Music**: These files have meta data lookup executed as well as local analysis (linux only).
- **Photos**: Treated as not having publicly available meta data.
- **Home Videos**: Treated as not having publicly available meta data.

.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_type.png
   :width: 90%
   :align: center


On selecting Movies the default name **Movies** and a language option is shown.


.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_movies.png
   :width: 90%
   :align: center


Once the Name has been confirmed a directory can be selected.


.. note::
    As mentioned before, plex libraries can consist of multiple directories or folders as they
    reference them:


.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_folders.png
   :width: 90%
   :align: center


From the previous summary screen or via the **Plex Settings** panel opened via
the **spanner icon** the *plex-data* share was mapped to the **data** directory. 
As there are no other mapped shares or sub directories, the *data* directory is directly selected
in this example.


.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_data.png
   :width: 90%
   :align: center


However, if it is already known what sub directory will be used (even if it has not been created yet, one could
for example add **Movies** to the end of the selection. Make sure to create this Directory when uploading your Movies.


.. image:: /images/interface/docker-based-rock-ons/plex_ss_add_library_data_movies.png
   :width: 90%
   :align: center

More plex libraries of various types and their associated directories can be
setup. Once that's done, the basic setup is complete and Plex branches to the Dasboard.

.. note::
    To add movies to the library from an external system, simply export the plex-data share using the Rockstor UI
    (Samba or nfs) in order to be able to upload directly into the Plex Media Server over the local network from any
    machine. The :ref:`shares` section contains links to methods by which this can be accomplished.
    The most common and compatible is probably the :ref:`samba_export` protocol.

More detailed Media server configuration can be found on the Plex website and the links mentioned above.


Now the Plex Media Server Rock-on should be ready to present films and music for streaming;
:ref:`plex_doc`
