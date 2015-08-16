.. _email_notifications:

Email Notifications
===================

Rockstor integrates an easy to use e-mail/postfix configuration section that
enables e-mail notifications.  By default all local root (system) e-mail will
be forwarded to a specified e-mail address.  This is accomplished by using a
dedicated (configurable) e-mail account that Rockstor can login too and send
e-mail from.

.. _email_setup:

Initial Email Setup
-------------------

Navigate to the **Email Alerts** section of the **System** page:-

..  image:: email_init.png

Press the **Setup E-Mail for alerts** button to begin.

Complete the following required fields

* **Name** - associated with this email ie firstname lastname
* **Email** - of the dedicated Rockstor sending account
* **Password** - for the above account
* **SMTP Server** - sending email server name for the above account
* **TLS** - use Transport Layer Security, most email servers support this
* **Recipient email** who is to receive the notification emails from Rockstor

..  image:: email_config.png
    :scale: 80%
    :align: center

**Submit** button when done

..  _email_current:

Current Configuration
---------------------

Upon submitting the desired configuration the following is displayed
summarizing the previously entered / current information and advising on how
this configuration might be tested.

**Email Alerts** section of the **System** page with existing configuration.

..  image:: email_done.png
    :scale: 80%
    :align: center

**Note the Bin icon** in case anything is incorrect or needs replacing.