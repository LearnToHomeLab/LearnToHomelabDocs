# How to Install Docmost on Proxmox with SSL

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/FoFEen6DQ5g?si=ASDbGQOzS1dPw29L" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Welcome to another video guys, in this video we will cover how to install Docmost on Proxmox to include an SSL certificate for our site! The SSL certificate is required to get all the features out of Docmost. Any browser note taking application will require SSL and websocket support for features like code block auto copy and paste to work. You can follow the previous episode (episode 26) if you have not setup a reverse proxy with an SSL certificate. 

## Create a Container on Proxmox 

This step has been covered in many episodes, if you want specific details please watch our video linked above. 

1. Go to our node's local storage and download the CT Ubuntu template (if you have not done this already for previous CT installs you have done or videos you have followed from us).

2. Configure the CT settings (it is very important to select the correct Networking settings DHCP or self assign a static IP).

3. Then start our machine.

To Login to your CT, go to your console tab and type the following

4. Username: `root`

5. Password: (Is what you set during the  creation of the CT)

## Installing Docker

We are going to use their documentation found [here](https://docs.docker.com/engine/install/ubuntu/)

Set up Docker's apt repository.

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

<a href="/images/EP27_docmost/SSD 1_1.6.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.6.1.png" alt="Description of your image">
</a>


Install the Docker packages.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

<a href="/images/EP27_docmost/SSD 1_1.7.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.7.1.png" alt="Description of your image">
</a>

Verify that the installation is successful by running the hello-world image:

```
sudo docker run hello-world
```

<a href="/images/EP27_docmost/SSD 1_1.8.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.1.png" alt="Description of your image">
</a>

## Install Docmost

Setup the Docker compose file​

Create a new directory for Docmost and download the Docker compose file with commands below:

```
mkdir docmost
cd docmost
curl -O https://raw.githubusercontent.com/docmost/docmost/main/docker-compose.yml
```

<a href="/images/EP27_docmost/SSD 1_1.8.2.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.2.png" alt="Description of your image">
</a>

We are going to use their documentation found [here](https://docmost.com/docs/installation/)

Before we edit that file we need to get a key for our app_secret which will be used in our docker compose file using the following command:

```
openssl rand -hex 32
```

<a href="/images/EP27_docmost/SSD 1_1.8.3.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.3.png" alt="Description of your image">
</a>

We then need to get our machines IP address to enter into this file using (make sure you write down your IP and key somewhere)

```
ip a
```

<a href="/images/EP27_docmost/SSD 1_1.8.4.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.4.png" alt="Description of your image">
</a>

For the below exmapel you need to change the following parameters:

1. The `APP_URL` should be replaced with your chosen domain. E.g. `https://example.com` or `https://docmost.example.com`.

2. The `APP_SECRET` value must be replaced with a long random secret key (32 characters minimum) you created a second out with the openssl command.
**You can generate the secret with openssl rand -hex 32. If you leave the default value, the app will fail to start.**

3. Replace `STRONG_DB_PASSWORD` in the `POSTGRES_PASSWORD` environment variable with a secure password of your making.

4. Update the `DATABASE_URL` default `STRONG_DB_PASSWORD` value with your chosen Postgres password you created in step 3 (they need to match).

You are going to edit those four parameters in the following document:

Open the file with nano:

```
nano docker-compose.yml
```

<a href="/images/EP27_docmost/SSD 1_1.8.5.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.5.png" alt="Description of your image">
</a>

Example/template:

```
version: "3"

services:
  docmost:
    image: docmost/docmost:latest
    depends_on:
      - db
      - redis
    environment:
      APP_URL: "http://localhost:3000"
      APP_SECRET: "REPLACE_WITH_LONG_SECRET"
      DATABASE_URL: "postgresql://docmost:STRONG_DB_PASSWORD@db:5432/docmost?schema=public"
      REDIS_URL: "redis://redis:6379"
    ports:
      - "3000:3000"
    restart: unless-stopped
    volumes:
      - docmost:/app/data/storage

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: docmost
      POSTGRES_USER: docmost
      POSTGRES_PASSWORD: STRONG_DB_PASSWORD
    restart: unless-stopped
    volumes:
      - db_data:/var/lib/postgresql/data

  redis:
    image: redis:7.2-alpine
    restart: unless-stopped
    volumes:
      - redis_data:/data

volumes:
  docmost:
  db_data:
  redis_data:
  ```

  <a href="/images/EP27_docmost/SSD 1_1.8.6.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.6.png" alt="Description of your image">
</a>

## After Docmost Install

Start the Services​

Make sure you are inside the docmost directory which contains the docker-compose.yml file.

To start the services, run:

```
docker compose up -d
```

<a href="/images/EP27_docmost/SSD 1_1.8.7.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.8.7.png" alt="Description of your image">
</a>

Now you can go to your Docmost instance at:

```
http://<ip_address>:3000
```

You will be prompted with the following screen to create your own account:

NOTE: it only asks for a password one time SO MAKE SURE YOU TYPE IT RIGHT!

<a href="/images/EP27_docmost/SSD 1_1.13.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.13.1.png" alt="Description of your image">
</a>

## How to Configure/Use Docmost

### Change theme to light or dark mode

To change to Darkmost you can click your profile at the top right / my preferneces / and select dark mode under theme. 

<a href="/images/EP27_docmost/SSD 1_1.14.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.14.1.png" alt="Description of your image">
</a>


<a href="/images/EP27_docmost/SSD 1_1.14.2.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.14.2.png" alt="Description of your image">
</a>

### Create Spaces

You can organize your notes into "books" or what they call Spaces. You can use Spaces for specific topics or control user access to spaces which is really cool. This can be found under settings / spaces

<a href="/images/EP27_docmost/SSD 1_1.14.3.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.14.3.png" alt="Description of your image">
</a>

To change between spaces you will click the drop down when in notes. (Reminder, if you just created a space you may need to refresh your browser to see it)

<a href="/images/EP27_docmost/SSD 1_1.17.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.17.1.png" alt="Description of your image">
</a>

### Creat folders

To create folders by topics you can create a page and then drag and hold it over another, this will imbed the page and create a drop down folder. 

<a href="/images/EP27_docmost/SSD 1_1.19.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.19.1.png" alt="Description of your image">
</a>

*here is what that looks like*

<a href="/images/EP27_docmost/SSD 1_1.19.2.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.19.2.png" alt="Description of your image">
</a>

### Adding sections / features / Code blocks

Docmost used the */* command, this will then present you with a menu of all the items you can add to your page

<a href="/images/EP27_docmost/SSD 1_1.21.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.21.1.png" alt="Description of your image">
</a>

## Adding the SSL certificate 

Again, if you do not have an SSL certificate for SSL you can watch our previous episode (EP 26) found in the far left column or on our YouTube Channel [here](https://www.youtube.com/watch?v=DjKom4B4USo&t=843s&ab_channel=LearnToHomeLab)

<a href="/images/EP27_docmost/SSD 1_1.24.1.png" class="image-expand">
    <img src="/images/EP27_docmost/SSD 1_1.24.1.png" alt="Description of your image">
</a>

## How to Update Docmost

To upgrade:

Make sure you run the following in your Docmost directory and run the following commands ALSO be sure to save any files or not be working in Docmost when performing these commands:

*docker pull docmost/docmost*

*docker compose up --force-recreate --build docmost -d*

(sorry I cannot make this a copy code box or it breaks the page for some reason)

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)
