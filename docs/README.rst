F5 Docs-Like-Code Training
==========================

Introduction
------------

This training repo can be used by any project that follows the docs-like-code method to create and publish documentation.

.. important:: 

   For documentation specific to Project Blue, see `Blue API Docs Training </guides/blue/blue-tools-workflow.md>`_.

.. toctree::
   :glob:
   :hidden:

   pages/*
   pages/foo/*

Project Setup
-------------

1. Fork this repo to your account.
    
   .. note:: 
   
      You'll need to request access to contribute to this project before you can fork it.    

2. Clone your fork to your local dev machine / laptop.

   ::

      git clone <your-fork>
      cd f5-docs-training

3. Install the project requirements.

   ::

      pip install –r requirements.txt


   .. tip::

      If you regularly use Python, we recommend doing this in a `virtual environment`_ to avoid package version conflicts.

How to build documentation
--------------------------

#. Clone this repo using the ``https`` or ``ssh`` link.

#. Install the requirements using ``pip install -r requirements.txt``, then run ``make html`` in your terminal of choice.
   
   --OR--   
   
#. Install `Docker <https://www.docker.com/>`_ and run ``make docker-docs``.

#. Open ``index.html`` in your browser.

How to Test Documentation
-------------------------

Just like code, all docs must pass quality tests and undergo peer code review prior to release.

Add the contents of the ./scripts directory to your project to test sphinx syntax, validate links, and check grammar.

.. important::

   Run the ``make`` command from the directory containing the makefile.
   If you choose to run the command from a different directory, use the ``-C`` flag to identify the directory where the makefile lives.


Manual testing
``````````````

Run the test-docs script locally
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the command below in a terminal.

::

   ./scripts/test-docs.sh


Run the test-docs script in a Docker container
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Run the ``docker-test`` make command.

   ::

      make docker-test


Set up automated testing with GitLab-CI for your project
````````````````````````````````````````````````````````

To run docs tests automatically using GitLab CI (for GitLab and GitSwarm projects):

1. Add the scripts/ directory to your project.

2. Add the following to your ``.gitlab-ci.yaml``:

   ::

      build docs:
      image: f5devcentral/containthedocs:latest
      script:
        - ./scripts/test-docs.sh
      tags:
        - docker
      stage: test


   .. note::

      - You can set the ``stage`` as appropriate for your project.


Set up automated testing with Travis-CI for your GitHub project
```````````````````````````````````````````````````````````````

1. Add the scripts/ directory to your project.
2. Add the following to your ``.travis.yaml``:

   ::

      sudo: required
      services:
      - docker
      before_install:
      - docker pull f5devcentral/containthedocs:latest
      install: true
      script:
      - ./scripts/docker-docs.sh ./scripts/test-docs.sh


Example Sphinx project
----------------------

The ``new_project_setup/`` directory in this repo contains an example Sphinx project.
Copy the entire directory into your project and you're ready to start writing, building, and publishing docs like code!


.. _virtual environment: https://virtualenv.pypa.io/en/stable/
