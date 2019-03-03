.. _biocontainersregistry

BioContainers Registry
==============================

Every container is deployed and permanent deposited in a public registry `Docker Hub <http://hub.docker.com>`__ or
`Quay.io <quay.io>`__. These two registries allows developers and contributors to deploy their software to a public repository without needs to implement a new registry.

.. note:: The BioContainers community use currently for docker containers two docker registries (quay.io and docker hub). In both cases we use the same name space ``biocontainers`` to group all BioContainers: `Docker Hub <https://hub.docker.com/u/biocontainers>`__ and `Quay.io <https://quay.io/organization/biocontainers>`__

What is Docker Hub
~~~~~~~~~~~~~~~~~~

`Docker Hub <https://docs.docker.com/docker-hub/>`__ provides a centralized resource for container image discovery, distribution and
change management, user and team collaboration, and workflow automation throughout the development pipeline.

Useful Links:

-  `Docker Hub <https://docs.docker.com/docker-hub/>`__ Documentation.
-  `Docker Hub <https://hub.docker.com/>`__

What is Quay.io
~~~~~~~~~~~~~~~~~~

`Quay.io <https://quay.io/>`__ is a non-profit docker registry whose major advantage is that it supports ``docker`` and ``rkt`` technologies. In Quay.io each Container is presented with the maximum amount of useful information, including a full tags list, markdown based description and repository push and pull counts.

The BioContainers Registry
--------------------------

`BioContainers Registry UI <http://biocontainers.pro/registry/>`__ provides the interface to and UI to **search**, **tag**, and
**document** a BioContainers across all the registries.

The users can search containers by using the search box:

The containers registry allow the users to ``sort`` the containers by
any of these properties:

-  **Container Name**: Container Name
-  **Description**: Description Provided by the developer of the
   container.
-  **Real Name**: The corresponding registry + container name
-  **Last Modified**: Last date where the container has been modified.
-  **Starred/Start**: If the container has been starred in any of the
   repos.
-  **Popularity**: How many times a container has been pull from a
   registry.
-  **Registry Link**: the registry Link.

Visualizing a Container Information
-----------------------------------

The user can click the container name `for example, BLAST </101/running-example/>`__ and see all the documentation related
with the container.

.. note:: Depending on the container provider, the registry will show the original ``Dockerfile`` provided by the developer or it will provide the ``Yaml`` (see example) configuration file for the ``Conda based`` containers.



