# Installing Tailscale on Proxmox

## Introduction 

In this episode we are going to cover installing Tailscale on a Proxmox VM and showing you how to connect back to your local Nextcloud server!

By doing so, you will be able to back up any pictures or documents you take/create well away from your home network. 

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
    <p>Do not be like me, when you go on a vacation, upload your pictures each night to your Nextcloud backup! The next day your phone could get lost, stolen, or water damaged! Having picture memories is so important!</p>
</div>

</body>
</html>

## Tailscale introduction

Tailscale is a secure, open-source Virtual Private Network (VPN) service that allows users to connect devices and services across networks.

How it works: Tailscale creates a peer-to-peer mesh network, called a tailnet, that allows devices to connect directly to each other. This differs from traditional VPNs, which tunnel all traffic through a central gateway server.

You are making it so your two geographically separate devices appear to be on one network, like both devices being on your home network even when you are on the other side of the world. This allows you to access all your home hosted services!

## Our Video on this topic

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/bsdxcfVt6vg?si=IahsvHM7HZ5yDjf4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Create a Proxmox VM


First open Proxmox and create an Ubuntu VM, default settings are fine kind of okay: 15gb of storage, 2 vCPU, 2GB of RAM (you can lower this to a half gig of RAM AFTER install). Everything else can stay the same.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.4.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.4.1.png" alt="Description of your image">
</a>

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
    <p>During the actual Ubuntu install ensure you enable the SSH option!</p>
</div>

</body>
</html>

<a href="/images/EP9_tailscale/Still 2024-12-31 184715_1.5.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 184715_1.5.1.png" alt="Description of your image">
</a>

Next login to your VM using SSH

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.5.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.5.1.png" alt="Description of your image">
</a>


## Installing Tailscale 
Now we can get the download script [here](https://tailscale.com/download/linux)

(Linux) Others operating systems can be found on their site.
```
curl -fsSL https://tailscale.com/install.sh | sh
```

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.6.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.6.1.png" alt="Description of your image">
</a>

Type that command into your VM to install Tailscale

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.7.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.7.1.png" alt="Description of your image">
</a>

After the install is complete, we need to run the command

```
sudo tailscale up
```
Which will present us with our URL to login/create an account for our Tailscale network.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.9.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.9.1.png" alt="Description of your image">
</a>

Use whatever method you prefer to make your account

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.10.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.10.1.png" alt="Description of your image">
</a>

In our case we are going to use for personal use (which is true) but it is also free for three users and 100 devices.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.10.2.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.10.2.png" alt="Description of your image">
</a>

## Make Tailscale an Exit Node for LAN access

There is one more step we need to perform by SSHing into our Tailscale server. We need to make it an exit node, this allows your remote connections to exit your Tailscale VM and access the other VMs on your home network.

There are three commands we need to type in to make our Tailscale VM the exit node:

1. Advertise a device as an exit node config file:

```
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```
2. Then we need to advertise the exit node by restarting the tailscale service:

```
sudo tailscale set --advertise-exit-node
sudo tailscale up
```
3. Then we need to advertise our route including your networks CIDR notation:

```
sudo tailscale up --advertise-routes=<your LAN network IP range>/24 --reset
```

<a href="/images/EP9_tailscale/Still 2025-01-04 172122_1.12.3.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2025-01-04 172122_1.12.3.png" alt="Description of your image">
</a>

After that you need to go login to Tailscales site and find your VM now assigned as an exit node, click the three dots <kbd>...</kbd> and select **Edit route settings**

<a href="/images/EP9_tailscale/Still 2025-01-04 172122_1.12.4.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2025-01-04 172122_1.12.4.png" alt="Description of your image">
</a>

After that, just select the two boxes and you have set up your exit node.

<a href="/images/EP9_tailscale/Still 2025-01-04 172122_1.12.5.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2025-01-04 172122_1.12.5.png" alt="Description of your image">
</a>

## Adding other devices to your MESH network for remote access

Now you need to add a device that will create your mesh Tailscale network. In our example we have downloaded Tailscale on our phone and will connect back to our network through Tailscale to upload pictures to our Nextcloud backup server.

1. Tailscale for Android can be found [here](https://play.google.com/store/apps/details?id=com.tailscale.ipn&hl=en_US&pli=1)
2. Tailscale for Iphones can be found [here](https://apps.apple.com/us/app/tailscale/id1470499037)
3. Tailscale for Windows/MacOS can be found [here](https://tailscale.com/download/windows)

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.11.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.11.1.png" alt="Description of your image">
</a>

## Connecting to our home network remotely using Tailscale

On our phone we have installed the Tailscale app and logged into the same account that we used when creating our server.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.12.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.12.1.png" alt="Description of your image">
</a>

You will then be able to see all the devices connected to your mesh network as well as the ability to turn Tailscale on or off.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.13.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.13.1.png" alt="Description of your image">
</a>

Now your phone is just like being on your home network. We can open the Nextcloud app and put the LOCAL IP address of our Nextcloud backup server and connect to it as if we were on our home network.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.15.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.15.1.png" alt="Description of your image">
</a>

Look at that, now you have a way to upload your very important vacation images to your home NAS/Nextcloud backup server remotely! 

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.16.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.16.1.png" alt="Description of your image">
</a>

## Managing Tailscale machines

Lastly, you can also login to your Tailscale account and manage your devices and see what devices have access to your mesh network.

<a href="/images/EP9_tailscale/Still 2024-12-31 194421_1.19.1.png" class="image-expand">
    <img src="/images/EP9_tailscale/Still 2024-12-31 194421_1.19.1.png" alt="Description of your image">
</a>

## Conclusion

Now you are able to access ANY device on your local home network via your Tailscale server, this means your NAS, game servers, Plex server, etc. Tailscale is like your computer or phone being on your home network where you can browse to anything locally.

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)