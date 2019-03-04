
Integration with workflow engines
==================================


Galaxy Integration
---------------------

`Galaxy <https://galaxyproject.org/>`__ tools (also called wrappers) are able to use Conda packages and Docker containers as dependency resolvers. Galaxy recommends to use Conda packages as primary dependency resolver, mainly because Docker is not
available on every (HPC-) system. Conda on the other hand can be installed by Galaxy and maintained entirely in user-space. Nevertheless, Docker (Containers in general) has some unique features and there are many use-cases in the Galaxy community which makes containerized systems very appealing.

Galaxy supports running tools in Docker containers via a special `container annotation`_ inside of the requirement field.

.. code-block:: xml
       <requirements>
           <!-- Container based dependency handling -->
           <container type="docker">busybox:ubuntu-14.04</container>
           <!-- Conda based dependency handling -->
           <requirement type="package" version="8.22">gnu_coreutils</requirement>
       </requirements>

Here we demonstrate a solution that can create Containers out of Conda packages automatically. This can be either used to support communities like BioContainers_ to create Containers
before deploying a Galaxy tool, or this can be used by Galaxy to create Containers on-demand and on-the-fly if one is not available already.


