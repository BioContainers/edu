``rkt`` is a next-generation container manager for Linux clusters. In
contrast to the Docker daemon, ``rkt`` is a single binary that is
currently available on CoreOS and Kubernetes only. It is designed for
modern Linux clusters environments.

It is also possible to run Docker-based images with ``rkt``. Since there
is no signature verification, the only difference relies on the running
syntax:

To reference a Docker image, use the ``docker://`` prefix when fetching
or running images.

::

    > rkt --insecure-options=image run docker://biocontainers/comet

According to the original documentation:

This behaves similarly to the Docker client, if no specific registry is
named, the Docker Hub is used by default. As with Docker, alternative
registries can be used by specifying the registry as part of the image
reference. For example, the following command will fetch an nginx Docker
image hosted on quay.io:

::

    > rkt --insecure-options=image fetch docker://quay.io/biocontainers/blast

Since the BioContainers images have no difference from traditional
containers, you can also use ``rkt`` to manage and execute the
containers.
