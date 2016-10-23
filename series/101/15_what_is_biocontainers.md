---
title: 'BioContainers?'
layout: series_item
series: '101'
permalink: 101/what_is_biocontainers/
estimated-time: 5
---

![Containers]({{ site.baseurl}}img/series/101/docker-gif.gif){:height="250px" class="center"}
{:style="font-size: 9px; text-align: center"}  


Basically a software container <i class="fa fa-archive" aria-hidden="true"></i> is used to encapsulate a software component and the correponding dependencies. You don't start from scratch or install all the software over and over. 


>Container-based virtualization, also called operating system virtualization, is an approach to virtualization in which the virtualization layer
>runs as an application within the operating system (OS). In this approach, the operating system's kernel runs on the hardware node with several
>isolated guest virtual machines (VMs) installed on top of it. The isolated guests are called containers. 


What exactly is a BioContainer?
-------------------------------

Is a __Independently deployable bits of code__ that can be used to build and run agile applications. It could be anything from a FASTA parser, a tree algorithm or a simple visualization module.


- Containers encapsulate discrete components of application logic provisioned only with the minimal resources needed to do their job.
- Containers are easily packaged, lightweight and designed to run anywhere
- Multiple containers can be deployed in a single VM.

Lets install a container quickly: 

{% hlblock info %}
`docker pull biodckr/dia-umpire` This simple sentence install dia-umpire and all its dependencies
{% endhlblock %}


What is BioContainers?
----------------------

<a href="http://biocontainers.pro">BioContainers</a> is a community-driven project that provides the infrastructure and basic guidelines to create, manage and distribute Bioinformatics Docker containers with special focus in Proteomics, Genomics, Transcriptomics and Metabolomics.
BioDocker is based in the popular <a href="#what-is-docker">Docker framework</a>. A revolutionary platform for developers and sysadmins to build, ship, and run applications
anywhere. With Docker you can build an image containing your software and all dependencies and ship it ready to use (see <a href="#what-is-docker">Details</a>).

## BioContainers Goals

BioContainers community and project have three major goals:
 <ul>
  <li>A central registry with containers ready to be use: <a href="http://biocontainers.pro/registry">The BioContainers Registry</a></li>
  <li>Specifications about how to create a BioContainers container/image and infrastructure to deploy them.</li>
  <li>A complete infrastructure create, share and request docker images from bioinformatics software</li>
 </ul>

[BioContainers containers](https://github.com/BioContainers/containers)facilitate the usage, integration and reproducibility of software and algorithms into more comprehensive bioinformatics pipelines. 
Finally, we presented the guidelines and specifications to create a container, contribute to the group or request a container from the group. Our guidelines and specifications are part of community efforts like [open-containers](https://github.com/opencontainers) ando [Bioconda](https://bioconda.github.io/) to make installation, addition, evaluation and benchmarking of new algorithms and
tools accessible to researchers, minimizing the efforts for installation and configuration.



<img class="splashIcon" src="{{ site.baseurl}}img/series/101/toolbox-color.png"> BioContainers is an open source and community-driven framework which provides system-agnostic executable environments for bioinformatics software with special focus on proteomics, genomics, metabolomics and transcriptomics.[BioContainers](http://biocontainers.pro) is based on
the popular **Docker framework** that allows software to be installed and executed under an isolated and controllable environment. BioContainers is based in four main components:

- [Containers](https://github.com/BioContainers/containers) provides all the containers maintained by the BioContainers community and ready to be use by the community.    

- [Biocontainers Registry](https://biocontainers.pro/registry) is hosted registry of all biocontainers images that are ready to be use.

- [BioDocker SandBox](https://github.com/BioContainers/sandbox) is used to host all the new software, broken containers. Users can ask for a new container by creating a new [issue](https://github.com/BioDocker/sandbox/issues). 
Also developers can contribute with the group by generating a container for the requested software. 

- [Specifications](https://github.com/BioContainers/specs) define a set of guidelines and rules to contribute with BioContainers.


<!--
* Easy to start:
* Easy to test
-->

What you get using BioContainers
--------------------------------

In the next video you can check out what you can achieve by using docker containers:


<iframe width="100%" height="600px" src="https://www.youtube.com/embed/aLipr7tTuA4" frameborder="0"></iframe>
