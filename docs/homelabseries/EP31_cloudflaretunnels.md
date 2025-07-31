# How to Set up CloudFlare Tunnels in 2025

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/wyKkeb3w5lI?si=lZfB9wOiqsqGqjyC" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Introduction 

A Cloudflare Tunnel is a technology that establishes a secure, outbound-only connection between your home network and the Cloudflare global network. It essentially creates a "tunnel" that allows you to expose your services running on your home network to the internet, without requiring you to open ports or configure complex firewall rules. This can be particularly useful for homelabs, as it allows you to easily access your self-hosted services from anywhere in the world. 

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
    <p>It is assumed you create a dedicated VM for your CloudFlare Tunnel Install, or install it on an existing VM. We show the install on an existing VM, BUT recommend a dedicated VM</p>
</div>

</body>
</html>


## How to Create a CloudFlare Tunnel

First, go to CloudFlare’s website and log in (you can create an account with your Google account) [here](https://www.cloudflare.com/)

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.5.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.5.1.png" alt="Description of your image">
</a>

If you do not have a domain associated with your account, go ahead and buy one now; they are about 11 dollars a year. 

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.6.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.6.1.png" alt="Description of your image">
</a>

After you have a domain, we need to select the *zero trust* page on the left.

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.8.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.8.1.png" alt="Description of your image">
</a>

You will be presented with the following screen, select *networks* then *tunnels*

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.1.png" alt="Description of your image">
</a>

On the Tunnels screen we will select *Add a tunnel*

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.2.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.2.png" alt="Description of your image">
</a>

From here we will select the reccomended option *Select Cloudflared*

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.3.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.3.png" alt="Description of your image">
</a>

Name your tunnel to whatever you want.

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.4.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.10.4.png" alt="Description of your image">
</a>

Next we will select our operating system, in this case that will be *Debian*.

Next we need to take the following two commands and paste them into a dedicated VM for Cloudflare which will be used as our exit node within our home network. This will give Cloudflare access to your whole home network, thus a tunnel can be created for ANY services within your homelab. For the purpose of this video we simply installed the tunnel on our KASM VM and showed you how to access KASM from the public domain we bought at the beginning of this tutorial. 

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.12.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.12.1.png" alt="Description of your image">
</a>

SSH into your machine to paste the two above commands:

```
ssh <username>@<server_ip>
```

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.13.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.13.1.png" alt="Description of your image">
</a>

*pasted commands*

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.13.2.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.13.2.png" alt="Description of your image">
</a>

Next we will see the tunnel connection has been made.

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.14.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.14.1.png" alt="Description of your image">
</a>

Now you will select your subdomain (based on your service), domain name you want to use, and the service: protocol + Ip_address of the software/application you want to make accessible. In our case KASM uses HTTPS and then we did the local IP of the KASM VM.

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.15.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.15.1.png" alt="Description of your image">
</a>

After that is created we will need to click the 3 dots on the far right and edit our new tunnel:

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.16.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.16.1.png" alt="Description of your image">
</a>

You will then be presented with the following screen, select *additional application settings*, *TLS*, and under *No TLS Verify* turn that on and click save. 

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.17.1.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.17.1.png" alt="Description of your image">
</a>

Now go into another browser tab and access your service at the URL you created under your tunnel! 

<a href="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.17.2.png" class="image-expand">
    <img src="/images/EP31_cloudflaretunnels/Still 2025-05-22 203133_1.17.2.png" alt="Description of your image">
</a>

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)

## Previous video

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/0oZLQZclnQs?si=_xH0nqPaHDKnHn4z" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>