
Samba/CIFS
==========

Rockstor supports making Shares available to SMB and CIFS clients via Samba
software suite. Samba service must be turned on before exposing shares.

.. _sharesamba:

Enable or disable Samba/CIFS access for a Share
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the web-ui, click on the *Storage* tab to enter the main Storage view. Now
click on *Samba* in the left sidebar to go to the *Samba* view. 

Click on the *Add Samba Export* button. Fill in the form with the appropriate values as explained below.

In the list of shares, select the shares that you want to export through Samba.

In the *Admin Users* field, enter a space separated list of usernames who will have access to this share. These users can be local users, or users from NIS or Active Directory.

Set *Browsable* to *yes* if you want clients to be able to see the exported shares.

Set *Guest OK* to *yes* if you want to permit guest access.

Set *Read only* to *yes* if the share should not be writable by clients.


.. image:: samba_add.gif
   :scale: 65%
   :align: center

To disable Samba/CIFS access, go to the *Samba* view as before, and click on the trash icon for the appropriate share to delete the Samba export for that share.
