.. _accessshares:

Accessing Shares from Clients
=============================

Data is stored and organized by users in Shares, which are exported to clients
via various protocols including :ref:`samba`, :ref:`nfs`, and :ref:`afp`.
Before storing any data at least one :ref:`share <shares>` must be created.
See :ref:`createshare` for a detailed description.

Accessing Shares via Samba/CIFS
-------------------------------

Samba/CIFS is the standard way to store and access data in Shares from Windows,
Mac, and Linux clients such as desktops and laptops. In order to access a
Share, it must first be made available. See :ref:`sharesamba` for details.
Once a Share is configured for Samba/CIFS availability, data can be stored
and accessed from various clients as described below.

Unix/Linux
^^^^^^^^^^

   On a Unix/Linux client, the Rockstor server will appear in the
   File explorer application as an entry of the form **Rockstor@<ip-address>** under **Browse Network** . Clicking on the server will display the available exported shares that have Browseable true.

   If the Rockstor server does not appear in the File explorer, a connection can be made by selecting 'Connect to Server'

   .. image:: smb_linux_network.png
      :scale: 65%
      :align: center

   Connecting to a share can be done by clicking on it, and authenticating as a specific user who has permissions to access the share, or as a guest user.

   .. image:: smb_linux_share.png
      :scale: 65%
      :align: center

Windows
^^^^^^^

   Coming soon...

Mac OS
^^^^^^

   On a Mac OS, the Rockstor server will appear in the Finder sidebar, as an entry of the form **Rockstor@<ip-address>**. Connecting to the server can be done by clicking on the entry, and authenticating as a specific user who has permissions to access the share, (or as a guest user, if the share has Guest OK set to true) as shown below.

   .. image:: smb_mac_auth.png
      :scale: 65%
      :align: center

   If the Share has browseable set to true, it will appear as a folder in the **Finder** after successfully connecting to the server.

   .. image:: smb_mac_share.png
      :scale: 65%
      :align: center

   On the command line, the available exported shares will appear as folders under /Volumnes

Accessing NFS shares
---------------------

   Coming soon...

