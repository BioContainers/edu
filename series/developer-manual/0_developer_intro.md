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

BioContainers has two major ways of creating containers: **Dockefile based images** and **mulled images**

### Developing Dockerfile based containers

The first method correspond to the traditional way of creating a container. In order to do that we will need to create something
called Dockerfile. But first, lets review each step necessary before having a Docker container.

1) Install Docker

Make sure that you have the docker daemon installed on your system. You can check [here](http://biocontainers.pro/docs/101/getting_started/) for more information on how to find the proper
guidelines for you.

2) Have a Software to Work with

Make sure you have a piece of software capable of being containerized. The BioContainers base image is based
on an Ubuntu distribution, so your software and its libraries must be compatible to Linux.

3) Read the Documentation

For a Docker container you basically need a simple Dockerfile, but our BioContainers project is based on a series
of specifications and guidelines, so before start creating your Dockerfile we suggest you to read our [documentation](http://biocontainers.pro/docs/developer-manual/biocontainers-dockerfile/)
first, there you will find out, amongst other things, how to create a Dockerfile compatible with BioContainers.

4) Adding Things to the Container
Once you have everything in place, you need now to figure out how to add your software to the container. There are different ways of doing this; if you software is available via apt install, you can do that and the software will be available inside the container. If that's not your case you have a few other options:

  * You can push the software file inside the container using the Dockerfile directives called `ADD` or `COPY` ([example](https://github.com/BioContainers/containers/blob/master/pia/1.1.0-SNAPSHOT/Dockerfile)).
  * You can host the software somewhere on-line and download it via command line inside the container ([example](https://github.com/BioContainers/containers/blob/master/comet/2016012/Dockerfile)).
  * You can you use other solutions like Conda to download your software ([example](https://github.com/BioContainers/containers/blob/master/blast/2.2.31/Dockerfile), also see below).

5) Build the Container
In order to build the container you need to use the docker daemon with the `build` command:

~~~
$ docker build -t <name> <folder_with_dockerfile>
~~~

So, if you are running this command in the same folder the Dockerfile is, we can type something like this:

~~~
$docker build -t MyApp .
~~~

In the following minutes you will see the log output from the docker daemon while it builds your container.

6) Run it!, Test it!
Once the container is ready you should test it, try to run your program using the `run` command, check if all its functionalities are in order.

7) contribute
If everything looks OK, you can contribute to the BioContainers project by sending us your **Dockerfile**. You can follow the instructions we have [here](https://github.com/BioContainers/containers/blob/master/blast/2.2.31/Dockerfile), and after **ready**, your software will be available using the docker daemon fetch command. 

### Developing mulled containers

BioContainers offers a very easy way to create efficient containers that are minimal in size,
tested and not rely on writing a Dockerfile.

The preferred way to do this is to write a [conda package](https://conda.pydata.org)
and submit this it the BioConda communtiy. As soon as your PR is merged and continues
integration testing was successful, we will build you automatically a container and publish
it at [quay.io/biocontainers](https://quay.io/organization/biocontainers).

The BioConda specification [Contribution Guide](https://bioconda.github.io/contributing.html) define how to create a recipe. In summary,
a BioConda recipe should contain the following parts ():

- Source URL is stable (details)
- md5 or sha256 hash included for source download (details)
- Appropriate build number (details)
- .bat file for Windows removed (details)
- Remove unnecessary comments (details)
- Adequate tests included
- Files created by the recipe follow the FSH (details)
- License allows redistribution and license is indicated in meta.yaml
- Package does not already exist in the defaults, r, or conda-forge channels with some
  exceptions (details)
- Package is appropriate for bioconda
- If the recipe installs custom wrapper scripts, usage notes should be added to ```extra -> notes``` in the meta.yaml.

Example Yaml for bowtie2:

~~~

package:
  name: unicycler
  version: 0.3.0b

build:
  number: 0
  skip: True # [py27]

source:
  fn: unicycler_0.3.0b.tar.gz
  url: https://github.com/rrwick/Unicycler/archive/906a3e7f314c7843bf0b4edf917593fc10baee4f.tar.gz
  md5: 5f06d2bd8ef5065c8047421db8c7895f

requirements:
  build:
  - python
  - setuptools
  - gcc

  run:
  - python
  - libgcc
  - spades >=3.6.2
  - pilon
  - java-jdk
  - bowtie2
  - samtools >=1.0
  - blast
  - freebayes

test:
  commands:
    - unicycler -h
    - unicycler_align -h
    - unicycler_check -h
    - unicycler_polish -h

about:
  home: https://github.com/rrwick/Unicycler
  license: GPL-3.0
  license_file: LICENSE
  summary: 'Hybrid assembly pipeline for bacterial genomes'
~~~

When the recipe is ready a Pull Request should be created (https://bioconda.github.io/contribute-a-recipe.html#push-changes-wait-for-tests-to-pass-submit-pull-request). Finally
the container is automatically created for the new BioConda Package.
