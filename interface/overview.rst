.. _rockons_intro:

Rock-ons (Docker Plugins)
=========================

**Rock-ons** are Rockstor's name for it's use of `docker
<https://www.docker.com/>`_ containers to provide a **Plugin System** to easily
expand the functions of a base Rockstor install. This feature is relatively new
to Rockstor but is proving to be quite popular and is under active development.

Each Rock-on aims to provide a single additional service and the list of
:ref:`rockons_available` is expanding all the time.

.. _rockons_preinstall:

Initial Rock-ons Setup
----------------------

As Rock-ons / docker containers are like mini linux installs they require
somewhere to live.  In Rockstor it is recommended that you setup a Share
specifically for this purpose.

Note that all Rock-ons will then be installed into this shared area but each
will remain independent and during the setup of each Rock-on you are given the
option to store their respective configuration and data in other shares. This
is good practice as it keeps your Rock-on config and data apart from the
Rock-ons themselves. You do not have to separate the config and data within
each rock-on but that is also good practice, and is why this option is offered.

It is assumed you have already setup your :ref:`pools` and one or more
shares in those pools (see our :ref:`createshare`) appropriate for your
Rock-ons, i.e. a plex-movies share and a plex-config share.

But we also need to create the :ref:`rockons_root` share.

.. _rockons_root:

The Rock-ons root
^^^^^^^^^^^^^^^^^
All Rock-ons require the **Rock-on service** to be enabled and prior to
enabling this service it must be configured. This is a simple matter of
configuring a sufficiently large share for the rock-ons to be installed into.
It is possible to use the existing 'out of the box' home share but this is not
recommended.

The following shows a **Recommended Minimum 5 GB rock-ons-root** share backed
by a previously created pool named **rock-pool**.

.. image:: /images/interface/docker-based-rock-ons/rockons_root_share.png
   :width: 100%
   :align: center

Note that during the lifetime of Rock-ons several snapshots will be created so
plan to be able to expand this share if need be.

Then click on the **spanner** next to the **Rock-on service** on the **System**
page.

.. image:: /images/interface/docker-based-rock-ons/small_services.png
   :width: 100%
   :align: center

Now to **select** the share to use for your **Rock-ons root**.

.. image:: /images/interface/docker-based-rock-ons/rockons_root_config.png
   :width: 100%
   :align: center

**Select** the **rock-on-root** share that we created earlier and **Submit**

You can now **enable** the **Rock-on service** and proceed to the Rock-ons
page.

.. image:: /images/interface/docker-based-rock-ons/rockons_page.png
   :width: 100%
   :align: center

If no Rock-ons are showing on the **All** tab then click the **Update** button
to refresh the list of available Rock-ons. To install a listed Rock-on use
its **Install** button on the Rock-ons WebUI page.

.. _rockons_user_group:

UID and GID usage in Rock-ons
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

During the configuration of Rock-ons, quite a few require the specification of
a User ID (UID) and/or a Group ID (GID). Aside from the various options using
the command line to determine existing UIDs and GIDs, the simplest way is to
take advantage of the User and/or Group management screens. Navigate to System
--> Users (or Groups if necessary).

.. image:: /images/interface/docker-based-rock-ons/users_page.png
   :width: 100%
   :align: center

The two highlighted columns show the UID and GID. In the example above, the
user :code:`plex` has the UID 1001, as well as the GID 1001, which could then
be used to set up the Plex rock-on.

.. _adding_rockons:

Adding your own Rock-on
-----------------------

The `rockon-registry <https://github.com/rockstor/rockon-registry>`_ contains
the current list of freely available rock-on definition files and servers
as the repository for :ref:`rockons_available`. Please consider contributing,
or asking your favourite project to contribute, a rock-on via a GitHub pull
request to this repository (see :ref:`contributerockons` for more
information). Note that it is also possible to add to the available Rock-ons
by placing a suitably configured and named json file in the
*/opt/rockstor/rockons-metastore* directory of your Rockstor install. For full
instructions and examples please see the rockon-registry
`README.md <https://github.com/rockstor/rockon-registry/blob/master/README.md>`_.
Some projects prefer to host their own Rock-on plugins and this feature enables
the use of other projects official Rock-ons. An example of a project that takes
advantage of this feature is `Emby <https://emby.media>`_ with their official
`Rock-on <https://github.com/MediaBrowser/Emby.Build/blob/master/rockstor-plugins/embyserver.json>`_
definition file for the Emby server component. However this same Emby Rock-on
has now been added to the official Rockstor Rock-on registry.

