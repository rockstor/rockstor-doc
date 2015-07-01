.. _rockons_intro:

Rock-ons Introduction
=====================

**Rock-ons** are Rockstor's name for it's use of `docker
<https://www.docker.com/>`_ containers to provide a **Plugin System** to easily
expand the functions of a base Rockstor install. This feature is relatively new
to Rockstor but is proving to be quite popular and is under active development.

Each Rock-on aims to provide a single additional service and the list of
supported services is expanding all the time.

.. _rockons_preinstall:

Initial Rock-ons Setup
----------------------

As Rock_ons / docker containers are like mini linux installs they require
somewhere to live.  In Rockstor it is recommend that you setup a Share
specifically for this purpose.

Note that all Rock-on will then be sorted in this shared area but each will
remain independant and during the setup of each you are given the option to
store their respective configuration and data in another location.  This is
good practice as it keeps your Rock-on config / data concerns apart from the
rocksons themselves.  You do not have to separate the config and data within each
rockon but that is also good practice, and is why this option is offered.


The Rock-ons space
^^^^^^^^^^^^^^^^^^
TODO - create the rock-on share.


.. _rockons_available:

Currently available Rock-ons
----------------------------

Please see the following for specific Rock-on install details

.. toctree::
   :maxdepth: 2

   plex_howto
   syncthing_howto
   transmission_howto
   owncloud_howto
   btsync_howto
