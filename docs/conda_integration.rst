.. _conda_integration

Integration with BioConda
=================================

**Biocontainers build automatically docker containers for all BioConda package**. For this reason a BioContainer can be created not only using Dockerfile :ref:`biocontainers`. This automatic containers has the benefit that the user can switch between ``docker`` and ``conda environments`` knowing that the tools are available in both environments.

`Bioconda <https://bioconda.github.io/>`__ is a channel for the conda package manager specializing in bioinformatics software:

- a repository of recipes hosted on GitHub
- a build system that turns these recipes into conda packages
- a repository of more than 6000 bioinformatics packages ready to use with conda install

The conda package manager makes installing software a vastly more streamlined process. Conda is a combination of other package managers you may have encountered, such as ``pip``, ``CPAN``, ``CRAN``, ``Bioconductor``, ``apt-get``, and ``homebrew``. Conda is both language- and OS-agnostic, and can be used to install C/C++, Fortran, Go, R, Python, Java etc programs on Linux, Mac OSX, and Windows.

.. note:: Installing Conda: `Bioconda <https://bioconda.github.io/#install-conda>`__ requires the conda package manager to be installed. If you have an Anaconda Python installation, you already have it. Otherwise, the best way to install it is with the `Miniconda <http://conda.pydata.org/miniconda.html>`__ package. The Python 3 version is recommended.

Defining a Conda package
-------------------------

The preferred way to build a conda package is to write a `conda recipe <https://conda.pydata.org>`_ and submit this it the BioConda community. As soon as your PR is merged and continues integration testing was successful, we will build you automatically a container and publish it at `quay.io/biocontainers <https://quay.io/organization/biocontainers>`_ and `BioContainers Registry <http://biocontainers.pro/#/registry>`__.

The BioConda specification `Contribution Guide <https://bioconda.github.io/contributing.html>`_ define how to create a recipe. In summary, a BioConda recipe should contain the following parts:

- Source URL is stable (details)
- md5 or sha256 hash included for source download (details)
- Appropriate build number (details)
- .bat file for Windows removed (details)
- Remove unnecessary comments (details)
- Adequate tests included
- Files created by the recipe follow the FSH (details)
- License allows redistribution and license is indicated in meta.yaml
- Package does not already exist in the defaults, r, or conda-forge channels with some
  exceptions (details)
- Package is appropriate for bioconda
- If the recipe installs custom wrapper scripts, usage notes should be added to ``extra -> notes`` in the meta.yaml

Example Yaml for bowtie2:

.. code-block:: yaml

   package:
     name: unicycler
     version: 0.3.0b

   build:
     number: 0
     skip: True # [py27]

   source:
     fn: unicycler_0.3.0b.tar.gz
     url: https://github.com/rrwick/Unicycler/archive/906a3e7f314c7843bf0b4edf917593fc10baee4f.tar.gz
     md5: 5f06d2bd8ef5065c8047421db8c7895f

   requirements:
     build:
     - python
     - setuptools
     - gcc

     run:
     - python
     - libgcc
     - spades >=3.6.2
     - pilon
     - java-jdk
     - bowtie2
     - samtools >=1.0
     - blast
     - freebayes

   test:
     commands:
       - unicycler -h
       - unicycler_align -h
       - unicycler_check -h
       - unicycler_polish -h

   about:
     home: https://github.com/rrwick/Unicycler
     license: GPL-3.0
     license_file: LICENSE
     summary: 'Hybrid assembly pipeline for bacterial genomes'

When the recipe is ready, a Pull Request should be created (https://bioconda.github.io/contributor/workflow.html). Finally, the container is automatically created for the new BioConda Package.


Automatic build from conda recipes
-----------------------------------

We utilize `mulled <https://github.com/mulled/mulled>`_ with `involucro <https://github.com/involucro/involucro>`_ in an automatic way. This is for example used to convert all packages in ``bioconda`` into Linux Containers (Docker and rkt at the moment). We have developed small utilities around this technology stack which is currently included in galaxy-lib.

.. code-block:: bash

   pip install galaxy-lib

Here is a short introduction:

Search for conda-based containers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This will search for containers in the biocontainers organisation.

.. code-block::bash

   $ mulled-search -s vsearch -o biocontainers

Build all packages from bioconda from the last 24h
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The BioConda community is building a container for every package they create with a command similar to this:

.. code-block:: bash


   $ mulled-build-channel --channel bioconda --namespace biocontainers \
         --involucro-path ./involucro --recipes-dir ./bioconda-recipes --diff-hours 25 build

Building Docker containers for local Conda packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Conda packages can be tested with creating a busybox-based container for this particular package in the following way.
This also demonstrates how you can build a container locally and on-the-fly.

.. note:: We modified the samtools package to version 3.0 to make clear we are using a local version.


1) Build your recipe

.. code-block:: bash

   $ conda build recipes/samtools

2) Index your local builds

.. code-block:: bash

   $ conda index /home/bag/miniconda2/conda-bld/linux-64/

3) Build a container for your local package

.. code-block:: bash

   $ mulled-build build-and-test 'samtools=3.0--0' \
         --extra-channel file://home/bag/miniconda2/conda-bld/ --test 'samtools --help'

The ``--0`` indicates the build version of the conda package. It is recommended to specify this number otherwise
you will override already existing images. For Python Conda packages this extension might look like this ``--py35_1``.

Build, test and push a conda-forge package to biocontainers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: You need to have write access to the biocontainers repository

You can build packages from other Conda channels as well, not only from BioConda. ``pandoc`` is available from the conda-forge channel and conda-forge is also enabled by default in Galaxy. To build ``pandoc`` and push it to BioContainers, you could do something along these lines:

.. code-block:: bash


      $ mulled-build build-and-test 'pandoc=1.17.2--0' --test 'pandoc --help' -n biocontainers
      $ mulled-build push 'pandoc=1.17.2--0' --test 'pandoc --help' -n biocontainers


* Galaxy Conda documentation: ./conda_faq.rst
* IUC: https://wiki.galaxyproject.org/IUC
* Container annotation:  https://github.com/galaxyproject/galaxy/blob/dev/test/functional/tools/catDocker.xml#L4
* BioContainers: https://github.com/biocontainers
* bioconda: https://github.com/bioconda/bioconda-recipes
* BioContainers Quay.io account: https://quay.io/organization/biocontainers
* galaxy-lib: https://github.com/galaxyproject/galaxy-lib
