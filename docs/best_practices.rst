Best Practices
==============

The  BioContainers community develop and build guidelines to create, build containers. Here, we describe the guidelines to create Dockerfile containers. If you are interested to read more about BioContainers guidelines, you can follow our recent manuscript in `F1000 <https://f1000research.com/articles/7-742/v1>`__.

- Gruening, B., Sallou, O., Moreno, P., da Veiga Leprevost, F., Ménager, H., Søndergaard, D., Röst, H., Sachsenberg, T., O'Connor, B., Madeira, F. and Del Angel, V.D., BioContainers Community, Perez-Riverol Y. 2018. `Recommendations for the packaging and containerizing of bioinformatics software <https://f1000research.com/articles/7-742/v2>`__. F1000Research, 7.

Language Specific
-----------------

Python
^^^^^^

* Use requirements.txt instead of listing dependencies
* Define library versions


Optimization
------------

* Use environment variables to avoid repeating yourself

This is a trick I picked up from reading the Dockerfile (link) of the "official" node.js docker image. As an aside, this Dockerfile is great. My only criticism is that it sits on top of a huge buildpack-deps (link) image, with all sorts of things I don't want or need.

You can define environment variables with ENV and then reference them in subsequent RUN commands. Below, I've paraphrased an excerpt from the linked Dockerfile:

.. code-block:: bash


   ENV NODE_VERSION 0.10.32

   RUN curl -SLO "http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" && \
       tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 && \
       rm "node-v$NODE_VERSION-linux-x64.tar.gz"


**Merge RUN commands**

instead of running:

.. code-block:: bash

   RUN acb
   RUN cbd
   RUN bde

run:

.. code-block:: bash

   RUN acb && cbd && bde

or:

.. code-block:: bash

   RUN acb && \
       cbd && \
       bde

.. note::
   * Whenever possible, reuse the same base image and use a LTS (Long Term Support) image preferably (Ubuntu 12.04 or 14.04)
   * You can use our biocontainers/biocontainers image based on ubuntu 14.04 with frequent updates and default folders created.
   * Use a .dockerignore file: In most cases, it’s best to put each Dockerfile in an empty directory. Then, add to that directory only the files needed for building the Dockerfile.
   * Avoid installing unnecessary packages: In order to reduce complexity, dependencies, file sizes, and build times, you should avoid installing extra or unnecessary packages just because they might be “nice to have.” For example, you don’t need to include a text editor in a database image.
   * Run only one process per container: In almost all cases, you should only run a single process in a single container. Decoupling applications into multiple containers makes it much easier to scale horizontally and reuse containers. If that service depends on another service, make use of container linking.
   * Minimize the number of layers: You need to find the balance between readability (and thus long-term maintainability) of the Dockerfile and minimizing the number of layers it uses. Be strategic and cautious about the number of layers you use.
   * Sort multi-line arguments: Whenever possible, ease later changes by sorting multi-line arguments alphanumerically. This will help you avoid duplication of packages and make the list much easier to update. This also makes PRs a lot easier to read and review. Adding a space before a backslash () helps as well.

Here’s an example from the buildpack-deps image:

.. code-block:: bash

   RUN apt-get update && apt-get install -y \
       bzr \
       cvs \
       git \
       mercurial \
       subversion

.. note:: Note: Don't install build tools without good reason: Build tools take up a lot of space, and building from source is often slow. If you're just installing somebody else's software, it's usually not necessary to build from source and it should be avoided. For instance, it is not necessary to install python, gcc, etc. to get the latest version of node.js up and running on a Debian host. There is a binary tarball available on the node.js downloads page. Similarly, redis can be installed through the package manager.

There are at least a few good reasons to have build tools:


* you need a specific version (e.g. redis is pretty old in the Debian repositories).
* you need to compile with specific options.
* you will need to npm install (or equivalent) some modules which compile to binary.

In the second case, think really hard about whether you should be doing that. In the third case, I suggest installing the build tools in another "npm installer" image, based on the minimal node.js image.

Don't leave temporary files lying around

The following Dockerfile results in an image size of 109 MB:

.. code-block:: bash

   FROM debian:wheezy
   RUN apt-get update && apt-get install -y wget
   RUN wget http://cachefly.cachefly.net/10mb.test
   RUN rm 10mb.test

On the other hand, this seemingly-equivalent Dockerfile results in an image size of 99 MB:

.. code-block:: bash

   FROM debian:wheezy
   RUN apt-get update && apt-get install -y wget
   RUN wget http://cachefly.cachefly.net/10mb.test && rm 10mb.test

Thus it seems that if you leave a file on disk between steps in your Dockerfile, the space will not be reclaimed when you delete the file. It is also often possible to avoid a temporary file entirely, just piping output between commands. For instance,

.. code-block:: bash

   wget -O - http://nodejs.org/dist/v0.10.32/node-v0.10.32-linux-x64.tar.gz | tar zxf -


* Clean up after the package manager

If you run apt-get update in setting up your container, it populates /var/lib/apt/lists/ with data that's not needed once the image is finalized. You can safely clear out that directory to save a few megabytes.

This Dockerfile generates a 99 MB image:

.. code-block:: bash

   FROM debian:wheezy
   RUN apt-get update && apt-get install -y wget

while this one generates a 90 MB image:

