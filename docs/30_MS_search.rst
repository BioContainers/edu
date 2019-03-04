
----

title: 'MS Search'
layout: series_item
series: 'containers-examples'
permalink: /containers-examples/ms-search/

estimated-time: 5
-----------------

Proteomics data analysis is dominated by database-based search engines strategies. 
Perhaps the most common protocol today is to retrieve raw data from a mass spectrometry, convert the
raw data from binary format to a text-based format and then process it using a database search algorithm.
The resulting data need to be statistically filtered in order to converge to a final list of identified peptides
and proteins. Amount Search Engines, Comet (the youngest son of SEQUEST) is one of the most popular nowadays.
Today we are going to show how to run a simple analysis protocol using the Comet database search engine followed
by statistical analysis using PeptideProphet and ProteinProphet, two of the most known and robust processing
algorithms for proteomics data.

This pipeline is available in TPP, however several users prefer to use the individual components rather than Trans-proteomics Pipeline.  The big differential here is how we are going to do it. Instead of going through the step-by-step in how to install and configure Comet and TPP, we are going to run the pipeline using Docker containers from the BioContainers project (you can get more information on the project here).

Installing Docker
-----------------

Docker is a freely distributed software, compatible with all operating systems. If you need directions on how to install it, follow the instructions on Docker's documentation here.

Getting ready
-------------

First thing to do is to arrange the necessary files. For this pipeline we are going to need converted raw files from some mass spectrometry analysis and a protein database in FASTA format.
This are the files I'm using for this tutorial:


* b1930_293T_proteinID_10A_QE3_122212.mzXML
* b1931_293T_proteinID_11A_QE3_122212.mzXML
* database.fa

I'm placing all these files inside a folder called /home/felipe/workspace/

Preparing the Containers
------------------------

The Docker containers wee need are already available to use via Biodocker project. The main goal of this project is to provide ready-to-use containers with bioinformatics software inside. For this tutorial we are going to download 3 containers; Comet and both Prophets.
If you are not familiar with Docker, you should read the material from the original project website. In short words, containers are analogous to virtual machines, except that they do not contain a whole operating system inside. In practical terms we have an isolated lightweight environment with a private file system. Software inside a container can be accessed through command line using the docker daemon._
Back to the tutorial... Lets download the containers we need. Run the following commands, one by one (depending on your configuration, you may need to use sudo for executing commands with the docker daemon):

.. code-block::

   $ docker pull biocontainers/comet
   $ docker pull biocontainers/peptideprophet
   $ docker pull biocontainers/proteinprophet

Running Comet
-------------

In order to run Comet we need to print a new parameter file:

.. code-block::

   > docker run -v /home/felipe/workspace/:/data/ biocontainers/comet comet -p

To have access to files inside the container, and vice-versa, we need to map a local folder inside the container, that way all files inside this mapped folder will be visible and accessible to us and to the container. This is possible using the parameter -v and passing the complete path from our folder that we wish to map inside the container. In this case we are mapping /home/felipe/workspace into /data/, a pre-existent folder inside the container._
biocontainers/comet is the name of the container we pulled from BioContainers. The 'comet' right after is the name of the program inside the container we are running.
After running this command you will see a new file in the folder called comet.params.new, let's rename it to comet.params and edit some of the options.
In this case I will just change two parameters:

``database_name = /data/database.fa``

``decoy_search = 1``

Remember that the files inside the container are actually inside a folder called /data/, so that's how we are going to pass the file location to the programs.
Now we can start the database search:

.. code-block::

   > docker run -v /home/felipe/workspace/:/data/ biocontainers/comet comet -Pcomet.params b1930_293T_proteinID_10A_QE3_122212.mzXML b1931_293T_proteinID_11A_QE3_122212.mzXML`

If everything went well you should see two new files on your folder; b1930_293T_proteinID_10A_QE3_122212.pep.xml and b1931_293T_proteinID_11A_QE3_122212.pep.xml

Running PeptideProphet
----------------------

For the next step we need to run PeptideProphet, that will overwritte the .pep.xml files we already have:

.. code-block::

   > docker run -v /home/felipe/workspace/:/data/ biocontainers/peptideprophet PeptideProphet /data/b1930_293T_proteinID_10A_QE3_122212.pep.xml ZERO ACCMASS PPM INSTRWARN DECOY=DECOY_ DECOYPROBS NONPARAM`
   > docker run -v /home/felipe/workspace/:/data/ biocontainers/peptideprophet PeptideProphet /data/b1931_293T_proteinID_11A_QE3_122212.pep.xml ZERO ACCMASS PPM INSTRWARN DECOY=DECOY_ DECOYPROBS NONPARAM`

This parameters are specific to the data set I'm using, you can change them with no problems. To see all the parameters just run:

.. code-block::

   > docker run biocontainers/peptideprophet PeptideProphet`

Running ProteinProphet
----------------------

Finally, for the last step, we need to run ProteinProphet:

.. code-block::

   > docker run -v /home/felipe/workspace/:/data/ biocontainers/proteinprophet ProteinProphet /data/b1930_293T_proteinID_10A_QE3_122212.pep.xml /data/b1931_293T_proteinID_11A_QE3_122212.pep.xml /data/result.prot.xml`

and that's it, now you have your prot.xml file with the identified proteins.

Conclusion
----------

Again we show how versatile BioContainers containers can be. Even complete analysis protocols like the one showed above can be managed easily without the need to install complex software or manipulating Makefiles. Please feel free to make comments and suggestions.
