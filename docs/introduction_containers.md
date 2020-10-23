---
layout: page
title: Introduction to Containers
navigation: 2
---

# What are containers ?

<a href="https://www.synopsys.com/blogs/software-security/wp-content/uploads/2018/04/containers-rsa.jpg"><img src="https://www.synopsys.com/blogs/software-security/wp-content/uploads/2018/04/containers-rsa.jpg" width="700/"></a>

A Container can be seen as a **minimal virtual environment** that can be used in any Linux-compatible machine (and beyond).

Using containers is time- and resource-saving as they allow:
* Controlling for software installation and dependencies.
* Reproducibility of the analysis.

Containers allow us to use **exactly the same versions of the tools**.

## Virtual machines or containers ?

### Virtualisaton

* Abstraction of physical hardware
* Depends on hypervisor (software)
* Do not confuse with hardware emulator
* Enable virtual machines:
	* Every virtual machine with an OS (Operating System)

### Containerisation (aka lightweight virtualisation)

* Abstraction of application layer
* Depends on host kernel (OS)
* Application and dependencies bundled all together

### Virtual machines vs containers

<a href="https://zdnet2.cbsistatic.com/hub/i/r/2017/05/08/af178c5a-64dd-4900-8447-3abd739757e3/resize/770xauto/78abd09a8d41c182a28118ac0465c914/docker-vm-container.png"><img src="https://zdnet2.cbsistatic.com/hub/i/r/2017/05/08/af178c5a-64dd-4900-8447-3abd739757e3/resize/770xauto/78abd09a8d41c182a28118ac0465c914/docker-vm-container.png" width="700/"></a>

source https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/

**Pros and cons**

|| Virtualisation | Containerisation |
| :------ | :------------: | :--------------: |
| PROS | * Very similar to a full OS <br> * With current solutions, high OS diversity| * No need of full OS installation (less space) <br> * Faster than virtual machines <br> * Easier automation <br> * Current solutions allow easier distribution of recipes. More portability.|
| CONS | * Need of more space and resources <br> * Slower than containers <br> * Not as good automating | * Some cases might not be exactly the same as a full OS <br> * With current solutions, still less OS diversity |

## History of containers

### chroot

* chroot jail (BSD jail): first concept in 1979
* Notable use in SSH and FTP servers
* Honeypot, recovery of systems, etc.

<a href="https://sysopsio.files.wordpress.com/2016/09/linux-chroot-jail.png"><img src="https://sysopsio.files.wordpress.com/2016/09/linux-chroot-jail.png" width="550/"></a>

Source: https://sysopsio.wordpress.com/2016/09/09/jails-in-linux/

### Additions in Linux kernel

* cgroups (control groups), before "process containers"
	* isolate resource usage (CPU, memory, disk I/O, network, etc.) of a collection of processes
* Linux namespaces
	* one set of kernel resources restrict to one set of processes

<img src="/ELIXIR_containers_nextflow/images/linux-vs-docker-comparison-architecture-docker-lxc.png" width="600" />
Source: https://sysopsio.wordpress.com/2016/09/09/jails-in-linux/

|          |       |      |
| :------- | :---: | ---: |
| [Previous page](https://biocorecrg.github.io/ELIXIR_containers_nextflow/) | [Home](https://biocorecrg.github.io/ELIXIR_containers_nextflow/)  | [Next page](https://biocorecrg.github.io/ELIXIR_containers_nextflow/docker.html) |
