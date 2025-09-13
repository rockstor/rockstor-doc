.. _nginx_rockon:

nginx Rock-on
==============

Please be aware of the common prerequisites for all Rockstor
:ref:`rockons_intro`; specifically the :ref:`rockons_preinstall` and
:ref:`rockons_root` requirement.

Our `nginx Rock-on forum <https://forum.rockstor.com/t/rock-on-nginx-topic-for-all-things-nginx/9617>`_
area.

.. _nginx_whatis:

What is nginx
--------------

nginx [engine x] is an HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server,
originally written by Igor Sysoev. For a long time, it has been running on many heavily loaded Russian sites
including Yandex, Mail.Ru, VK, and Rambler. Here are some of the success stories: Dropbox, Netflix, FastMail.FM.

The sources and documentation are distributed under the 2-clause BSD-like license:

* Basic HTTP server features
* Serving static and index files, autoindexing; open file descriptor cache
* Accelerated reverse proxying with caching; load balancing and fault tolerance
* Accelerated support with caching of FastCGI, uwsgi, SCGI, and memcached servers; load balancing and fault tolerance
* Modular architecture. Filters include gzipping, byte ranges, chunked responses, XSLT, SSI, and image transformation filter
* Multiple SSI inclusions within a single page can be processed in parallel if they are handled by proxied or FastCGI/uwsgi/SCGI servers
* SSL and TLS SNI support
* Support for HTTP/2 with weighted and dependency-based prioritization
* Support for HTTP/3


.. _nginx_doc:


nginx Documentation
--------------------

For online documentation and support please refer to `nginx.org <https://nginx.org>`_.


.. _nginx_install:

Installing nginx Rock-on
-------------------------

First please consider the pre-requisites for any Rockstor Rock-on; these are linked to at
:ref:`top <nginx_rockon>` of this document. Note also that the nginx Rock-on will require 2 Shares to use as
it’s config and data working directories.

.. note::
   This is in addition to the :ref:`rockons_root` that may well already have been made.

1.	After you complete the configuration of the Rock-on service, push the **update** button on the top right of the page to copy in all of the latest Rock-ons to your server.

.. image:: /images/interface/docker-based-rock-ons/nginx_install_step1.png
   :width: 90%
   :align: center

2.	Select the All tab to see all available Rock-ons and locate the nginx rock-on. Before installing this Rock-on you must create 2 shares. One is for config files and the other is for Data such as web pages. Name them nginx-config and nginx-data. I will explain their use below.

3.	Now you can begin the nginx Rock-on install. Click the **Install** button next to the nginx listing on the Rock-ons page.

4.	During the install you will be asked to identify the config and data shares. Just follow the prompts and enter the names of the shares you created in step 2.

5.	When the install completes you may or may not have to turn it on. You do so by clicking the Off button which will toggle it to “on”. If it says “on” already that is good and you are all set.

.. image:: /images/interface/docker-based-rock-ons/nginx_install_step3.png
   :width: 90%
   :align: center

6.  If you now click the nginx UI button you will see an intro page with links to some nginx information.

.. image:: /images/interface/docker-based-rock-ons/nginx_install_step5.png
   :width: 90%
   :align: center

7.  To check the options, you have entered go back to the Rock-on screen and click the tool icon.

.. image:: /images/interface/docker-based-rock-ons/nginx_install_step6.jpg
   :width: 90%
   :align: center

You will get the following if all is correct.

.. image:: /images/interface/docker-based-rock-ons/nginx_install_step7.png
   :width: 90%
   :align: center

8.  At this point you’re finished with the install of the sample server. Be sure to link to the shared directory from another machine to install any config file changes.

.. warning::
   **DO NOT** change configurations on the system drive because those datasets belong to the system nginx server.


.. _nginx_advanced_config:


Advanced nginx configuration
----------------------------

If you need or want to make changes to the config you will need to put your changed config or data files in the appropriate shared directories and turn the server off and back on via the Rockon page to make them active (other ways are described below).

Introduction
^^^^^^^^^^^^

There are many parts to this:

* The Base OS which is SUSE
* NGINX running on the base OS is the front end to running the Rockstor web interface where the majority of the NAS controls are.
* Rockstor which is running on the base OS as the NAS solution. The interface is Web based and is accessed via the IP that you receive as you complete the SUSE/Rockstor instalation. It is also displayable with the Myip command.
* The Rock-on section of Rockstor NAS contains Rock-ons for the nginx web server as well as other utilities.
* Once installed this web server is run in a Docker image. Docker is like a virtual machine and requires the use of the Rockstor interface and Docker commands to talk to the VM and the nginx server (see diagram below).


For more information, here is the link to the :ref:`advanced configuration <rockons_advanced_config>` of Rockons.

.. image:: /images/interface/docker-based-rock-ons/nginx_install_diag.png


.. _nginx_commands:


Using nginx commands
^^^^^^^^^^^^^^^^^^^^


These commands will only talk to the main nginx server unless formated differently. For interaction with the nginx Rockon see Docker commands below.


1. **systemctl status nginx** (This gives a lot of information on tasks running in the OS instance.)

