---
title: 'Dockerfile Template'
layout: series_item
series: 'developer-manual'
permalink: /developer-manual/biocotainers-dockerfile/
estimated-time: 5
---

# BioContainers dockerfile template

This is a standard template for creating a new Dockerfile for BioContainers:

> Note: Please always follow the [best practices](/developer-manual/best-practices/) and help pages [Using input and Output files](/developer-manual/biocontainers-input-output/) information.

Bellow is the complete example of a BioContainers Dockerfile:

~~~
# Base Image
FROM biocontainers/biocontainers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="3"
LABEL software="Comet"
LABEL software.version="2016012"
LABEL description="an open source tandem mass spectrometry sequence database search tool"
LABEL website="http://comet-ms.sourceforge.net/"
LABEL documentation="http://comet-ms.sourceforge.net/parameters/parameters_2016010/"
LABEL license="http://comet-ms.sourceforge.net/"
LABEL tags="Proteomics"

# Maintainer
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>

USER biodocker

RUN ZIP=comet_binaries_2016012.zip && \
  wget https://github.com/BioDocker/software-archive/releases/download/Comet/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /home/biodocker/bin/Comet/ && \
  chmod -R 755 /home/biodocker/bin/Comet/* && \
  rm /tmp/$ZIP

RUN mv /home/biodocker/bin/Comet/comet_binaries_2016012/comet.2016012.linux.exe /home/biodocker/bin/Comet/comet

ENV PATH /home/biodocker/bin/Comet:$PATH

WORKDIR /data/

CMD ["comet"]
~~~


## Header

Every Dockerfile must have a metadata header with the following items:

- **Base Image**: All containers are based on a specific GNU/Linux system. There is no preference for a specific OS flavor but, to reduce disk usage, we recommend to use our own biocontainers/biocontainers image.
- **Dockerfile Version**: This is a single-number version system (ex: v1, v2, v3 ...). Every change in the file must increase in 1.
- **Software**: The name of the software installed inside the container. This can be a little tricky because some software demand libraries or dependencies. In this case the idea is to describe the "principal" software of the container, or the reason for built it.
- **Software Version**: The version of the software installed.
- **Description**: Single line description of the tool.
- **Website**: URL(s) for the program developer.
- **Documentation**: URL(s) containing information about how to use the software.
- **License**: URL(s) containing Licensing information.
- **Tags**: Program tags: Genomics, Protemomics, Transcriptomics, Metabolomics, General.



## Image Setting - FROM

The next element is the base image and any configuration to the system you are installing:

In the example above the Base Image is defined as biocontainers/biocontainers which is based on ubuntu latest LTS (Long Term Support) release and kept up to date with updates.

## Signature - MAINTAINER

The File Author/ Maintainer signature. By default the Dockerfile only accepts one MAINTAINER tag. This will be the place the original author name. After updates are added to the file, the contributors name should appear in commented lines.

~~~

# Maintainer
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br

~~~

## Installation - RUN

The installation area is where you instructions to build the software will be defined. Here is the correct place to put Dockerfile syntax and system commands.

~~~
USER biodocker

RUN ZIP=comet_binaries_2016012.zip && \
  wget https://github.com/BioDocker/software-archive/releases/download/Comet/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /home/biodocker/bin/Comet/ && \
  chmod -R 755 /home/biodocker/bin/Comet/* && \
  rm /tmp/$ZIP

RUN mv /home/biodocker/bin/Comet/comet_binaries_2016012/comet.2016012.linux.exe /home/biodocker/bin/Comet/comet

ENV PATH /home/biodocker/bin/Comet:$PATH

WORKDIR /data/

CMD ["comet"]
~~~

- Commands should be merged with '&& \' whenever possible in order to create fewer intermediate images.
- A biodocker user has been created (id 1001) so that applications are not run as root.
- If possible, add the program to /usr/bin, otherwise, add to /home/biodocker/bin
- return to the regular USER
- change the WORKDIR to the data folder
- set the VOLUME to be exported (/data and /config are exported by default by the base image)
- EXPOSE ports (if necessary)
