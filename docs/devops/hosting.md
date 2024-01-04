# Hosting

## Recommended Reading

-   [Remote Development using SSH on VSCode](https://code.visualstudio.com/docs/remote/ssh)
    -   If you already use VSCode for development, using VSCode's ssh extension streamlines the experience of connecting your server.
    -   Once connected you can drag files into your VSCode file system to upload them, right click files to download, and perform all of VSCode's normal features (editing files, using the terminal, etc).
-   [The Linux Command Line for Beginners](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
-   [How to Use Systemctl](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

## Overview

After developing software we need to host it on a server. It's recommended to host on a cloud platform, so you don't need to worry about hardware maintenance of the server. Most cloud platforms run on the Linux operating system since it's free and open-source. This article will go over hosting on a Linux platform.

It's recommended to host the server on Linode, since their cheapest option is a `Nanode`, which charges $5 a month.

!!! note

    Currently, the club hosts the backend on a Nanode under a Linode account registered with the rutgerscogs@gmail.com account. If you're the current webmaster, please ensure you have access to this account.

## Service Management

First you need to get the built files for the backend and discord bot onto your server. If your server is powerful enough, you can clone the repository onto the the server itself and then run a build there. Otherwise, you can build them locally on your machine, and then upload them to the server.

-   [Discord bot repository](https://github.com/RUCOGS/rucogs-discord-bot)
-   [Backend repository](https://github.com/RUCOGS/rucogs.github.io-backend)

On Linux, there is a `systemd` or "System Daemon" program that's in charge of starting, stopping, and restarting processes. We use `systemd` to run the backend, discord-bot, and music bots since it allows these services to always be up -- even if they crash, they will restart themselves automatically. To manage these `systemd` services, we will use the `systemctl` or "System Control", which is a command-line tool to interact with `systemd`. Using `systemctl`, we can enable/disable the services managed by `systemd`.

Note that both the backend and discord bot repositories have a `.service` file in them. Make sure you have these files on your server as well. By default, these service files assume you cloned the repositories on your root directory, and that you've built a production version of the repositories on the server itself. This means the `.serivce` files expect the built files for each backend application to be stored in a `dist` folder underneath each backend application's repository. If you decide to place the built files in a different location, don't forget to change the file paths in each of the service files.

Below is a visualization of how this guide expects the various repository folders to be set up. Note that some files are omitted for brevity.

```
/root
├─ rucogs-discord-bot
│  ├─ dist
│  │  └─ BUILT FILES FOR DISCORD BOT
│  └─ rucogs-discord.service
├─ rucogs-music
│  ├─ BUILT FILES FOR MUSIC
│  └─ rucogs-music.service
└─ rucogs.github.io-backend
   └─ dist
   │  └─ BUILT FILES FOR BACKEND
   └─ rucogs.service
```

To make `.service` files visible to `systemd`, it must be placed within the `/etc/systemd/system/` folder. However instead of moving the files, you can instead create a "symbolic link" for each `.service` file, and place each link inside the `/etc/systemd/system/` folder. Symbolic links in Linux are similar to shortcuts on Windows, and act as "pointers" to files. By having a symbolic link to our service files, we don't need to dig through the `/etc/systemd/system/` folder to find the service files whenever we want to edit them. Instead, we can access them directly from each repository folder, which is very convenient.

`systemctl` can actually create a symbolic link for us inside of the `/etc/systemd/system` folder. This is done by running the following command.

```bash
systemctl enable /root/path/to/myservice.service
```

!!! note

    For example, if you wanted to add the `rucogs.service`, you can run

    ```bash
    systemctl enable /root/rucogs.github.io-backend/rucogs.service
    ```

    Note that enabling a service will also ensure the service starts whenever the computer boots up. This can ensure you're services are always online, event after your cloud server has rebooted due to a crash or periodic maintenance.

Finally, you can start it manually by navigating to the directory containing the service file and then running

```bash
systemctl start myservice
```

!!! note

    So in order to start the backend and discord bots, you need to navigate to the directory containing `rucogs.service` and run

    ```bash
    systemctl start rucogs
    ```

    Then navigate to the directory containing `rucogs-discord.service` and run

    ```bash
    systemctl start rucogs-discord
    ```

To check the status of a service and view it's output, you can do

```bash
systemctl status myservice
```

To restart a service, you can do

```bash
systemctl restart myservice
```

!!! note

    The `rucogs.service` and `rucogs-discord.service` files are configured to restart themselves if they ever crash.

To setup the music bot, follow the instructions on the [JMusicBot wiki](https://jmusicbot.com/setup/). This site includes information on setting up a `.service` file for the bot.

!!! note

    You may need to install the required dependencies on your server to get the services to run. Both `rucogs` and
    `rucogs-discord` services require Node.js and the music bot requires Java.

### Config Files

The backend and discord bot applications both read data from special `config.json` files under their `src/config/` folders. The `src/config/` folders are located underneath the root of each repository. These config files contain sensitive information, and are excluded from the GitHub repositories by default. Please ensure these config files are set up properly. The documentation on the config files are linked below.

-   [Backend Config](../backend/config.md)
-   [Discord-Bot Config](../discord-bot/config.md)

### Linode Mailing Setup

By default, Linode blocks mail ports to prevent spam. If you are using Linode for your server hosting, please make sure to open a support ticket to request mail port access. You should explain to the support team that you need the mailing port to host a backend for the game development club at Rutgers University, which may send mail to club members for identity verification purposes. They should lift the mail port ban in a few business-days after seeing your request.

## NGINX

NGINX is a web server designed for use cases involving high volumes of traffic, and it’s a popular, lightweight, high-performance solution. We can use NGINX to setup SSL/TLS certificates, as well use it as a proxy server to forward traffic from specific URL locations to our running services.

For example instead of having to connect to our backend service using a port with `mydomain.com:8000`, you can use `mydomain.com/rucogs/backend` to connect to the server.

Please check of the following guides to set up NGINX:

-   [setting up NGINX in an Ubuntu 20.04 Linode](https://www.linode.com/docs/guides/how-to-install-and-use-nginx-on-ubuntu-20-04/)
-   [Beginner's Guide to NGINX](https://nginx.org/en/docs/beginners_guide.html)
-   [Sites Enabled with NGINX or Apache](https://www.linode.com/docs/guides/how-to-enable-disable-website/)

Here's an example NGINX `conf` file used by Alan to host the backend on his personal website at [atlinx.net](https://atlinx.net). It's stored underneath the `site-enabled` directory of NGINX.

```NGINX
# /etc/nginx/sites-enabled/default
server {
    server_name backend.cogs.club www.cogs.club;

    root /var/www/html;

	location /backend/ {
        proxy_pass http://localhost:3000/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        client_max_body_size 100M;
    }

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/backend.cogs.club/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/backend.cogs.club/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}

server {
    if ($host = www.backend.cogs.club) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    if ($host = backend.cogs.club) {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    listen 80;
    listen [::]:80;
    server_name backend.cogs.club www.backend.cogs.club;

    return 404; # managed by Certbot
}
```

### Lets Encrypt

An important part of setting up the server is getting SSL/TLS certificates. These certificates let you encrypt traffic to the server, making communication more secure. Sites that have SSL/TLS certificates will show a lock icon in the browser when connecting to them. If you are using NGINX, you can follow [this NGINX guide on setting up Let's Encrypt.](https://www.nginx.com/blog/using-free-ssltls-certificates-from-lets-encrypt-with-nginx/).

!!! note

    It's important to pass on hosting of the backend as new Webmasters replace old ones.

    Member who is paying for the backend and discord bot as of **5/27/23**:

    - Alan Tong (Linode Nanode - $5 a month) (Discord: `atlinx`)

!!! note

    	It's important to ensure we have access to the cogs.club domain.

    	Alumni who currently owns the cogs.club domain:

    	- Harry Stern (Discord: `ohmyachingtentacles`)