.. code::

 nginx.service - The nginx HTTP and reverse proxy server - 30-rockstor-nginx-override.conf
 Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: disabled)
 Drop-In: /etc/systemd/system/nginx.service.d
          └─30-rockstor-nginx-override.conf
 Active: active (running) since Fri 2024-07-05 12:46:31 EDT; 3 days ago
 Process: 9810 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
 Process: 9812 ExecStartPre=/usr/sbin/nginx -t -c /opt/rockstor/etc/nginx/nginx.conf (code=exited, status=0/SUCCESS)
 Main PID: 9814 (nginx)
 Tasks: 3 (limit: 4915)
 CPU: 1min 13.697s
 CGroup: /system.slice/nginx.service
          ├─3344 "nginx: worker process"
          ├─3345 "nginx: worker process"
          └─9814 "nginx: master process /usr/sbin/nginx -c /opt/rockstor/etc/nginx/nginx.conf"
 Jul 05 12:46:31 vault systemd[1]: Starting The nginx HTTP and reverse proxy server - 30-rockstor-nginx-override.conf...
 Jul 05 12:46:31 vault nginx[9810]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
 Jul 05 12:46:31 vault nginx[9810]: nginx: configuration file /etc/nginx/nginx.conf test is successful
 Jul 05 12:46:31 vault nginx[9812]: nginx: the configuration file /opt/rockstor/etc/nginx/nginx.conf syntax is ok
 Jul 05 12:46:31 vault nginx[9812]: nginx: configuration file /opt/rockstor/etc/nginx/nginx.conf test is successful
 Jul 05 12:46:31 vault systemd[1]: Started The nginx HTTP and reverse proxy server - 30-rockstor-nginx-override.conf.



2. **journalctl -xeu nginx.service** also gives a lot of status information.

.. code::

 ░░ A stop job for unit nginx.service has finished.
 ░░
 ░░ The job identifier is 13750 and the job result is done.
 Jul 05 12:46:31 vault systemd[1]: nginx.service: Consumed 1.437s CPU time.
 ░░ Subject: Resources consumed by unit runtime
 ░░ Defined-By: systemd
 ░░ Support: https://lists.freedesktop.org/mailman/listinfo/systemd-devel
 ░░
 ░░ The unit nginx.service completed and consumed the indicated resources.
 Jul 05 12:46:31 vault systemd[1]: Starting The nginx HTTP and reverse proxy server - 30-rockstor-nginx-override.conf...
 ░░ Subject: A start job for unit nginx.service has begun execution
 ░░ Defined-By: systemd
 ░░ Support: https://lists.freedesktop.org/mailman/listinfo/systemd-devel
 ░░
 ░░ A start job for unit nginx.service has begun execution.
 ░░
 ░░ The job identifier is 13750.
 Jul 05 12:46:31 vault nginx[9810]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
 Jul 05 12:46:31 vault nginx[9810]: nginx: configuration file /etc/nginx/nginx.conf test is successful
 Jul 05 12:46:31 vault nginx[9812]: nginx: the configuration file /opt/rockstor/etc/nginx/nginx.conf syntax is ok
 Jul 05 12:46:31 vault nginx[9812]: nginx: configuration file /opt/rockstor/etc/nginx/nginx.conf test is successful
 Jul 05 12:46:31 vault systemd[1]: Started The nginx HTTP and reverse proxy server - 30-rockstor-nginx-override.conf.
 ░ Subject: A start job for unit nginx.service has finished successfully
 ░░ Defined-By: systemd
 ░░ Support: https://lists.freedesktop.org/mailman/listinfo/systemd-devel
 ░░ A start job for unit nginx.service has finished successfully.
 ░░
 ░░ The job identifier is 13750.


3. **nginx** command has the following options

.. code::

  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit  -- Helps to see which config files are in use
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr//)
  -e filename   : set error log file (default: /var/log/nginx/error.log)
  -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
  -g directives : set global directives out of configuration file



.. _Docker_commands:



Docker command examples for nginx Rockon
----------------------------------------

1. For help with Docker go to Docker.com and create an ID. For users subscribed to Dockers free plan, here are some resources that are available to you:

- Docker Community Forums: https://forums.docker.com/
- Third-Party Communities: https://www.docker.com/community/
- Docker Documentation: https://docs.docker.com/

2. To execute commands such as nginx -T` or nginx -s reload inside your Nginx container, you need to access the container's shell. You can do this using the `docker exec` command.


.. code:: bash

  docker exec -it <container_name_or_id> /bin/sh



Once inside the container, you can run your desired Nginx commands.


.. code:: bash

   nginx -T   # To view the configuration files
   nginx -s reload   # To reload Nginx



the default Nginx configuration files are typically located at /etc/nginx/nginx.conf.sample within the container. To verify the configuration file being used and display the active configuration files and their locations, you can run:

.. code:: bash

    nginx -T



The default log files for Nginx are usually found at:
   - Access Logs: /var/log/nginx/access.log
   - Error Logs: /var/log/nginx/error.log


If you made changes to the configuration files, ensure that the directory is properly mapped to the container. Check your Docker run command or Docker Compose file.

.. code::

   volumes:
      - /path/to/nginx-config:/etc/nginx


 Or after making changes, reload Nginx within the container to apply them:

.. code::

   nginx -s reload


.. note::

   There are a lot of other nginx and docker commands that you will have to learn to make this a useful tool for you. Remember, these are just the basics.
