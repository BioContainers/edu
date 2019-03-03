The latest information about BioContainers is available via
`https://BioContainers.pro <https://Biocontainers.pro/>`__

|Join the chat at https://gitter.im/BioContainers/Lobby|

Containers
----------

Repository of approved bioinformatics containers

Links:
------

Web Page : http://biocontainers.pro/

Project Definition : https://github.com/BioContainers/specs

Contribution Rules :
https://github.com/BioContainers/specs/blob/master/CONTRIBUTING.md

Containers : https://github.com/BioContainers/containers

Containers Development: https://github.com/BioContainers/sandbox

Email : biodockers@gmail.com

License
-------

`Apache 2 <http://www.apache.org/licenses/LICENSE-2.0>`__

Contents
--------

1. `BioContainers Architecture <#1-biocontainers-architecture>`__

2. 1 `How to Request a Container <#11-how-to-request-a-container>`__

3. 2 `Use a Container <#12-use-a-bioContainer.>`__

4. 3 `Reporting problem with
   Container <#13-reporting-a-problem-with-a-container>`__
5. `Get involved <#41-get-involved>`__

1. BioContainers Architecture
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

BioContainers is a community-driven project that allows bioinformatics
to request, build and deploy bioinformatics tools using containers. The
following figure present the general BioContainers workflow:

.. figure:: https://raw.githubusercontent.com/BioContainers/specs/master/imgs/workflow.png
   :alt: What is Container

   What is Container
The next sections explain in details the presented workflow:

-  

   (i) How to request a workflow

-  

   (ii) Use a BioContainer

-  

   (iii) Developing containers

{% hlblock info %} Importantly the BioContainers community designed a
labeled legend to tag each issue in the `containers
repository <http://github.com/BioContainers/containers/issues>`__ that
should be used properly for on each issue. For example, the for the new
containers the label **Container Request** should be used. {% endhlblock
%}

|Containers|\ {:height="250px" class="center"}

1.1 How to Request a Container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Users can request a container by opening an issue in the [containers
repository] (http://github.com/BioContainers/containers/issues)
``(In the previous workflow this is the first step performed by user henrik)``.
The issue should contains the name of the software, the url of the code
or binary to be package and information about the software `see
BioContainers
specification <http://github.com/BioContainers/container-specs.md>`__.
When the containers is deploy and fully functional, the issue will be
close by the developer or the contributor to BioContainers.

1.2 Use a BioContainer.
^^^^^^^^^^^^^^^^^^^^^^^

When a container is deploy and the developer close the issue in GitHub
the user ``(henrik)`` received a notification that the container is
ready. The user can then used `docker <http://www.docker.com>`__ or
`rkt <https://coreos.com/rkt/docs/latest/>`__ to pull or fetch the
corresponding container.

::

    docker run biocontainers/blast

1.3 Reporting a problem with a container
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the user find a problem with a container an issue should be open in
the `container
repository <https://github.com/BioContainers/containers/issues>`__, the
user should use the **broken tag** (see tags). Developers of the project
will pick-up the issue and deploy a new version of the container. A
message will be delivery when the containers has been fixed.

2. Get involved
~~~~~~~~~~~~~~~

Whether you want to make your own software available to others as a
container, to just use them on your pipelines and analysis or just give
opinions, you are most welcome. This is a community-driven project, that
means everyone has a voice.

Here are some general ideas:

-  Browse our list of containers
-  Propose your own ideas or software
-  Interact with other if you think there is something missing.

.. |Join the chat at https://gitter.im/BioContainers/Lobby| image:: https://badges.gitter.im/Join%20Chat.svg
   :target: https://gitter.im/BioContainers/BioContainers?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge
.. |Containers| image:: {{%20site.baseurl}}/img/series/101/labels.png
