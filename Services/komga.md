# Komga

## What is Komga ?

Komga is a media server for your comics, mangas, BDs and magazines.

## Availability of Live demo

A demonstration website is available at: [https://demo.komga.org](https://demo.komga.org/)

You can log in using the following credentials:

- Login: `demo@komga.org`
- Password: `komga-demo`

## Features ⭐

- Browse libraries, series and books via a responsive web UI that works on desktop, tablets and phones
- Organize your library with collections and read lists
- Edit metadata for your series and books
- Import embedded metadata automatically
- Webreader with multiple reading modes
- Manage multiple users, with per-library access control, age restrictions, and labels restrictions
- Offers a REST API, many community tools and scripts can interact with Komga
- Download book files, whole series, or read lists
- Duplicate files detection
- Duplicate pages detection and removal
- Import books from outside your libraries directly into your series folder
- Import ComicRack `cbl` read lists

## Credits to Author

[gotson/komga](https://github.com/gotson/komga)

## What are the Requirements ?

- Some Kind of Ubuntu Environment
  
  - WSL Running Ubuntu
  
  - Ubuntu on a machine
  
  - Ubunut on a VM

- Docker and Docker-compose Installed

### Skills required

- Basic Ubuntu

- Basic Docker, Docker compose

## Getting started 🔧

### Firstly Create a folder named Docker inside home/username Directory

> This guide presumes the existence of a non-root user on your host. If such a user does not exist, please create one. It is crucial to ensure that this user has the necessary permissions to write data in their user library folder. We frequently establish Docker containers without root privileges for security reasons. Please adhere to these instructions for a successful setup.
> [Why non-root containers are important for security](https://docs.bitnami.com/tutorials/why-non-root-containers-are-important-for-security)

1. Create a Directory Structure as such
   
   /home/username/docker/komga
   
   `mkdir -p /home/username/docker/komga`

2. Browse into the Directory `cd /home/username/docker/komga`

3. Create a Docker compose file inside the directory `nano docker-compose.yml`

4. Copy and Paste the Docker-compose Template from below.

```bash
---
version: '3.3'
services:
  komga:
    image: gotson/komga
    container_name: komga
    volumes:
      - type: bind
        source: ./config
        target: /config
      - type: bind
        source: ./data
        target: /data
    ports:
      - 4002:25600
    user: "1000:1000"
    restart: unless-stopped
```

### Docker run breakdown 🧬

This is a Docker Compose file that defines a single service named `komga`. 
Here’s what each part of the file does:

- `version: '3.3'`: This specifies the version of Docker Compose file format. 

- `services:`: This section contains the configuration for all the services (containers) that will be created.

- `komga:`: This is the name of the service. You can use this name to interact with the service using Docker Compose commands.

- `image: gotson/komga`: This specifies the Docker image to use for this service. In this case, it’s using the `gotson/komga` image from Docker Hub.

- `container_name: komga`: This sets the name of the container that will be created from this service.

- `volumes:`: This section defines the volumes that will be mounted into the container. There are two bind mounts defined:
  
  - The first bind mount maps the `./config` directory from the host to the `/config` directory in the container.
  - The second bind mount maps the `./data` directory from the host to the `/data` directory in the container.

- `ports:`: This section maps the port `4002` on the host to the port `25600` in the container.

- `user: "1000:1000"`: This sets the user and group IDs for the process running inside the container. This can be useful for managing file permissions.

- `restart: unless-stopped`: This means the container will always restart unless it has been manually stopped. This ensures that the service remains running.

## Configuration ⚙

Visit `http:127.0.0.1:4002`

Setup the admin account

![](https://i.imgur.com/uH7NdUO.png)

Now you'll be greeted with the Komga homescreen Web UI

![](https://i.imgur.com/dLlF50S.png)

## Additional Configuration Options

## Customization ✨

## Remote Access 📡

## Security Consideration 🔐

## Monitoring options 📈

## Backup & Restore Instances 💾

## Updating ⚡
