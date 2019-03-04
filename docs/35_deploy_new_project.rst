.. role:: raw-html-m2r(raw)
   :format: html


----

title: 'Deploy to DockerHub'
layout: series_item
contributors: Yassset Perez-Riverol
series: 'developer-manual'
permalink: /developer-manual/deploy-dockerhub/

estimated-time: 5
-----------------

In order to deploy a new Docker project with your software you must follow this steps:


#. 
   Clone our `Sandbox <https://github.com/BioContainers/sandbox>`_ repository

#. 
   Create a folder to your program with the necessary files following our `guidelines <https://github.com/BioContainers/specs/wiki/Project-organization>`_.

#. 
   `Create a Dockerfile <https://github.com/BioContainers/specs/wiki/Dockerfile-template>`_ following the general guidelines.

#. 
   Build the container in your own computer and test the image. If it works properly, then you may follow.

#. 
   Push the container to your fork of our Sandbox and create an pull request following our `contribution guidelines <https://github.com/BioContainers/specs/blob/master/CONTRIBUTING.md>`_.If you can't do that, try our public Gitter chat 
   .. image:: https://badges.gitter.im/Join%20Chat.svg
      :target: https://gitter.im/BioContainers/BioContainers?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge
      :alt: Join the chat at https://gitter.im/BioContainers/BioContainers

   so that we can help you adding your program.

#. 
   Upon acceptance, we will create an :raw-html-m2r:`<a href="https://docs.docker.com/docker-hub/builds/">automatic build</a>` on DockerHub (this will allow people to search for the container using docker search).

#. 
   Spread the news!
