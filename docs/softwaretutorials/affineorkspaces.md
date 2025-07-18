## How to Install Affine Workspace Notes App in Your Homelab  Step-by-Step Tutorial

# Affine Hardware Requirements

1.  100 MB storage space growth per 1k documents with 1k words per document, so you decide how much you think you'll need (leave around 10 gigs for the OS/docker too).
2.  4 Cores (you can set 4 cores), but it will rarely use them unless you are actively performing hard tasks.
3.  4 GB of RAM (for docs with over 10K words or 2GB for more normal usage).
4.  A reverse proxy, we will use the Nginx Proxy Manager from our video you can find [here](https://www.youtube.com/watch?v=DjKom4B4USo&ab_channel=LearnToHomeLab)

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/oUwv6MjE6BU?si=N1G55AGJzfQjs1Gp" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
-----

# Create LXC on Proxmox

Go ahead and create an LXC within your Proxmox environment with the recommended settings above.

# Install Docker/Docker Compose

1.  Install using the apt repo.

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2.  Install the Docker packages.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify that the installation is successful by running the `hello-world` image:

```
sudo docker run hello-world
```

Verify the compose version:

```
docker compose version
```

# Installing Affine

It is best practice to create a dedicated directory for each Docker container to better backup data.

```
mkdir affine
cd affine
```

We are going to download the latest version of Affine

```
wget -O docker-compose.yml https://github.com/toeverything/affine/releases/latest/download/docker-compose.yml
```

A `.env` A file is required to configure Docker volumes, mapping them to a specific location where the user data will be persisted, and other required environment variables.

```
wget -O .env https://github.com/toeverything/affine/releases/latest/download/default.env.example
```

# Editing the .env file

Here is the default install you will see when you open the Affine .env file

```
# select a revision to deploy, available values: stable, beta, canary
AFFINE_REVISION=stable

# set the port for the server container it will expose the server on
PORT=3010

# set the host for the server for outgoing links
# AFFINE_SERVER_HTTPS=true
# AFFINE_SERVER_HOST=affine.yourdomain.com
# or
# AFFINE_SERVER_EXTERNAL_URL=https://affine.yourdomain.com

# position of the database data to persist
DB_DATA_LOCATION=~/.affine/self-host/postgres/pgdata
# position of the upload data(images, files, etc.) to persist
UPLOAD_LOCATION=~/.affine/self-host/storage
# position of the configuration files to persist
CONFIG_LOCATION=~/.affine/self-host/config

# database credentials
DB_USERNAME=affine
DB_PASSWORD=
DB_DATABASE=affine
```

You can access this configuration file with nano within your _Affine_ directory

```
nano .env
```

Change the following variables and uncomment them by removing the _#_ (pound sign) so you can access Affine exclusively over a secure connection:

```
AFFINE_SERVER_HTTPS=true
AFFINE_SERVER_HOST=affine.yourdomain.com
```

Now we can start Affine with the following Docker command:

```
docker compose down
docker compose up -d
```

# Adding Affine to Nginx Proxy Manager

Log in to your Nginx Proxy Manager and perform the following:

1.  Select _hosts_ from the top
2.  Select _proxy hosts_
3.  Select _Add proxy host_ top right
4.  Input the URL you set earlier in the .env file
5.  Add the IP address and put port 3010
6.  Leave the HTTP option as is
7.  Turn on websockets support
8.  Go to the SSL tab and add your SSL certificate
9.  Select _save_
10. Now, click the domain name in your

## You Will Log in with:

You will log in to the Affine admin with the */admin* subpage or **the normal page without it:**

```
http://<ip>:3010/admin
```

# Accept Affine Cloud

This error is not very clear, because this is self-hosted, it does not realize you are not connected to the cloud, so when it says sink with the cloud, it means it will store your data within your PostgreSQL database locally, because that is what is set in our config files by default.

# Upgrading Affine

If you ever need to update to the latest release, you can follow their documentation [here](https://docs.affine.pro/self-host-affine/install/upgrade)

All their related documentation can be found [here](https://docs.affine.pro/index)

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)