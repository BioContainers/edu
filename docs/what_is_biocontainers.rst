What is BioContainers?
===========================

BioContainers is a community-driven project that provides the infrastructure and basic guidelines to create, manage and distribute bioinformatics packages (e.g conda) and containers (e.g docker) with special focus on proteomics, genomics, transcriptomics and metabolomics.

BioContainers are based on the popular frameworks **Conda** and **Docker**. A revolutionary platform for developers and sysadmins to build, ship, and run applications anywhere. For example, with Docker you can build an image containing your software and all dependencies and ship it ready to use.

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

-  `Biocontainers Registry <https://biocontainers.pro/registry>`__ is a hosted registry of all biocontainers images that are ready to be used.

-  `Specifications <https://github.com/BioContainers/specs>`__ defines a set of guidelines and rules to contribute with BioContainers.



