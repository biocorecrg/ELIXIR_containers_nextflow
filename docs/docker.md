---
layout: page
title: Docker
navigation: 3
---

# Docker

- [Introduction to Docker](#introduction-to-docker)
- [Docker hub](#docker-hub)
   + [Running existing images](#running-existing-images)
   + [Manipulate image](#manipulate-image)
- [Docker recipes](#docker-recipes)


## Introduction to Docker

<a href="https://connpass-tokyo.s3.amazonaws.com/thumbs/80/52/80521f18aec0945dfedbb471dad6aa1a.png"><img src="https://connpass-tokyo.s3.amazonaws.com/thumbs/80/52/80521f18aec0945dfedbb471dad6aa1a.png" width="400/"></a>

* Platform for developing, shipping and running applications
* Infrastructure as application / code
* First version: 2013
* Company. Original dotCloud (2010), later named Docker
* Established [Open Container Initiative](https://www.opencontainers.org/)

As a software:
* [Docker Community Edition](https://www.docker.com/products/container-runtime)
* Docker Enterprise Edition

**Docker components**

<a href="http://apachebooster.com/kb/wp-content/uploads/2017/09/docker-architecture.png"><img src="http://apachebooster.com/kb/wp-content/uploads/2017/09/docker-architecture.png" width="700/"></a>

* Read-only templates
* Containers are run from them
* Images are not run
* Images have several layers

<a href="https://i.stack.imgur.com/vGuay.png"><img src="https://i.stack.imgur.com/vGuay.png" width="700/"></a>


**Images versus containers**

Image: set of layers. read-only templates. Inert.
An instance of an image is called a container.
When you start an image, you have a running container of this image. You can have many running containers of the same image.

The image is the recipe, the container is the cake.

https://stackoverflow.com/questions/23735149/what-is-the-difference-between-a-docker-image-and-a-container

**Docker vocabulary**

```bash
docker
```

<img src="images/docker_vocab.png" width="550/">

Get help:

```bash
docker run --help
```

<img src="images/docker_run_help.png" width="550/">


## Using existing images

### Explore Docker hub

Images can be stored locally or shared in a registry.
<br>
[Docker hub](https://hub.docker.com/) is the main public registry for Docker images.
<br>

Let's search the keyword **ubuntu**:

<img src="images/dockerhub_ubuntu.png" width="900/">

### docker pull: import image

* get latest image / latest release

```bash
docker pull ubuntu
```

<img src="images/docker_pull.png" width="650/">


* choose the version of Ubuntu you are fetching: check the different tags

<img src="images/dockerhub_ubuntu_1804.png" width="850/">

```bash
docker pull ubuntu:18.04
```

### Biocontainers

https://biocontainers.pro/

Specific directory of Bioinformatics related entries

* Entries in [Docker hub](https://hub.docker.com/u/biocontainers) and/or [Quay.io](https://quay.io) (RedHat registry)
* Normally created from [Bioconda](https://bioconda.github.io)

Example: **FastQC**

https://biocontainers.pro/#/tools/fastqc

    docker pull biocontainers/fastqc:v0.11.9_cv7

### docker images: list images

```bash
docker images
```
<img src="images/docker_images_list.png" width="650/">

Each image has a unique **IMAGE ID**.

### docker run: run image, i.e. start a container

Now we want to use what is **inside** the image.
<br>
**docker run** creates a fresh container (active instance of the image) from a **Docker (static) image**, and runs it.

<br>
The format is:<br>
docker run image:tag **command**

```bash
docker run ubuntu:18.04 /bin/ls
```

<img src="images/docker_run_ls.png" width="200/">

Now execute **ls** in your current working directory: is the result the same?

<br>

You can execute any program/command that is stored inside the image:

```bash
docker run ubuntu:18.04 /bin/whoami
docker run ubuntu:18.04 cat /etc/issue
```

You can either execute programs in the image from the command line (see above) or **execute a container interactively**, i.e. **"enter"** the container.

```bash
docker run -it ubuntu:18.04 /bin/bash
```

Run container as daemon (in background)

```bash
docker run --detach ubuntu:18.04 tail -f /dev/null
```

Run container as daemon (in background) with a given name

```bash
docker run --detach --name myubuntu ubuntu:18.04 tail -f /dev/null
```

### docker ps: check containers status

List running containers:

```bash
docker ps
```

List all containers (whether they are running or not):

```bash
docker ps -a
```

Each container has a unique ID.

### docker exec: execute process in running container

```bash
docker exec myubuntu uname -a
```

* Interactively

```bash
docker exec -it myubuntu /bin/bash
```

### docker stop, start, restart: actions on container

Stop a running container:

```bash
docker stop myubuntu

docker ps -a
```

Start a stopped container (does NOT create a new one):

```bash
docker start myubuntu

docker ps -a
```

Restart a running container:

```bash
docker restart myubuntu

docker ps -a
```

Run with restart enabled

```bash
docker run --restart=unless-stopped --detach --name myubuntu2 ubuntu:18.04 tail -f /dev/null
```
* Restart policies: no (default), always, on-failure, unless-stopped

Update restart policy

```bash
docker update --restart unless-stopped myubuntu
```

### docker rm, docker rmi: clean up!

```bash
docker rm myubuntu
docker rm -f myubuntu
```

```bash
docker rmi ubuntu:18.04
```

#### Major clean

Check used space
```bash
docker system df
```

Remove unused containers (and others) - **DO WITH CARE**
```bash
docker system prune
```

Remove ALL non-running containers, images, etc. - **DO WITH MUCH MORE CARE!!!**
```bash
docker system prune -a
```

* Reference: https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes

## Volumes

Docker containers are fully isolated. It is necessary to mount volumes in order to handle input/output files.

Syntax: **--volume/-v** *host:container*

```bash
mkdir datatest
touch datatest/test
docker run --detach --volume $(pwd)/datatest:/scratch --name myfastqc biocontainers/fastqc:v0.11.9_cv7 tail -f /dev/null
docker exec -ti fastqc /bin/bash
> ls -l /scratch
> exit
```

* Exercises:
1. Copy the 2 fastq files from available datasets in Github repository and place them in mounted directory
2. Run fastqc interactively (inside container): ```fastqc  /scratch/myfastq.fastq.gz```
3. Run fastqc outside the container

## Ports

The same as with volumes, but with ports, to access Internet services.

Syntax: **--publish/-p** *host:container*


```bash
docker run --detach --name webserver nginx
curl localhost:80
docker exec webserver curl localhost:80
docker rm -f webserver

```

```bash
docker run --detach --name webserver --publish 80:80 nginx
curl localhost:80
docker rm -f webserver
```

```bash
docker run --detach --name webserver -p 8080:80 nginx
curl localhost:80
curl localhost:8080
docker exec webserver curl localhost:80
docker exec webserver curl localhost:8080
docker rm -f webserver
```

## Docker recipes: build your own images

### Building recipes

All commands should be saved in a text file, named by default **Dockerfile**.

#### Basic instructions

Each row in the recipe corresponds to a **layer** of the final image.

**FROM**: parent image. Typically, an operating system. The **base layer**.

```docker
FROM ubuntu:18.04
```

**RUN**: the command to execute inside the image filesystem.
<br>
Think about it this way: every **RUN** line is essentially what you would run to install programs on a freshly installed Ubuntu OS.

```docker
RUN apt install wget
```

A basic recipe:

```docker
FROM ubuntu:18.04

RUN apt update && apt -y upgrade
RUN apt install -y wget
```

#### More instructions

**MAINTAINER**

Who is maintaining the container?

```docker
MAINTAINER Toni Hermoso Pulido <toni.hermoso@crg.eu>
```

**WORKDIR**: all subsequent actions will be executed in that working directory

```docker
WORKDIR ~
```

**ADD, COPY**: add files to the image filesystem

Difference between ADD and COPY explained [here](https://stackoverflow.com/questions/24958140/what-is-the-difference-between-the-copy-and-add-commands-in-a-dockerfile) and [here](https://nickjanetakis.com/blog/docker-tip-2-the-difference-between-copy-and-add-in-a-dockerile)

**COPY**: lets you copy a local file or directory from your host (the machine from which you are building the image)

**ADD**: same, but ADD works also for URLs, and for .tar archives that will be automatically extracted upon being copied.


```docker
# COPY source destination
COPY ~/.bashrc .
```

**ENV, ARG**: run and build environment variables

Difference between ARG and ENV explained [here](https://vsupalov.com/docker-arg-vs-env/).


* **ARG** values: available only while the image is built.
* **ENV** values: available for the future running containers.


```bash
```

**CMD, ENTRYPOINT**: command to execute when generated container starts

The ENTRYPOINT specifies a command that will always be executed when the container starts. The CMD specifies arguments that will be fed to the ENTRYPOINT

<br>

In the example below, when the container is run without an argument, it will execute `echo "hello world"`.<br>
If it is run with the argument **nice** it will execute `echo "nice"`

```docker
FROM ubuntu:18.04
ENTRYPOINT ["/bin/echo"]
CMD ["hello world"]
```

A more complex recipe (save it in a text file named **Dockerfile**:

  ```docker
FROM ubuntu:18.04

MAINTAINER Toni Hermoso Pulido <toni.hermoso@crg.eu>

WORKDIR ~

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y wget

ENTRYPOINT ["/usr/bin/wget"]
CMD ["https://cdn.wp.nginx.com/wp-content/uploads/2016/07/docker-swarm-hero2.png"]
```

### docker build

Implicitely looks for a **Dockerfile** file in the current directory:

```bash
docker build .
```

Same as:

```bash
docker build --file Dockerfile .
```

Syntax: **--file / -f**

**.** stands for the context (in this case, current directory) of the build process. This makes sense if copying files from filesystem, for instance. **IMPORTANT**: Avoid contexts (directories) overpopulated with files (even if not actually used in the recipe).

You can define a specific name for the image during the build process.

Syntax: **-t** *imagename:tag*. If not defined ```:tag``` default is latest.

```bash
docker build -t mytestimage .
```

The last line of installation should be **Successfully built ...**: then you are good to go.
<br>
Check with ``docker images`` that you see the newly built image in the list...


Then let's check the ID of the image and run it!

```bash
docker images

docker run f9f41698e2f8
docker run mytestimage
```

```bash
docker run f9f41698e2f8 https://cdn-images-1.medium.com/max/1600/1*_NQN6_YnxS29m8vFzWYlEg.png
```

### docker tag

To tag a local image with ID "e23aaea5dff1" into the "ubuntu_wget" image name repository with version "1.0":

```bash
docker tag e23aaea5dff1 --tag ubuntu_wget:1.0
```

### Build cache ###

Every line of a Dockerfile is actually an image/layer by itself.

Modify for instance the last bit of the previous image (let's change the image URL) and rebuild it (even with a different name/tag):

```docker
FROM ubuntu:18.04

MAINTAINER Toni Hermoso Pulido <toni.hermoso@crg.eu>

WORKDIR ~

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y wget

ENTRYPOINT ["/usr/bin/wget"]
CMD ["https://cdn-images-1.medium.com/max/1600/1*_NQN6_YnxS29m8vFzWYlEg.png"]
```

```bash
docker build -t mytestimage2 .
```

It will start from the last line.
This is OK most of the times and very convenient for testing and trying new steps, but it may lead to errors when versions are updated (either FROM image or included packages). For that it is benefitial to start from scratch with ```--no-cache``` tag.

```bash
docker build --no-cache -t mytestimage2 .
```
### More advanced image building

Different ways to build images.

Know your base system and their packages. Popular ones:
* [Debian](https://packages.debian.org)
* [CentOS](https://centos.pkgs.org/)
* [Alpine](https://pkgs.alpinelinux.org/packages)
* Conda. [Anaconda](https://anaconda.org/anaconda/repo), [Conda-forge](https://conda-forge.org/feedstocks/), [Bioconda](https://anaconda.org/bioconda/repo), etc.


### Additional commands

* **docker inspect**: Get details from containers (both running and stopped). Things such as IPs, volumes, etc.

* **docker logs**: Get *console* messages from running containers. Useful when using with web services.

* **docker commit**: Turn a container into an image. It make senses to use when modifying container interactively. However this is bad for reproducibility if no steps are saved.

Good for long-term reproducibility and for critical production environments:

* **docker save**: Save an image into a tar archive.

* **docker export**: Save a container into a tar archive.

* **docker import**: Import a tar archive into an image.

#### Exercises

We explore interactively the different examples in the container/docker folders.



|          |       |      |
| :------- | :---: | ---: |
| [Previous page](https://biocorecrg.github.io/ELIXIR_containers_nextflow/introduction_containers.html) | [Home](https://biocorecrg.github.io/ELIXIR_containers_nextflow/)  | [Next page](https://biocorecrg.github.io/ELIXIR_containers_nextflow/singularity.html) |
