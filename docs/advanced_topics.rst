Advanced topics
==========================

rkt
----------

`rkt <https://coreos.com/rkt/>`__ is a next-generation container manager for Linux clusters. In contrast to the Docker daemon, ``rkt`` is a single binary that is currently available on CoreOS and Kubernetes only. It is designed for
modern Linux clusters environments.

To reference a Docker image, use the ``docker://`` prefix when fetching or running images.

   .. code-block:: bash

      $ rkt --insecure-options=image run docker://biocontainers/comet

According to the original documentation:

This behaves similarly to the Docker client, if no specific registry is named, the Docker Hub is used by default. As with Docker, alternative registries can be used by specifying the registry as part of the image reference.


Docker useful tips
---------------------------

Bash interactive script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block::

   $ docker run -t -i ubuntu /bin/bash
   root@af8bae53bdd3:/#

In this example:


.. note:: ``-t`` flag assigns a pseudo-tty or terminal inside the new container. ``-i`` flag allows you to make an interactive connection by grabbing the standard in (STDIN) of the container. ``/bin/bash`` launches a Bash shell inside our container.

Let’s try running some commands inside the container:

.. code-block::

   root@af8bae53bdd3:/# ls
   bin boot dev etc home lib lib64 media mnt opt proc root run sbin srv sys tmp usr var

In this example ``ls`` displays the directory listing of the root directory inside the container.

.. note:: When completed, run the ``exit`` command or enter Ctrl-D to exit the interactive shell.


Start a daemonized Hello world
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let’s create a container that runs as a daemon.

.. code-block::

   $ docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
   1e5535038e285177d5214659a068137486f96ee5c2e85a4ac52dc83f2ebe4147

.. note:: ``-d`` flag runs the container in the background (to daemonize it). The command ``/bin/sh -c "while true; do echo hello world; sleep 1; done"`` run the container in an infinite loop.

We can use this container ID to see what’s happening with our hello world daemon. First, let’s make sure our container is running. Run the ``docker ps`` command. The docker ``ps`` command queries the Docker daemon for information about all the containers it knows about.

.. code-block::

   $ docker ps
   CONTAINER ID  IMAGE         COMMAND               CREATED        STATUS       PORTS NAMES
   1e5535038e28  ubuntu  /bin/sh -c 'while tr  2 minutes ago  Up 1 minute        insane_babbage

..

