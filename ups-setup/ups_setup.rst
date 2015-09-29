.. _ups_setup:

UPS / NUT Setup
===============

Overview
--------

Rockstor users the `NUT software collection <http://www.networkupstools.org/>`_
to orchestrate a graceful system shutdown in the presence of mains power
failure. It does this by continuously monitoring a UPS device to maintain a
knowledge of safe power conditions. In the event of those conditions changing
:ref:`email_notifications` can be sent and if the critical mains power
condition persists the system will be shutdown to avoid an otherwise
inevitable power cut affecting the system whilst in a live state. If you are
familiar with UPS and NUT please skip to :ref:`rockstor_nut_config`.

.. _what_is_a_ups:

What is a UPS
-------------

A **UPS** is a **Un-interruptable Power Supply** and is often associated with
mission critical electrical components such as computer servers and network
infrastructure. There function is to continue to provide mains power to the
equipment they are setup to protect in the event that the mains suffers a
blackout (mains disappears completely) or a brown out (the mains becomes sub
standard). A common facility of UPS devices is an ability to inform their
protected equipment of a critical mains event which in turn allows that
equipment to take evasive action and avoid suffering the consequences of the
power cut themselves.

In the case of servers this typically involves initiating
a safe shutdown which may also involve emailing administrative personal of the
critical event. Most domestic and pro consumer UPS's are intended to provide
mains power to their protected equipment for the duration required for this
evasive action to be taken. Care should be taken to size a UPS so that it's run
time in use is sufficient to meet this *safe shutdown* criteria.

.. _what_is_nut:

What is NUT
-----------

NUT stand for `Network UPS Tools <http://www.networkupstools.org/>`_ and is a
collection of GPLv2 licenced packages that enables the communication between
UPS systems and
their protected equipment. It also has the facility to share this information
on the local lan so that equipment that is powered by the UPS but is not
directly connected to the ups data wise can be informed of the critical mains
power events. This is particularly useful as generally in the low to mid range
of UPS's only one machine may be connected data wise to each UPS unit. With NUT
acting in :ref:`nut_netserver` it can inform any number of machines of the critical
power event. The other machines would receive this message by running their own
instance of NUT but in :ref:`nut_netclient` mode. Rockstor can be configured to work in
any of NUT 3 modes. The third mode is the most common and is called
:ref:`nut_standalone`. In this mode Rockstor is directly attached to UPS and
doesn't share the mains state information it gets with any other machines.

.. _rockstor_nut_config:

Rockstor NUT configuration
--------------------------
Nut in Rockstor is treated as a service. Please see our :ref:`services` section
for further information. From the **System - Services** page it is possible to
turn the NUT service **ON** and **OFF** and **configured** it via it's
**spanner icon**.

Please take care to read the mouse over tool tips; the **Nut Mode** is the
first thing to select in any nut configuration.

..  image:: nut_modes.png
    :scale: 80%
    :align: center

The 3 modes available are detailed in the following sections
:ref:`nut_standalone`, :ref:`nut_netserver`, :ref:`nut_netclient`

.. _nut_standalone:

Standalone Mode
^^^^^^^^^^^^^^^

This is the most common configuration. Rockstor is connected directly to the
data port of the UPS, usually via serial or USB connection, and doesn't share
the mains / ups data with any other machines.

This mode requires the following fields:

* **NUT Mode** - A drop down and in this case **standalone** is required
* **NUT Driver** - Please see NUT's `Hardware Compatibility List <http://www.networkupstools.org/stable-hcl.html>`_ to select the correct driver for your particular UPS make and model.
* **UPS Port** - the port name for how the UPS data cable is connected to the Rockstor machine; examples are **/dev/ttyS0** for the first serial port or **/dev/ttyUSB0** for a or **auto** for many direct usb connected UPSs.
* **NUT User** - N.B. this is not a system user but reserved solely for NUT use.
* **NUT User Password** - A password for the above nut user.

..  image:: nut_standalone_eg.png
    :scale: 80%
    :align: center

.. _nut_netserver:

Netserver Mode
^^^^^^^^^^^^^^

Netserver Mode is essential identical to :ref:`standalone` but with the
additional benefit of offering NUT services to other machines on the network by
way of those machines running NUT client software.

..  image:: nut_netserver.png
    :scale: 80%
    :align: center



.. _nut_netclient:

Netclient Mode
^^^^^^^^^^^^^^

..  image:: nut_netclient.png
    :scale: 80%
    :align: center