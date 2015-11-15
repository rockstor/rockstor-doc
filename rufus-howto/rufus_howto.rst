..  _rufus_howto:

Rockstor USB install disk using Rufus
=====================================

`Rufus <https://rufus.akeo.ie/>`_ is an open source multilingual general
purpose graphical utility for Windows XP and newer systems to help in the
creation of bootable USB flash drives. It is licenced under
`GNU GPLv3 or later <https://www.gnu.org/licenses/gpl.html>`_. Using it's
default settings it will NOT create a working Rockstor USB install disk but
using the following configuration options it can successfully prepare a working
USB flash drive to be used for Rockstor install. Please see the
:ref:`makeusbinstalldisk` in our :ref:`quickstartguide` guide for other tested
methods.

N.B. The following method and screen captures were graciously proved and
provided respectively by @Dragon2611 a
`Rockstor forum <http://forum.rockstor.com/>`_ member.

.. _rufus_steps:

Steps required
--------------

First download the latest
`Rockstor iso image <http://rockstor.com/download.html>`_ and the latest
version of `Rufus <https://rufus.akeo.ie/>`_ then insert your USB key and run
Rufus:-

* Under **Device** select your **USB key**, double check you selection.
* Using the **CD icon button** select the **Rockstor iso**, the mouse over tooltip reads *Click to select an ISO*
* Change the dropdown next to the CD icon button to read **DD Image** mode.
* Double check all settings and **Click Start**.

The following images and notes indicate the above steps.

First select the destination USB key using the **Device** drop down.

.. image:: rufus_select_device.png
   :scale: 100%
   :align: center

In the above example the Device selected was a 8 GB (7.7 GB) USB2 device.

Now select the **Rockstor iso image** using the **CD icon button**: a small
button at the end of the line with the *Create a bootable disk using* option.

.. image:: rufus_rockstor_selected.png
   :scale: 100%
   :align: center

The Rockstor iso file name should now be visible in the bottom of the Rufus
window.

Now select the **DD Image** option from the drop down between the
*Create a bootable disk using* option and the *CD icon* button.

.. image:: rufus_select_dd.png
   :scale: 100%
   :align: center

Note in the above we see the **DD Image** mode selection.

Double check all selections and then click the **Start Button**, the following
warning should result.

.. image:: rufus_warning.png
   :scale: 100%
   :align: center

Note the device label and size in the warning before preceding.

Upon confirming continuation we should have the following progress screen

.. image:: rufus_write_in_progress.png
   :scale: 100%
   :align: center

**Upon completion safely eject / remove / unmount the USB device before
removing it**



