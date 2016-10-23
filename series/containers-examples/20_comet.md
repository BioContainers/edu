---
title: 'Comet'
layout: series_item
series: 'containers-examples'
permalink: /containers-examples/Comet/
estimated-time: 5
---

## Run a Comet search engine

Let’s run a a proteomics search engine to identified proteins using [Comet](http://comet-ms.sourceforge.net/).

{% alert warn %}

Proteomics data analysis is dominated by database-based search engines strategies.
Amount Search Engines, Comet is one of the most popular nowadays. 
We are going to show how to run a simple analysis protocol using the [BioContainers Comet](https://github.com/BioContainers/containers/tree/master/Comet) database
search engine. 
{% endalert %}

## Get the docker container

~~~
$ docker pull biodckr/comet
~~~

Some insides into this commandline:

1. The [biodocker registry](/biodocker-registry/) **biodckr** contains all the BioDocker deployed containers ready to be use. 
2. **docker pull** download the latest container of Comet

If the user wants to download an specific version of the comet biodcoker container it can be done by providing the current corrsponding tag. 

~~~
$ docker pull biodckr/comet --tag="2016012" 
~~~


## Run the Docker Container 

>**Note**: First thing to do is to arrange the necessary [files to run your data](/biodocker-input-output/). 
For this pipeline we are going to need converted raw files from some mass spectrometry analysis and a protein
database in FASTA format. This are the files we are using for this tutorial:

- [b1930_293T_proteinID_10A_QE3_122212.mzXML]()
- [b1931_293T_proteinID_11A_QE3_122212.mzXML]()
- [database.fa]()

I'm placing all these files inside a folder called /home/user/workspace/

### Print Comet a new parameter file:

~~~
$ docker run -v /home/user/workspace/:/data/ biodckr/comet comet -p
~~~

Some notes about this commandline:

1. To have access to files inside the container, and vice-versa, we need to map a local folder inside the container,
that way all files inside this mapped folder will be visible and accessible to us and to the container.
2. This is possible using the **parameter -v** and passing the complete path from our folder that we wish to map inside the container. In this case we are mapping /home/user/workspace into /data/, a pre-existent folder inside the container.
3. **biodckr/comet** is the name of the container we pulled from BioDocker. 
4. The **comet** right after is the name of the program inside the container we are running.

After running this command you will see a new file in the folder called comet.params.new,
let's rename it to comet.params and edit some of the options.
In this case I will just change two parameters:
database_name = /data/database.fa
decoy_search = 1

>**Note**: Remember that the files inside the container are actually inside a folder called /data/, 
so that's how we are going to pass the file location to the programs.

### Start the database search:

~~~
    $ docker run -v /home/felipe/workspace/:/data/ biodckr/comet comet -Pcomet.params b1930_293T_proteinID_10A_QE3_122212.mzXML b1931_293T_proteinID_11A_QE3_122212.mzXML
~~~

If everything went well you should see two new files on your folder; b1930_293T_proteinID_10A_QE3_122212.pep.xml and b1931_293T_proteinID_11A_QE3_122212.pep.xml

## Other interesting options

Simple bash interactive script:

~~~
$ docker run -t -i ubuntu /bin/bash
root@af8bae53bdd3:/#
~~~

In this example:

1. docker run runs a container.
2. ubuntu is the image you would like to run.
3. -t flag assigns a pseudo-tty or terminal inside the new container.
4. -i flag allows you to make an interactive connection by grabbing the standard in (STDIN) of the container.
5. /bin/bash launches a Bash shell inside our container.

The container launches. We can see there is a command prompt inside it:

~~~
root@af8bae53bdd3:/#
~~~

Let’s try running some commands inside the container:

~~~
root@af8bae53bdd3:/# ls
bin boot dev etc home lib lib64 media mnt opt proc root run sbin srv sys tmp usr var
~~~

In this example:

1. ls displays the directory listing of the root directory of a typical Linux file system.

Now, you can play around inside this container. When completed, run the exit command or enter Ctrl-D to exit the interactive shell.

~~~
root@af8bae53bdd3:/# exit
~~~

>Note: As with our previous container, once the Bash shell process has finished, the container stops.

### Start a daemonized Hello world

Let’s create a container that runs as a daemon.

~~~
$ docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
1e5535038e285177d5214659a068137486f96ee5c2e85a4ac52dc83f2ebe4147
~~~

In this example:

1. docker run runs the container.
2. -d flag runs the container in the background (to daemonize it).
3. ubuntu is the image you would like to run.

Finally, we specify a command to run: **/bin/sh -c "while true; do echo hello world; sleep 1; done"**

In the output, we do not see hello world but a long string:

1e5535038e285177d5214659a068137486f96ee5c2e85a4ac52dc83f2ebe4147

This long string is called a container ID. It uniquely identifies a container so we can work with it.

>Note: The container ID is a bit long and unwieldy. Later, we will cover the short ID and ways to name our containers to make working with them easier.

We can use this container ID to see what’s happening with our hello world daemon.

First, let’s make sure our container is running. Run the **docker ps** command. The docker ps command queries the Docker daemon for information about all the containers it knows about.

~~~
$ docker ps
CONTAINER ID  IMAGE         COMMAND               CREATED        STATUS       PORTS NAMES
1e5535038e28  ubuntu  /bin/sh -c 'while tr  2 minutes ago  Up 1 minute        insane_babbage
~~~

In this example, we can see our daemonized container. The docker ps returns some useful information:

1. 1e5535038e28 is the shorter variant of the container ID.
2. ubuntu is the used image.
3. the command, status, and assigned name insane_babbage.

> Note: Docker automatically generates names for any containers started. We’ll see how to specify your own names a bit later.

Now, we know the container is running. But is it doing what we asked it to do? To see this we’re going to look inside the container using the docker logs command.

Let’s use the container name insane_babbage.

~~~
$ docker logs insane_babbage
hello world
hello world
hello world
. . .
~~~

In this example:

1. docker logs looks inside the container and returns hello world.

## Command Resume

So far, you launched your first containers using the docker run command. You ran an interactive container that ran in the foreground. You also ran a detached container that ran in the background. In the process you learned about several Docker commands:

- **docker run**  - Run a docker container 
- **dcoker pull** - Download the container from Biodocker Hub
- **docker ps**   - Lists containers.
- **docker logs** - Shows us the standard output of a container.
- **docker stop** - Stops running containers.

Now, you have the basis learn more about Docker [Go to “Run a simple application“](https://docs.docker.com/engine/userguide/containers/usingdocker/)