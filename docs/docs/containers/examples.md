---
layout: default-edit
title: Exercises
nav_order: 1
parent: Containers
permalink: /docs/containers/exercises
---

# Exercises

Docker can be installed on most operating systems including Windows
and macOS. However for consistency in the exercises, we will use
Docker running on a Linux system that has been deployed with nuv.la.

## Setup

To start, deploy the "docker-compose" application from the App Store
on nuv.la. This will provide everyone with a consistent interface and
allow us to take advantage of the better network connectivity on the
cloud. 

During the exercises, you will be creating your own containers. These
will be stored on [Docker Hub](https://hub.docker.com). To be able to
upload containers, create a account there. Uploading and storing
public containers is free; storing private containers requires a paid
account. 

## Sanity Checks

Log into the "docker-compose" virtual machine you started earlier with
SSH as root.

Verify that the docker command works:

```
docker --version 
Docker version 18.09.2, build 6247962
```

You may not see exactly the same version. To see the full set of
command options use `docker --help`.

The two primary types of Docker resources are:

 - **images**: Snapshots of complete machines stored (usually) on
   Docker Hub and cached locally when required.

 - **containers**: Running (or stopped) instances of an image.

You can list the local images and containers with the commands:

```
docker image ls
docker container ls
```

The responses will list no resources unless you've already tried
starting a container.

The subcommands mirror the standard Linux commands (`ls`, `rm`,
etc.). There are many variants of the Docker commands that perform
similar functions. For example, `docker ps` does the same as `docker
container ls`.  The syntax used above is the most consistent one.

## Hello World

Now run the "hello world" container:

```
$ docker run hello-world 

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:6540fc08ee6e6b7b63468dc3317e3303aae178cb8a45ed3123180328bcc1d20f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

Your output should be nearly identical to the above result.  Again,
the details of docker will be covered later, but here's a short
summary of what happened:

 - Docker searches in the local cache for the "hello-world" image and
   doesn't find it.
 - Docker pulls (downloads) the image "library/hello-world" from
   [Docker Hub](https://hub.docker.com).
 - Docker runs the image, which then spits out the rest of the
   output.

Note that the container stops after printing out the text. This is a
core concept with containers. They consist of a single main process.
**When that process stops, the container exits.**

## Interactive Containers

For developers, a very common use case is to spin up a container to
provide an interactive development environment for quick tests.

To do this, you run a shell (usually `/bin/bash`) as the main process
of the container.  For example to run Ubuntu 18.04:

```
docker run -it ubuntu:18.04 /bin/bash
```

This will download and start the Ubuntu 18.04 image, using `/bin/bash`
as the executable for the main process.  When you `exit` the shell,
the container will stop.

Similarly, for CentOS 7:

```
docker run -it centos:7 /bin/bash
```

Again, the container will stop when you `exit` the shell.

To list stopped containers as well as running containers, use the `-a`
option: `docker container ls -a`.

Use the search feature of Docker Hub to find other interesting
containers to run.  Try them out and see if they work for you. There
are many containers that provide preprepared versions of common
applications. Can you find images for R-Studio, Anaconda, and nginx?

## Services

Docker uses a complicated network configuration to allow all
containers to see each other through the network, while blocking all
access (by default) from the outside.

To make services accessible from the external network, you need to use
the `-p` option to map the port from a running container to a port on
the host machine.

Try running

```
docker run -d -p 80:80 nginx 
```

This will run the nginx container as a daemon and will map the
Docker internal port 80 to the external port 80 on the host
machine. You should be able to see the nginx welcome page at the URL
`http://vm-ip-address`.

Because the `-d` option was used, the container was run as a detached
daemon. To stop and remove the container, you must use the `docker
container stop` and `docker container rm` commands explicitly.

Change the `-p` option to put the web server on a different port
(e.g. 8080).

## Docker Build

Docker was conceived to make building your containers easy and
efficient. If you understand the deployment process for custom
SlipStream components, you will find the build process for Docker very
similar.

To create a container, create a new empty directory,
e.g. `container1`.  Inside that subdirectory, create an empty file
named `Dockerfile`. The `Dockerfile` contains the "recipe" for
transforming an existing container into a new, customized
container. The subdirectory forms the "context" of the build. 

The build process is controlled through a `Dockerfile`. If
you search on GitHub, you'll find many example of 

## Docker Compose

Single containers are useful in many circumstances; however, as a
developer you will often want to run a number of services together
when testing a system.

Defining a multi-container system and controlling the deployment is
done via `docker-compose`. If you deployed your Docker environment
from nuv.la, then the `docker-compose` command is already installed
and available.

