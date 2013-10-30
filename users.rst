.. _users:

User configuration
==================

RockStor allows the admin to add, delete and modify users in the system.
To access the Users (user list) page, go to System -> Users
This page lists the available users, and allows the admin to 
add users, change a user's password, or delete a user.

Add a user
----------

To add a user, click the 'Add User' button on the Users page. This will bring up the 'Create a User' page. Fill in a desired username, and the password fields.

If the 'Allow this user to login to RockStor Web UI' checkbox is unchecked, the created user will be only a system (unix) user, and will not be able to login to the RockStor Web UI. If it is checked, the user can login to both the system and the Web UI with the same password.


   .. image:: add-user.gif
      :scale: 75 % 
      :align: center

Edit user
---------

To change a user's password, click the edit icon next to that user in the user table on the Users page. This will bring up a change password form where you can change the user's password.

   .. image:: change-password.gif
      :scale: 75 % 
      :align: center

Remove user
-----------
