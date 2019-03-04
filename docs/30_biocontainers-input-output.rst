
----

title: 'Input/Outpout'
layout: series_item
contributors: Yassset Perez-Riverol
series: 'developer-manual'
permalink: /developer-manual/biocontainers-input-output/

estimated-time: 5
-----------------

Using input  and Output files
=============================

In many cases the software you are using requires an input or an output file to work.
This can be achieved using a container image, but it requires that you change the way how you execute
the docker daemon.

The first step is to have a specific folder in your computer to serve as a shared folder between your system and the container. In this case let's place a file called prot.fa inside a folder called ``/home/user/docker/``.

The ``/home/user/docker/`` folder will be mapped inside the container, that way this can server as a gateway for files, both the input and the output files will be placed there. 

After setting the folder and necessary files inside we can execute the image we want. In the example bellow we are running an image built from an example container:

.. code-block::

   $ docker run -v /home/user/docker/:/data/ biodckr/program -input /data/prot.fa -output /data/result.txt`

Our local path ``/home/user/docker/`` will map inside the container into a folder called ``/data/`` and the software will have access to the file. After the processing is done the result file will be saved on the same place and we can have it outside the container in the same folder.
In this scenario, the only difference is the use of the parameter ``-v`` when running the image, this parameter tells the docker daemon that when are mapping something from the host system internally.
