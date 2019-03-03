What is a Container?
======================

Basically a software container is used to encapsulate a software component and the corresponding dependencies. You don't start from scratch or install all the software over and over.

  .. note:: Container-based virtualization, also called operating system virtualization, is an approach to virtualization in which the virtualization layer runs as an application within the operating system (OS). In this approach, the operating system's kernel runs on the hardware node with several isolated guest virtual machines (VMs) installed on top of it. The isolated guests are called containers.

What is a Container in details
----------------------------

It contains **independently deployable bits of code** that can be used to build and run agile applications. It could be anything from a FASTA parser, a tree algorithm or a simple visualization module.

-  Containers encapsulate discrete components of application logic provisioned only with the minimal resources needed to do their job.

-  Containers are easily packaged, lightweight, and designed to run anywhere

-  Multiple containers can be deployed in a single VM.

Let's install a container quickly:

  .. code-block:: bash

   $ docker pull biocontainers/dia-umpire:v1.4256_cv2

  .. note:: This simple command installs dia-umpire and all its dependencies

Containers are build from existing operating systems. They are different from virtual machines because they don't posses an entire guest OS inside, instead, containers are build using optimized system libraries and use the host OS memory management and process controls. Containers normally are centralized around a specific software and you can make them executable by instantiating images from them.

.. image:: images/container.png
   :alt: What is Container

Why should I use a container?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Most of the time when a bioinformatics analysis is performed, several bioinformatics tools and software should be installed and configured. This process can take several hours and demand a lot of effort including the installation of multiple dependencies and tools. BioContainers provide ready-to-use packages and tools that can be easily deployed and used on local machines, HPC and cloud architectures.

What you get using Container
--------------------------------

In the next video you can check out what you can achieve by using docker containers:

.. raw:: html

   <iframe width="100%" height="600px" src="https://www.youtube.com/embed/aLipr7tTuA4" frameborder="0"></iframe>

