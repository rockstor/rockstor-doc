.. _immich_rockon:

Immich Rock-on
==========================

Before you install the Immich rock-on, you should understand the
prerequisites and configurations common to all Rockstor :ref:`rockons_intro`;
specifically the :ref:`rockons_preinstall` and :ref:`rockons_root`
requirements.


.. _immich_whatis:

What is Immich
---------------

`Immich <https://immich.app/>`_ is a free and open-source, self-hosted photo and 
video management solution. It allows you to easily back up, organize, and manage 
your personal media on your own server, ensuring that your privacy and data ownership 
are preserved. With Immich, you can upload photos and videos directly from your 
mobile devices, browse and search them with advanced tagging and metadata support, 
and view them in a modern, responsive interface. Immich also supports features 
such as automatic backup, multi-user accounts, EXIF data extraction, reverse geocoding, 
and AI-powered object detection and classification.
For further details and the most up-to-date description of Immich, please visit the 
`project's documentation <https://docs.immich.app/overview/quick-start/>`_.  

.. _immich_req:

System Requirements
---------------------

A system with at least 4GB of RAM and 2 CPU cores. 

Recommended is a system with at least 6GB of RAM and 4 CPU cores. 

Real world usage data for Immich v2.2.3: 
for ~70k photos/videos, up to 4GB (8GB peak) of RAM is normally being used. 
CPU usage is mostly negligible, but it will shoot up when new files are ingested.

This can be controlled via the administration settings. See: :ref:`immich_other_settings`.

You can read about requirements 
`in more detail <https://docs.immich.app/install/requirements/>`_.

.. _immich_install:

Installing the Immich rock-on
------------------------------
The Immich Rock-on requires 3 
`shares to be created <https://rockstor.com/docs/interface/storage/shares-btrfs-subvolumes.html#creating-a-share>`_
before the installation can begin:

- Library share: used by Immich to store uploaded photos/videos,
- Database share,
- Cache share: used by Immich's machine-learning functionality

We are now ready to start the installation of the Immich rock-on. 

#. Click the *Install* button next to the **Immich** listing on the *Rock-ons* page.
#. In the first step, please select the 3 shares that you created previously.
#. Click **Next**.
#. Set the port used to reach Immich's WebUI.
#. Click **Next**.                       
#. Set environment variables.
    - **Log level**: Input the desired log level. You will want to use **log** for normal operations. Other available values: verbose, debug, warn, error.
    - **Ignore error checks**: Input whether you want to skip mount error checks. You will want to use **false**, unless you have `issues with your Immich instance <https://docs.immich.app/administration/system-integrity>`_.
#. Click **Next**.
#. Verify the information you've provided is correct, then click **Submit**.
#. You'll see a screen indicating the Rock-on is being installed. Click *Close*.
#. Click on the **Immich UI** button to open the web configuration and complete 
   the Immich-specific set-up. (See: :ref:`immich_setup`)

                                   
.. _immich_mounting_external_library:

Mounting External Libraries
---------------------------

In case you already have a share full of existing photos and videos, you probably 
want to import them into Immich. 
You can `read more about them <https://docs.immich.app/features/libraries>`_.
                                   
.. warning:: 
    Mounting an external library of photos/videos via the Web-UI will give Immich 
    write-access by default. This also means you will be able to delete files via Immich.

    If you want to restrict Immich to read-only-access, you will need to modify the 
    `Rock-on <https://github.com/rockstor/rockon-registry/blob/master/immich.json>`_
    and insert your share via a bind-mount Docker command, including the :code:`:ro` postfix.
                                   
1. To make the share available to Immich, you will need to first stop the running Immich instance.
2. Now click on the small wrench icon right next to the red **OFF** button, and click on the **Add Storage** button.

.. image:: /images/interface/docker-based-rock-ons/immich_add_external_library.png
   :width: 70%
   :align: center
                                   
3. **Storage**: select the share that contains your existing photos/videos.
4. **Rock-on directory**: input a path under which your share will be available in the Immich instance.
5. Click **Next**.
6. If everything looks fine on the summary configuration page, then click on **Next** again, and then **Submit**.
7. After the Immich will be up-and-running again, go into your admin **External Libraries** configuration page in Immich, and add the supplied path (i.e. ``/data/test1``).

.. _immich_setup:

Finishing the Immich set-up
------------------------------

#. If you haven't already, click on the **Immich UI** button. At which point the web UI will load.
#. Click on the **Getting Started** button.
#. First you will create an admin account. 
    - If you intend to use the `email notification <https://docs.immich.app/administration/email-notification/>`_ feature, 
      then it is recommended to use your actual email address. 
      Otherwise, you can input any kind of email-like string into the *Admin Email* field.
