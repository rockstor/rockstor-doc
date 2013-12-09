Accessing Shares from Clients
==============================

Accessing Samba shares 
----------------------

Unix / Linux client
^^^^^^^^^^^^^^^^^^^

   On a Linux client, the RockStor server will appear in the File explorer application, under **Browse Network** . Clicking on the server will display the available exported shares that have Browseable true. 
   
   .. image:: smb_linux_network.png
      :scale: 65%
      :align: center

   Connecting to a share can be done by clicking on it, and authenticating as a specific user who has permissions to access the share, or as a guest user.

   .. image:: smb_linux_share.png
      :scale: 65%
      :align: center

Windows client
^^^^^^^^^^^^^^
   
   Coming soon...

Mac OS client
^^^^^^^^^^^^^
   
   On a Mac OS client, the RockStor server will appear in the Finder sidebar, as an entry of the form 'RockStor@<ip-address>'. Connecting to the server can be done by clicking on the entry, and authenticating as a specific user who has permissions to access the share, (or as a guest user, if the share has Guest OK set to true) as shown below. 

   .. image:: smb_mac_auth.png
      :scale: 65%
      :align: center

   If the share has browseable set to true, it will appear as a folder in the Finder after successfully connecting to the server.

   .. image:: smb_mac_share.png
      :scale: 65%
      :align: center
  
   On the command line, the available exported shares will appear as folders under /Volumnes



Accessing NFS shares
---------------------

1. Unix / Linux client

2. Windows client

3. Mac OS client