.. _rockons_available:

Rock-ons available by default
-----------------------------

As this list is continually growing the best place to view the currently
included by default Rock-ons is at the
`rockon-registry <https://github.com/rockstor/rockon-registry>`_ or on the
Rock-ons page *All* tab within the Rockstor WebUI directly after pressing the
**Update** button.

.. _rockons_without_writeups:

Rock-ons without write-ups
^^^^^^^^^^^^^^^^^^^^^^^^^^

Although the following Rock-ons are currently without specific install
instructions they are like all Rock-on installs, fairly self explanatory.

* `Bitcoin <https://bitcoin.com/>`_: Bitcoin full node
* `Bitwarden <https://github.com/dani-garcia/vaultwarden>`_: Unofficial server written in Rust for the password manager Bitwarden
* `Booksonic <https://booksonic.org>`_: Audiobooks streaming server
* `Cardigann <https://github.com/cardigann/cardigann>`_: A proxy server for adding new indexers to Sonarr and other media managers
* `Collabora online <https://www.collaboraoffice.com/code/>`_: LibreOffice-based online office suite
* `COPS <https://blog.slucas.fr/projects/calibre-opds-php-server/>`_: links to your Calibre library database and provides automation features
* `CouchPotato <https://couchpota.to/>`_: Downloader for usenet and bittorrent users
* `Crashplan <https://www.crashplan.com/en-us/>`_: Automatic cloud-based backups
* `Deluge <https://deluge-torrent.org/>`_: Deluge is a movie downloader for bittorrent users
* `Dropbox <https://www.dropbox.com>`_: Cloud-based file syncing solution
* `Duck DNS <https://www.duckdns.org>`_: Free dynamic DNS service
* `Duplicati 2.0 <https://www.duplicati.com>`_: Free backup software to store encrypted backups online
* `ecoDMS <https://www.ecodms.de/index.php/en/>`_: Electronic Document Managing System
* `Emby server <https://emby.media/>`_: Emby media server
* `Ghost <https://ghost.org/>`_: A publishing platform for professional bloggers
* `GitLab CE <https://about.gitlab.com/>`_: Git repository hosting and collaboration
* `Gogs <https://gogs.io/>`_: Go Git Service, a lightweight Git version control server and front end
* `Gollum <https://github.com/gollum/gollum>`_: Gollum is a simple wiki system built on top of Git
* `Haproxy <https://github.com/daniel-illi/docker-haproxy-letsencrypt/tree/rock-on>`_: Reliable, High Performance TCP/HTTP Load Balancer with letsencrypt integration
* `Headphones <https://github.com/rembo10/headphones>`_: Automated music downloader for NZB and Torrent
* `Home Assistant <https://www.home-assistant.io/>`_: Open-source home automation platform
* `HTTP to HTTPS redirect <https://github.com/geldim/docker-https-redirect>`_: Access the Rockstor web UI without having to remember to type "https:"
* `Jackett <https://github.com/Jackett/Jackett>`_: Proxy server for queries from apps such as Sonarr, CouchPotato, and Mylar
* `JDownloader 2 <https://jdownloader.org/>`_: Free, open-source download management tool
* `Koel <https://koel.dev/>`_: Simple web-based personal audio streaming service
* `Lazy Librarian <https://lazylibrarian.gitlab.io>`_: Automated ebook downloader for NZB and Torrent
* `Logitech Squeezebox <https://mysqueezebox.com/index/Home>`_: Server for Squeezebox Devices
* `MariaDB <https://mariadb.org/>`_: MariaDB, relational database management system
* `Medusa <https://pymedusa.com>`_: Automatic video library manager for TV shows
* `Minecraft <https://www.minecraft.net/en-us/>`_: Minecraft server
* `Muximux <https://github.com/mescon/Muximux>`_: Lightweight portal to view & manage your HTPC apps
* `Mylar <https://github.com/evilhero/mylar>`_: Automated Comic Book (cbr/cbz) downloader
* `Nextcloud <https://nextcloud.com/>`_: Next generation open source enterprise file sync and share
* `NZBGet <https://nzbget.net/>`_: The most efficient usenet downloader
* `NZBHydra <https://github.com/theotherp/nzbhydra>`_: Meta search for NZB indexers
* `Ombi <https://ombi.io/>`_: Host your own Plex Request and user management system
* `OwnCloud-Official <https://owncloud.com/>`_: Secure file sharing and hosting
* `Pi-hole <https://pi-hole.net/>`_: A black hole for Internet advertisements
* `PocketMine <https://www.pocketmine.net/>`_: Server software for Minecraft: Pocket Edition
* `Radarr <https://github.com/Radarr/Radarr>`_: Radarr is a PVR for Movies on Usenet and Torrents
* `Resilio Synch <https://www.resilio.com/>`_: Fast, private file sharing for teams and individuals
* `Rocket.Chat <https://rocket.chat/>`_: Open Source Chat Platform
* `SaBnzbd <https://sabnzbd.org/>`_: The best usenet downloader
* `Seafile <https://www.seafile.com/>`_: Secure file sharing and hosting
* `SmokePing <https://oss.oetiker.ch/smokeping/>`_: Network latency history monitor
* `Sonarr <https://sonarr.tv/>`_: (formerly NZBdrone) A PVR for usenet and bittorrent users
* `Subsonic <http://www.subsonic.org>`_: Music server
* `Tautulli <https://github.com/Tautulli/Tautulli>`_: Plex usage tracker
* `Teamspeak <https://teamspeak.com/en/>`_: VoIP software
* `TFTP server <https://github.com/jumanjihouse/docker-tftp-hpa>`_: TFTP server
* `Transmission with OpenVPN <https://haugene.github.io/docker-transmission-openvpn/>`_: Transmission torrent client with webUI while connecting to OpenVPN
* `Ubuiquiti Unifi by Linuxserver.io <https://ui.com/consoles//>`_: Unifi Access Point controller, provided by Linuxserver.io
* `Unifi Controller <https://ui.com/consoles/>`_: Unifi Access Point controller
* `uTorrent <https://github.com/domibarton/docker-utorrent>`_: BitTorrent client
* `Watchtower <https://github.com/containrrr/watchtower>`_: A process for automating Docker container base image updates
* `Xeoma <https://felenasoft.com/xeoma/en>`_: Video surveillance
* `Zabbix-XXL <https://github.com/monitoringartist/zabbix-xxl>`_: Network and application monitoring
* `ZeroNet <https://zeronet.io>`_: Decentralized websites using Bitcoin crypto and the BitTorrent network


