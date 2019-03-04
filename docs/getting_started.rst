.. _getting_started

Getting started with Docker
============================

Docker Configuration
---------------

`Docker <https://www.docker.com/>`__ is the world’s leading platform for software containerization. Docker includes multiple tools and components such as: `docker <https://docs.docker.com/>`__, `docker engine <https://docs.docker.com/engine/installation/>`__, `docker hub <https://docs.docker.com/docker-hub/>`__.

.. hint:: Open your terminal of choice and check whether you have the command ``docker`` installed. You should be able to run the following command without any error.

Other commands:

.. code-block:: bash
    $ docker --version
    Docker version 1.12.0, build 8eab29e

    $docker-compose --version
    docker-compose version 1.8.0, build f3628c7

    $docker-machine --version
    docker-machine version 0.8.0, build b85aac1


If your machine is already set up, continue to the :doc:`running_example`.

The following sections provided a short summary of how to install **docker**. If these steps do not work for you, please refer to the full documentation of `docker <https://docs.docker.com/>`__. You can also get in contact with us using `Specifications Issues <https://github.com/BioContainers/specs>`__.

Mac OSX
~~~~~~~~~~

`On Mac <https://docs.docker.com/docker-for-mac/>`__ installing Docker can be done by installing the complete `Docker Toolbox <https://www.docker.com/products/docker-toolbox>`__ available in Mac and Windows. The Docker Toolbox contains the Docker Engine, Compose, Machine, etc.

.. note:: Mac Docker ToolBox can be download from `this page <https://docs.docker.com/docker-for-mac/>`__. The installation provides Docker Engine, Docker CLI client, Docker Compose, and Docker Machine.

Linux
~~~~~

Installing `Docker in Linux <https://docs.docker.com/engine/installation/>`__ can be done using the specific Linux distribution. Some of the supported
distributions are: `Arch Linux <https://docs.docker.com/engine/installation/linux/archlinux/>`__, `CentOS <https://docs.docker.com/engine/installation/linux/centos/>`__, `CRUX Linux <https://docs.docker.com/engine/installation/linux/cruxlinux/>`__, `Debian <https://docs.docker.com/engine/installation/linux/debian/>`__, `Fedora <https://docs.docker.com/engine/installation/linux/fedora/>`__, `Gentoo <https://docs.docker.com/engine/installation/linux/gentoolinux/>`__, `Oracle Linux <https://docs.docker.com/engine/installation/linux/oracle/>`__, `Red Hat Enterprise Linux <https://docs.docker.com/engine/installation/linux/rhel/>`__, `openSUSE and SUSE Linux Enterprise <https://docs.docker.com/engine/installation/linux/SUSE/>`__, `Ubuntu <https://docs.docker.com/engine/installation/linux/ubuntulinux/>`__

Windows
~~~~~~~

Docker for Windows is our newest offering for PCs. It runs as a native Windows application and uses Hyper-V to virtualize the Docker Engine environment and Linux kernel-specific features for the Docker daemon.

.. note:: Please read through these topics on how to get started. To give us your feedback on your experience with the app and report bugs or problems, log in to `Docker for Windows forum <https://forums.docker.com/c/docker-for-windows>`__.


How does a Docker image work?
------------------------------

Docker images are read-only templates from which Docker containers are launched. Each image consists of a series of layers. Docker makes use of union file systems to combine these layers into a single image. Union file systems allow files and directories of separate file systems, known as branches, to be transparently overlaid, forming a single coherent file system.

One of the reasons Docker is so lightweight is because of these layers. When you change a Docker image—for example, update an application to a new version— a new layer gets built. Thus, rather than replacing the whole image or entirely rebuilding, as you may do with a virtual machine, only that layer is added or updated. Now you don’t need to distribute a whole new image, just the update, making distributing Docker images faster and simpler.

Every image starts from a **Base image** , for example ubuntu, a base Ubuntu image, or fedora, a base Fedora image. You can also use images of your own as the basis for a new image.

Docker images are then built from these base images using a simple, descriptive set of steps we call instructions. Each instruction creates a new layer in our image. Instructions include actions like:


* Run a command
* Add a file or directory
* Create an environment variable
* What process to run when launching a container from this image

These instructions are stored in a file called a Dockerfile. A **Dockerfile** (see example of a BioContainers Dockerfile :ref:`biocontainers`) is a text based script that contains instructions and commands for building the image from the base image. Docker reads this Dockerfile when you request a build of an image, executes the instructions, and returns a final image.


Docker input and output files
------------------------------

In many cases the software you are using requires an input or an output file to work. This can be achieved using a container image, but it requires that you change the way how you execute the docker daemon. The first step is to have a specific folder in your computer to serve as a shared folder between your system and the container. In this case let's place a file called prot.fa inside a folder called ``/home/user/docker/``. The ``/home/user/docker/`` folder will be mapped inside the container, that way this can server as a gateway for files, both the input and the output files will be placed there.

After setting the folder and necessary files inside we can execute the image we want. In the example bellow we are running an image built from an example container:

.. code-block::

   $ docker run -v /home/user/docker/:/data/ biocontainers/program:version -input /data/prot.fa -output /data/result.txt`

Our local path ``/home/user/docker/`` will map inside the container into a folder called ``/data/`` and the software will have access to the file. After the processing is done the result file will be saved on the same place and we can have it outside the container in the same folder.
In this scenario, the only difference is the use of the parameter ``-v`` when running the image, this parameter tells the docker daemon that when are mapping something from the host system internally.


References
------------------

* `Understand Docker Architecture <https://docs.docker.com/engine/understanding-docker/>`_
* `Docker Tutorial - What is Docker & Docker Containers, Images, etc? <https://www.youtube.com/watch?v=pGYAg7TMmp0>`_
* `Docker Ecosystem <https://www.digitalocean.com/community/tutorials/the-docker-ecosystem-an-introduction-to-common-components>`_