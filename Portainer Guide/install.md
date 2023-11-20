# Install Portainer CE with Docker on Linux

## [Introduction](#introduction)

Portainer consists of two elements, the *Portainer Server*, and the *Portainer Agent*. Both elements run as lightweight Docker containers on a Docker engine. This document will help you install the Portainer Server container on your Linux environment. To add a new Linux environment to an existing Portainer Server installation, please refer to the 

## [Portainer Agent installation instructions](/admin/environments/add/docker/agent).

To get started, you will need:

- The latest version of Docker installed and working

- sudo access on the machine that will host your Portainer Server instance

- By default, Portainer Server will expose the UI over port `9443` and expose a TCP tunnel server over port `8000`. The latter is optional and is only required if you plan to use the Edge compute features with Edge agents.

The installation instructions also make the following assumptions about your environment:

- Your environment meets [our requirements](/start/requirements-and-prerequisites). While Portainer may work with other configurations, it may require configuration changes or have limited functionality.

- You are accessing Docker via Unix sockets. Alternatively, you can also connect via TCP.

- SELinux is disabled on the machine running Docker. If you require SELinux, you will need to pass the `--privileged` flag to Docker when deploying Portainer.

- Docker is running as root. Portainer with rootless Docker has some limitations, and requires additional configuration.

## [Deployment](#deployment)

First, create the volume that Portainer Server will use to store its database:

```bash
docker volume create portainer_data
```

Then, download and install the Portainer Server container:

```bash
docker run -d -p 2002:8000 -p 2003:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

## Accessing

Open https://localhost:2003 you should be able to access it

Create a admin account,
![](https://i.imgur.com/y6vLf4Y.png)

Overview of Portainer

![](https://i.imgur.com/oOyeUFa.gif)

Removing a container with it's volume

![](https://i.imgur.com/nga727Q.gif)


