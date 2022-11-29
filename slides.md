---
marp: true
paginate: true
---

# Introduction to Docker Containers

Gregg Roemhildt
github: roemhildtg
:email: roemhildtg@gmail.com

![background bg right](./images/pexels-julius-silver-753331.jpg)

---


# Who am I?

 - Bachelors @ UW-RF in Computer Science and Geography
 - Lead Developer@wsb


 Interests:

 - DevOps
 - JavaScript/NodeJS
 - Python


<!-- 
  - Graduated in 2013
  - Spent some time in Chicago and then Faribault in public sector
  - Moved to private sector in 2017 at WSB

 - Now develop mainly spatial applications that help automate field staff workflows. 
-->

---

# What are Containers?

> A container is a standard **unit** of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another


<!-- 
 - Containers are kind of like virtual machines that you can just download and run. 
 - They are different from virtual machines because they are far more efficient in resource usage. 
 - Virtual machines require you to allocate X GB of RAM and resources prior to starting them. 
 - Containers generally run on the host operating system and don't have the same limitations or requirements of VM's
-->

---

# So what is Docker?

 - **API** for building, sharing, and deploying containers
 - Single unified interface - many different environments
 - Dynamic underlying architecture


![w:200](./images/2022-11-28-18-46-38.png) ![w:200](./images/2022-11-28-18-47-04.png) ![w:200; pa](./images/2022-11-28-18-48-09.png)

<!--
 - Docker is essentially a user interface, API, and toolkit for users to quickly start using container technology. 
 - Using the docker CLI or Docker Desktop, you can run applications locally, on your Mac, remotely on servers, or in the cloud. 
 - Underlying architecture can change while the docker API, command line, etc can continue being used. 
-->

---

# Using Docker

 - Docker Desktop
 - Docker CLI (most common)
 - Docker Compose (via cli)


---

# Installation

## Linux:

Install docker via package manager

```sh
# example
pamac install docker
```

## MacOS and Windows:

Install docker via [Docker Desktop](https://www.docker.com/products/docker-desktop/)


---

# Using docker cli

```sh
docker --help
docker run --help
docker container --help
```

## Useful commands:

```sh
# list all containers running
docker ps

# get logs from a container 
docker logs -f <container_name>
```

--- 

# Docker run

 - image
 - ports
 - environment variables
 - volumes


```sh
docker run \
    # run in background (optional)
    -d \
    # port/ip mapping
    -p [host_ip]:[host_port]:[container_port] \
    # volume mapping
    -v [/host/volume/location]:[/container/storage] \
    # image name
    image_name
```
<!--
 - image: the image tag that you want to install/run
 - ports: the tcp/udp ports that you want to expose/map to your local machine
 - environment variables: configuration variables that control how your container will run, for example what username and password to run on your webserver, how to connect to a database, etc. 
 - volumes: where to store persistent data, like database data, user configuration files, or images, etc. 
-->

---

# Docker Compose

YAML syntax for defining docker containers

```yaml
version: '3.9'

services:
  database:

    # image name
    image: postgres:15.1

    # port mapping
    ports:
    - 5432:5432

    # volume mapping
    volumes:
    - /home/gregg/Documents/postgres:/var/lib/postgresql/data

  pgadmin:
    image: dpage/pgadmin4:6.16

    ports:
    - 8888:80
```

---

# Docker Compose

Save file as postgres/docker-compose.yml

```sh
cd postgres
# tell docker to parse yaml file and create containers
# -d means run in background
docker compose up -d
```