.. code-block:: bash

   FROM debian:wheezy
   RUN apt-get update && apt-get install -y wget && apt-get clean && apt-get purge && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


* Pin package versions

While a docker image is immutable (and that's great), a Dockerfile is not guaranteed to produce the same output when run at different times. The problem, of course, is external state, and we have little control over it. It's best to minimize the impact of external state on your Dockerfile to the extent that it's possible. One simple way to do that is to pin package versions when updating through a package manager. Here's an example of how to do that:

.. code-block:: bash

   # apt-get update
   # apt-cache showpkg redis-server
   Package: redis-server
   Versions:
   2:2.4.14-1
   # apt-get install redis-server=2:2.4.14-1


* Map log files outside

General
-------


* ADD vs COPY: Both ADD and COPY adds local files when building a container but ADD does some additional magic like adding remote files and ungzipping and untaring archives. Only use ADD if you understand this difference.
* WORKDIR and ENV: Each command will create a new temporary image and runs in a new shell hence if you do a `cd <directory>` or `export <var>=<value>` in your Dockerfile it won't work. Use WORKDIR to set your working directory across multiple commands and ENV to set environment variables.
* CMD and ENTRYPOINT: CMD is the default command to execute when an image is run. The default ENTRYPOINT is /bin/sh -c and CMD is passed into that as an argument. We can override ENTRYPOINT in our Dockerfile and make our container behave like an executable taking command line arguments (with default arguments in CMD in our Dockerfile).
* ADD your code last: ADD invalidates your cache if files have changed. Don't invalidate the cache by adding frequently changing stuff too high up in your Dockerfile. Add your code last, libraries and dependencies first. For node.js apps that means adding your package.json first, running npm install and only then adding your code.
* USER in Dockerfiles: By default docker runs everything as root but you can use USER in Dockerfiles. There's no user namespacing in docker so the container sees the users on the host but only uids hence you need the add the users in the container.
* CMD: The CMD instruction should be used to run the software contained by your image, along with any arguments. CMD should almost always be used in the form of CMD [“executable”, “param1”, “param2”…]. Thus, if the image is for a service (Apache, Rails, etc.), you would run something like CMD ["apache2","-DFOREGROUND"]. Indeed, this form of the instruction is recommended for any service-based image.
* ENV: In order to make new software easier to run, you can use ENV to update the PATH environment variable for the software your container installs. For example, ENV PATH /usr/local/nginx/bin:$PATH will ensure that CMD [“nginx”] just works. The ENV instruction is also useful for providing required environment variables specific to services you wish to containerize, such as Postgres’s PGDATA.
* USER: If a service can run without privileges, use USER to change to a non-root user. Start by creating the user and group in the Dockerfile with something like 

.. code-block:: bash

   RUN groupadd -r postgres && useradd -r -g postgres postgres.

..

   Note: Users and groups in an image get a non-deterministic UID/GID in that the “next” UID/GID gets assigned regardless of image rebuilds. So, if it’s critical, you should assign an explicit UID/GID.
   You should avoid installing or using sudo since it has unpredictable TTY and signal-forwarding behavior that can cause more problems than it solves. If you absolutely need functionality similar to sudo (e.g., initializing the daemon as root but running it as non-root), you may be able to use “gosu”.


Lastly, to reduce layers and complexity, avoid switching USER back and forth frequently.


* WORKDIR: For clarity and reliability, you should always use absolute paths for your WORKDIR. Also, you should use WORKDIR instead of proliferating instructions like RUN cd … && do-something, which are hard to read, troubleshoot, and maintain.

Volumes
-------


* Should always map to the same /data and /config folders
* Should be RW (read/write) unless there's a good reason not to
* Config and Log files can be mapped to the host but should preferentially be symbolically linked to the /data or /config folder
* Additional mappings can be created if necessary

Images
------


* Images should be based on the latest LTS image available (Ubuntu 12.04 and 14.04) or to one of our images

Using the BioContainers base image
----------------------------------

BioContainers project is using a custom base image for most of its containers. The image is based on Ubuntu Trusty 14.04 LTS
and its going to be updated frequently.

Image name and versions
-----------------------

`biodckr/biodocker:latest <https://github.com/Biocontainers/containers/blob/master/base/Dockerfile>`_

Core Software and Packages
--------------------------


* curl
* fuse
* git
* wget
* zip
* openjdk-7-jre
* build-essential
* python
* python-dev
* python-pip
* zlib1g-dev

Sources and Useful Links
------------------------


* `https://github.com/veggiemonk/awesome-docker#optimizing-images <https://github.com/veggiemonk/awesome-docker#optimizing-images>`_
* `https://labs.ctl.io/optimizing-docker-images/?hvid=1OW0br <https://labs.ctl.io/optimizing-docker-images/?hvid=1OW0br>`_
* `https://docs.docker.com/articles/dockerfile_best-practices/ <https://docs.docker.com/articles/dockerfile_best-practices/>`_
* `http://csaba.palfi.me/random-docker-tips/ <http://csaba.palfi.me/random-docker-tips/>`_
* `https://docs.docker.com/articles/dockerfile_best-practices/ <https://docs.docker.com/articles/dockerfile_best-practices/>`_
* `http://jonathan.bergknoff.com/journal/building-good-docker-images <http://jonathan.bergknoff.com/journal/building-good-docker-images>`_
