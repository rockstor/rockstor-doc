.. _accessshares:

Accessing Shares from Clients
=============================

Data is stored and organized for use in Shares which are exported to clients
via various protocols: :ref:`samba_export`, :ref:`nfs`, and :ref:`sftp`.
Before storing any data, at least one :ref:`Share <shares>` must be
created. See :ref:`createshare` for detailed instructions.

The choice of sharing protocol depends on a variety of factors. The most
important one is the nature of the client(s) that will be used to access the
share. For instance, while **Samba** exports can be accessed by Linux, Windows,
and macOS clients alike, **NFS** exports cannot be easily accessed from Windows
clients. In addition, each protocol varies in its performance and ease of
access. As a result, the decision of using a protocol over another for a given
share ultimately depends on your exact needs. We can however make the general
recommendations below:

- If your share needs to be accessed by at least one Windows clients, use
  **Samba**. See our :ref:`samba_export` section for details.
- If your share needs to be accessed by Linux clients *only*, use **NFS**.
  See our :ref:`nfs` section for details.

.. note::

   Still unsure of what file sharing protocol to use? Don't hesitate to come
   ask for feedback on our `friendly forum! <https://forum.rockstor.com>`_
