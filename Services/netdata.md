![](https://camo.githubusercontent.com/f597a7d5ab43d2afeeafdd5dac89057bef384ca770f4f6f95c3ffa259e39bd80/68747470733a2f2f7777772e6e6574646174612e636c6f75642f696d672f726561646d652d696d616765732f6e6574646174615f726561646d655f6c6f676f5f6461726b2e706e67)

# What are we hosting today ?

Tool to Monitor your servers, containers, and applications, 
in high-resolution and in real-time.

[**FRANKFURT**](https://frankfurt.netdata.rocks/) | [**NEWYORK**](https://newyork.netdata.rocks/) | [**ATLANTA**](https://atlanta.netdata.rocks/) | [**SANFRANCISCO**](https://sanfrancisco.netdata.rocks/) | 
[**TORONTO**](https://toronto.netdata.rocks/) | [**SINGAPORE**](https://singapore.netdata.rocks/) | [**BANGALORE**](https://bangalore.netdata.rocks/)

They are clustered Netdata Parents. They all have the same data. Select the one closer to you. All these run with the default configuration. We only clustered them to have multi-node dashboards.

![](https://i.imgur.com/JWxpSXR.png)

### ⭐Features

- 💥 **Collects metrics from 800+ integrations**  
  Operating system metrics, container metrics, virtual machines, hardware sensors, applications metrics, OpenMetrics exporters, StatsD, and logs.

- 💪 **Real-Time, Low-Latency, High-Resolution**  
  All metrics are collected per second and are on the dashboard immediately after data collection. Netdata is designed to be fast.

- 😶‍🌫️ **Unsupervised Anomaly Detection**  
  Trains multiple Machine-Learning (ML) models for each metric collected and detects anomalies based on the past behavior of each metric individually.

- 🔥 **Powerful Visualization**  
  Clear and precise visualization that allows you to quickly understand any dataset, but also to filter, slice and dice the data directly on the dashboard, without the need to learn any query language.

- 🔔 **Out of box Alerts**  
  Comes with hundreds of alerts out of the box to detect common issues and pitfalls, revealing issues that can easily go unnoticed. It supports several notification methods to let you know when your attention is needed.

- 📖 **systemd Journal Logs Explorer**  
  Provides a `systemd` journal logs explorer, to view, filter and analyze system and applications logs by directly accessing `systemd` journal files on individual hosts and infrastructure-wide logs centralization servers.

- 😎 **Low Maintenance**  
  Fully automated in every aspect: automated dashboards, out-of-the-box alerts, auto-detection and auto-discovery of metrics, zero-touch machine-learning, easy scalability and high availability, and CI/CD friendly.

- ⭐ **Open and Extensible**  
  Netdata is a modular platform that can be extended in all possible ways and it also integrates nicely with other monitoring solutions.

### Who's the author ?

[GitHub - netdata/netdata: Monitor your servers, containers, and applications, in high-resolution and in real-time!](https://github.com/netdata/netdata)

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
Inside that create a folder named netdata

1. Create a Directory Structure as such
   
   /home/username/docker/netdata
   
   `mkdir -p /home/cyberalliance/docker/netdata`

2. Browse into the Directory
   `cd /home/cyberalliance/docker/netdata`

3. Create a Docker compose file inside the directory
   `nano docker-compose.yml`

4. Copy and Paste the Docker-compose Template from below

```
version: '3'
services:
  netdata:
    image: netdata/netdata
    container_name: netdata
    pid: host
    network_mode: host
    port:
      - "2000:19999"
    restart: unless-stopped
    cap_add:
      - SYS_PTRACE
      - SYS_ADMIN
    security_opt:
      - apparmor:unconfined
    volumes:
      - ./netdataconfig:/etc/netdata
      - ./netdatalib:/var/lib/netdata
      - ./netdatacache:/var/cache/netdata
      - /etc/passwd:/host/etc/passwd:ro
      - /etc/group:/host/etc/group:ro
      - /etc/localtime:/etc/localtime:ro
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /etc/os-release:/host/etc/os-release:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro

volumes:
  netdataconfig:
  netdatalib:
  netdatacache:
```

### Docker-compose configuration break-down

- `version: '3'`: This specifies the version of Docker Compose file format.

- `services:`: This section defines the services, which are the containers you want to run

- `netdata:`: This is the name of the service

- `image: netdata/netdata`: This tells Docker to use the `netdata/netdata` image from Docker Hub

- `container_name: netdata`: This sets the name of the container

- `pid: host` and `network_mode: host`: These give the container full access to the processes and network stack of the host

- `port: - "2000:19999"`: This maps port 2000 on the host to port 19999 inside the container

- `restart: unless-stopped`: This means the container will always restart unless explicitly stopped

- `cap_add:`: This adds Linux capabilities

- `security_opt:`: This sets security options

- `volumes:`: This section mounts paths from the host to the container

- `volumes:` (at the end): This creates named volumes that can be used by services

### Spinning up 🐳 container

Run the command `docker compose up -d`

When you execute this command, Docker Compose reads your configuration file, creates and starts the specified services (containers), and detaches them in the background. It’s like bringing your multi-container application to life with a single command!

![](https://i.imgur.com/uZbi1iD.png)

> netdata Published ports are discarded when using host network mode
> Hence it will now default back to `19999`

Check if the container is up & Running using the cmd `docker ps -a` ![](https://i.imgur.com/C97FFeh.png)

If it's running then process to next section
else contact us if you need any help.

## Configuring the Instance ⚙

Browse to `127.0.0.1:19999` or `localhost:19999` (change 4000 to the host port you had chosen in your Docker Compose configuration) to access the netdata web interface.

![](https://i.imgur.com/U3iv6Cx.png)

### More Configurations options (Soon)

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

## Updating Instance [soon]

## Backuping up & restoring Containers and Their volumes

https://wiki.opensourceisawesome.com/books/updating-docker-containers/page/update-docker-keep-your-data-too
