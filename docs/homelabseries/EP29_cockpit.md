# How to Install Cockpit for Linux Server

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/V7TVWiYpWfk?si=IlzUL7dysPyqfUjL" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Manage Linux Servers With Cockpit

The first step you need to take is to create an Ubuntu Linux Server in your virtual environment of choice. We are using Proxmox for this tutorial. Ensure you have the latest Ubuntu Server installed, which can be found [here\](https://releases.ubuntu.com/). In our case, we are going with 24.04 LTS.

## Update Ubuntu Server

First thing we want to do is ensure all packages are up to date before installing anything with:

```
sudo apt update && sudo apt upgrade -y
```

We are using the documentation that can be found [here](https://cockpit-project.org/running.html)

## Installing Cockpit

This repository is enabled by default, so all we want to do is make sure everything is up to date with the following commands.

```
. /etc/os-release
sudo apt install -t ${VERSION_CODENAME}-backports cockpit
```

To access the cockpit, open your preferred browser and go to the following.

```
https://IP_ADDRESS_OF_MACHINE:9090
```

## Software Tab

Go ahead and drop down to the software tab and perform any missing updates before continuing.

## Fix Cache Whilst Offline Error

You may run into an error like “Cannot download packages whilst offline.” This is a standard error with Ubuntu Server and can be fixed by following the documentation found [here](https://cockpit-project.org/faq.html#error-message-about-being-offline)

Commands to solve the error:

```
sudo nano /etc/NetworkManager/conf.d/10-globally-managed-devices.conf
```

Then add the following:

```
 [keyfile]
 unmanaged-devices=none
```

Lastly, you will set up a dummy network interface with:

```
sudo nmcli con add type dummy con-name fake ifname fake0 ip4 1.2.3.4/24 gw4 1.2.3.1
```

Then reboot your system:

```
sudo reboot
```

## How to use Cockpit

### Overview

The first tab, overview, allows you to see the overall health of your system, hardware details, bugs, and configuration settings.

### Logs

Logs creates an easy place to access logs on the system for investigations or oversight.

### Storage

This area allows you to see the usage of partitions, capacity, and drive mounting locations. You can even use the three dots at the top right next to the “Hard Disk Drive” name to create more partitions, or select the three dots next to the current partitions to change the sizing and formatting if they are set up correctly.

### Networking

The networking tab is a great tool to ensure your Ethernet connections are not throttling your device. You can also add VPNS, bonds, teams, bridges, and more under this tab.

### Accounts

Accounts are one of the things people struggle with the most. Under this tab, you can create tabs, manage users' access, and see what groups they are a part of and when they last logged in. You can easily add SSH keys for users from their profile when clicking the three dots to the far right of their name.

### Services

This tab allows you to see processes running on the device.

### Applications

Applications are one of the best features of Cockpit, as they allow you to manage things from your browser, like containers and virtual machines. Official applications can be found \[here\](https://cockpit-project.org/applications), but there are also community ones you can find online

We will be installing the application for virtual machines found [here](https://github.com/cockpit-project/cockpit-machines)

Command-line installation is also possible using the package name like seen below:

```
sudo apt install cockpit cockpit-machines
```

Then you need to refresh your browser to see the application

Start and enable the cockpit services.

```
sudo systemctl start cockpit
```

```
sudo systemctl enable cockpit
```

### Software Updates

We already covered this page briefly but this tab is where you will go to update your machine.

### Terminal

This tab is self-explanatory, but it allows you to access your machine via SSH.

## Cockpit Server Accounts

Another advantage of Cockpit is your ability to manage multiple machines by clicking your name at the top left and adding more hosts. This allows you to switch between machines easily.

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)