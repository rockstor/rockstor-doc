
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

**Configuration**

To configure AD, you can specify the following values on the AD configuration page.

1. Domain 

   Specifies the Windows Active Directory or domain controller to connect to.

2. Controllers

   Which domain controller to use.

3. Security

   The security model to use, which configures how clients should respond to 
   Samba. The options are
   
   1. user. A client must first log in with a valid username and password.
   2. server. In this mode, Samba will attempt to validate the username/password by authenticating it through another SMB server (for example, a Windows NT Server). If the attempt fails, the user mode will take effect instead.
   3. domain. In this mode, Samba will attempt to validate the username/password by authenticating it through a Windows NT Primary or Backup Domain Controller, similar to how a Windows NT Server would.
   4. ads. This mode instructs Samba to act as a domain member in an Active Directory Server (ADS) realm. 
   

4. Realm

   When the ads Security Model is selected, this allows you to specify the ADS Realm the Samba server should act as a domain member of.

5. Template shell
   
   The login shell for the user

6. Allow offline login


NTP
---

NTP is a service to maintain system time in synchronization with Internet
standard time server. This service must always be turned on.

**Configuration**

To configure NTP, you can specify the address of an Internet standard time server in the NTP configuration page.

   .. image:: ntp-config.png
      :scale: 70 % 
      :align: center

LDAP
----

LDAP is a directory service to connect to LDAP server.

**Configuration**

To configure LDAP, you can specify the following values on the LDAP configuration page.

1. LDAP Server

   The IP address of the LDAP server


2. Search base DN

   Specifies that user information should be retrieved using the listed Distinguished Name (DN). 

3. Enable TLS 

   If this is checked, TLS will be used to encrypt passwords sent to the LDAP server.

4. Certificate URL 

   If the ``Enable TLS`` checkbox is checked, you can specify a URL from which to download a valid CA (Certificate Authority) Ceritifcate. A valid CA Certificate must be in PEM (Privacy Enhanced Mail) format. 

   .. image:: ldap-config.png
      :scale: 70 % 
      :align: center

NIS
---

NIS is a directory service to connect to a NIS server.

**Configuration**

To configure NIS, the following values can be provided on the NIS configuration page.

1. Domain
   
   NIS domain.

2. Server
   
   IP address of NIS server.

   .. image:: nis-config.png
      :scale: 70 % 
      :align: center

