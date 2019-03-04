
Integration with workflow engines
==================================


Galaxy Integration
---------------------

`Galaxy <https://galaxyproject.org/>`__ tools (also called wrappers) are able to use Conda packages and Docker containers as dependency resolvers. Galaxy recommends to use Conda packages as primary dependency resolver, mainly because Docker is not
available on every (HPC-) system. Conda on the other hand can be installed by Galaxy and maintained entirely in user-space. Nevertheless, Docker (Containers in general) has some unique features and there are many use-cases in the Galaxy community which makes containerized systems very appealing.

Galaxy can be configured to run jobs in container runtimes (read more `here <https://docs.galaxyproject.org/en/latest/admin/jobs.html#running-jobs-in-containers>`__). Currently the two supported runtimes are [Docker](https://www.docker.com) and [Singularity](https://www.sylabs.io/). Each ``<destination>`` can enable container support with ``<param id="docker_enabled">true</param>`` and/or ``<param id="singularity_enabled">true</param>``, as documented in the [advanced sample job_conf.xml](https://github.com/galaxyproject/galaxy/blob/dev/config/job_conf.xml.sample_advanced).

In the case of Docker, containers are run using **sudo** unless ``<param id="docker_sudo">false</param>`` is specified, thus the user that Galaxy runs as should be able to run ``sudo docker`` without a password prompt for Docker containers to work.

The images used for containers can either be specified explicitely in the ``<destination>`` using the **docker_default_container_id**, *docker_container_id_override*, **singularity_default_container_id** and **singularity_container_id_override** parameters, but (perhaps more commonly) the image to use can be derived from the tool requirements of the Galaxy tool being executed. In this latter case the image is specified by the tool using a ``<container>`` tag in the ``<requirements>`` section.

Nextflow Integration
----------------------------
