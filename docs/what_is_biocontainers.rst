.. _biocontainers

BioContainers
===========================

BioContainers is a community-driven project that provides the infrastructure and basic guidelines to create, manage and distribute bioinformatics packages (e.g conda) and containers (e.g docker, singularity). BioContainers is based on the popular frameworks `Conda <https://conda.io/>`__, `Docker <https://www.docker.com/>`__ and `Singularity <https://www.sylabs.io/docs/>`__.

BioContainers Goals
-------------------

-  Provide a base specification to easily build and deploy new bioinformatics software including the source and examples.

-  Define a complete infrastructure to develop, deploy and test new bioinformatics containers using continuous integration suites such as Travis Continuous Integration (https://travisci. org/) or manually built solutions.

-  Provide a series of containers ready to be used by the bioinformatics community (https://biocontainers.pro/registry).

-  Provide guidelines and help on how to create reproducible pipelines by defining, reusing and reporting specific container versions which will consistently produce the exact same result and always be available in the history of the container.

-  Coordinate and integrate developers and bioinformaticians to produce best practices of documentation and software development.

Main components of BioContainers:
---------------------------------

-  `Docker Containers <https://github.com/BioContainers/containers>`__ provides a lit of `Dockerfile recipes` to automatically build containers in BioContainers.

-  `Conda based Containers <https://github.com/bioconda/bioconda-recipes/>`__ provides a list of `Conda recipes` to automatically build **first a conda package** and then a docker container.

-  `Biocontainers Registry <https://biocontainers.pro/registry>`__ is a hosted registry of all biocontainers images that are ready to be used (read more here :doc:`biocontainersregistry`).

-  `Specifications <https://github.com/BioContainers/specs>`__ defines a set of guidelines and rules to contribute with BioContainers.


BioContainers Community Architecture
------------------------------------

BioContainers is a community-driven project that allows bioinformaticians/developers to request, build and deploy bioinformatics containers. The following figure present the general BioContainers Architecture:

.. image:: images/arch.png
   :alt: BioContainers Architecture.

How to Request a Container
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Users can request a container by opening an issue in the `containers repository <http://github.com/BioContainers/containers/issues>`__ , In the previous workflow this is ``the first step`` performed by user ``henrik``. The issue should contains the name of the software, the url of the code or binary to be package and information about the software `see BioContainers specification <http://github.com/BioContainers/container-specs.md>`__. When the containers is deploy and fully functional, the issue will be close by the developer or the contributor to BioContainers.

.. note:: Before requesting a Container you should check the `BioContainers Registry <http://biocontainers.pro/registry>`__ to make sure your requested tool do not exist already (read more about the registry in: :doc:`biocontainersregistry`).

.. hint:: Importantly, the BioContainers community has implemented a "labeled legend" to tag each issue in the `containers repository <http://github.com/BioContainers/containers/issues>`__ that should be used properly for on each issue. For example, the for the new containers the label **Container Request** should be used.

Use a Docker BioContainer.
~~~~~~~~~~~~~~~~~~~~~~~~~~

When a container is deploy and the developer close the issue in GitHub the user ``henrik`` received a notification that the container is ready. Then, the user can use ``docker`` command to pull or fetch the corresponding container.

.. code-block:: bash

   $ docker run biocontainers/blast

.. note:: You can read other sections about :doc:`condapackages` and :doc:`singularitycontainers`

Reporting a problem with a container
-------------------------------------

If the user find a problem with a container an issue should be open in
the `container repository <https://github.com/BioContainers/containers/issues>`__, the user should use the **broken tag** (`see tags <https://github.com/BioContainers/containers/labels>`_). Developers of the project will pick-up the issue and deploy a new version of the container. A message will be delivery when the containers has been fixed.


Get involved
----------------------

|Slack|    |Gitter|      |IRC|

Whether you want to make your own software available to others as a container, to just use them on your pipelines and analysis or just give opinions, you are most welcome. This is a community-driven project, that
means everyone has a voice.

Here are some general ideas:

-  Browse our list of containers
-  Propose your own ideas or software
-  Interact with other if you think there is something missing.


.. |Slack| image:: https://img.shields.io/badge/slack-join%20chat-ff69b4.svg
   :target: https://biocontainers.slack.com
.. |Gitter| image:: https://badges.gitter.im/BioJS.png
   :target: https://gitter.im/biocontainers/Lobby
.. |IRC| image:: https://img.shields.io/badge/irc-%23BioContainers-yellow.svg
   :target: https://kiwiirc.com/client/irc.freenode.net/BioContainers

