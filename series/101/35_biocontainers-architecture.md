---
title: 'BioContainers Architecture'
layout: series_item
series: '101'
permalink: /101/biocontainers-architecture/
estimated-time: 20
---

The latest information about BioContainers is available via [https://BioContainers.pro](https://Biocontainers.pro/)


[![Join the chat at https://gitter.im/BioContainers/Lobby](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/BioContainers/BioContainers?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


Containers
--------
Repository of approved bioinformatics containers

Links:
-------
Web Page              : http://biocontainers.pro/

Project Definition    : https://github.com/BioContainers/specs

Contribution Rules    : https://github.com/BioContainers/specs/blob/master/CONTRIBUTING.md

Wiki of the project   : https://github.com/BioContainers/specs/wiki

Containers            : https://github.com/BioContainers/containers

Containers Development: https://github.com/BioContainers/sandbox

Email                 : biodockers@gmail.com

License
----------

[Apache 2](http://www.apache.org/licenses/LICENSE-2.0)

Contents
----------

  1. [BioContainers Architecture](#24-biocontainers-architecture)
  2.4.1 [How to Request a Container](#241-how-to-request-a-container)  
  2.4.2 [Use a Container](#242-use-a-bioContainer.)      
* [Developing containers](#3-developing-containers)  
  3.1. [What do I need to develop?](#31-what-do-i-need-to-develop)  
  3.2. [How to create a container?](#32-how-to-create-a-container)  
* [Support](#4-support)  
  4.1  [Get involved](#41-get-involved)  


### 1. BioContainers Architecture

BioContainers is a community-driven project that allows bioinformatics to request, build and deploy bioinformatics tools using containers. The following figure
present the general BioContainers workflow:

![What is Container](https://raw.githubusercontent.com/BioContainers/specs/master/imgs/workflow.png)

The next sections explain in details the presented workflow:

 * (i) How to request a workflow
 * (ii) Use a BioContainer
 * (iii) Developing containers


#### 2.4.1 How to Request a Container

Users can request a container by opening an issue in the [containers repository] (http://github.com/BioContainers/containers/issues) `(In the previous workflow this is the first step performed by user henrik)`. The issue
should contains the name of the software, the url of the code or binary to be package and information about the software [see BioContainers specification](http://github.com/BioContainers/container-specs.md). When the containers
is deploy and fully functional, the issue will be close by the developer or the contributor to BioContainers.

#### 2.4.2 Use a BioContainer.

When a container is deploy and the developer close the issue in GitHub the user `(henrik)` received a notification that the container is ready.
The user can then used [docker](http://www.docker.com) or [rkt](https://coreos.com/rkt/docs/latest/) to pull or fetch the corresponding container.


3. Developing containers
-----------------------

### 3.1. How to build BioContainer's

There are two different ways to build a container.

* Go to the GitHub repository with the recipe of the software you want, clone it, and build it yourself on your machine.
* Use the docker daemon to search for a ready-to-use version of the containerized software you want.

Inside the central repository there is a list of softwares with docker recipes, there you can find more information about how to work with them.

### 3.2. What do I need to develop?

BioContainers are based on Linux systems, so you will need a computer with Linux installed, you also will need the `docker` or `rkt` daemon and the software you want to containerize.

### 3.3. How to create a Docker based Biocontainer?

Having all in hands now you need to create a Dockerfile. Dockerfiles are simple recipes to instruct the daemon on how to set an appropriate OS and how to download, manage, install and
give access to the software inside.

You can check the [Docker](https://docs.docker.com/reference/builder/) documentation for more information.

Once the container is ready you can get in touch with us so we can make the appropriate arrangements to make your container available to everyone in the community by giving an automated build system.

### 3.3. How to create a rkt based Biocontainer?

Having all in hands now you need to create a rkt. rkt containers are simple recipes to instruct the daemon on how to set an appropriate OS and how to download, manage, install and
give access to the software inside.

You can check the [rkt](https://github.com/coreos/rkt/blob/master/Documentation/getting-started-guide.md) documentation for more information.

Once the container is ready you can get in touch with us so we can make the appropriate arrangements to make your container available to everyone in the community by giving an automated build system.


4. Support
----------

### 4.1. Get involved

Whether you want to make your own software available to others as a container, to just use them on your pipelines and analysis or just give opinions, you are most welcome. This is a community-driven project, that means everyone has a voice.

Here are some general ideas:

* Browse our list of containers
* Propose your own ideas or software
* Interact with other if you think there is something missing.
