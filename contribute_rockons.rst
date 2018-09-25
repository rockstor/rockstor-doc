.. _contributerockons:

Contributing to Rockstor Rock-ons
======================================

Rock-ons are Docker plugins (see :ref:`rockons_intro` for more information) 
defined by a JSON file stored in the **rockon-registry** repository on 
`github.com <https://github.com/rockstor/rockon-registry>`_. As detailed
in the :ref:`adding_rockons` section, please refer to rockon-registry `README.md <https://github.com/rockstor/rockon-registry/blob/master/README.md>`_ 
for full instructions and examples on how to write your own Rock-on definition file.

If you are interested in donating a Rock-on for your favorite project, please 
consider contributing to the `rockon-registry <https://github.com/rockstor/rockon-registry>`_ 
by submitting a pull-request. Steps for doing so are similar to those required 
for :ref:`contributetorockstor` or :ref:`contributedocs`. Briefly, these would 
consist in: 

1. Creating an *issue* in the **rockon-registry** repository.
2. Creating your own *fork* of the **rockon-registry**.
3. Create a *new branch* dedicated to the issue you just created (ideally containing the 
   issue #).
4. Write your Rock-on JSON definition file following the `README.md <https://github.com/rockstor/rockon-registry/blob/master/README.md>`_ 
   as guideline.
5. Once you're finished writing and testing your new Rock-on definition file, upload it 
   to this branch.
6. Submit a *pull-request* to the **rockon-registry** repository. 

Which Docker image should I use?
--------------------------------

`Docker hub <https://hub.docker.com>`_ centralizes a very large number 
of docker images. As a result, it can sometimes be difficult to select the 
best image among dozens for very popular projects. While it is nearly 
impossible to provide a simple "rule" for selecting the best image, the best 
image for a Rock-on will be secure, maintained in the long-term, compatible 
with Rockstor, and allow for "all-in-one" use for the end-user. In this context, 
the following guidelines can help: 

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
