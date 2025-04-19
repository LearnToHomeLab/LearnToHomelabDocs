# How to Install VaultWarden in 2025

We are using the documentation found [here](https://github.com/dani-garcia/vaultwarden)

## Prerequisites

You will need to give this site an SSL certificate to be able to access the site. You also want this because it prevents man-in-the-middle attacks from seeing your passwords. We have made a video on that, you can find it here:

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/DjKom4B4USo?si=2mTOOYuxy4Zwk7-l" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

The article on our site can be found [here](https://www.learntohomelab.com/homelabseries/EP26_nginxproxymanagerssl/)

## Create a Container/VM in Proxmox

The CT will be configured with 512MB of ram, 2 CPU cores, and 10 GB of storage.

1.  Log in with the username _root_ and the password you created during setup.
2.  Do the following command to get the IP address of your CT:
    
```
ip a
```

<a href="/images/EP28_vaultwarden/Still 2025-04-19 115016_1.7.1.png" class="image-expand">
    <img src="/images/EP28_vaultwarden/Still 2025-04-19 115016_1.7.1.png" alt="Description of your image">
</a>

## Installing Vaultwarden Video

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/HNW9jKKz-Xw?si=7EpeqaphNn4lLAhL" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


## Installing Docker & Compose

We will be following the documentation found [here](https://docs.docker.com/engine/install/ubuntu/)

See the following commands to install Docker:

Run the following command to uninstall all conflicting packages:

```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

<a href="/images/EP28_vaultwarden/Still 2025-04-19 115234_1.7.2.png" class="image-expand">
    <img src="/images/EP28_vaultwarden/Still 2025-04-19 115234_1.7.2.png" alt="Description of your image">
</a>

Set up Docker's `apt` repository.

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
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Install the Docker packages.

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

## Create a compose file

To use Docker Compose, you need to create a `compose.yaml` which will hold the configuration for running the Vaultwarden container.

```
nano compose.yml
```

Then you paste the following configuration:

```
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: unless-stopped
    environment:
      DOMAIN: "https://vw.domain.tld"
    volumes:
      - ./vw-data/:/data/
    ports:
      - 80:80
```

Start the Docker Compose file with (the -d runs it in the background so you can still use your CLI:)

```
docker compose up -d
```

## Set up your SSL Certificate

If you have not followed our previous video on how to set up SSL certificates with Nginx Proxy Manager, please follow that video [here](https://www.youtube.com/watch?v=DjKom4B4USo)

## After logging into Vaultwarden

1.  Open Vaultwarden via the new URL you created.
2.  Create a username and password
3.  login
4.  Select “Install Browser Extension.”
5.  On the top right of Chrome, find your Vaultwarden extension
6.  Select “Accessing” (Bitwarden), there will be a self-hosted option, select that, and type the URL of your own Bitwarden server.

<a href="/images/EP28_vaultwarden/Still 2025-04-19 115234_1.19.1.png" class="image-expand">
    <img src="/images/EP28_vaultwarden/Still 2025-04-19 115234_1.19.1.png" alt="Description of your image">
</a>

7.  You will then be able to go to your common websites and add your username and password into Vaultwarden for use at later times, change your passwords to a more complex password, and much more.