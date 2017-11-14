---
title: 'Registry UI'
layout: series_item
contributors: Yassset Perez-Riverol
series: '101'
permalink: /101/biocontainers-registry/
estimated-time: 5
---

Every Biocontainer is deployed and permanent deposited in a public registry [Docker Hub](http://hub.docker.com) or [Quay.io](quay.io). These two registries allows developers and contributors 
to deploy their software to a public repository without needs to implement a new registry. 

### What is Docker Hub 

[Docker Hub](https://docs.docker.com/docker-hub/) is a cloud-based registry service which allows you to link to code repositories, build your images and test them, stores manually pushed images,
and links to Docker Cloud so you can deploy images to your hosts. It provides a centralized resource for container image discovery, distribution and change management,
user and team collaboration, and workflow automation throughout the development pipeline.
 
Useful Links: 

- [Docker Hub](https://docs.docker.com/docker-hub/) Documentation. 
- [Docker Hub](https://hub.docker.com/)
  
### What is Quay.io 


Quay.io is a non-profit docker registry whose major advantage is that it supports `docker` and `rkt` technologies. In Quay.io each Container is presented with the maximum amount of useful information, including a full tags list, markdown based 
description and repository push and pull counts. Repositories can be linked to GitHub, BitBucket, GitLab or custom git repositories, with automatic building of the Dockerfile(s) found on push.


## The BioContainers Registry

[BioContainers Registry UI](http://biocontainers.pro/registry/) provides the interface to and UI to **search**, **tag**, and **document** a BioContainers across all the registries.

 
<img class="splashIcon" src="{{ site.baseurl}}/img/series/101/registry.png" width="800px">      

The users can search containers by using the search box: 


<img class="splashIcon" src="{{ site.baseurl}}/img/series/101/search.png" width="800px">  


                                                                                                                                                 
The containers registry allow the users to `sort` the containers by any of these properties: 
  
- **Container Name**: Container Name  
- **Description**: Description Provided by the developer of the container.  
- **Real Name**: The corresponding registry + container name 
- **Last Modified**: Last date where the container has been modified.
- **Starred/Start**: If the container has been starred in any of the repos. 
- **Popularity**: How many times a container has been pull from a registry. 
- **Registry Link**: the registry Link. 

## Visualizing a Container Information

The user can click the container name [for example, BLAST](/101/running-example/) and see all the documentation related with the container. 

<img class="splashIcon" src="{{ site.baseurl}}/img/series/101/blast.png" width="400px">  

{% alert info %}
 
Depending on the container provider, the registry will show the original `Dockerfile` provided by the developer or it will provide the `Yaml` (see example) configuration file for the `Dockerfile free`
containers. 

{% endalert %} 

<img class="splashIcon" src="{{ site.baseurl}}/img/series/101/bedtools.png" width="400px">  

                                                                                                                                                                                                                                                                                                                       
