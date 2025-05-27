# How to Enable Automatic Security Updates on Linux Ubuntu Server

## Linux Ubuntu Server Hardening

In this series we will cover how to harden your Linux Debian based distros. We are going to follow best practice to make your network more secure, as well as get your machines ready to face the public internet. 

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/sAR1B5bNI-0?si=bSiAEwQy8cL54ToY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Introduction

We will cover the following topics over the next 6 videos/articles

1.  Enable automatic security updates (live updates, no downtime to services, maintenance).

2.  SSH Key authentication (security).

3.  Enable the firewall (UFW) (security)

4.  Install Fail2Ban (security, protect against brute force attacks)

5.  Remove unnecessary packages (maintenance/security).

6.  Upload Public SSH Keys to Github (this allows you to auto-download your SSH keys during fresh server installs).

## Updating Linux

The first thing we want to do is make sure our system has the latest updates.

```
sudo apt update && sudo apt upgrade -y
```

## 1. Enable Automatic Security Updates

When we have services/software hosted for extremely long periods of time, we need to ensure we have consistent updates, new-found vulnerabilities come out daily, and we want to ensure our systems are as secure as possible.

The first command we want to run ensures that unattended upgrades are installed. You may get a response that it is already installed. We still need to make sure it is set to automatic updates.

```
sudo apt install unattended-upgrades
```

Let’s ensure it is running properly with:

```
systemctl status unattended-upgrades
```

To enable automatic security updates, we will edit the following file:

You should see the following parameters set to “1”:

_APT::Periodic::Update-Package-Lists "1";_

*APT::Periodic::Unattended-Upgrade "1";*

```
sudo nano /etc/apt/apt.conf.d/20auto-upgrades
```

### OPTIONAL

If you would like to dive deeper into automatic updates, you can edit the following file, you will have to do your own research on the options found within that folder which are past the scope of this article:

```
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```