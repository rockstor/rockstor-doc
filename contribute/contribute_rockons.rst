.. _contributerockons:

Contributing a Rock-on
======================

Rock-ons are Docker/Podman/OCI image based plugins: see :ref:`rockons_intro` for more information.
Each is defined by a JSON file developed in the `rockon-registry <https://github.com/rockstor/rockon-registry>`_.
Or developed locally in the :code:`/opt/rockstor/rockons-metastore` directory of a Rockstor install.

.. _addmyownrockon:

How can I add my own Rock-on?
-----------------------------

As already detailed in the :ref:`adding_rockons` section, if you are familiar
with Docker and know how to run apps by hand, you can create a Rock-on for
the same with a little bit of craft. There are three broad steps:

1. Configure the Rock-on service on your Rockstor system. Follow the steps
described here :ref:`rockons_intro`.

2. Create your Rock-on profile file, [app].json following the clues on
the Rock-on structure described in the Rock-on repository
`readme.md <https://github.com/rockstor/rockon-registry/blob/master/README.md>`_.

3. Upload the file to ``/opt/rockstor/rockons-metastore/[app].json``. Hit
update in the Web-UI and install your brand new Rock-on!

If you would like to share your app with the rest of the Rockstor community, open
an issue describing what you are trying to contribute and then a subsequently
linked pull request in this repository.
Please follow these guidelines when opening a pull request:

1. One Rock-on per pull request please. If you are working on multiple apps,
separate them out. It will make testing and merging a lot more manageable.

2. Add a comment to your pull request detailing how you've tested it out.
Link to the previously created issue. The more details the better as it will
help ensure quality and benefit the whole community!

3. We are trying to offer Rock-ons that are based on a multi-architecture
docker image, i.e., it is available for :code:`amd64` (Intel/AMD CPUs) and
:code:`arm64` (ARM-based) devices. While that might not always be possible,
depending on the app or service which you are interested in, please keep
that in mind and see whether you can select a docker image that has a
multi-architecture manifest. When submitting, please add the supported
architectures to the end of the Rockon description using the
:code:`<p>` and :code:`</p>` tags (take a look at the descriptions of some
of the more recent Rock-on submissions).


.. _addvsupdrockon:

Adding vs. updating a Rock-on
-----------------------------

While there are no hard and fast rules, you can follow these guidelines to
decide whether it is better to update an existing Rock-on or submit a new one
that contains substantial changes:

1. If no Rock-on exists for your app already, create a new one. The obvious
choice.

2. Create a new Rock-on if one already exists for this project, but the new
one will use a different docker image. E.g., an existing Rock-on uses an
image from linuxserver.io, while the one you are interested in submitting
uses an image created by the owner of the project. You can subsequently
submit a proposal to deprecate the existing Rock-on. Reasons for that could
be that the underlying docker container has not been maintained in a long
time, or the new Rock-on will have the same or more functionality and is
more popular with the community.

3. Update the existing Rock-on if the changes do not include the use of a
different image. E.g., the Handbrake Rock-on was expanded with a few useful
user parameters over time, but continued to use the same underlying docker
image. Here it made more sense to update the existing Rock-on instead of
submitting a new version.


Which Docker image should I use?
--------------------------------

`Docker hub <https://hub.docker.com>`_ centralizes a very large number of
docker images. As a result, it can sometimes be difficult to select the best
image among dozens for very popular projects. While it is nearly impossible to
provide a simple "rule" for selecting the best image, the best image for a
Rock-on will be secure, maintained in the long-term, compatible with Rockstor,
and allow for "all-in-one" use for the end-user. In this context, the following
guidelines can help:

* Is there an official image for your project of interest? Official images are
  clearly labeled in Docker hub and provide assurance with regards to security,
  and long-term maintenance of the image.
* Does the project provide its own docker image? These usually ensure the good
  quality of the image and best experience with the respective project.
