# Zabbix Agent install on a VM (Linux)

## Introduction 

In this episode we are going to be covering how to setup a Zabbix Agent specifically for Linux but this method really applies for all ways when it comes to configuring the devices. 

If you want to know how to setup the Zabbix server please find our article/video on that [here](/homelabseries/EP10_zabbixserver)

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/JYr1iXsgra8?si=epf_2LG90cJUi1Qd" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


## Getting started

1. Find the current agent commands [here](https://www.zabbix.com/download) Select the current Zabbix version you are installing, OS, OS version, Zabbix component (AGENT), database will be MYSQL, and Web server is APACHE

2. Login to your Zabbix Server Panel in the Browser

3. Lastly, select what VM/Machine(s) you want to install your agent(s) on.


## Step by step guide

Now go ahead and login to your select VM/Machine(s)

```
ssh username@ip_address_of_machine
```

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.1.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.1.png" alt="Description of your image">
</a>

We are going to start installing the Zabbix Agent using the commands found from our getting started section step 1. In this case we are installing 7.0 for the following commands:


Makes you a super user:

```
sudo -s
```

Install the REPO:

```
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu22.04_all.deb
```

Unpackage the REPO:

```
dpkg -i zabbix-release_latest_7.0+ubuntu22.04_all.deb
```

Update the REPOS:

```
apt update
```

Install the Agent

```
apt install zabbix-agent
```

Start the Zabbix Process

```
systemctl restart zabbix-agent
```
AND
```
systemctl enable zabbix-agent
```

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.2.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.2.png" alt="Description of your image">
</a>


## Configure the Zabbix Agent Config file

Now we need to change two entires in our config file. We need to point our AGENT AT the IP address of our **Zabbix SERVER!**

That will be done with the following commands:

```
sudo nano /etc/zabbix/zabbix_agentd.conf
```

Within that file you need to find:

1. Change **server=(your zabbix server IP)**

2. Change **serveractive=(your server IP)**

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.3.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.3.png" alt="Description of your image">
</a>

AND 

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.4.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.4.png" alt="Description of your image">
</a>

## Check the Status of Your Zabbix Agent

Now you can verify your Agent is running with the following commands and will run after a VM reboot:

```
sudo systemctl enable zabbix-agent
```

Verify the setting:

```
systemctl is-enabled zabbix-agent
```

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.5.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.3.5.png" alt="Description of your image">
</a>

## Adding an Agent to your Zabbix Server

Now we need to add an agent on the far right under Monitoring / Hosts.

On the far right you will see a blue create hosts button.

Give the device a hostname, grab the correct template in our case it is the **Linux by Zabbix agent** NOT the Agent Live one.

Then input the IP address of your VM/machine you just installed your Agent on and click add. 

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.4.1.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.4.1.png" alt="Description of your image">
</a>

Now wait about 30 seconds to 5 minutes for the Availability ZBX sign to go green, and you will know its working. Red means its not, and gray is unknown (usually shown when you first add them).

You can also click the Latest data tab to see what information it can gather or is gathering. This can take a couple hours to grab more specific data if the machine is even offering that type of data.

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.4.2.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.4.2.png" alt="Description of your image">
</a>

Picture showing data it is currently pulling:

<a href="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.4.3.png" class="image-expand">
    <img src="/images/EP11_zabbixagent/Still 2025-01-08 081514_1.4.3.png" alt="Description of your image">
</a>

## Closing thoughts

That is it! Pretty simple right? Now in another episode we will cover how to add these hosts to data panels on your dashboard but Zabbix is so extensive I would reccomend you Google around yourself and find what you want and add them that way.

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)