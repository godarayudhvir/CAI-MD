# What are we hosting today ?

Your very own Personal audio Streaming Service called [Navidrome](https://www.navidrome.org/#td-block-1)

### Live Demo 🤹‍♀️

Just head to official [demo site](https://demo.navidrome.org/) and enjoy some free music while exploring Navidrome features. The demo server works with all [Subsonic clients](https://www.navidrome.org/docs/overview/#apps), just use the server address [https://demo.navidrome.org](https://demo.navidrome.org/) Not all features are enabled in the demo. For instance, settings are disabled. The server is running on the inexpensive [PikaPods](https://www.pikapods.com/pods?run=navidrome)

With the following Configuration

- 1 Core Processor
- 512MB Memory
- 10GB Disk Space
- Approximate Cost: $2.27/month

### ⭐ Features

- Handles very **large music collections**
- Streams virtually **any audio format** available
- Reads and uses all your beautifully curated **metadata**
- Great support for **compilations** (Various Artists albums) and **box sets** (multi-disc albums)
- **Multi-user**, each user has their own play counts, playlists, favourites, etc...
- Very **low resource usage**
- **Multi-platform**, runs on macOS, Linux and Windows. **Docker** images are also provided
- Ready to use binaries for all major platforms, including **Raspberry Pi**
- Automatically **monitors your library** for changes, importing new files and reloading new metadata
- **Themeable**, modern and responsive **Web interface** based on [Material UI](https://material-ui.com/)
- **Compatible** with all Subsonic/Madsonic/Airsonic [clients](https://www.navidrome.org/docs/overview/#apps)
- **Transcoding** on the fly. Can be set per user/player. **Opus encoding is supported**
- Translated to **various languages**

### Who's the author ?

[GitHub - navidrome/navidrome: 🎧☁️ Modern Music Server and Streamer compatible with Subsonic/Airsonic](https://github.com/navidrome/navidrome)

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
Inside that create a folder named uptime-kuma

1. **Create a Directory Structure**:
   
   - Start by creating a directory named `Docker` inside your home directory. This will serve as the root directory for your Docker-related files and projects.
   
   - Open your terminal or command prompt and navigate to your home directory using the `cd /home/username` 
   
   - Create the `Docker` directory:
     
     ```bash
     mkdir Docker
     ```

2. **Create a Specific Project Folder**:
   
   - Inside the `Docker` directory, create a subfolder named `uptime-kuma`. This subfolder will be dedicated to storing our docker compose file and other config if required.
   
   - Navigate into the `Docker` directory:
     
     ```bash
     cd Docker
     ```
   
   - Create the `navidrome` folder:
     
     ```bash
     mkdir navidrome
     ```

3. **Creating a Docker Compose file**:
   
   - Now create a docker compose file by using the command `nano docker-compose.yml` after navigating to navidrome.
   - Copy and paste the commands from below

```yaml
version: "3"
services:
  navidrome:
    image: deluan/navidrome:latest
    user: 1000:1000
    ports:
      - "4000:4533"
    restart: unless-stopped
    environment:
      ND_SCANSCHEDULE: 1h
      ND_LOGLEVEL: info
      ND_SESSIONTIMEOUT: 24h
    volumes:
      - "./data:/data"
      - "./music:/music:ro"
```

### Docker-compose configuration break-down

- `version: "3"`: This specifies the version of the Docker Compose file format.

- `services:`: This is where you define your application’s services, which are the different containers that your application will use.

- `navidrome:`: This is the name of the service. In this case, it’s a Navidrome server, which is a music server.

- `image: deluan/navidrome:latest`: This specifies the Docker image to use for this service. It’s using the latest version of the `deluan/navidrome` image.

- `user: 1000:1000`: This sets the user and group IDs for the service. This should be the owner of the volumes.
  
  - So, a user with UID 1000 is typically the first normal user (non-root user) created on the system
  
  - Check UID for a username with `id -a username`
    In my case it returned 1000 means this docker will have non-admin permissions. if your users returns value 1000 you might wanna create a non root user with the command below
  
  - ```bash
    sudo useradd -u 1000 -g 1000 username
    sudo passwd username
    ```

- `ports: - "4000:4533"`: This maps port 4533 inside the Docker container to port 4000 on the host machine.

- `restart: unless-stopped`: This means the Docker service will always restart unless explicitly stopped.

- `environment:`: This is where you can set environment variables for the service. In this case, it’s setting various Navidrome configuration options.

- `volumes:`: This is where you define any data volumes for the service. It’s mapping directories from the host machine to directories in the Docker container. The `:ro` at the end of the last volume means it’s read-only.

### Spinning up 🐳 container

Run the command `docker compose up -d`

When you execute this command, Docker Compose reads your configuration file, creates and starts the specified services (containers), and detaches them in the background. It’s like bringing your multi-container application to life with a single command!
![](https://i.imgur.com/F2dS4xv.png)

Check if the container is up & Running using the cmd `docker ps -a`
![](https://i.imgur.com/onTV3CA.png)

If it's running then process to next section
else contact us if you need any help.

## Configuring the Instance ⚙

Browse to `127.0.0.1:4000` or `localhost:4000` (change 4000 to the host port you had chosen in your Docker Compose configuration) to access the Uptime Kuma web interface.

![](https://i.imgur.com/aXjSxDy.png)

Create your admin account

![](https://i.imgur.com/D7xStlR.png)

Now we've navidrome running so lets configure it for use now

### Adding Music

Just add music files to the /music folder in current directory.

Once you are done with it navidrome should auto populate the songs if not manually rescan the library with the option shown below


![](https://i.imgur.com/VnvTPW7.png)

### Multi user setup

### Accessing from a Mobile Client via Subsonic API

### Enabling/Disabling transcoding

### Sharing public links to albums/songs/playlists

### Setting a default theme

### Enable/Disable Media Download

### Thirdparty Metadata fetch

### Login Background

### Welcome Message

### Monitoring Options

### Security considerations

### More configurations options

https://www.navidrome.org/docs/usage/configuration-options/

## Setting up for Remote Access 📡

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

## Updating Instance

## Backuping up & restoring Containers and Their volumes

https://wiki.opensourceisawesome.com/books/updating-docker-containers/page/update-docker-keep-your-data-too

## Going Plus Ultra 💪🏼

### Custom Theme

![](https://i.imgur.com/a3K5pTl.png)

![](https://i.imgur.com/hKNcNHe.png)

![](https://i.imgur.com/zs0KnmR.png)

docker create --name temp_container louislam/uptime-kuma:1
docker cp temp_container:/path/in/container /home/username/docker/uptime-kuma/
docker rm temp_container