.. _rockons_with_writeups:

Rock-ons with write-ups
^^^^^^^^^^^^^^^^^^^^^^^

Please see the following sections for some specific Rock-on install details.
Note that not all Rock-ons have their own specific instructions in these docs.

.. toctree::
   :maxdepth: 2

   docker-based-rock-ons/jenkins
   docker-based-rock-ons/minio
   docker-based-rock-ons/netdata_official
   docker-based-rock-ons/openvpn-server
   docker-based-rock-ons/owncloud
   docker-based-rock-ons/plex-media-server
   docker-based-rock-ons/scrutiny
   docker-based-rock-ons/syncthing
   docker-based-rock-ons/transmission-bittorrent
   docker-based-rock-ons/youtrack
   docker-based-rock-ons/zoneminder


.. _rockons_advanced_config:

Advanced Configuration
----------------------

While the installation and initial setup of Rock-ons is kept as simple and
user-friendly as possible, it is possible to further customize their
configuration post-install. At the time of writing, users can customize their
existing rock-on installation with additional storage, customized docker
container labels, alter ports, or connect and disconnect user-defined rocknets.
Note that this area is under active development to provide further
customization options.

.. _rockons_add_storage:

Add Storage
^^^^^^^^^^^
The **Add Storage** feature allows the binding of any Rockstor share to an
installed Rock-on. As any share can be added as storage to multiple Rock-ons,
this represents a convenient and easy way to make a set of files accessible to
multiple Rock-ons.

To start, make sure the Rock-on is turned OFF, and click on the little wrench
icon next to the ON / OFF toggle to display a summary of the Rock-on's
settings.

.. image:: /images/interface/docker-based-rock-ons/addstorage_wrench.png
   :width: 100%
   :align: center

This summary table displays, all volumes, ports, environment variables, labels,
and devices used by the Rock-on (if any). After a fresh Rock-on install, all
objects set during the install are reported here. In our example, the
*Syncthing* Rock-on has the Rockstor **shares** *syncthing_conf* and
*syncthing_sync* mapped to the ``/config`` and ``/home/syncthing/Sync`` paths
inside the Rock-on, respectively, exposes three different ports to the host,
and uses two environment variables (*PUID* and *GUID*).

.. image:: /images/interface/docker-based-rock-ons/addstorage_settings_summary.png
   :width: 100%
   :align: center

