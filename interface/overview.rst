.. _rockons_intro:

Rock-ons (Docker Plugins)
=========================

**Rock-ons** are Rockstor's name for its use of `docker <https://www.docker.com/>`_ containers.
Providing a **Plugin System** to easily and freely expand the functions of a base Rockstor install.

Each Rock-on aims to provide a single additional service,
with the list of :ref:`rockons_available` expanding all the time.

.. note::
    We are striving to provide Rock-ons as multi-architecture apps,
    namely for :code:`amd64` (Intel/AMD CPUs) and :code:`arm64` (ARM-based) devices.
    This is not always possible, however the supported architectures are
    usually noted in the Rock-on description in the WebUI.

.. _rockons_preinstall:

Initial Rock-ons Setup
----------------------

As Rock-ons/docker containers are like mini linux installs, they require
somewhere to live. In Rockstor it is recommended that you setup a Share
specifically for this purpose.

.. warning::
    It is recommended to **not** use the system disk to store Rock-ons and their
    configurations on. Storing Rock-ons on the system disk will make Rock-on
    restores more difficult. See :ref:`rockonrestore` for more information.

.. note::
    All Rock-ons will then be installed into this shared area but each
    will remain independent and during the setup of each Rock-on you are given
    the option to store their respective configuration and data in other shares.
    This is good practice as it keeps your Rock-on config and data apart from
    the Rock-ons themselves. You do not have to separate the config and data
    within each rock-on but that is also good practice, and is why this option
    is offered.

It is assumed that :ref:`pools` and one or more shares in those pools
(see our :ref:`createshare`) have already been created, appropriate for the
Rock-on requirements, e.g. a *plex-media* share and a *plex-config* share.

As a one-time setup activity, it is also necessary to create
the :ref:`rockons_root` share.

.. _rockons_root:

The Rock-ons root
^^^^^^^^^^^^^^^^^
All Rock-ons require the **Rock-on service** to be enabled and prior to
enabling this service it must be configured. This is a simple matter of
configuring a sufficiently large share for the rock-ons to be installed into.

It is recommended to create a *dedicated* share to be used as the Rock-ons root.
While any share can be chosen as the Rock-ons root, it is **strongly** recommended
to create a share to be used **only** as the Rock-ons root to prevent any
conflict that may arise with a mixed-use share. The Rock-ons root share is
used by Docker to store permanent data such as images and container
layers. As a result, any conflict or alteration of these data that might result
from a mixed-use share has the potential to break the installed Rock-ons.
Note that the rock-ons root share can be part of any :ref:`pool<pools>`
and does not require the creation of a dedicated pool.

.. note::
    While it is possible to use the existing 'out of the box' home share
    this is **not recommended** for the reason described above. Similarly,
    while it is possible to create the rock-ons root share on the system pool,
    this is **not recommended** either.

As an example, the following shows a **Recommended Minimum 5 GB rock-ons-root**
share backed by a previously created pool named **rock-pool**.

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

Now **enable** the **Rock-on service** and proceed to the Rock-ons
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

During the configuration of Rock-ons, quite a few of them require the specification
of a User ID (UID) and/or a Group ID (GID). Aside from the various options using
the command line to determine existing UIDs and GIDs, the simplest way is to
take advantage of the User and/or Group management screens. Navigate to *System
--> Users* (or *Groups*, if necessary).

.. image:: /images/interface/docker-based-rock-ons/users_page.png
   :width: 100%
   :align: center

The two highlighted columns show the UID and GID. In the example above, the
user :code:`plex` has the UID 1001, as well as the GID 1001, which could then
be used to set up the Plex rock-on.

.. _adding_rockons:

Adding your own Rock-on
-----------------------

The `rockon-registry <https://github.com/rockstor/rockon-registry>`_ GIT repo contains all the :ref:`rockons_available` definition files.
Consider contributing, or asking your favourite project to contribute to this repository;
see :ref:`contributerockons` for more information.

.. note::
    You can also add to your available Rock-ons locally.
    Just place one or more appropriate JSON file/s in your local install's
    :code:`/opt/rockstor/rockons-metastore` directory.
    For full instructions and examples see the :ref:`addmyownrockon` section.
    Some projects prefer to host their own Rock-on definition files,
    taking advantage of this local only capability.
    An example is `Emby <https://emby.media>`_ with their official `Rock-on
    <https://github.com/MediaBrowser/Emby.Build/blob/master/rockstor-plugins/embyserver.json>`_
    definition file for the Emby server component.
    This same Emby Rock-on forms the basis of what we now include by default.

.. _rockons_available:

Available Rock-ons
------------------

See the Rock-ons page within the Rockstor Web-UI (*All* tab) for a full list.
Pressing the **Update** button on this page refreshes the list.
See also our GIT repository:
`rockon-registry <https://github.com/rockstor/rockon-registry>`_.

- **There are around 90 Rock-ons available**, mostly contributed by the community.

.. _rockons_without_writeups:

Rock-ons without guides
^^^^^^^^^^^^^^^^^^^^^^^

Currently the large majority of Rock-ons are without specific **Rock-on guides**,
but most Rock-on installs are fairly self explanatory.

- To contribute a **Rock-on guide** to the following section see our :ref:`contributedocs`.

