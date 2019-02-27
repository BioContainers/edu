---
title: 'BioContainer example'
layout: series_item
series: '101'
permalink: /101/running-example/
estimated-time: 5
---

{% alert warn %}
We will run the first example with BLAST. The Basic Local Alignment Search Tool for comparing primary biological sequence
information, such as the amino-acid sequences of different proteins or the nucleotides of DNA sequences.
We chose BLAST because it is one of the most common and useful software in bioinformatics.
{% endalert %}

First step to be able to run any software is to install it. This can be a difficult and challenged process starting by download
the software, dependencies, etc; installation of multiple packages; dealing with dependencies crashes, etc. See all the steps
to install `blast` [here](https://www.ncbi.nlm.nih.gov/books/NBK279671/).  

Here is, where **BioContainers** plays his major role. See how to download and "install" blast in your local machine:

~~~
 $ docker pull biocontainers/blast:2.2.31
~~~

This is the docker and containers magic, the software is distributed with all the dependencies and shared OS needed to run.

<img class="splashIcon" src="{{ site.baseurl}}/img/series/101/what.gif">

Docker allows applications to be isolated into containers with instructions for exactly what they need to survive that can be easily ported
from machine to machine. If you have 30 Docker containers that you want to run, you can run them all on a single VM.

{% alert info %}
 In contrast (for example) to run 30 virtual machines, you’ve got to boot 30 operating systems with at least minimum resource
 requirements available before factoring the hypervisor for them to run on with the base OS.
{% endalert %}

### Running BLAST

~~~
 $ docker run biocontainers/blast:2.2.31 blastp -help
~~~

This will print the help page for `blastp` tool. The first part of the command `docker run biocontainers/blast` enable docker
to identified the correct container in your local registry. The second part `blastp -help` is the command that you want to
use in the container.

{% alert info %}
 If you want to [list all the containers/images](https://docs.docker.com/engine/reference/commandline/images/) you have pull from public repositories and are available in your
 local machine, you can use the following command: `$ docker images`
{% endalert %}

For this example let's try something practical, suppose that we are molecular biologists studying [prion proteins](https://en.wikipedia.org/wiki/PRNP), and we want to find out if the zebrafish, a model organism, has a prion protein similar to the human form.

1) Downloading the human prion sequence

We can grab the human prion FASTA sequence from UniProt:

~~~
$ wget http://www.uniprot.org/uniprot/P04156.fasta
~~~

2) Downloading the zebrafish database

Now, lets download and unpack our database, from NCBI

~~~
$ curl -O ftp://ftp.ncbi.nih.gov/refseq/D_rerio/mRNA_Prot/zebrafish.1.protein.faa.gz
$ gunzip zebrafish.1.protein.faa.gz
~~~

3) Preparing the database

We need to prepare the zebrafish database with `makeblastdb` for the search, but first we need to make our files available inside the containers. The docker daemon has a parameter called volume (-v), it allows us to map a folder from our operating system inside the container, that way all files in that folder will be visible inside the container, and the BLAST results will also be available to us, outside the container. In the example below, I'm mapping the folder /Users/yperez/workplace (my computer) into /data/ (the container). When running the command on your computer, you should use the correct paths for your files.


~~~
 $ docker run -v /Users/yperez/workplace:/data/ biocontainers/blast makeblastdb -in zebrafish.1.protein.faa -dbtype prot
~~~

The programs log will be displayed on the terminal, indicating if the program finished correctly. Also, you will see some new files on your local folder, those are part of the BLAST database.

{% alert info %}                                                                                                                  

 Here, we explain multiples concepts in the same command. The most important component is `-v /Users/yperez/workplace:/data/`. This command creates a symbolic link
 between the `workplace` where the downloaded files are store and the `/data/` inside the container. You can [check here](/developer-manual/biocontainers-input-output/) for more documentation.

{% endalert %}

No, that you know how to run a container with all the tricks, then lets go for the final alignments:

~~~
 $ docker run -v /Users/yperez/workplace:/data/ biocontainers/blast:2.2.31 blastp -query P04156.fasta -db zebrafish.1.protein.faa -out results.txt
~~~

The results will be saved on the results.txt file, then you can proceed to analyze the matches. By looking the list of the best hits we can observe that zebrafish has a few predicted proteins matching to the human prion with better scores than the 
predicted prion protein (score:33.9, e-value: 0.22). That's interesting isn't ?

Now that you have enough information to start comparing sequences using BLAST, you can move your analysis even further.

We hope that this short example can provide some light on how important and easy it is to run containerized software.

### Summary

~~~
 $ cd /home/user/workplace
 $ docker pull biocontainers/blast:2.2.31
 $ docker run biocontainers/blast:2.2.31 blastp -help
 $ wget http://www.uniprot.org/uniprot/P04156.fasta    
 $ curl -O ftp://ftp.ncbi.nih.gov/refseq/D_rerio/mRNA_Prot/zebrafish.1.protein.faa.gz
 $ gunzip zebrafish.1.protein.faa.gz
 $ docker run -v /Users/yperez/workplace:/data/ biocontainers/blast makeblastdb -in zebrafish.1.protein.faa -dbtype prot
 $ docker run -v /Users/yperez/workplace:/data/ biocontainers/blast blastp -query P04156.fasta -db zebrafish.1.protein.faa -out results.txt
~~~
