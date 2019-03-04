Advanced topics
==========================

rkt
----------

`rkt <https://coreos.com/rkt/>`__ is a next-generation container manager for Linux clusters. In contrast to the Docker daemon, ``rkt`` is a single binary that is currently available on CoreOS and Kubernetes only. It is designed for
modern Linux clusters environments.

To reference a Docker image, use the ``docker://`` prefix when fetching or running images.

   .. code-block:: bash

      $ rkt --insecure-options=image run docker://biocontainers/comet

According to the original documentation:

This behaves similarly to the Docker client, if no specific registry is named, the Docker Hub is used by default. As with Docker, alternative registries can be used by specifying the registry as part of the image reference.