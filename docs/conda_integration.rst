.. _conda_integration

Integration with BioConda
=================================

**Biocontainers build automatically docker containers for all BioConda package**. For this reason a BioContainer can be created not only using Dockerfile :ref:`biocontainers`. This automatic containers has the benefit that the user can switch between ``docker`` and ``conda environments`` knowing that the tools are available in both environments.

`Bioconda <https://bioconda.github.io/>`__ is a channel for the conda package manager specializing in bioinformatics software:

- a repository of recipes hosted on GitHub
- a build system that turns these recipes into conda packages
- a repository of more than 6000 bioinformatics packages ready to use with conda install

The conda package manager makes installing software a vastly more streamlined process. Conda is a combination of other package managers you may have encountered, such as ``pip``, ``CPAN``, ``CRAN``, ``Bioconductor``, ``apt-get``, and ``homebrew``. Conda is both language- and OS-agnostic, and can be used to install C/C++, Fortran, Go, R, Python, Java etc programs on Linux, Mac OSX, and Windows.

.. note:: Installing Conda: `Bioconda < https://bioconda.github.io/#install-conda>`__ requires the conda package manager to be installed. If you have an Anaconda Python installation, you already have it. Otherwise, the best way to install it is with the `Miniconda <http://conda.pydata.org/miniconda.html>`__ package. The Python 3 version is recommended.

Defining a Conda package
-------------------------

The preferred way to build a conda package is to write a `conda recipe <https://conda.pydata.org>`_ and submit this it the BioConda communitiy. As soon as your PR is merged and continues integration testing was successful, we will build you automatically a container and publish it at `quay.io/biocontainers <https://quay.io/organization/biocontainers>`_ and `BioContainers Registry <http://biocontainers.pro/registry>`__.

The BioConda specification `Contribution Guide <https://bioconda.github.io/contributing.html>`_ define how to create a recipe. In summary, a BioConda recipe should contain the following parts ():

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
- If the recipe installs custom wrapper scripts, usage notes should be added to ``extra -> notes`` in the meta.yaml.

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

When the recipe is ready a Pull Request should be created (https://bioconda.github.io/contribute-a-recipe.html#push-changes-wait-for-tests-to-pass-submit-pull-request). Finally, the container is automatically created for the new BioConda Package.