.. _rockons_with_writeups:

Rock-ons with guides
^^^^^^^^^^^^^^^^^^^^

The following are specific **Rock-on guides**, where available.

.. toctree::
   :maxdepth: 2

   docker-based-rock-ons/adguard-home
   docker-based-rock-ons/bareos-backup-server
   docker-based-rock-ons/immich
   docker-based-rock-ons/jenkins
   docker-based-rock-ons/minio
   docker-based-rock-ons/nginx
   docker-based-rock-ons/netdata_official
   docker-based-rock-ons/openvpn-server
   docker-based-rock-ons/plex-media-server
   docker-based-rock-ons/rustfs
   docker-based-rock-ons/scrutiny
   docker-based-rock-ons/spoolman
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
(`docker documentation <https://docs.docker.com/engine/manage-resources/labels/>`_)
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
In the event the above uninstallation process of a Rock-on is not possible, a
script is provided to force the deletion of a Rock-on. While this tool has not
yet been integrated into Rockstor's :ref:`web-UI <webui>`, it can easily be
used from the command line as follows.
Running this script (as the 'root' user) without argument will detail its usage:

**Rockstor versions 4.5.4-0 and newer**

.. code-block:: console

    cd /opt/rockstor
    poetry run delete-rockon
    Delete metadata, containers and images of a Rock-on
        Usage: delete-rockon <rockon name>

**Older Rockstor versions**

.. code-block:: console

    /opt/rockstor/bin/delete-rockon
    Delete metadata, containers and images of a Rock-on
        Usage: /opt/rockstor/bin/delete-rockon <rockon name>

Note that the :code:`rockon name` refers to the name of the Rock-on as it is
displayed in the list of available Rock-ons in Rockstor's web-UI. As the
Rock-on name is case-sensitive, and can contain spaces, we recommend wrapping it in quotes.
For the Rock-on named *Emby server*, for instance, the commands would be:

.. code-block:: console

    cd /opt/rockstor
    poetry run delete-rockon "Emby server"

*This example is for newer Rockstor versions.*

.. _rockons_root_reset:

Reset the Rock-ons Root
-----------------------
In rare instances reported by users, issues during installation and operation 
of Rock-ons can be traced back to an inconsistent :ref:`rockons_root` share.
Symptoms are things like:

* The installation fails without a discernible
  error when checking the logs. Or error messages are logged indicating missing subvolumes
  or snapshots within the Rock-ons Root share and referencing docker containers.
* A deletion of the Rock-on using the command line as described in :ref:`rockons_force_delete`
  and a subsequent attempt to re-install it does not seem to work.
* The Rock-on fails to start when it worked in previous cases without any
  issues. However, this could also be related to a breaking update of
  the underlying image used for the Rock-on.
* The WebUI throws an error like this when uninstalling/reinstalling a
  Rock-on:

  * :code:`Unknown internal error doing a GET to /api/rockons?page...`.

The symptoms described above could point to some inconsistent docker layers stored in the Rock-ons root.
Often times this can be resolved using the command line with the following docker maintenance command:

.. code-block:: console

    docker system prune -a --volumes

In case that this does not yield any improvement in the Rockons' installation or startup behavior, 
the best resolution might be to reset the Rock-on root. This will effectively remove all underlying 
docker containers that have been previously installed.

To reset the Rock-ons root, follow the sequence below:

.. warning::

   While the configuration and data volumes associated with installed Rock-ons won't be affected, 
   any currently installed Rock-ons will have to be re-installed (even if they did not show any
   issues).

* If possible, note the settings of the still installed Rock-ons.

.. note::

    If, alternatively, using the :ref:`config_backup` option to back-up the 
    settings of installed Rock-ons, then you should follow the
    *recreate* Rock-ons root option described below.

* Uninstall all installed Rock-ons (likely requires the command line as described 
  in :ref:`rockons_force_delete`).

.. note::

   All shares that were used for any of the Rock-ons will not be affected by these process
   steps, so a later re-installation of an associated Rock-on should put the situation
   right back to where it was before the Rock-ons root reset process.

* Turn off the Rock-ons Service (either on the Rockons page directly, or via the 
  **System --> Services** web page).
* Following :ref:`rockons_root`, to either create a new Rock-ons root share with
  a different name, or delete and recreate the Rock-ons root share with its original name.

.. note::

  In the case of creating a new Rock-ons root share with a different name, adjust the Rock-ons
  Service setting by selecting the new share name from the dropdown. If the Rock-ons root
  share has been re-created with the same name, no change is necessary. Delete the old
  Rock-on root share to free up disk space.

* Restart the Rock-ons Service.
* Run an update on the list of available Rock-ons.

Now the Rock-ons root should be consistent, albeit empty, once again, and (re-)installation
of Rock-ons should work as before. Or, if the configuration backup was created
this could now be executed, which should skip all existing configuration elements
and only result in the re-installation of the previously installed Rock-ons.


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
    Although some of the applications inside Rock-ons have an "Update"
    in their own user interface, it is generally not functional due to the
    nature of Docker containers. It is therefore always recommended to follow
    the procedure described above to update a Rock-on.

    There are very few exceptions to this rule, however, so make sure to have a
    look at the "more info" window for each Rock-on (if present) for
    instructions!
