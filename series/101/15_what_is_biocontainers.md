---
title: 'BioContainers?'
layout: series_item
series: '101'
permalink: /101/what_is_biocontainers/
estimated-time: 5
---

![Containers]({{ site.baseurl}}/img/series/101/docker-gif.gif){:height="250px" class="center"}
{:style="font-size: 9px; text-align: center"}  


Basically a software container <i class="fa fa-archive" aria-hidden="true"></i> is used to encapsulate a software component and the correponding dependencies. You don't start from scratch or
install all the software over and over.


>Container-based virtualization, also called operating system virtualization, is an approach to virtualization in which the virtualization layer.
>runs as an application within the operating system (OS). In this approach, the operating system's kernel runs on the hardware node with several
>isolated guest virtual machines (VMs) installed on top of it. The isolated guests are called containers.


What exactly is a Container?
----------------------------

Is a __Independently deployable bits of code__ that can be used to build and run agile applications. It could be anything from a FASTA parser, a tree algorithm or a simple visualization module.


- Containers encapsulate discrete components of application logic provisioned only with the minimal resources needed to do their job.

- Containers are easily packaged, lightweight and designed to run anywhere

- Multiple containers can be deployed in a single VM.

Lets install a container quickly:

{% hlblock info %}
`docker pull biocontainers/dia-umpire` This simple sentence install dia-umpire and all its dependencies
{% endhlblock %}

Containers are build from existing operating systems. They are different from Virtual machines because they don't posses an entire guest OS inside, instead, containers are build using optimized system
libraries and use the host OS memory management and process controls. Containers normally are centralized around a specific
software and you can make them executable by instantiating images from them.

![What is Container](https://raw.githubusercontent.com/BioContainers/specs/master/imgs/container.png)

### What do I need to use a container?

Most of the time when a bioinformatics analysis is performed, several bioinformatics tools and software should be installed and
configure. This process can take several hours and demand a lot of efforts including the installation of multiple dependencies
and tools. BioContainers provides ready to use packages and tools that can be easily deployed and used in local machines, HPC and cloud architectures.


What is BioContainers?
----------------------

<a href="http://biocontainers.pro">BioContainers</a> is a community-driven project that provides the infrastructure and basic guidelines to create, manage and distribute Bioinformatics containers with special focus in Proteomics, Genomics, Transcriptomics and Metabolomics.
BioContainers is based on the popular frameworks **Docker framework** and **rkt**. A revolutionary platforms for developers and sysadmins to build, ship, and run applications
anywhere. For example, with Docker you can build an image containing your software and all dependencies and ship it ready to use (see <a href="#what-is-docker">Details</a>).

## BioContainers Goals

* Provide a base specification and images to easily build and deploy new bioinformatics/proteomics software
including the source and examples.

* Provide a series of containers ready to be used by the bioinformatics community (https://github.com/BioContainers/containers).

* Define a set of guidelines and specifications to build a standardized container that can be
used in combination with other containers and bioinformatics tools.

* Define a complete infrastructure to develop, deploy and test new bioinformatics containers
using continuous integration suites such as Travis Continuous Integration (https://travisci.
org/), Shippable (https://app.shippable.com/) or manually built solutions.

* Provide support and help to the bioinformatics community to deploy new containers for researchers that do not have bioinformatics support.

* Provide guidelines and help on how to create reproducible pipelines by defining, reusing
and reporting specific container versions which will consistently produce the exact same
result and always be available in the history of the container.

* Coordinate and integrate developers and bioinformaticians to produce best practice of
documentation and software development.

<img class="splashIcon" src="{{ site.baseurl}}/img/series/101/toolbox-color.png"> BioContainers is an open source and community-driven framework which provides system-agnostic executable environments for bioinformatics software with special focus on proteomics, genomics, metabolomics and transcriptomics.[BioContainers](http://biocontainers.pro) is based on
the popular **Docker framework** that allows software to be installed and executed under an isolated and controllable environment. BioContainers is based in four main components:

- [Containers](https://github.com/BioContainers/containers) provides all the containers maintained by the BioContainers community and ready to be use by the community.    

- [Biocontainers Registry](https://biocontainers.pro/registry) is hosted registry of all biocontainers images that are ready to be use.

- [Specifications](https://github.com/BioContainers/specs) define a set of guidelines and rules to contribute with BioContainers.


<!--
* Easy to start:
* Easy to test
-->

What you get using BioContainers
--------------------------------

In the next video you can check out what you can achieve by using docker containers:


<iframe width="100%" height="600px" src="https://www.youtube.com/embed/aLipr7tTuA4" frameborder="0"></iframe>
