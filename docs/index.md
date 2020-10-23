---
layout: page
title: Home
navigation: 1
---

![logo](https://raw.githubusercontent.com/CRG-CNAG/BioCoreMiscOpen/master/logo/biocore-logo_small.png) 

# ELIXIR_containers_nextflow

ELIXIR VIB-CRG courses on containers (Docker + Singularity) and Nextflow.

Webpage [https://biocorecrg.github.io/ELIXIR_containers_nextflow/](https://biocorecrg.github.io/ELIXIR_containers_nextflow/)

## When & Where

26 & 27 Oct 2020 - online<br>

Schedule:
- 9:30  - 11:00 - session
- 11:00 - 11:15 - break
- 11:15 - 12:45 - session
- 12:45 - 13:45 - lunch
- 13:45 - 15:15 - session
- 15:15 - 15:30 - break
- 15:30 - 17:00 - session

## Target audience

Bioinformaticians with no or little knowledge of containers.

## Requirements

If trainees bring their own laptop, they should install:

* VNC viewer

* Discord / Zoom / GoTo meeting

## Format

2 full days:
* Day 1: Containers
  * Introduction to containers
    * History of containers
    * What are containers? Why to use them?
    * Containers vs. virtual machines
  * Docker
    * Installation
    * Images and containers
    * Docker architecture
    * Docker files, Docker image layers, Docker caching
    * Docker hub: get images from and load images to: *push, pull*
    * Build and run Docker image from existing recipe:
      * Build and from recipe *build, run*
      * Use Docker image interactively *run -it*
      * Checking running containers, stopping a starting containers: *ps, rm*
      * Remove images: *rmi*
      * Exporting containers into tar files and importing them back
      * Tagging an image: *tag*
    * Docker "recipes":
      * Understand the main sections: *FROM, RUN, ADD, ENV, CP*
      * Write basic recipe: e.g. Ubuntu base layer + ncbi-blast
      * Build and run.
    * Working with volumes: *docker run -v ...*
    * Working with ports
  * Singularity
    * Installation ?
    * Differences between Singularity and Docker: why and when to use one or the other. Pros and cons.
    * Building a basic Singularity image
      * Pull and run an image with Singularity, from Docker hub or local Docker daemon
      * Singularity "recipes"
    * Use Singularity image interactively: *singularity shell*
    * Volumes in Singularity
    * Instances

* Day 2: Nextflow
  * Installation, update and versioning
  * Simple Nextflow pipeline given as an example:
    * Run pipeline
    * Going into detail
      * understand config and pipeline (.nf) files
      * *work* job directory structure
      * PID and log files
    * Pipeline modification and resume
  * Basic concepts
   * processes
     * input
     * output
     * script
     * when
     * directives: tag, publishDir, etc.
   * channels
   * operators
  * Write and run a simple Nextflow pipeline (e.g. print text, process a simple calculation)
  * Executors
    * local vs queue vs cloud systems
    * memory, time and CPU allocation
  * Including Docker and Singularity containers in Nextflow pipelines
  * Additional functions
    * Tracing, charts
    * Workflow
    * Mail notification
    * Web monitoring: tower.nf

## Learning objectives

* Learn the concept of containers: what is a container, what is an image ?
* Understand the difference between Docker and Singularity
* Understand a container's "recipe"
* Learn about Docker hub
* Understand Nextflow's basic concepts: processes, channels, ...
* Learn how to write and run a Nextflow pipeline

## Learning outcomes

* Docker images and containers: run, push, pull, remove
* Write Docker recipe
* Build and run Docker image
* Pull and push Docker container to / from Docker hub
* Pull Docker container as Singularity image
* Write and run a simple Nextflow pipeline
* Write and run a simple Nextflow pipeline using a Singularity container




## Instructors

|[Luca Cozzuto](mailto:luca.cozzuto@crg.eu)|[Toni Hermoso](mailto:toni.hermoso@crg.eu) |
| :---:  | :---:  |
|<a href="https://biocore.crg.eu/wiki/User:Lcozzuto"><img src="images/lcozzuto.jpg" width="100"/> </a>|<a href="https://biocore.crg.eu/wiki/User:Thermoso"><img src="images/Thermoso.jpg" width="100"/>| 

from the [CRG](https://www.crg.eu/) [Bioinformatics core facility](https://biocore.crg.eu/) in Barcelona, Catalonia, Spain.


## Prerequisites

[Familiarity with the Linux command line](https://biocorecrg.github.io/advanced_linux_2019/)

|          |       |
| :------- | :---: |
| [Home](https://biocorecrg.github.io/ELIXIR_containers_nextflow/)  | [Next page](https://biocorecrg.github.io/ELIXIR_containers_nextflow/introduction_containers.html) |

