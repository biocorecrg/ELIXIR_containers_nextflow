# ELIXIR_containers_nextflow

ELIXIR VIB-CRG courses on containers (Docker + Singularity) and Nextflow.

## When & Where ?

Mon 11 & Tue 12 May 2020

Clemenspoort Ghent (confirmed). 

## Target audience

Bioinformaticians with no or little knowledge of containers.

## Requirements

If trainees bring their own laptop, they should install:
* ...

## Format

2 full days, organized as follows:
* Day 1: containers
  * Introduction to containers
    * History of containers
    * What are containers? Why use them?
    * Containers vs virtual machines
  * Docker
    * Installation
    * Images and containers
    * Docker architecture
    * Docker files, Docker image layers, Docker caching
    * Docker hub: get images from and load images to: *push, pull*
    * Build and run Docker image from existing recipe:
      * Build and from recipe *build, run*
      * Use Docker image interactively *run -it*
      * Checki running containers, stopping an starting containers: *ps, rm*
      * Remove images: *rmi*
      * Exporting containers into tar files and importing them back
      * Tagging an image: *tag*
    * Docker "recipes":
      * Understand the main sections: *FROM, RUN, ADD, ENV, CP*
      * Write basic recipe: e.g. Ubuntu base layer + ncbi-blast
      * Build and run.
    * Working with volumes: *docker run -v ...*
    * Working with ports
    * ...
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
    * Pipeline modication and resume
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


## Useful resources

* https://docker-curriculum.com/
* https://www.tutorialspoint.com/docker/index.htm
* https://intellipaat.com/blog/tutorial/devops-tutorial/docker-tutorial/
* http://containertutorials.com/
* https://singularity-tutorial.github.io/
* https://github.com/biocorecrg/containers-course
* https://www.nextflow.io/docs/latest/index.html
* https://nf-co.re/usage/nextflow_tutorial
