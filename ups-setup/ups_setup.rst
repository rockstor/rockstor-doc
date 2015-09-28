.. _ups_setup:

UPS / NUT Setup
===============

Overview
--------

Rockstor users the `NUT software collection <http://www.networkupstools.org/>`_
to orchestrate a graceful system shutdown in the presence of mains power
failure. It does this by continuously monitoring a UPS device to maintain a
knowledge of safe power conditions. In the event of those conditions changing
:ref:`email_notifications` can be sent and if the critical main power
condition persists the system will be shutdown to avoid an otherwise
inevitable power cut affecting the system while in an active state.

.. _what_is_a_ups:

What is a UPS
-------------

A **UPS** is a **Un-interruptable Power Supply** and is often associated with
mission critical electrical components such as computer servers and network
infrastructure. There function is to continue to provide mains power to the
equipment they are setup to protect in the event that the mains suffers a
blackout (mains disappears completely) or a brown out (the mains becomes sub
standard). A common facility of UPS devices is an ability to inform their
protected equipment of the critical mains event which in turn allows that
equipment to take evasive action and avoid suffering the consequences of the
power cut themselves.

In the case of servers this typically involves initiating
a safe shutdown which may also involve emailing administrative personal of the
critical event. Most domestic and pro consumer UPS's are intended to provide
mains power to their protected equipment for the duration required for this
evasive action to be taken. Care should be taken to size a UPS so that it's run
time in use is efficient to meet this *safe shutdown* criteria.

.. _what_is_nut:

What is NUT
-----------

NUT stand for `Network UPS Tools <http://www.networkupstools.org/>`_ and is a
collection of packages that enables the communication between UPS systems and
their protected equipment. It also has the facility to share this information
on the local lan so that equipment that is powered by the UPS but is not
directly connected to the ups data wise can be informed of the critical mains
power events. This is particularly useful as generally in the low to mid range
of UPS's only one machine may be connected data wise to each UPS unit. With NUT
acting in netserver mode it can inform any number of machines of the critical
power event. The other machines would receive this message by running their own
instance of NUT but in netclient mode. Rockstor can be configured to work in
any of NUT 3 modes. The third mode is the most common and is called standalone
mode. In this mode Rockstor is directly attached to UPS and doesn't share the
mains state information it gets with any other machines.




