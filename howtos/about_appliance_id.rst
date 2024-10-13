.. _aboutapplianceid:

About Appliance ID
==================

During the initial :ref:`webui_setup` stage of a Rockstor install,
an **Appliance ID** is automatically generated.
This ID, intended as a Universal Unique Identifier (UUID),
is an exact copy of the host system's, read motherboard's, response to:

.. code-block:: console

    cat /sys/class/dmi/id/product_uuid

.. note::

    With the majority of systems,
    this is a genuinely unique reference; and no intervention of any sort is required.

The implied uniqueness is assumed by multiple current Rockstor subsystems, e.g.
when :ref:`add_appliance` as part of setting up a Share :ref:`sharereplication`.
And as part of configuring a system to use the :ref:`stable_channel` updates.

.. warning::

    WARNING: some systems, via lax firmware implementations, return a NON-Unique/fake product_uuid.

.. _knownfakeapplianceids:

Fake Appliance ID examples
--------------------------

The following are examples on non-unique Appliance IDs,
all recognised by the latest version of Rockstor.

- **03000200-0400-0500-0006-000700080009** -
  ASRock N3700-ITX, ASRock C2550D4I - Rockstor devs.
  ASRock J3455 ITX - Thanks to forum member adworacz.
- **00020003-0004-0005-0006-000700080009** -
  ZOTAC 880G-ITX (880GITX-A-E) - Thanks to forum member mmmdonuts.
- **5c4606fa-192f-453a-b299-7b088c63bb9b** -
  GIADA N70E-DR - Thanks to forum member hammerite.
- **31393138-3538-5a43-3135-353130323750** -
  HP/HPE ProLiant MicroServer Gen8 - Thanks to David via support email.
- **00000000-0000-0000-0807-060504030201** -
  Reported by Appman
- **00000000-2093bfe3-e53b-4fc3-9cb1-9217ea6228c7** -
  Reported by Appman

For all non-unique Appliance IDs known to the bundled version of Rockstor within an installer,
a fail-over Appliance ID is substituted automatically.
This has the advantage of ensuring that Rockstor's Appliance ID dependant subsystems are functional.
But the disadvantage is that upon re-install, using the same motherboard,
a new Appliance ID will be generated.

.. note::

    `Appman <https://appman.rockstor.com/>`_
    a complementary service for Stable Updates subscription members,
    has the facility to trivially, and with immediate effect,
    transfer an active Stable Updates subscription *activation code* via an Appliance ID edit function.
    But far better that this is not required.
    Hence our initial use of hardware-static Appliance IDs.

.. _setapplianceid:

Set Appliance ID
----------------

For whatever reason,
mostly notably if you have a non-unique Appliance ID that is not known to Rockstor,
the following procedure can assert an Appliance ID of your choice:

1. Generate a genuinely unique UUID, e.g. from `Online UUID Generator <https://www.uuidgenerator.net>`_.

2. Via a local console, as the `root` user, substitute your generated UUID in the following:

(i.e. replace your-generated-appliance-id-here with the Generated UUID).

.. code-block:: console

  psql -U rocky storageadmin
  UPDATE storageadmin_appliance SET uuid='your-generated-appliance-id-here' WHERE current_appliance=True;
  \q
  exit

The above will expect entry of the password 'rocky'. Our DB is configured, as per upstream defaults,
To only be accessible via the local host: hence the local console requirement.

Confirm your new Appliance ID by visiting/refreshing the System -> Appliances Web-UI page.
