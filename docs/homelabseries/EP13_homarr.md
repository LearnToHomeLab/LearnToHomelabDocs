# How to Install The Homarr Dashboard 

<a href="/images/EP13_homarr/homarr outdated.png" class="image-expand">
    <img src="/images/EP13_homarr/homarr outdated.png" alt="Description of your image">
</a>

[EP 22 - Homarr 1.0 Install/Upgrade:](/homelabseries/EP22_homarr1.0upgrade)


## Introduction

In this episode we are going to cover how to install the Homarr Dashboard. Homarr is a dashboard that helps you manage your server by providing access to all your apps and services in one place. It's highly customizable and integrates with self-hosted applications.

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/rJCjVhstjTI?si=cj6cRKk7lsi_CzzG" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
------------------------------------------


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Informative Section</title>
<style>
.informative-section {
    background-color: #8CD2F4; /* light blue background color */
    color: black; /* Text color to contrast with dark background */
    padding: 20px; /* Padding inside the box */
    border-radius: 10px; /* Rounded corners */
    display: flex;
    align-items: center;
}
.circle-emoji {
    width: 50px;
    height: 30px;
    border-radius: 50%;
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-right: 15px;
    font-size: 20px;
    color: #231F20; /* Dark gray color for the exclamation mark */
}
</style>
</head>
<body>

<div class="informative-section">
    <div class="circle-emoji">!</div>
    <p>The following commands will work with EITHER a Proxmox VM or Proxmox container!</p>
</div>

</body>
</html>

## Getting Started

The first thing you will need to do is create a Proxmox VM or container. Please see the image below with the example of the configuration we used for our Homarr Vm. 

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.1.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.1.png" alt="Description of your image">
</a>

If you want to know where I got the commands shown in the video, they are from the following/trial and error: 

## Useful Links

1. [Docker for Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
2. [Docker Compose](https://docs.docker.com/compose/install/linux/#install-using-the-repository)
3. [Homarr for Docker Compose](https://homarr.dev/docs/getting-started/installation#-docker-compose)
4. [After the Homarr Install, how to configure the panel](https://homarr.dev/docs/getting-started/after-the-installation/)

## How to Install Homarr

After creating your VM/container, SSH into your about to be Homarr Machine. 

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.2.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.2.png" alt="Description of your image">
</a>

Now we are going to start installing all the packages (Docker, Docker Compose, and Homarr). 

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.3.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.3.png" alt="Description of your image">
</a>

### Installing Docker

Adding the GPG keys and Docker repo:

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

Install the Latest Package:

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Ensure Docker is running after Install, you will get a response like this.

```
sudo docker run hello-world
```

<a href="/images/EP13_homarr/docker hello response_1.3.1.png" class="image-expand">
    <img src="/images/EP13_homarr/docker hello response_1.3.1.png" alt="Description of your image">
</a>

#### If Docker hello fails do the following

if you do not get a response try

```
systemctl status docker.service
```

If that shows failed messages, try the following

```
sudo systemctl daemon-reload
sudo systemctl restart docker
```

Then try to see its status once again:

```
systemctl status docker.service
```

<a href="/images/EP13_homarr/docker status_1.3.2.png" class="image-expand">
    <img src="/images/EP13_homarr/docker status_1.3.2.png" alt="Description of your image">
</a>

### Install Docker Compose

Install Docker Compose with:

```
sudo apt install docker-compose
```

Verify that docker compose is installed

```
docker compose version
```

<a href="/images/EP13_homarr/docker compose version number_1.3.3.png" class="image-expand">
    <img src="/images/EP13_homarr/docker compose version number_1.3.3.png" alt="Description of your image">
</a>

## Install Homarr

Then create a docker compose file:

```
nano docker-compose.yml
```

Copy the following file config in there from Homarr

```
#---------------------------------------------------------------------#
#     Homarr - A simple, yet powerful dashboard for your server.      #
#---------------------------------------------------------------------#
services:
  homarr:
    container_name: homarr
    image: ghcr.io/ajnart/homarr:latest
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # Optional, only if you want docker integration
      - ./homarr/configs:/app/data/configs
      - ./homarr/icons:/app/public/icons
      - ./homarr/data:/data
    ports:
      - '7575:7575'
```

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.4.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.4.png" alt="Description of your image">
</a>

Then run the following to start it:

```
sudo docker compose up -d
```

Then to login to your machine you will type the following into your browser to access the panel:

```
ip_address:7575
```

After you go to the site you will be presented with this screen, make a username and matching password.

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.5.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.5.png" alt="Description of your image">
</a>

To edit the dashboard you will select the following icon from the top right

<a href="/images/EP13_homarr/edit homarr dashboard_1.3.4.png" class="image-expand">
    <img src="/images/EP13_homarr/edit homarr dashboard_1.3.4.png" alt="Description of your image">
</a>

You will then be presented with the options APPS / WIDGETS / CATEGORIES. APPS are used to connect VMs, containers, etc. as hyperlinks so we can access those sites/resources quickly.

<a href="/images/EP13_homarr/dashboard homarr options_1.3.5.png" class="image-expand">
    <img src="/images/EP13_homarr/dashboard homarr options_1.3.5.png" alt="Description of your image">
</a>

When adding VMs, Containers, or other services you will use the IP address and the port number for both the internal and external address sections after selecting the APP option.

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.6.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.6.png" alt="Description of your image">
</a>

## Starting and Stopping Homarr

Start and stop

```
sudo systemctl stop docker
```
Restart:

```
sudo systemctl restart docker
```
Check the status:

```
sudo systemctl status docker
```

and start docker compose:

```
sudo docker compose up -d
```

## Next Steps After Installing Homarr

After you are done installing Homarr check out their content on how to setup Widgets and organize the Dashboard [here](https://homarr.dev/docs/getting-started/after-the-installation/)


If you would like to know how to add websites, and your Proxmox machines information like found in the screenshot below, please watch our next episode (EP14)

<a href="/images/EP13_homarr/Still 2025-01-13 155148_1.3.8.png" class="image-expand">
    <img src="/images/EP13_homarr/Still 2025-01-13 155148_1.3.8.png" alt="Description of your image">
</a>