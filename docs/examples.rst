.. _examples

BioContainers in Examples
======================================

In this section we provide a set of examples about how to use BioContainers in your analysis. Please feel free to contribute to this help with your own examples.

Peptide MS search engine (Tide)
-------------------------

Let’s run a proteomics search engine to identified proteins using `Tide <http://crux.ms/commands/tide-index.html>`_.

.. note:: Proteomics data analysis is dominated by database-based search engines strategies. Amount Search Engines, **Tide** is one of the most popular nowadays.

Get the docker container
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block::

   $ docker pull biocontainers/crux:v3.2_cv3

.. note:: The BioContainers community had decided to remove the ``latest`` tag. Then, the following command ``docker pull biocontainers/crux`` will fail. Read more about this decision in :doc:`getting_started`


Run the Docker Container
~~~~~~~~~~~~~~~~~~~~~~~~

First thing to do is to arrange the necessary. For this pipeline we need some mass spectrometry data  and a protein database in FASTA format. This are the files we are using for this tutorial:


* `demo.ms2 <https://raw.githubusercontent.com/bigbio/nf-workflows/master/ms-crux-id-nf/data/demo.ms2>`__
* `small-yeast.fasta <https://raw.githubusercontent.com/bigbio/nf-workflows/master/ms-crux-id-nf/data/small-yeast.fasta>`__

I'm placing all these files inside a folder in your machine, in my case I will use /Users/yperez/workspace/

Start searching
~~~~~~~~~~~~~~~~~~~~~~

.. code-block::

   $ docker run -v /Users/yperez/workplace/:/data/ biocontainers/crux:v3.2_cv3 crux tide-index small-yeast.fasta yeast-index

.. note:: To have access to files inside the container, and vice-versa, we need to map a local (``/Users/yperez/workplace``) folder inside the container (``/data/``). This is possible using the ``-v`` and passing the complete path from our folder that we wish to map inside the container.

After running this command you will see a new folder called yeast-index in your path (``/Users/yperez/workplace``).


.. code-block::

       $ docker run -v /Users/yperez/workplace/:/data/ biocontainers/crux:v3.2_cv3 crux tide-search --compute-sp T --mzid-output T demo.ms2 yeast-index

If everything went well you should see two new folder (`crux-output`) containing the result files.



Other interesting options
-------------------------

Simple bash interactive script:

.. code-block::

   $ docker run -t -i ubuntu /bin/bash
   root@af8bae53bdd3:/#

In this example:


#. docker run runs a container.
#. ubuntu is the image you would like to run.
#. -t flag assigns a pseudo-tty or terminal inside the new container.
#. -i flag allows you to make an interactive connection by grabbing the standard in (STDIN) of the container.
#. /bin/bash launches a Bash shell inside our container.

The container launches. We can see there is a command prompt inside it:

.. code-block::

   root@af8bae53bdd3:/#

Let’s try running some commands inside the container:

.. code-block::

   root@af8bae53bdd3:/# ls
   bin boot dev etc home lib lib64 media mnt opt proc root run sbin srv sys tmp usr var

In this example:


#. ls displays the directory listing of the root directory of a typical Linux file system.

Now, you can play around inside this container. When completed, run the exit command or enter Ctrl-D to exit the interactive shell.

.. code-block::

   root@af8bae53bdd3:/# exit

..

   Note: As with our previous container, once the Bash shell process has finished, the container stops.


Start a daemonized Hello world
-------------------------------

Let’s create a container that runs as a daemon.

.. code-block::

   $ docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
   1e5535038e285177d5214659a068137486f96ee5c2e85a4ac52dc83f2ebe4147

In this example:


#. docker run runs the container.
#. -d flag runs the container in the background (to daemonize it).
#. ubuntu is the image you would like to run.

Finally, we specify a command to run: **/bin/sh -c "while true; do echo hello world; sleep 1; done"**

In the output, we do not see hello world but a long string:

1e5535038e285177d5214659a068137486f96ee5c2e85a4ac52dc83f2ebe4147

This long string is called a container ID. It uniquely identifies a container so we can work with it.

..

   Note: The container ID is a bit long and unwieldy. Later, we will cover the short ID and ways to name our containers to make working with them easier.


We can use this container ID to see what’s happening with our hello world daemon.

First, let’s make sure our container is running. Run the **docker ps** command. The docker ps command queries the Docker daemon for information about all the containers it knows about.

.. code-block::

   $ docker ps
   CONTAINER ID  IMAGE         COMMAND               CREATED        STATUS       PORTS NAMES
   1e5535038e28  ubuntu  /bin/sh -c 'while tr  2 minutes ago  Up 1 minute        insane_babbage

In this example, we can see our daemonized container. The docker ps returns some useful information:


#. 1e5535038e28 is the shorter variant of the container ID.
#. ubuntu is the used image.
#. the command, status, and assigned name insane_babbage.

..

   Note: Docker automatically generates names for any containers started. We’ll see how to specify your own names a bit later.


Now, we know the container is running. But is it doing what we asked it to do? To see this we’re going to look inside the container using the docker logs command.

Let’s use the container name insane_babbage.

.. code-block::

   $ docker logs insane_babbage
   hello world
   hello world
   hello world
   . . .

In this example:


#. docker logs looks inside the container and returns hello world.

Command Resume
--------------

So far, you launched your first containers using the docker run command. You ran an interactive container that ran in the foreground. You also ran a detached container that ran in the background. In the process you learned about several Docker commands:


* **docker run**  - Run a docker container
* **dcoker pull** - Download the container from Biodocker Hub
* **docker ps**   - Lists containers.
* **docker logs** - Shows us the standard output of a container.
* **docker stop** - Stops running containers.

Now, you have the basis learn more about Docker `Go to “Run a simple application“ <https://docs.docker.com/engine/userguide/containers/usingdocker/>`_
