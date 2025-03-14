# How to Setup The Nginx Proxy Manager and DuckDNS for Local SSL Certificates

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/DjKom4B4USo?si=2mTOOYuxy4Zwk7-l" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Create a Virtual Machine or Container

Setup a VM or CT on your preferred platoform, in our case we are going to create a CT on Proxmox:

Watch our video shown above if you need to know how to do this!

<a href="/images/EP26_nginxproxymanagerssl/ct overview.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/ct overview.png" alt="Description of your image">
</a>

## Installing Docker
We are going to use their documentation found [here](https://docs.docker.com/engine/install/ubuntu/)

First, ensure your system is up to date with

```
sudo apt update && sudo apt upgrade -y
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.15.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.15.1.png" alt="Description of your image">
</a>

Next we need to set up Docker's apt repository.

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

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.16.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.16.1.png" alt="Description of your image">
</a>

Install the Docker packages.

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.16.2.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.16.2.png" alt="Description of your image">
</a>

Verify that the installation is successful by running the hello-world image:

```
sudo docker run hello-world
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.18.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124231_1.18.1.png" alt="Description of your image">
</a>

## Creating the Nginx Docker Compose File

Go ahead and create the docker-compose file with

```
nano docker-compose.yml
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124914_1.18.2.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124914_1.18.2.png" alt="Description of your image">
</a>

Then you need to paste the MINIMUM required to compose file content, which is:

```
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124914_1.19.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124914_1.19.1.png" alt="Description of your image">
</a>

Bring up your stack with:

```
docker-compose up -d

# If using docker-compose-plugin
docker compose up -d
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124914_1.21.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 124914_1.21.1.png" alt="Description of your image">
</a>

## How to Login to Nginx Proxy Manager

When your docker container runs, connect to the IP on the port 81 for the admin interface. Sometimes, this can take a little bit because of the entropy of keys. Then create your own username, email, and password.

If you do not know your VM/CT IP you can use the following command to find it:

```
ip a
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 125654_1.23.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 125654_1.23.1.png" alt="Description of your image">
</a>

Then head to the site in your browser using:

```
http://<your VM/Container IP>:81
```

Email:

``` 
admin@example.com
```

Password:

```
changeme
```

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 125654_1.25.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 125654_1.25.1.png" alt="Description of your image">
</a>

## Creating your DuckDNS SSL Certificate

Head over to DuckDNS's website and login with your google account or other [here](https://www.duckdns.org/)

After you have logged in create a subdomain and add the IP address of your Nginx Proxy Manager VM/CT/Device. 

NOTE: This is also where you will get your token ID. 

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 130708_1.37.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 130708_1.37.1.png" alt="Description of your image">
</a>

 Now on your Nginx Proxy Manager Site click *SSL certificates* at the top and *Add SSL Certificate*

 <a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 130624_1.39.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 130624_1.39.1.png" alt="Description of your image">
</a>

 Fill out the information as shown below. Keep in mind you will add your `<subdomain_youcreated>.duckdns.org` AND a `*.<subdomain_youcreated>.duckdns.org`. ***Pay close attention to that wildcard, this will allow you to create many sub-sub domains on your local network!***

 <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Warning Box Example</title>

<style>
.warning-box {
    background-color: #E4141E; /* Light red background color */
    border-left: 6px solid #8CD2F4; /* Red border on the left side */
    padding: 10px; /* Padding inside the box */
    margin-bottom: 20px; /* Margin at the bottom to separate from other content */
}
</style>
</head>
<body>

<div class="warning-box">
    <p>YOU MAY GET A FAILED ERROR after clicking SAVE, this is due to all the public DNS servers in the world have not populated your new domain name yet. Wait a couple minutes, click save again and see if it works. </p>
</div>

</body>
</html>


 <a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 130624_1.43.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 130624_1.43.1.png" alt="Description of your image">
</a>

We now have a succesful SSL certificate (after about 5 minutes of waiting for the DNS record to populate around the world)

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 131610_1.45.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 131610_1.45.1.png" alt="Description of your image">
</a>

Now on your Proxy Dashboard click *hosts* at the top then click *Proxy hosts* then *add proxy host* at the top right. 

In this example you can see we added the `<pve>` <kbd>.</kbd> part to our domain `lthlearn.duckdns.org` that is how we can use the wild card `*` we created earlier. For all services on our network we will replace that wildcard with the site name we want. Also be mindful, Proxmox uses HTTPs by default but for most services you will probably select HTTP in the *scheme* box.

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Warning Box Example</title>

<style>
.warning-box {
    background-color: #E4141E; /* Light red background color */
    border-left: 6px solid #8CD2F4; /* Red border on the left side */
    padding: 10px; /* Padding inside the box */
    margin-bottom: 20px; /* Margin at the bottom to separate from other content */
}
</style>
</head>
<body>

<div class="warning-box">
    <p>Some services may require you to enable the `websockets support` option to work properly. Example: Code boxes that auto copy the commands require it.</p>
</div>

</body>
</html>


<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 131610_1.48.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 131610_1.48.1.png" alt="Description of your image">
</a>

After you click save you should now see your SSL/Domain entry. Try clicking it, for some of you it may work! If you use OPNsense like me, it will not, it will be blocked so we have one more step!

<a href="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 131610_1.49.1.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/Still 2025-03-14 131610_1.49.1.png" alt="Description of your image">
</a>

## Create an OPNSense Local DNS Wild Card Entry

Enable Unbound DNS:

Navigate to Services > Unbound DNS > General Settings.

Ensure that Unbound DNS is enabled.

<a href="/images/EP26_nginxproxymanagerssl/part 1 _ OPNsense.localdomain.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/part 1 _ OPNsense.localdomain.png" alt="Description of your image">
</a>

Add a Wildcard DNS Override:


Go to Services > Unbound DNS > Overrides.


Click the orange + Add button under Host Overrides.

<a href="/images/EP26_nginxproxymanagerssl/part 2 _ OPNsense.localdomain.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/part 2 _ OPNsense.localdomain.png" alt="Description of your image">
</a>

Fill out the form:

Host: * (wildcard for all subdomains).

Domain: duckdns.org.

Type: Select A for IPv4.

IP Address: Enter the internal IP of your Nginx Proxy Manager server (e.g., 192.168.50.234).

Optionally, add a description like "Wildcard for DuckDNS domains."

Save and apply changes.

<a href="/images/EP26_nginxproxymanagerssl/part 3_ OPNsense.localdomain.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/part 3_ OPNsense.localdomain.png" alt="Description of your image">
</a>

Flush DNS Cache:

After creating the override, flush the DNS cache on your local machine:

Open your CMD and type the following:

Windows:
```
ipconfig /flushdns
```

## Assign More domains to your outher services

Now go back to your Nginx Proxy Manager and click on your domain again and it should work!

Repeat the *proxy host* process for all the services you want to have SSL certifications to get rid of those annoying unsecure SSL errors! 

<a href="/images/EP26_nginxproxymanagerssl/2025-03-14 13_33_30-Nginx Proxy Manager.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/2025-03-14 13_33_30-Nginx Proxy Manager.png" alt="Description of your image">
</a>

*Secured websites are now working*

<a href="/images/EP26_nginxproxymanagerssl/2025-03-14 13_35_11-Nginx Proxy Manager.png" class="image-expand">
    <img src="/images/EP26_nginxproxymanagerssl/2025-03-14 13_35_11-Nginx Proxy Manager.png" alt="Description of your image">
</a>


## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)
