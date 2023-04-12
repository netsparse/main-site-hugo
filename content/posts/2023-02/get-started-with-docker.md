---
layout: post
author: Angel
date: 2023-02-09T17:54:59-05:00
title: "Get Started with Docker"
tags: ["docker", "containers", "devops", "docker-compose"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) are powerful tools that allow you to run and manage applications in containers, making it easy to set up and run applications on any machine, whether it be a laptop, desktop or server. 

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy Gjnup-PuquQ >}}

## Overview

Docker is a platform that enables developers to create, deploy, and run applications in containers. 

Containers are lightweight, portable, and self-contained units of software that can run virtually anywhere. 

With Docker, developers can package an application and its dependencies into a single container that can run on any system that has Docker installed.

The isolation and security allows you to run many containers simultaneously on a given host. 

## Components

### Dockerfile

A Dockerfile is a text file that contains instructions for building a Docker image. It specifies the base image to use, the commands to run to set up the environment, and any additional configuration or customization needed. 

Once the Dockerfile is created, it can be used to build a [Docker image](/posts/2023-02/get-started-with-docker/#images) that can then be used to run container instances.

Here's an example of a simple Dockerfile that sets up a Python environment with Flask:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim-buster

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

Another example you can take a look at is [Pi-hole's Dockerfile](https://github.com/pi-hole/docker-pi-hole/blob/master/src/Dockerfile)

### Images

A Docker image is a snapshot of an application and its dependencies, which can be used to run one or more containers. 

Images are created from [Dockerfiles](/posts/2023-02/get-started-with-docker/#dockerfile) and can be stored in a [registry](https://hub.docker.com/). 

Images are lightweight, portable, and provide a consistent environment for running applications.

### Docker Compose

Docker Compose is a tool that enables you to define and run multi-container Docker applications.

With Docker Compose, you can define your application's services, networks, and volumes in a single `YAML` file, making it easy to manage your application's components.

Here's a general outline of a `docker-compose.yml`.

```yml
version: "3"
services:
  <service_name>:
    image: <image_name>:<tag>
    ports:
      - "<host_port>:<container_port>"
    volumes:
      - "<host_path>:<container_path>"
    environment:
      - <key>=<value>
```

## Getting Started

### Docker Desktop
Docker provides [Docker Desktop](https://docs.docker.com/desktop/) for [Windows](https://docs.docker.com/desktop/install/windows-install/), [macOS](https://docs.docker.com/desktop/install/mac-install/), and [Linux](https://docs.docker.com/desktop/install/linux-install/). Which provides a GUI environment to manage your containers without relying entirely on the CLI.

### Docker Engine

If you wish to utilize just the Docker Engine and CLI, download the engine [here](https://docs.docker.com/engine/install/) for your given platform.

#### Manage Docker as a non-root user

The Docker daemon binds to a Unix socket, not a TCP port. By default it’s the root user that owns the Unix socket, and other users can only access it using `sudo`. The Docker daemon always runs as the root user.

If you don’t want to preface the docker command with `sudo`, create a Unix group called `docker` and add users to it. 

When the Docker daemon starts, it creates a Unix socket accessible by members of the docker group. 

On some Linux distributions, the system automatically creates this group when installing Docker Engine using a package manager. In that case, there is no need for you to manually create the group.

To create the docker group and add your user:

Create the docker group.

```
sudo groupadd docker
```

Add your user to the docker group.

```
sudo usermod -aG docker $USER
```

Log out and log back in so that your group membership is re-evaluated.

### Registry (Docker Hub)

To run a container, you first need to find an image for the container you want to run. 

[Docker Hub](https://hub.docker.com/search) is a popular repository of Docker images, you can search Docker Hub for an image that meets your needs.

### Docker Run

Once you have found an image, you can use the `docker run` command to start a container from that image. 

For example, to run an instance of the `nginx` web server, you can run the following command:

```
docker run -d -p 80:80 nginx
```

This command starts a container from the `nginx` image, maps port 80 on the host to port 80 in the container, and runs the container in the background `(-d)`.

You can access the container from your browser at `localhost`. You'll then be greeted with the default "Welcome to nginx!" message.

### Docker Compose

Docker Compose] is typically installed as part of the Docker Desktop installation on Windows and macOS. On Linux, you can install Docker Compose using your distribution's package manager or by downloading directly from the [Docker website](https://docs.docker.com/compose/install/).

Once you have Docker Compose installed, you can create a `docker-compose.yml` file to define your application's services, networks, and volumes. Here is an example `docker-compose.yml` file that defines a simple web application with a web server and a database:

```yml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: password

```

This `docker-compose.yml` file defines two services: `web` and `db`. 

The `web` service runs an instance of the nginx web server, and maps port 80 on the host to port 80 in the container. 

The `db` service runs an instance of the MySQL database server and sets the root password to `password`.

To start the application, you can run the following command:

```
docker-compose up -d
```

This command starts the application in the background (-d) using the configuration in the `docker-compose.yml` file.

### Versioning

Docker Compose can also be used with version control systems like [Git](/posts/2023-03/getting-started-with-git) to help manage, deploy, and revert changes of multi-container Docker applications. 

## Conclusion

Docker and Docker Compose are powerful tools that enable you to easily run and manage applications in containers. 

With Docker, you can package your application and its dependencies into a single container that can run on any system. 

With Docker Compose, you can define and run multi-container applications using a single configuration file.

### Learn More
- [Official Documentation](https://docs.docker.com/)
- [Docker Overview](https://docs.docker.com/get-started/overview/)
- [Reference Documentation](https://docs.docker.com/reference/)
- [CLI Reference](https://docs.docker.com/engine/reference/commandline/cli/)
- [Alex Ellis' Blog](https://blog.alexellis.io/)
- [Alex Ellis' Hands-on Docker Guide](https://github.com/alexellis/HandsOnDocker/blob/master/Labs.md)
- [Play With Docker Classroom](https://training.play-with-docker.com/)
- [Veggiemonk GitHub Awesome-Docker](https://github.com/veggiemonk/awesome-docker)