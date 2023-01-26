.. _running_example

Running first container
================================

.. sidebar:: More Examples
   :subtitle: **It can make your life easier** if you want to explore individual examples:

   - :doc:`examples`

We will run the first example with BLAST. The Basic Local Alignment Search Tool for comparing biological sequence information, such as the amino-acid sequences of proteins or the nucleotides of DNA sequences. We chose BLAST because it frequently used
in bioinformatics.

The first step is to ``pull`` the software from Biocontainers registry:

  .. code-block:: bash

     $ docker pull biocontainers/blast:2.2.31

.. note:: This is the magic of containers; the software is distributed with all the dependencies and shared OS needed to run.

Docker allows applications to be isolated into containers with instructions for exactly what they need to survive and these
instructions can be easily ported from machine to machine.

Running BLAST
--------------------

  .. code-block:: bash

     $ docker run biocontainers/blast:2.2.31 blastp -help

This will print the help page for ``blastp`` tool. The first part of the command ``docker run biocontainers/blast`` enables docker to identify the correct container in your local registry. The second part ``blastp -help`` is the command that you want to use in the container.

.. note:: If you want to `list all the containers/images <https://docs.docker.com/engine/reference/commandline/images/>` you have pulled from public repositories and are available in your local machine, you can use the following command: ``docker images``.

For this example let's try something practical, suppose that we are molecular biologists studying `prion
proteins <https://en.wikipedia.org/wiki/PRNP>`__, and we want to find out if the zebrafish, a model organism, has a prion protein similar to the human form.

1) Downloading the human prion sequence, We can grab the human prion FASTA sequence from UniProt:

    .. code-block:: bash

      $ docker run biocontainers/blast:2.2.31 curl https://www.uniprot.org/uniprot/P04156.fasta >> P04156.fasta

.. note:: Some biocontainer base images contain multiple linux command that are useful for bioinformatics like ``curl``, ``wget``. You should note that not all the containers contains those additional tools.

2) Downloading the zebrafish database

Now, let's download and unpack our database, from NCBI

    .. code-block:: bash

      $ mkdir host-data
      $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 curl -O ftp://ftp.ncbi.nih.gov/refseq/D_rerio/mRNA_Prot/zebrafish.1.protein.faa.gz
      $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 gunzip zebrafish.1.protein.faa.gz

.. note:: The docker command can be run with the option ``-v``; this will bind a local volume (in the example path host-data within the current working directory) into a container volume /data/. You can read more about `here <https://docs.docker.com/storage/volumes/>`__ . In the example every operation performed in ``/data/`` will be stored in the bind directory.

3) Preparing the database

We need to prepare the zebrafish database with ``makeblastdb`` for the search, but first we need to make our files available inside the containers. The docker daemon has a parameter called volume (-v), it allows us to map a folder from our operating system inside the container, that way all files in that folder will be visible inside the container, and the BLAST results will also be available to us, outside the container. In the example below, I'm mapping the folder /Users/yperez/workplace (my computer) into /data/ (the container). When running the command on your computer, you should use the correct paths for your files.

     .. code-block:: bash

        $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 makeblastdb -in zebrafish.1.protein.faa -dbtype prot

The program's log will be displayed on the terminal, indicating if the program finished correctly. Also, you will see some new files in your local folder, those are part of the BLAST database.

Download a query sequence from the UniProt Knowledgebase (UniProtKB).

     .. code-block:: bash

        $ docker run biocontainers/blast:2.2.31 curl https://www.uniprot.org/uniprot/P04156.fasta >> host-data/P04156.fasta

Now, that you know how to run a container with all the tricks, let's go for the final alignments:

     .. code-block:: bash

        $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 blastp -query P04156.fasta -db zebrafish.1.protein.faa -out results.txt

The results will be saved in the results.txt file, then you can proceed to analyze the matches. By looking at the list of the best hits we can observe that zebrafish have a few predicted proteins matching the human prion with better scores than the predicted prion protein (score:33.9, e-value: 0.22). That's interesting isn't ?

Now that you have enough information to start comparing sequences using BLAST, you can move your analysis even further.

We hope that this short example can shed some light on how important and easy it is to run containerized software.

Run everything in one go
~~~~~~~

  .. code-block:: bash

     $ cd /Users/yperez/workplace   # Replace by your path
     $ mkdir host-data
     $ docker run biocontainers/blast:2.2.31 blastp -help
     $ docker run -v `pwd`/host-data/ biocontainers/blast:2.2.31 curl -O ftp://ftp.ncbi.nih.gov/refseq/D_rerio/mRNA_Prot/zebrafish.1.protein.faa.gz
     $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 gunzip zebrafish.1.protein.faa.gz
     $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 makeblastdb -in zebrafish.1.protein.faa -dbtype prot
     $ docker run biocontainers/blast:2.2.31 curl https://www.uniprot.org/uniprot/P04156.fasta >> host-data/P04156.fasta
     $ docker run -v `pwd`/host-data/:/data/ biocontainers/blast:2.2.31 blastp -query P04156.fasta -db zebrafish.1.protein.faa -out results.txt



