.. _examples

BioContainers in Examples
======================================

In this section we provide a set of examples about how to use BioContainers in your analysis. Please feel free to contribute to this help with your own examples.

Peptide MS search engine (Tide)
-------------------------

Let’s run a proteomics search engine to identified proteins using `Tide <http://crux.ms/commands/tide-index.html>`_. Proteomics data analysis is dominated by database-based search engines strategies. Amount Search Engines, **Tide** is one of the most popular nowadays.

Get the docker container
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block::

   $ docker pull biocontainers/crux:v3.2_cv3

.. note:: The BioContainers community had decided to remove the ``latest`` tag. Then, the following command ``docker pull biocontainers/crux`` will fail. Read more about this decision in :doc:`getting_started`


Getting the data
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



Command Resume
--------------

So far, you launched your first containers using the docker run command. You ran an interactive container that ran in the foreground. You also ran a detached container that ran in the background. In the process you learned about several Docker commands:


* **docker run**  - Run a docker container
* **dcoker pull** - Download the container from Biodocker Hub
* **docker ps**   - Lists containers.
* **docker logs** - Shows us the standard output of a container.
* **docker stop** - Stops running containers.

Now, you have the basis learn more about Docker `Go to “Run a simple application“ <https://docs.docker.com/engine/userguide/containers/usingdocker/>`_
