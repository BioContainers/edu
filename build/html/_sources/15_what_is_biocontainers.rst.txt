|Containers|\ {:height="250px" class="center"} {:style="font-size: 9px;
text-align: center"}

Basically a software container is used to encapsulate a software
component and the correponding dependencies. You don't start from
scratch or install all the software over and over.

    Container-based virtualization, also called operating system
    virtualization, is an approach to virtualization in which the
    virtualization layer runs as an application within the operating
    system (OS). In this approach, the operating system's kernel runs on
    the hardware node with several isolated guest virtual machines (VMs)
    installed on top of it. The isolated guests are called containers.

What exactly is a Container?
----------------------------

It contains **independently deployable bits of code** that can be used
to build and run agile applications. It could be anything from a FASTA
parser, a tree algorithm or a simple visualization module.

-  Containers encapsulate discrete components of application logic
   provisioned only with the minimal resources needed to do their job.

-  Containers are easily packaged, lightweight, and designed to run
   anywhere

-  Multiple containers can be deployed in a single VM.

Let's install a container quickly:

{% hlblock info %} ``docker pull biocontainers/dia-umpire`` This simple
command installs dia-umpire and all its dependencies {% endhlblock %}

Containers are build from existing operating systems. They are different
from virtual machines because they don't posses an entire guest OS
inside, instead, containers are build using optimized system libraries
and use the host OS memory management and process controls. Containers
normally are centralized around a specific software and you can make
them executable by instantiating images from them.

.. figure:: https://raw.githubusercontent.com/BioContainers/specs/master/imgs/container.png
   :alt: What is Container

   What is Container
Why should I use a container?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Most of the time when a bioinformatics analysis is performed, several
bioinformatics tools and software should be installed and configured.
This process can take several hours and demand a lot of effort including
the installation of multiple dependencies and tools. BioContainers
provide ready-to-use packages and tools that can be easily deployed and
used on local machines, HPC and cloud architectures.

What are BioContainers?
-----------------------

 BioContainers is a community-driven project that provides the
infrastructure and basic guidelines to create, manage and distribute
bioinformatics containers with special focus on proteomics, genomics,
transcriptomics and metabolomics. BioContainers are based on the popular
frameworks **Docker framework** and **rkt**. A revolutionary platform
for developers and sysadmins to build, ship, and run applications
anywhere. For example, with Docker you can build an image containing
your software and all dependencies and ship it ready to use (see
Details).

BioContainers Goals
-------------------

-  Provide a base specification and images to easily build and deploy
   new bioinformatics/proteomics software including the source and
   examples.

-  Provide a series of containers ready to be used by the bioinformatics
   community (https://github.com/BioContainers/containers).

-  Define a set of guidelines and specifications to build a standardized
   container that can be used in combination with other containers and
   bioinformatics tools.

-  Define a complete infrastructure to develop, deploy and test new
   bioinformatics containers using continuous integration suites such as
   Travis Continuous Integration (https://travisci. org/), Shippable
   (https://app.shippable.com/) or manually built solutions.

-  Provide support and help to the bioinformatics community to deploy
   new containers for researchers that do not have bioinformatics
   support.

-  Provide guidelines and help on how to create reproducible pipelines
   by defining, reusing and reporting specific container versions which
   will consistently produce the exact same result and always be
   available in the history of the container.

-  Coordinate and integrate developers and bioinformaticians to produce
   best practices of documentation and software development.

Main components of BioContainers:
---------------------------------

-  `Containers <https://github.com/BioContainers/containers>`__ provides
   all the containers maintained by the BioContainers community and
   ready to be used by the community.

-  `Biocontainers Registry <https://biocontainers.pro/registry>`__ is a
   hosted registry of all biocontainers images that are ready to be
   used.

-  `Specifications <https://github.com/BioContainers/specs>`__ defines a
   set of guidelines and rules to contribute with BioContainers.

.. raw:: html

   <!--
   * Easy to start:
   * Easy to test
   -->

What you get using BioContainers
--------------------------------

In the next video you can check out what you can achieve by using docker
containers:

.. raw:: html

   <iframe width="100%" height="600px" src="https://www.youtube.com/embed/aLipr7tTuA4" frameborder="0"></iframe>

.. |Containers| image:: {{%20site.baseurl}}/img/series/101/docker-gif.gif
