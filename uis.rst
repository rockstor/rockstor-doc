
User Interfaces
===============
RockStor supports multiple ways for a user to interact 
with the appliance. It supports operations through a browser based
interface (Web UI), a command line interface (CLI) that can be used for 
scripting common operations, or a RESTful API that enables complete
programmatic control of the appliance.

Web UI
------

The RockStor browser based interface or Web UI is supported on the Firefox 
web browser. 

The initial setup of the appliance should be done through the 
Web UI, and once it is completed, any of the supported interfaces can be used
to interact with it.

.. _setup:

Setup
^^^^^^

Once you have completed RockStor installation as described in the 
:ref:`installation` section, visit https://<appliance_ip> in your browser 
to setup the appliance. 

1. User 
   
   When you go to https://<appliance_ip> after installation, you will be 
   presented with the RockStor user setup screen. 
   
   Enter a suitable username and password in the corresponding input fields, 
   and click Next to go to the disk setup. An admin user with the corresponding 
   username and password will be created by RockStor. 

2. Disks
   
   The appliance will discover the free disks present in the system and list
   them. You can click Rescan to scan the disks again. 
   If all expected disks are displayed in the list, click Next. 
   
   This will complete the Setup process and you will be logged in as the 
   user you created in Step 1, and presented with the RockStor dashboard.
    
   The image below illustrates the setup process

   .. image:: rockstor-setup.gif
      :scale: 60 % 
      :align: center

.. _cli:

CLI
---

RockStor provides a command line interface that can be used by a user to 
administer the appliance, or used for scripting to automate repetitive
tasks.

To access the CLI, ssh to the appliance as the admin user that you created in the setup process. This will place you into the command line shell. The CLI is structured as a collection of subsystems. 

At any point in the CLI, entering 'help' will give you a list of available subsystems or commands, and entering any particular subsystem name or command from that list will take you to the corresponding subsystem, or execute that command.

   .. image:: cli.png
      :align: center

The subsections and commands will be further explained in the corresponding 
sections of the documentation that they are related to.

.. _api:

API
---



