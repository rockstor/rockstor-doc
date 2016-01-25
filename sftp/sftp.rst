.. _sftp:

Secure File Transport Protocol (SFTP)
=====================================

This is a basic method / protocol for transferring data based on the ancient
and insecure File Transfer Protocol (FTP), only updated to be more secure. The
internal system used by Rockstor is that included as a subsystem within the
openssh server.

Unlike other file sharing systems like :ref:`samba` or :ref:`afp` sftp has
no built in discovery or service publishing components. This makes it a
simpler system but one that requires a little more effort to connect with.
Most notably is it required that you manually enter the Rockstor's hostname
or ip address on the clients that wish to connect.

.. _rockstor_sftp:

The Rockstor SFTP System
------------------------

By default no user other than root are allowed to login via ssh or user sftp.
This restriction improves security but means there are certain conditions that
must be met to gain sftp access to a Rockstor share.

* the **SFTP user** must be a **Rockstor user**
* the **SFTP user** must also be the **owner** of an **exported SFTP share**

These restrictions make Rockstor's SFTP implimentation more suited for
individual storage needs as opposed to a shared storage area accessed by
multiple users. In the following example we will setup a secure share for use by
a single user, ie for secure backup purposes.

Note also that the share or shares owned by the SFTP user will be mounted within
a chroot environment, internally this is located at
*/mnt3/<username>/<sharename>*.

.. _create_sftp_share:

Creating a SFTP Share
---------------------

In order to establish an SFTP share it is first necessary to have a
pre-configured storage pool, a share of this pool or part there of, and a
Rockstor user to authenticate against this share. Finally the share must be
exported via the SFTP method. The following list details a suggested order
and gives links to the documentation on each of these steps.

* To create a storage pool see :ref:`createpool` in the :ref:`pools` section.
* :ref:`Add a Rockstor user <adduser>` to use in the SFTP authentication process, see the :ref:`users` section.
* A :ref:`Share <shares>` of this storage pool is then required, see :ref:`createshare` in the :ref:`pools` section.
* Finally this Share is exported via :ref:`sftp_export`.

.. _sftp_pool:

The SFTP Pool
^^^^^^^^^^^^^

The following example shows a general purpose **rock_pool** has been created.

..  image:: rock_pool.png
    :scale: 80%
    :align: center

*A Raid1 pool of 2 drives*

.. _sftp_share:

The SFTP Share
^^^^^^^^^^^^^^^^

Here a :ref:`Share <shares>` has been created on the above rock-pool disk set.

..  image:: sftp_share.png
    :scale: 80%
    :align: center

A 20GB share of the rock-pool resource.

Note the required setting of owner is set here to the intended user, this page
appears when the share name is clicked on and the **Access control** tab is
selected. An **Edit button** brings up the following display.

.. image:: sftp_perms.png
   :scale: 80%
   :align: center

Please note the **required setting** of **owner** has to be **non root**. If not
then when a SFTP export is attempted a warning will be given.

..  _sftp_export:

Add SFTP Export
^^^^^^^^^^^^^^^

Finally **export** the **Share** via the **SFTP** entry in **File Sharing**.
This menu entry is available in the **Storage** section. Note that the **SFTP
Service** must be **ON**, which is the the default, before these options are
available.

..  image:: add_sftp_export.png
    :scale: 80%
    :align: center

Note the **Writable** or **Read only** settings for this export option.

The resulting SFTP export is then displayed in summary form:

..  image:: sftp_export_summary.png
    :scale: 80%
    :align: center

Note that even if the share is writable by the user the export *read only*
option will take precedence.