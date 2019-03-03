BioContainers Architecture
==============================

BioContainers is a community-driven project that allows bioinformaticians/developers to request, build and deploy bioinformatics containers. The following figure present the general BioContainers Architecture:

.. image:: images/workflow.png
   :alt: BioContainers Architecture.

How to Request a Container
-------------------------------

Users can request a container by opening an issue in the [containers repository] (http://github.com/BioContainers/containers/issues). ``(In the previous workflow this is the first step performed by user henrik)``. The issue should contains the name of the software, the url of the code or binary to be package and information about the software `see BioContainers specification <http://github.com/BioContainers/container-specs.md>`__. When the containers is deploy and fully functional, the issue will be close by the developer or the contributor to BioContainers.

.. note:: Importantly, the BioContainers community has implemented a "labeled legend" to tag each issue in the `containers repository <http://github.com/BioContainers/containers/issues>`__ that should be used properly for on each issue. For example, the for the new containers the label **Container Request** should be used.

Use a BioContainer.
----------------------

When a container is deploy and the developer close the issue in GitHub the user ``(henrik)`` received a notification that the container is ready. Then, the user can use `docker <http://www.docker.com>` to pull or fetch the corresponding container.

.. code-block:: bash

   $ docker run biocontainers/blast

Reporting a problem with a container
-------------------------------------

If the user find a problem with a container an issue should be open in
the `container repository <https://github.com/BioContainers/containers/issues>`__, the user should use the **broken tag** (see tags). Developers of the project will pick-up the issue and deploy a new version of the container. A message will be delivery when the containers has been fixed.

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