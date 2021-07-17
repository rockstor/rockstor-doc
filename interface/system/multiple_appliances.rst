
Multiple Rockstor appliances
============================

Rockstor runs on a single node or appliance, and can be managed with it's
Web-UI from a client computer's browser. Multiple appliances running Rockstor
are their own independent servers manageable from their respective
Web-UI's. However, features such as Rockstor-to-Rockstor replication require
the two appliances to be able to communicate with each other. Besides, it's
convenient to be able to hop from one appliance's UI to the other easily.

Every Rockstor appliance has a list of all appliances it's setup to communicate
with. They can be managed from **System -> Appliances** menu. By default, the
list only contains itself.

.. image:: /images/interface/system/multiple_appliances/initial_appliance_list.png
   :width: 100%
   :align: center


.. _add_appliance:

Adding a remote Rockstor appliance
----------------------------------

To add a remote Rockstor appliance to the list, click on the *Add Appliance*
button. Note that for this to work, the remote appliance must be reachable over
the network. In a common scenario, the remote appliance is inside the same LAN
or setup with appropriate firewall rules so the access is not restricted to it.

.. image:: /images/interface/system/multiple_appliances/add_appliance_form.png
   :width: 100%
   :align: center

Each input field has a helpful tooltip displayed when you mouse over it. Remote
**Appliance IP or Hostname** should be resolvable from the current
appliance. The **Management Port** refers to the management port of remote
appliance's Web-UI and defaults to **443**.

**Access Key ID** and **Access Key Secret** are the credentials of
the remote appliance. They can be obtained from **System -> Access keys** menu
of the remote appliance's Web-UI (see :ref:`access_keys`). Any available key,
including the default **cliapp** can be used.

.. image:: /images/interface/system/multiple_appliances/add_appliance_form2.png
   :width: 100%
   :align: center

In the above example, the remote appliance being added is identified by it's
ip(**192.168.1.123**) and I used credentials of a new access key created on it
earlier. Note that every field in this form refers to the information of the
remote appliance.

Many remote appliances can be added. There are three appliances including
itself in the below example.

.. image:: /images/interface/system/multiple_appliances/appliance_list.png
   :width: 100%
   :align: center

Clicking on an entry in the **Appliance IP** column will take you to the Web-UI
of that remote appliance.


Pairing up two Rockstor appliances
----------------------------------

So far, I've demonstrated how to add a remote Rockstor appliance to a given
Rockstor appliance. This is a symmetric feature and appliances can be added to
each other. By doing so, both appliances can communicate with each other
directly. This is necessary for certain features like Rockstor <--> Rockstor
replication of Shares.
