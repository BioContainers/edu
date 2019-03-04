.. _conda_integration

Integration with BioConda
=================================


Developing mulled containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

BioContainers offers a very easy way to create efficient containers that are minimal in size,
tested and not rely on writing a Dockerfile.

The preferred way to do this is to write a `conda package <https://conda.pydata.org>`_
and submit this it the BioConda communtiy. As soon as your PR is merged and continues
integration testing was successful, we will build you automatically a container and publish
it at `quay.io/biocontainers <https://quay.io/organization/biocontainers>`_.

The BioConda specification `Contribution Guide <https://bioconda.github.io/contributing.html>`_ define how to create a recipe. In summary,
a BioConda recipe should contain the following parts ():


* Source URL is stable (details)
* md5 or sha256 hash included for source download (details)
* Appropriate build number (details)
* .bat file for Windows removed (details)
* Remove unnecessary comments (details)
* Adequate tests included
* Files created by the recipe follow the FSH (details)
* License allows redistribution and license is indicated in meta.yaml
* Package does not already exist in the defaults, r, or conda-forge channels with some
  exceptions (details)
* Package is appropriate for bioconda
* If the recipe installs custom wrapper scripts, usage notes should be added to ``extra -> notes`` in the meta.yaml.

Example Yaml for bowtie2:

.. code-block::


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

When the recipe is ready a Pull Request should be created (https://bioconda.github.io/contribute-a-recipe.html#push-changes-wait-for-tests-to-pass-submit-pull-request). Finally
the container is automatically created for the new BioConda Package.