To **Add Storage** to this Rock-on, click the *Add Storage* button on the
bottom right corner. Note that this button will only be displayed if the
Rock-on supports this feature. In the following dialog window, select a
previously-created share (see our :ref:`createshare` section), and define the
path under which it will be seen from within the Rock-on.

.. image:: /images/interface/docker-based-rock-ons/addstorage_share_selection.png
   :align: left

In this example, the Rockstor **share** *test_share01* will be added as
``/opt/my_added_share01`` from within the Rock-on.

The next window summarizes the already-existing and new settings to be applied
(here: new share). If everything is correct, click "Next" and then "Submit" to
update the Rock-on settings with the newly-added storage. Internally, Rockstor
will first uninstall the Rock-on before re-installing it with the updated
settings summarized in the previous table.

.. image:: /images/interface/docker-based-rock-ons/addstorage_settings_verification.png
   :width: 100%
   :align: center



.. _rockons_add_labels:

Add Labels
^^^^^^^^^^
The **Add Labels** feature allows to apply customized *docker container labels*
(`docker documentation <https://docs.docker.com/config/labels-custom-metadata/>`_)
to any installed Rock-on. To add a new label within an existing Rock-on, make
sure the Rock-on is turned OFF, and click on the little wrench icon next to the
ON/OFF toggle to display a summary of the Rock-on's addlabels_settings_summary
(see :ref:`rockons_add_storage` for description of this table).

To add a label to a given Rock-on, click the **Add Label** button at the bottom
of the Rock-on settings summary page.

.. image:: /images/interface/docker-based-rock-ons/addlabels_settings_summary.png
   :width: 100%
   :align: center

Notably, as labels are applied at the *container* level, the next dialog will
allow you to select the container to which the label will be applied.
Conveniently, Rockstor will only list the containers included in the current
Rock-on. In the example below, the Rock-on includes two containers:
*helloworld1* and *helloworld2*.

.. image:: /images/interface/docker-based-rock-ons/addlabels_container_selection.png
   :align: center

To apply two different labels to the container *helloworld2*, simply add as
many label fields as needed, and type your labels.

.. image:: /images/interface/docker-based-rock-ons/addlabels_labels_selection.png
   :align: center

Click "Next" and verify your new label-to-container mapping(s) before finishing
the procedure by clicking "Next" and "Submit". Internally, Rockstor will first
un-install the Rock-on before re-installing it with the newly-defined labels.


.. _rockons_networking:

Networking
^^^^^^^^^^
Some elements of docker networking can be easily configured from Rockstor's
webUI for each rock-on. Any *container* of a given rock-on can thus be
connected to a **rocknet** (a user-defined docker network), and any published
port can be unpublished (and vice-versa). To customize these elements, make
sure the rock-on is turned OFF, and click on the little wrench icon next to the
ON/OFF toggle to display a summary of the rock-on's settings (see
:ref:`rockons_add_storage` for description of this table). Clicking on the
**Networking** button will present the following window:

.. image:: /images/interface/docker-based-rock-ons/networking_window.png
   :width: 100%
   :align: center

.. note::

   Please see :ref:`network_add_connection_docker` for how to create a rocknet.


.. _rockons_edit_ports:

Edit ports
""""""""""
The **Edit Ports** feature allows to alter the publication state of any port
mapped to the rock-on. By default, all ports defined during the rock-on
installation are published and thus available for communication. In some cases,
however, one may choose to unpublish a specific port, or re-publish a
previously unpublished port.

The top section of the **Networking** customization window lists all exposed
ports defined in the rock-on (if any) as well as their corresponding container,
description, port number on host, and port number mapped on the corresponding
container. Finally, a checkbox allows each port to be published (if checked) or
unpublished (if unchecked).

.. warning::
   **Important!** Unpublishing a port defined for the Rock-on's web-UI will
   make it inaccessible from Rockstor's Rock-ons page. For convenience, such
   ports are accompanied by a warning icon next to the checkbox.

Click *Next* and verify the new publication state for each port before
finishing the procedure by clicking *Next* and *Submit*. Internally, Rockstor
will first uninstall the rock-on before re-installing it with the new settings
(publishing only those ports set to be published).

.. _rockons_edit_rocknets:

Joining Rocknets
""""""""""""""""
The **Rocknets** section allows to connect and/or disconnect any container of a
given rock-on to a rocknet (see :ref:`network_add_connection_docker`). As each
rocknet is associated to a *container* rather than to a rock-on, Rockstor
offers the ability to connect/disconnect each container of a given rock-on to
one or more rocknets separately. As a result, one can for instance connect some
containers of one or more rock-ons to a backend rocknet, and others to a
frontend rocknet. In the example above, both containers of the rock-on are not
currently connected to any rocknet, so the lists are empty.

