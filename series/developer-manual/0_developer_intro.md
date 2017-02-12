---
title: 'Developer Intro'
layout: series_item
series: 'developer-manual'
permalink: /developer-manual/developer-intro/
estimated-time: 5
---

Before stating to contribute to BioContainers you should check your system for the following dependencies:

* [Git](https://github.com) is a version control system that will keep track of the changes you have made in code.

{% hlblock info %}
If you want to fresh up your `git` skills, check out the [Full Introduction for Bioinformatics](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004947) or [15 minutes interactive lesson](https://try.github.io/levels/1/challenges/1) by Codeschool.
{% endhlblock %}


Developing containers
-----------------------

BioContainers has two major ways of creating containers: **Dockefile based images** and **DockerFile less images**

### Developing Dockerfile based containers



### Developing mulled containers

BioContainers offers a very easy way to create efficient containers that are minimal in size,
tested and not rely on writing a Dockerfile.

The preferred way to do this is to write a [conda package](https://conda.pydata.org)
and submit this it the BioConda communtiy. As soon as your PR is merged and continues
integration testing was successful, we will build you automatically a container and publish
it at [quay.io/biocontainers](https://quay.io/organization/biocontainers).

The BioConda specification [Contribution Guide](https://bioconda.github.io/contributing.html) define how to create a recipe. In summary,
a BioConda recipe should contain the following parts ():

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
- If the recipe installs custom wrapper scripts, usage notes should be added to ```extra -> notes``` in the meta.yaml.

Example Yaml for bowtie2:

~~~
about:
  home: 'http://bowtie-bio.sourceforge.net/bowtie2/index.shtml'
  license: GPLv3
  summary: Fast and sensitive read alignment

package:
  name: bowtie2
  version: 2.3.0

source:
  fn: bowtie2-2.3.0-source.zip
  url: http://downloads.sourceforge.net/project/bowtie-bio/bowtie2/2.3.0/bowtie2-2.3.0-source.zip
  sha256: f9f841e780e78b1ae24b17981e2469e6d5add90ec22ef563af23ae2dd5ca003c
  patches:
    - bowtie2.patch

build:
  number: 1

requirements:
  build:
    - gcc   # [linux]
    - llvm  # [osx]
    - python
    - tbb
  run:
    - python
    - perl-threaded
    - libgcc    # [linux]
    - tbb

test:
  commands:
    - bowtie2 --help
    - bowtie2-align-l --help
    - bowtie2-align-s --help
    - bowtie2-build --help
    - bowtie2-build-l --help
    - bowtie2-build-s --help
    - bowtie2-inspect --help
    - bowtie2-inspect-l --help
    - bowtie2-inspect-s --help
~~~

When the recipe is ready a Pull Request should be created (https://bioconda.github.io/contribute-a-recipe.html#push-changes-wait-for-tests-to-pass-submit-pull-request). Finally
the container is automatically created for the new BioConda Package.