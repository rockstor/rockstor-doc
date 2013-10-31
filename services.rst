
Services
========

Rockstor supports many services that are necessary for a storage system to be functional.
Service management including configuration, turning a service on or off, can be done via the System tab of the Webui as well as the services console of the CLI.

The System -> Services page lists the services handled by Rockstor, and their current state (ON or OFF)

   .. image:: services.png
      :scale: 70 % 
      :align: center

To start or stop a service, click the ON or OFF buttons respecively.

Some services need to be configured before they can be turned on. To access the configuration page for a service, click the wrench icon next to the service name.

The supported services are described below.

NFS
---

NFS service represents the NFS server. It must be turned on to export shares
via NFS protocol.


Samba
-----

Samba service represents the Samba server. It must be turned on to make shares
available via SMB protocol.

AD
--

AD is a directory service to connect to Active Directory. It must be turned on
in order to be part of AD.

AD Configuration
^^^^^^^^^^^^^^^^^
To configure AD, you can specify the following values on the AD configuration page.

1. Domain 
2. Controllers
3. Security
4. Realm
5. Template shell
6. Allow offline login


NTP
---

NTP is a service to maintain system time in synchronization with Internet
standard time server. This service must always be turned on.

NTP Configuration
^^^^^^^^^^^^^^^^^
To configure NTP, you can specify the address of an Internet standard time server in the NTP configuration page.

LDAP
----

LDAP is a directory service to connect to LDAP server.

LDAP Configuration
^^^^^^^^^^^^^^^^^^

To configure LDAP, you can specify the following values on the LDAP configuration page.

1. LDAP Server
2. Search base DN
3. Enable TLS
4. Certificate URL (if TLS is enabled)

NIS
---

NIS is a directory service to connect to a NIS server.

NIS Configuration
^^^^^^^^^^^^^^^^^

To configure NIS, the following values can be provided on the NIS configuration page.

1. Domain
2. Server