* Is the image regulary updated? Generally, an image with active maintainer(s)
  and community will be able to offer better support and timely updates. The
  image history on its Docker hub page as well as the number of pulls/favorites
  can be a useful indicator of an active image.
* Does the image allow for an "all-in-one" user experience? Ideally, the image
  would allow for an easy install from the Rockstor's webUI without requiring
  user intervention at the command line before and/or after.
* Finally, the image size is another helpful factor, with smaller images being
  usually favored.

Environment setup
-----------------

Go to the `rockon-registry repo <https://github.com/rockstor/rockon-registry>`_
and click on the **Fork** button. This will fork the repository into your
profile which serves as your personal git remote called origin. The next few
git steps are demonstrated on a Linux terminal.

Create a local clone of your fork.

.. code-block:: console

    git clone git@github.com:your_github_username/rockon-registry.git

Configure this new git repo with your name and email address. This is
required to accurately record collaboration.

.. code-block:: console

    cd rockon-registry
    git config user.name "Firstname Lastname"
    git config user.email your_email_address

Add a remote called upstream to periodically rebase your local repository
with changes in the upstream made by other contributors.

.. code-block:: console

    git remote add upstream https://github.com/rockstor/rockon-registry.git

The above 4 steps help you setup your local environment. If you are familiar
with git and use an IDE, you can achieve the same outcome in a
different way. Here, we listed the simple terminal way of setting it up.

Steps to Contribute a Rock-on with a Pull Request
-------------------------------------------------

Rebase your master branch before making your own changes.

.. code-block:: console

    cd rockon-registry
    git checkout master
    git pull --rebase upstream master

Checkout a new/separate branch for your Rock-on

.. code-block:: console

   git checkout -b rockon_name

Add and commit your Rock-on to git. Say you are updating the
**Syncthing** Rock-on and have the :code:`syncthing.json` tested
and ready to go. First copy the file over to your repo. Next,

.. code-block:: console

    git add syncthing.json
    git commit -m 'update syncthing rock-on'

When adding a new Rock-on, e.g. based on the fictious **moonshine**
docker image and created the new file :code:`moonshine.json`, also
add the name of this file (case-sensitive) to the :code:`root.json`
file (it's alphabetically sorted). This means you add both files to
the commit,

.. code-block:: console

    git add moonshine.json root.json
    git commit -m 'add moonshine rock-on`

Now you can push your Rock-on to github. :code:`<branch_name>` is from
above where you checked out a new branch.

.. note::

   When updating to a new version (as mentioned in scenario 2 in the
   :ref:`addvsupdrockon` section, first submit a pull request adding
   the new Rock-On (you will have to use a slightly different name).
   Then follow the :ref:`deleterockons` process. This way, the history
   more clearly represents what transpired with this Rock-on.

.. code-block:: console

    git push origin <branch_name>

Now you can go to github, open an issue on the rockstor repo if you have
not done so already that describes the Rock-on that you were working on
and then open a pull request from your forked repo, populate it with the
requested info (e.g., link it to a previously opened issue) and
submit it.

.. _deleterockons:

Deleting a Rock-on
==================

The Rock-ons repository is predominantly community maintained/led.
As such we depend on community involvement to maintain its health.
On occasions a Rock-on will fall into disrepair.
If you find such a Rock-on, *i.e.* broken or built on an abandoned/deprecated
docker image, then please report this on our `friendly forum
<https://forum.rockstor.com/>`_. If there is then no community will/effort to
maintain/repair that rock-on, then we will happily accept a pull request to
delete it. Such a pull request would include the removal/deletion of the
associated JSON definition file and its associated entry within the
:code:`root.json` file. Please reference the relevant forum discussion upon
submitting such a pull request and limit each such Rock-on delete request to a
single Rock-on. Such 'weeding' is definitely encouraged and contributes to the
overall health of this repository and the project as a whole. It's always
frustrating to find something broken and if the community will is not there to
repair it, then it's best removed. We have in the past neglected to stress this
side of the community maintenance 'feedback' and are now moving to actively
encourage this much needed 'weeding'.