#. Click on the **Theme** button and choose the preferred theme.
#. Click on the **Language** button and choose the preferred language.
#. Click on the **Server Privacy** button.
    - **Map**: if enabled, it will use Immich's map tile service to show the location of where the photo was taken on a world map.
    - **Version Check**: if enabled, it will periodically check Immich's github repo, if a new release is available.
#. Click on the **User Privacy** button.
    - **Google Cast**: if enabled, it will load resources from Google to make Google Cast work.
#. Click on the **Storage Template** button.
    - This setting is about how files are organized on the disk. If you want to keep it simple, keep it disabled. 
      You can always migrate to storage templates at a later date.
    - But if you want to custom define what kind of folder structure and filenames you want to have,
      then you should enable this setting.
    - You can also 
      `check the detailed differences of using storage templates or not <https://docs.immich.app/administration/backup-and-restore#asset-types-and-storage-locations>`_.
#. Click on the **Backups** button and consider if you have any special backup requirements for your Immich instance.
#. Click on the **Mobile App** button and consider if you want to install their official mobile app.
    - Having the mobile app will allow you to access your files, 
      but more importantly, you will also be able to set automatic, background uploading of photos/videos to your Immich instance.
#. Click on the **Done** button to finish the set-up.

.. _immich_new_user:

New user account
------------------------------

If you wish, you can simply use the Admin account for now.
Otherwise, you can consider creating new user accounts.

1. Login to your Immich instance with your Admin account.
2. Click on your profile image on the top-right corner of the page, then click on **Administration**.
3. Click on the **Create user** link below your profile image on the top-right corner of the page.
4. Fill in the user account data. Note that files coming from external libraries do *not* count toward the Quota Size.
5. Click on the **Create** button to create the new user account.

.. _immich_external_library_import:

External Library Import
------------------------------

If you have an existing collection of photos and videos, you are probably going to want to include it into your Immich instance.

.. note::
    **Note that there is currently no good central sharing solution present in Immich!**
    If you wanted to have a central repository of photos/videos that is shared between different users, 
    `you will need to wait <https://github.com/immich-app/immich/issues/12614>`_ until it's implemented.

    Until then, here are some alternatives:

    #. Create a single user account that you share with other people: all people and devices will have access to the same library with all people/facial recognition data (and other metadata), and they will all be able to upload their own files to the library. Duplicates are detected on the whole library.
    #. `Use partner sharing <https://docs.immich.app/features/partner-sharing/>`_: other users will be able to view and download files (and their metadata) from your library, but won't also share the people/facial recognition data. You won't see other users' libraries automatically - they have to explicitly share back. Other users can't upload their files to your library. Duplicates are detected only on your library. Smart search and map features won't be shared.
    #. Create user accounts for each family member and one additional account with the external library, then using the partner sharing feature, share the external library with other users.
    #. Set-up the same external libraries for each user: causes unnecessary file metadata duplication.

Here is how you can import your files into Immich.

1. Prerequisite is that you have made your share available to Immich. See: :ref:`immich_mounting_external_library`. 
    - Also note that every external library must have an owner. If you haven't created your user account(s), do so now. See: :ref:`immich_new_user`
2. Click on your profile image on the top-right corner of the page, then click on **Administration**.       
3. Click on the **External Libraries** item in the left-side menu.   
4. Click on the **Create library** link below your profile image on the top-right corner of the page. 
5. Choose a user that will be the owner of the external library. 
   This means that all files from the external library will be imported to the selected user's library. 
    - The user may choose to `share their library with other users with some limitations <https://docs.immich.app/features/partner-sharing/>`_.
6. Click on the **Create** Button.
7. Input the path to the external library that you've defined at :ref:`immich_mounting_external_library`. 
   E.g. ``/data/test1``...
8. Click on the **Add** button.
9. Click on the **Validate** button to check if the external library is correctly configured.
10. In case or problems, please refer to `in-depth explanation and troubleshooting information <https://docs.immich.app/features/libraries>`_.

.. _immich_other_settings:

Other important settings
------------------------------

Depending on your hardware specifications and cooling capabilities, 
you will want to consider changing the default
`concurrency settings <https://docs.immich.app/administration/jobs-workers#jobs>`_
when new files are being ingested into your Immich instance.

Try importing a large (10k+ files) external library, then follow the system temperature and responsiveness.

If no sustained high temperatures are seen after 20 minutes or so, then you're done!

Otherwise, go to *Administration* > *Jobs* to see what is happening, then adapt the settings under the 
**Manage Concurrency** link on the top-left.

Non-problematic jobs: Sidecar metadata and External libraries.

Intensive jobs: Generate thumbnails, Smart search, Face detection and Transcode videos.

