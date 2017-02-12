---
title: 'Developer Intro'
layout: series_item
series: 'developer-manual'
permalink: /developer-manual/developer-intro/
estimated-time: 5
---

Before stating to contribute to BioContainers you should check your system for the following dependencies:

* [Git](https://github.com) is a version control system that will keep track of the changes you have made in code.

{% hlblock info %}
If you want to fresh up your `git` skills, check out the [Full Introduction for Bioinformatics](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004947) or [15 minutes interactive lesson](https://try.github.io/levels/1/challenges/1) by Codeschool.
{% endhlblock %}


Developing containers
-----------------------

BioContainers has two major ways of creating containers: **Dockefile based images** and **DockerFile less images**

### Developing Dockerfile based containers



### Developing Dockerfile-less containers

BioContainers offers a very easy way to create effcient containers that are minimal in size, tested and not rely on writing a Dockerfile. The preferred way to do this is to write a [conda package](https://conda.pydata.org) and submit this it the bioconda communtiy. As soon as your PR is merged and continues integration testing was successful, we will build you automatically a container and publish it at [quay.io/biocontainers](https://quay.io/organization/biocontainers). To read more about the conda packaging format, which we think has many advantages over plain Dockerfiles, can read the [Contribution Guide](https://bioconda.github.io/contributing.html) of BioConda or the even more detailed [Conda build](http://conda.pydata.org/docs/building/) documentation. 
