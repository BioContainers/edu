This page will help you prepare your computer for BioContainers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You will need to work in a terminal using **``docker``** .

{% hlblock info %} We will provide mainly examples using **docker**, the
BioContainers team is working on examples and documentation based on
**rkt**. {% endhlblock %}

-  `Docker <https://www.docker.com/>`__ is the world’s leading platform
   for software containerization. Docker includes multiple tools and
   components such as: `docker <https://docs.docker.com/>`__, `docker
   engine <https://docs.docker.com/engine/installation/>`__, `docker
   hub <https://docs.docker.com/docker-hub/>`__.

{% hlblock check %}

Open your terminal of choice and check whether you have the command
(``docker``) installed. You should be able to run the following command
without any error.

::

    docker help

{% endhlblock %}

If your machine is already set up, continue to the
`example </101/running-example>`__.

{% hlblock info %} The following sections provided a short summary of
how to install **docker**. If these steps do not work for you, please
refer to the full documentation of
`docker <https://docs.docker.com/>`__. You can also get in contact with
us using `Specifications
Issues <https://github.com/BioContainers/specs>`__. {% endhlblock %}

Otherwise, choose your operating system below to learn more:

-  `**Mac** <#mac>`__
-  `**Linux** <#linux>`__
-  `**Windows** <#windows>`__

{% hlblock question %} What does ``docker`` stand for? {% endhlblock %}

Mac OSX
~~~~~~~

`On Mac <https://docs.docker.com/docker-for-mac/>`__ installing Docker
can be done by installing the complete `Docker
Toolbox <https://www.docker.com/products/docker-toolbox>`__ available in
Mac and Windows. The Docker Toolbox contains the Docker Engine, Compose,
Machine, etc.

{% hlblock check %}

Mac Docker ToolBox can be download from `this
page <https://docs.docker.com/docker-for-mac/>`__. The installation
provides Docker Engine, Docker CLI client, Docker Compose, and Docker
Machine.

::

    Double-click Docker.dmg to open the installer, then drag Moby the whale to the Applications folder. You will be asked to authorize Docker.app with your system password during the install process. Privileged access is needed to install networking components and links to the Docker apps.

{% endhlblock %}

{% alert warn %}

If you are already running Docker on your machine, first read `Docker
for Mac vs. Docker
Toolbox <https://docs.docker.com/docker-for-mac/docker-toolbox/>`__ to
understand the impact of this installation on your existing setup, how
to set your environment for Docker for Mac, and how the two products can
coexist. If you have a old version of dockerboot and you want to remove
it, you can use the following
`script </faqs/manually-remove-dockerboot>`__

{% endalert %}

Then installed tools can be check using these commands:

::

    $ docker --version
    Docker version 1.12.0, build 8eab29e

    $docker-compose --version
    docker-compose version 1.8.0, build f3628c7

    $docker-machine --version
    docker-machine version 0.8.0, build b85aac1

Installing git can be done using Homebrew:

::

    brew install git

If you have problems installing docker you can find support here:
`BioContainers Gitter <https://gitter.im/biocontainers/Lobby>`__

Linux
~~~~~

Installing `Docker in
Linux <https://docs.docker.com/engine/installation/>`__ can be done
using the specific Linux distribution. Some of the supported
distributions are: `Arch
Linux <https://docs.docker.com/engine/installation/linux/archlinux/>`__,
`CentOS <https://docs.docker.com/engine/installation/linux/centos/>`__,
`CRUX
Linux <https://docs.docker.com/engine/installation/linux/cruxlinux/>`__,
`Debian <https://docs.docker.com/engine/installation/linux/debian/>`__,
`Fedora <https://docs.docker.com/engine/installation/linux/fedora/>`__,
`Gentoo <https://docs.docker.com/engine/installation/linux/gentoolinux/>`__,
`Oracle
Linux <https://docs.docker.com/engine/installation/linux/oracle/>`__,
`Red Hat Enterprise
Linux <https://docs.docker.com/engine/installation/linux/rhel/>`__,
`openSUSE and SUSE Linux
Enterprise <https://docs.docker.com/engine/installation/linux/SUSE/>`__,
`Ubuntu <https://docs.docker.com/engine/installation/linux/ubuntulinux/>`__

{% alert warn %}

If your linux distribution is not listed above, don’t give up yet. To
try out Docker on a distribution that is not listed above, go here:
`Installation from
binaries <https://docs.docker.com/engine/installation/binaries/>`__.

{% endalert %}

Windows
~~~~~~~

Docker for Windows is our newest offering for PCs. It runs as a native
Windows application and uses Hyper-V to virtualize the Docker Engine
environment and Linux kernel-specific features for the Docker daemon.

{% alert warn %}

Please read through these topics on how to get started. To give us your
feedback on your experience with the app and report bugs or problems,
log in to `Docker for Windows
forum <https://forums.docker.com/c/docker-for-windows>`__.

{% endalert %}

After downloading the
`InstallDocker.msi <https://download.docker.com/win/stable/InstallDocker.msi>`__
file, you can follow the next steps:

1. Double-click InstallDocker.msi to run the installer. It typically
   downloads to your Downloads folder, or you can run it from the recent
   downloads bar at the bottom of your web browser.

2. Follow the install wizard to accept the license, authorize the
   installer, and proceed with the install.

3. You will be asked to authorize Docker.app with your system password
   during the install process. Privileged access is needed to install
   networking components, links to the Docker apps, and manage the
   Hyper-V VMs.

Click Finish on the setup complete dialog to launch Docker.
