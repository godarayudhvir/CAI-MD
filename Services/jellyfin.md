# What are we hosting today ?

Your own media solution (Jellyfin) that puts you in control of your media.

![](https://i.imgur.com/QzcXARu.png)

### Live Demo 🤹‍♀️

None Available

### ⭐ Features

1. Control of Media Management and Streaming: 
   Jellyfin allows you to collect, manage, and stream your media.

2. Client-Server Model: 
   It follows a client–server model that allows for multiple users and clients to connect, even simultaneously, and stream digital media remotely.

3. Cross-Platform Support: Jellyfin is descended from Emby’s 3.5.2 release and ported to the .NET Core framework to enable full cross-platform support.

4. No Premium Licenses or Features: 
   There are no strings attached, no premium licenses or features, and no hidden agendas.

5. Plugins: Jellyfin supports plugins to extend its functionality.

### Who's the author ?

Jellyfin is the volunteer-built media solution made by team at [jellyfin.org](https://jellyfin.org/) and many other contributers from the community.

### What do we need ?

1. Some Kind of Ubuntu Environment
   
   - WSL Running Ubuntu
   
   - Ubuntu on a machine
   
   - Ubunut on a VM

2. Docker and Docker-compose Installed

### Skill Prerequisite ?

- Basic Ubuntu

- Basic Docker

## How to Install 🔧

Firstly Create a folder named Docker inside home/username Directory
Inside that create a folder named jellyfin

1. Create a Directory Structure as such
   
   /home/username/docker/jellyfin
   
   `mkdir -p /home/cyberalliance/docker/jellyfin`

2. Browse into the Directory `cd /home/cyberalliance/docker/jellyfin`

3. Create a Docker compose file inside the directory `nano docker-compose.yml`

4. Copy and Paste the Docker-compose Template from below

```
---
version: "2.1"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - ./config:/config
      - ./shows:/data/tvshows
      - ./movies:/data/movies
    ports:
      - 4001:8096
    restart: unless-stopped
```

### Docker-compose configuration break-down

- `version: "2.1"`: This specifies the version of Docker Compose to use. Version 2.1 supports most features and is widely compatible.

- `services:`: This section defines the services, or containers, that make up your app. In this case, there’s just one service, `jellyfin`.

- `jellyfin:`: This is the name of the service.

- `image: lscr.io/linuxserver/jellyfin:latest`: This tells Docker to use the latest Jellyfin image from the LinuxServer.io repository.

- `container_name: jellyfin`: This sets the name of the container to `jellyfin`.

- `environment:`: This section is used to set environment variables in the container. In this case, it’s setting `PUID` and `PGID` (which are used for file permissions), and `TZ` (which sets the timezone to UTC).

- `volumes:`: This section is used to mount paths on the host to paths in the container. In this case, it’s mounting the `config`, `shows`, and `movies` directories on the host to corresponding directories in the container.

- `ports:`: This section is used to map ports in the container to ports on the host. In this case, it’s mapping port 8096 in the container to port 4001 on the host.

- `restart: unless-stopped`: This tells Docker to always restart the container unless it’s explicitly stopped.

So, in summary, this Docker Compose file sets up a Jellyfin media server with specific file permissions and timezone, and with specific directories and ports mapped to the host. It also ensures that the Jellyfin container will always restart unless explicitly stopped.

### Spinning up 🐳 container

Run the command `docker compose up -d`

When you execute this command, Docker Compose reads your configuration file, creates and starts the specified services (containers), and detaches them in the background. It’s like bringing your multi-container application to life with a single command!

![](https://i.imgur.com/C9YHhMG.png)

Check if the container is up & Running using the cmd `docker ps -a`

![](https://i.imgur.com/TxqXSkH.png)

If it's running then process to next section
else contact us if you need any help.

### Configuring the Instance ⚙

Browse to `127.0.0.1:4001` or `localhost:4001` (change 4001 to the host port you had chosen in your Docker Compose configuration) to access the navidrome web interface.

![](https://i.imgur.com/dZe2uu6.png)

#### Complete the Intial Configuration

1. Choose Display language

2. Setup user credentials

3. Setup Media Library
   
   - Click add media library
   
   - Choose content type | Eg: movies
   
   - Click the + next to folders
   
   - Select the movies directory we earlier chose for movies in docker compose
   
   - Click ok
   
   - Add other libraries as required
   
   - Move to next section

4. Choose Metadata language settings

5. Next, Next others

---

Login into jellyfin using the credentials setup earlier

Now have a look around and see how things go

---



### Setting up for Remote Access 📡

These are few ways how we can go about doing that

1. If you have a domain name such as example.com
   then you might wanna setup a reverse proxy using
   
   - Nginx Proxy Manager
   
   - [Cloudflare Tunnel](https://github.com/godarayudhvir/shownotes/blob/main/Cloudflare/cf_tunnel.md)
   
   - Traefik
   
   - & More
   
   - After any of the above ^ set BaseUrl `ND_BASEURL` in compose file
     example: `https://music.example.com`

2. If you don't have a domain name or don't want public accessing it
   setup VPN one of the following services
   
   - Tailscale
   
   - Twingate
   
   - & More

## Updating Instance [soon]

## Backuping up & restoring Containers and Their volumes

https://wiki.opensourceisawesome.com/books/updating-docker-containers/page/update-docker-keep-your-data-to