To **join** a currently existing rocknet, simply click on the search field and
select it from the drop-down list, or type its name. Note that it is possible
to directly create a new rocknet from this field by typing a new rocknet name
and pressing *Enter*. Upon submission and completion of the rock-on update
procedure, a new rocknet with the corresponding name will be created and
connected to the given container.

To disconnect a container from a rocknet, simply delete the rocknet's name or
click the "x" next to it.

.. warning::
   **Important!** Rocknets newly-defined directly from this page will be
   created using Docker's default parameters. If different settings are
   desired, please create the rocknet first from the *System* > *Network* menu,
   and then connect the container to it. Alternatively, it is also possible to
   edit an existing rocknet's settings from the *System* > *Network* menu.

.. image:: /images/interface/docker-based-rock-ons/rocknets_join.png
   :width: 100%
   :align: center

Once all rocknets are connected and/or disconnected to containers as desired,
click *Next* and verify the new settings are correct before finishing the
procedure by clicking *Next* and *Submit*. Internally, if rocknets are the only
modifications made to the rock-on, Rockstor will apply the new settings on the
fly without first uninstalling the rock-on. If a port's publication state was
also modified, however, Rockstor will proceed with the full update procedure
(uninstalling and re-installing the rock-on with the new settings).

.. _rockons_uninstall:

Uninstall of a Rock-on
----------------------
Uninstalling a Rock-on is straightforward:

1. Toggle the Rock-on OFF. The *Uninstall* button will appear.
2. Click the *Uninstall* button, and confirm the process in the dialog window.

This will remove the underlying Docker container(s) and related entries in
Rockstor's database. Note that this will **not** delete or alter data in the
Share(s) that were used for the uninstalled Rock-on. This therefore represents
a convenient way to update a Rock-on if desired
(:ref:`see below <rockons_update>`).

.. _rockons_force_delete:

Force uninstall of a Rock-on
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In the event the uninstallation process of a Rock-on is not possible, we
provide a script to force the deletion of a Rock-on. While we do not yet have
integrated this tool in Rockstor's :ref:`web-UI <webui>`, it can easily be
used from the command line as follows. Running this script without argument
will detail its usage:

.. code-block:: bash

    /opt/rockstor/bin/delete-rockon
    Delete metadata, containers and images of a Rock-on
    Usage: /opt/rockstor/bin/delete-rockon <rockon name>

Note that the :code:`rockon name` refers to the name of the Rock-on as it is
displayed in the list of available Rock-ons in Rockstor's web-UI. As the
Rock-on name is case-sensitive, we recommend wrapping it in quotes. For the
Rock-on named *Emby server*, for instance, the command should thus be:

.. code-block:: bash

    /opt/rockstor/bin/delete-rockon "Emby server"


.. _rockons_update:

Updating a Rock-on
------------------
Updating a Rock-on implies updating its underlying Docker image(s). Given
Docker images are designed to be ephemeral, updating a Rock-on can simply be
achieved by *pulling* the latest Docker image, *removing* the currently used
image, and then *re-creating* the container(s) using the newly-pulled image(s).
In Rockstor, this can all be achieved through the web-UI as follows:

1. Stop the Rock-on
2. Uninstall the Rock-on
3. Re-install the Rock-on using the same Shares and settings as before

Upon re-install, Docker will check if a newer version of the image exists and
download it if it does. The newly-installed Rock-on will thus use the
latest image available while keeping the same data *Shares*, ensuring the
latter will remain intact. If you re-used the same *Shares* for the Rock-on as
before its uninstallation, you should thus be back in the same state as before,
but with the latest Docker image available.

Note, however, that some Rock-ons use pinned versions for their underlying
image(s); these therefore cannot be updated. These include the *PostgreSQL 9.5*,
*PostgreSQL 10.6*, and *YouTrack official* Rock-ons.

.. note::
    Although some of the applications ran inside Rock-ons have an "Update"
    in their own user interface, it is generally not functional due to the
    nature of Docker containers. It is therefore always recommended to follow
    the procedure described above to update a Rock-on.

    There are very few exceptions to this rule, however, so make sure to have a
    look at the "more info" window for each Rock-on (if present) for
    instructions!
