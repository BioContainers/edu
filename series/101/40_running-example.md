---
title: 'BioContainer example'
layout: series_item
series: '101'
permalink: 101/running-example/
estimated-time: 5
---

{% alert warn %}
We will run the first example with blast. The Basic Local Alignment Search Tool for comparing primary biological sequence 
information, such as the amino-acid sequences of different proteins or the nucleotides of DNA sequences.
We chose blast becuase is one of the most used and uaseful software in bioinformatics. 
{% endalert %}

First step to be able to run any software is to install it. This can be a difficult and challenged process starting by download 
the software, dependencies, etc; installation of multiple packages; dealing with depencencies craches, etc. See all the steps 
to install `blast` [here](https://www.ncbi.nlm.nih.gov/books/NBK279671/).  

Here is, where **BioContainers** plays his major role. See how to download and "install" blast in your local machine:

~~~
docker pull biodckr/blast
~~~

This is the docker and containers magic, the software is distributed with all the dependencies and shared OS needed to run. 

<img class="splashIcon" src="{{ site.baseurl}}img/series/101/what.gif">

Docker allows applications to be isolated into containers with instructions for exactly what they need to survive that can be easily ported
from machine to machine. If you have 30 Docker containers that you want to run, you can run them all on a single VM. 

{% alert info %}
 In contrast (for example) to run 30 virtual machines, you’ve got to boot 30 operating systems with at least minimum resource
 requirements available before factoring the hypervisor for them to run on with the base OS.
{% endalert %}

### Running blast 

~~~
docker run biodckr/blast blastp -help
~~~

This will print the help page for `blastp` tool. The first part of the command `docker run biodckr/blast` enable docker 
to identified the correct container in your local registry. The second part `blastp -help` is the command that you want to
use in the container.

{% alert info %}
 If you want to [list all the containers/images](https://docs.docker.com/engine/reference/commandline/images/) you have pull from public repositories and are available in your 
 local machine, you can use the following command: `$ docker images`
{% endalert %}
 
