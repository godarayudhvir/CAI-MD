# Firefly III

A free and open source personal finance manager

"Firefly III" is a (self-hosted) manager for your personal finances. It can help you keep track of your expenses and income, so you can spend less and save more. Firefly III supports the use of budgets, categories and tags. Using a bunch of external tools, you can import data. It also has many neat financial reports available.

Firefly III should give you **insight** into and **control** over your finances. Money should be useful, not scary. You should be able to *see* where it is going, to *feel* your expenses and to... wow, I'm going overboard with this aren't I?

But you get the idea: this is your money. These are your expenses. Stop them from controlling you. I built this tool because I started to dislike money. Having money, not having money, paying bills with money, you get the idea. But no more. I want to feel "safe", whatever my balance is. And I hope this tool can help you. I know it helps me.

Read more: [Firefly III: a personal finances manager](https://github.com/firefly-iii/firefly-iii/)

### Download Docker Compose file

Download **[the Docker Compose file](https://raw.githubusercontent.com/firefly-iii/docker/main/docker-compose.yml)** and place it somewhere convenient. It doesn't really matter where you place it, but I suggest a dedicated directory.

If you also want to use the Firefly III Data Importer, grab the [alternative Docker Compose file](https://raw.githubusercontent.com/firefly-iii/docker/main/docker-compose-importer.yml) instead.

Either way, grab the raw file, and don't copy-paste the text from your browser. The spaces in the file are very important. So use "Save As".

### Download environment variables

There are two environment variable-files you need to run this Docker Compose file. Download all files and save them next to the Docker Compose file.

- The first file contains Firefly III variables and can be downloaded from [the Firefly III repository](https://raw.githubusercontent.com/firefly-iii/firefly-iii/main/.env.example). Save it as a new file called `.env`.
- The second file contains the database variables and can be downloaded from [the Docker repository](https://raw.githubusercontent.com/firefly-iii/docker/main/database.env). Save it as a new file called `.db.env`.

If you've downloaded the Docker Compose file that *includes* the Data Importer, you'll need a third `.env` file:

- Download the [Data Importer environment variables](https://raw.githubusercontent.com/firefly-iii/data-importer/main/.env.example) and save it as a new file called `.importer.env`.

It is **important** that you rename the file as instructed here. You can see in the Docker compose file why this is. There is a reference to it: `env_file:`. If you don't name it as it is in the Docker Compose file, you must edit the Docker compose file to match the file names.

If you include the data importer, you MUST do this:

1. Change `FIREFLY_III_URL` in `.importer.env` to `http://app:8080`

Either way, you should also do this (not mandatory):

1. Change `DB_PASSWORD` in `.env` to something else. Pick a nice password.
2. Change `MYSQL_PASSWORD` in `.db.env` to the SAME value

### Start the container

Run the following command in the directory where both `docker-compose.yml` and all environment variable files are present.

```text
docker compose -f docker-compose.yml up -d --pull=always
```

You can follow the progress of the installation by running this command:

```text
docker compose -f docker-compose.yml logs -f
```

When the installation is done, Firefly III will thank you for installing it. Once you see this message, you can visit Firefly III. It will be running at your `localhost:portno`

### First Splash

Creat account to get started

![](https://i.imgur.com/l63mK7b.png)

After that you will see this
![](https://i.imgur.com/noxawy8.png)

Now fill this up and get up & Running.
This guide will be update once I have filled my instance with some data.

### Accessing from Outside Network

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

### Troubleshoot

#### T-1 Help with Firefly not showing graphics behind cloudflare tunnel

If you used reverse proxy to stup firefly-iii then please do these following steps

1. Edit the .env file and look for this section and do what is told
   
   TRUSTED_PROXIES is a useful variable when using Docker and/or a reverse proxy. Set it to ** and reverse proxies work just fine.
   
   TRUSTED_PROXIES=**

2. In the same file look for APP_URL and set it to your domain

#### T-2 My Account Mail is shown as [email protected] why is this?

The email obfuscation by Cloudflare blocking bots to view that email. 
You should find it under Scrape Shield disable that.
![](https://i.imgur.com/GL8w94D.png)
