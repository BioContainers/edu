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

