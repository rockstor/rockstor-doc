.. _contributerockons:

Contributing a Rock-on
======================

Rock-ons are Docker plugins (see :ref:`rockons_intro` for more information)
defined by a JSON file stored in the **rockon-registry** repository on
`github.com <https://github.com/rockstor/rockon-registry>`_.
As detailed in the :ref:`adding_rockons` section,
please refer to the rockon-registry `README.md
<https://github.com/rockstor/rockon-registry/blob/master/README.md>`_ for full
instructions and examples on how to write your own Rock-on definition file.

If you are interested in contributing a Rock-on to enable your chosen project
on Rockstor, please submit a pull-request to the `rockon-registry
<https://github.com/rockstor/rockon-registry>`_. Steps for doing so are similar
to those required for :ref:`contributetorockstor` or :ref:`contributedocs`. If
you are familiar with git, then working on an issue branch in a local clone of
your GitHub fork is favoured. If you are not then the following is a quick and
easy method but far less flexible.

A GitHub account is required.

1. Create a *New issue* (button) in the **rockon-registry** `issues section
   <https://github.com/rockstor/rockon-registry/issues>`_ and explain what you
   are proposing.
2. Creating your own *Fork* (button) of the `rockon-registry
   <https://github.com/rockstor/rockon-registry>`_ (GitHub login required).
3. Write and test your Rock-on JSON definition file following the `README.md
   <https://github.com/rockstor/rockon-registry/blob/master/README.md>`_.
4. In your forked copy on GitHub select **create new file** (button) and paste
   your JSON file and name it (no spaces).
5. Before **Commit new file** (button), ensure **"Create a new branch for this
   commit and start a pull request..."** is selected.
6. After the selection in 5. change the suggested branch name to e.g. **"#1234
   Add project Y as Rock-on"** where the number is that of your issue.

You are then ready to **Propose new file** (button). Please then read and edit,
the presented pull request appropriately; you can always edit it later.

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
