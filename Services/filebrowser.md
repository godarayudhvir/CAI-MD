# What are we hosting Today ?

A comprehensive file management interface called [filebrowser](https://github.com/filebrowser/filebrowser)

![](https://i.imgur.com/SKKV3m6.png)

### Live Demo 🤹‍♀️

Experience it firsthand by exploring the url: [https://demo.filebrowser.org/](https://demo.filebrowser.org/)

Login with the credentials: `demo`/`demo`

### ⭐Features

- **Secure Authentication**: Users can securely sign in using their unique username and password.

- **Intuitive User Interface**: The application boasts a user-friendly and intuitive user interface.

- **Advanced User Management**: Comprehensive user management system with customizable permissions for different roles.

- **Integrated Editor**: The application comes with an inbuilt editor for seamless user experience.

- **Command Line Interface**: The application provides a command line interface for advanced users.

- **High Customizability**: The application offers high customizability to cater to the specific needs of the users.

### Who's the Author ?

Team of the project contains following authors

[o1egl (Oleg Lobanov) · GitHub](https://github.com/o1egl)

[hacdias (Henrique Dias) · GitHub](https://github.com/hacdias)

[Equim-chan (Equim) · GitHub](https://github.com/Equim-chan)

### What do we need ?

1. Some Kind of Ubuntu Environment
   
   - WSL Running Ubuntu
   
   - Ubuntu on a machine
   
   - Ubunut on a VM

2. Docker and Docker-compose Installed

### Skill Prerequisite ?

- Basic Ubuntu

- Basic Docker, Docker-compose

## How to Install 🔧

- Create Directory and browse into it
  
  ```bash
  mkdir -p /home/username/docker/filebrowser
  cd /home/username/docker/filebrowser
  ```

- Create a docker compose file
  
  ```bash
  nano docker-compose.yml
  ```

- Paste the content provided below

- Save the docker file

```dockerfile
services:
  file-browser:
    image: filebrowser/filebrowser
    container_name: file-browser
    user: 0:0 #option1
    user: 1000:1000 #option2
    ports:
      - 2001:80 #Web Gui Will be available on port 8081
    volumes:
      - /:/srv #serves enire server storage works only with option1
      - /home/username/:/srv #serves home directory of user
      - /home/username/docker/filebrowser/filebrowser.db:/database.db
      - /mnt/e/Media Libraries:/srv/public/
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
```

This Docker Compose file is used to define and run a service called `file-browser` using Docker. Here’s a breakdown of what each line does:

- `services:`: This keyword is used to define the services that make up your app.

- `file-browser:`: This is the name of the service you’re defining.

- `image: filebrowser/filebrowser`: This line tells Docker to use the `filebrowser/filebrowser` image from Docker Hub.

- `container_name: file-browser`: This sets the name of the container to `file-browser`.

- `user: 0:0`: This sets the user and group ID for the process inside the container to `0:0`, which corresponds to the root user.

- `user: 1000:1000`: This sets the user and group ID for the process inside the container to `1000:1000`, which corresponds to the first non root user.

- `ports:`: This keyword is used to expose ports.
  
  - `- 2001:80`: This maps port 80 in the container to port 2001 on the host.

- `volumes:`: This keyword is used to mount paths.
  
  - `- /:/srv`: This mounts the root directory of the host to the `/srv` directory in the container.
  - `- /home/username/docker/filebrowser/filebrowser.db:/database.db`: This mounts the `filebrowser.db` file from your host to `/database.db` in the container.
  - `- /mnt/e/Media Libraries:/srv/public/`: This mounts the `Media Libraries` directory from your `E:` drive to `/srv/public/` in the container.

- `restart: unless-stopped`: This tells Docker to automatically restart the container if it crashes, unless it was manually stopped.

- `security_opt:`: This keyword is used to modify security options.
  
  - `- no-new-privileges:true`: This prevents the processes in the container from gaining additional privileges.

Create a file "**filebrowser.db**" with "touch"

```bash
touch filebrowser.db
```

Run Docker compose

```bash
docker compose up -d
```

This is the expected output

```
 ✔ Network filebrowser_default  Created                                                          0.2s
 ✔ Container file-browser       Started                                                          0.4s
```

Verify if docker container is running

```bash
docker ps
```

Expected outcome (Stauts healthy and up)

```bash
CONTAINER ID   IMAGE                     COMMAND          CREATED          STATUS                    PORTS                                   NAMES
34ad15cbb1c4   filebrowser/filebrowser   "/filebrowser"   59 seconds ago   Up 57 seconds (healthy)   0.0.0.0:8081->80/tcp, :::8081->80/tcp   file-browser
```

## Configuring the Instance ⚙

1. Open the filebrowser web gui using `127.0.0.1:2001` or `localhost:2001`
   Login into the GUI via Default credentials `admin` for username and password
   
   ![](https://i.imgur.com/johoqDV.png)

2. Goto Settings and Change the admin user credentials
   ![](https://i.imgur.com/1t5AcK2.png)

3. You can change the password here if you plan on keeping current username
   Else go to user management
   ![](https://i.imgur.com/saL8GDa.png)

4. Click on the pencil icon to edit this user
   ![](https://i.imgur.com/OJW7InO.png)

5. Change the username/password to your preference
   ![](https://i.imgur.com/Xn9cgpO.png)

6. Save the changes then logout

7. Login with new credentials

### User Management

#### User default settings

Under Global settings choose the permission you would like to be filled out by default when creating a new user. below is an example of how I like to keep it.
![](https://i.imgur.com/GqrhpFz.png)

#### Creating a new user

![](https://i.imgur.com/esRgPe4.gif)

#### Deleting a user account

![](https://i.imgur.com/SWhxotw.gif)

#### Enabling Self-registration

![](https://i.imgur.com/UpYnuGn.gif)

### User scopes

Under user management and default settings for user you will notice a option called scope. Imagine you want only one folder and its subfolders to be accessible by the new user this is exactly what you need for it.

`/public` will allow new users to only access files in public folder and it's subfolders

![https://i.imgur.com/JB4cf72.gif](https://i.imgur.com/JB4cf72.gif)

Add it to default if required

![](https://i.imgur.com/ZPgbaZs.png)  

### Customization

#### Enabling Dark theme

![](https://i.imgur.com/9ZwIU0x.gif)

### Sharing Files & Management

> First make sure that user has sharing permission (Admin already has)

#### Sharing a File/Folder

![](https://i.imgur.com/rZ9IHpK.gif)

#### Managing Shares

![](https://i.imgur.com/UyHoTlZ.gif)

## Setting up for Remote Access 📡

These are few ways how we can go about doing that

1. If you have a domain name such as example.com
   then you might wanna setup a reverse proxy using
   
   - Nginx Proxy Manager
   
   - [Cloudflare Tunnel](https://github.com/godarayudhvir/shownotes/blob/main/Cloudflare/cf_tunnel.md)
   
   - Traefik
   
   - & More

2. If you don't have a domain name or don't want public accessing it
   setup VPN one of the following services
   
   - Tailscale
   
   - Twingate
   
   - & More

## Updating Instance

## Backup/Restore Instance
