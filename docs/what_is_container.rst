What is a Container?
======================

Basically a software container is used to encapsulate a software component and the corresponding dependencies. You don't start from scratch or install all the software over and over. It contains **independently deployable bits of code** that can be used to build and run agile applications. It could be anything from a FASTA parser, a tree algorithm or a simple visualization module.

-  Containers encapsulate discrete components of application logic provisioned only with the minimal resources needed to do their job.

-  Containers are easily packaged, lightweight, and designed to run anywhere.

Let's install a container quickly:

  .. code-block:: bash

   $ docker pull biocontainers/dia-umpire:v1.4256_cv2

  .. note:: This simple command installs dia-umpire and all its dependencies

Containers are built from existing operating systems. They are different from virtual machines because they don't posses an entire guest OS inside; instead, containers are built using optimized system libraries and use the host OS memory management and process controls. Containers normally are centralized around a specific software and you can make them executable by instantiating images from them.

.. image:: images/container.png
   :alt: What is Container

Why should I use a container?
-----------------------------

Most of the time when a bioinformatics analysis is performed, several bioinformatics tools and software should be installed and configured. This process can take several hours and demand a lot of effort including the installation of multiple dependencies and tools. BioContainers provide ready-to-use packages and tools that can be easily deployed and used on local machines, HPC and cloud architectures.

In the next video you can check out what you can achieve by using docker containers:

.. raw:: html

   <iframe width="100%" height="600px" src="https://www.youtube.com/embed/aLipr7tTuA4" frameborder="0"></iframe>

.. raw:: html
   </b>

Container technologies
----------------------

BioContainers has been built around three main technologies: **Conda**, **Docker** and **Singulatiry**. The BioContainers Community release for every bioinformatics software containers in these three technologies or flavours.

.. note:: We do not provide detailed documentation about these three technologies because that can be found on their corresponding web sites, although we may explain some concepts important for understanding BioContainers as needed.

Conda
~~~~~~~~~~

`Conda <https://conda.io/>`__ is an open source package management system and environment management system that runs on Windows, macOS and Linux. Conda quickly installs, runs and updates packages and their dependencies. It was created for Python programs, but it can package and distribute software for any language.


Docker
~~~~~~~~~~

`Docker <https://www.docker.com/>`__ provides container software that is ideal for developers and teams looking to get started and experimenting with container-based applications. It provides an integrated container-native development experience; and access to the largest library of community and certified Linux and Windows Server content from Docker Hub.

Singularity
~~~~~~~~~~~~~

`Singularity <https://www.sylabs.io/docs/>`__ enables users to have full control of their environment. Singularity containers can be used to package entire scientific workflows, software and libraries, and even data. This means that you don’t have to ask your cluster admin to install anything for you - you can put it in a Singularity container and run.

