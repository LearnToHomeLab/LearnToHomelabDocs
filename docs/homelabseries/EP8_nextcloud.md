# NextCloud Setup inside of Proxmox

In this episode, we are going to cover how to set up a NextCloud server (container) within Proxmox Virtual environment in just a few clicks using TurnKey.
These container templates come with Proxmox already, making it a super simple task to have a network-wide backup server for your pictures and documents. 
 

## Back Story
Learn from me: my wife went on a honeymoon cruise to the Bahamas and virtually have NO pictures of our trip because our phones got water damaged! Backing up your
pictures at the end of each day to your NextCloud server could save you much heartache! We learned, though, that our Europe trip of 2024 was full of me backing up our content daily! *This Episode won't cover how to back up your content outside of your network, but our TailScale episode will!*

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/SbGSgMMt6gg?si=lPlB3rZp0Svq9eyk" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Install Steps

First log into Proxmox and go to:

1. *server* / *local (pve)* (or whatever your server name is) 
2. / *CT Templates* / *Templates*

and then search for Nextcloud and select download! Wait for that *Task OK* and move on with the next steps!

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.3.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.3.1.png" alt="Description of your image">
</a>

Now we are going to click create CT on the top right of our environment and follow the creation wizard for our container.

The general tab password is for the containers root user. The container default username is root and then the password you set.

I am not going to show every tab, but you can see from the image below there is general, templates, etc. We are concerned about the templates tab where you will select nextcloud, the *Disks* tab SET THIS AS HIGH AS YOU CAN. This is determines how many pictures you can save., and then under the network tab we need to set a static IP address for our machine. We need to ensure in OPNsense or your router that the IP you are assigning has not already been issued to another machine.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.4.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.4.1.png" alt="Description of your image">
</a>

We can verify what FREE IP addresses we have by opening OPNsense and going to (Services / ISC DHCPv4 / [LAN] & Leases) tabs. As long as you do not see either one of those tabs with the IP you want to use, you are good to assign the container that address.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.7.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.7.1.png" alt="Description of your image">
</a>

Going back to Proxmox we can see we have moved all the way to the Network Tab. AGAIN, do not forget to assign the proper disk space to save images and the other CPU and memory tab could be left default if you want.

Now assign the IPv4 address you have chosen and ensure you add your networks CIDR notation to the end. 99% of you it will be a /24 for a basic home network. 

Then assign the gateway which is the IP of your home router or OPNsense box. 

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.8.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.8.1.png" alt="Description of your image">
</a>

Here is an overview of my Containers settings. Disk is not shown but again make sure you make that nice and big so you can save loads of images. You will probably want somewhere in the ballpark of 100Gbs+.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.8.2.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.8.2.png" alt="Description of your image">
</a>


## Nextcloud Install Wizard 

Select your container from the right menu, you will notice containers sit above Virtual Machines so make sure you aren't missing it! 

under the console tab click start, and after boot login with 

Username: Root

Password: (the one you set on the general tabs page of container creation)

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.1.png" alt="Description of your image">
</a>

Login screen image:

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.2.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.2.png" alt="Description of your image">
</a>

Soon as you login you will be prompted by the NextCloud install wizard.

Follow the wizard through, it is very explanatory, and you are really creating passwords for accounts.

Keep these account passwords stored in your notes for later!

Mysql
<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.3.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.3.png" alt="Description of your image">
</a>

Nextcloud Admin (YOU WILL LOGIN WITH THIS ONE!)
<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.4.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.4.png" alt="Description of your image">
</a>

You can skip this one, we are not going to access Nextcloud with a URL.
<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.5.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.5.png" alt="Description of your image">
</a>

We are not going to use Turnkey backup so you can click your tab key twice and then enter for skip.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.6.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.6.png" alt="Description of your image">
</a>

You can enter an email here for notifications if you'd like.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.7.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.7.png" alt="Description of your image">
</a>

Always ensure you have the latest security updates so click install.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.8.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.9.8.png" alt="Description of your image">
</a>

At this point you have reached the end, copy this info into your notes and then you can do <kbd>ctrl</kbd> + <kbd>enter</kbd> to exit the menu.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.10.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.10.1.png" alt="Description of your image">
</a>

Going to the Nextcloud IP address in our browser we can see there is a security feature that prevents us from accessing it:

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.1.png" alt="Description of your image">
</a>

If click doumentation we are taking to this page that gives us some insight on how to fix this.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.2.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.2.png" alt="Description of your image">
</a>

We need to go into the following settings directory to make the correct changes.

```
nano /var/www/nextcloud/config/config.php
```

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.3.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.3.png" alt="Description of your image">
</a>

You will be presented with the following file and we are going to edit the following 'trusted_domains' section.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.4.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.4.png" alt="Description of your image">
</a>

We want to make that sections in ours look like this:

```
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => '192.168.50.20', 
),
```

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.5.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.5.png" alt="Description of your image">
</a>

Now we can go back to the site and login:

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.6.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.11.6.png" alt="Description of your image">
</a>

Before we continue, we need to set the static IP address of our NextCloud container in OPnsense.

First lets grab the Mac address of our container under our container network settings location. Select the network card and click edit, they copy the MAC.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.16.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.16.1.png" alt="Description of your image">
</a>

Now go over to OPNsense and we can create a static listing under Services / ISC DHCPv4 / [LAN] and selecting the + button.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.12.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.12.1.png" alt="Description of your image">
</a>

Now we can take that MAC address and our IP address and add it into our static assignment. Then click save.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.16.2.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.16.2.png" alt="Description of your image">
</a>

Going back over to Nextcloud after you logged in, we can use the *new* button to create new folders or upload a file to the current folder you are in.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.16.3.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.16.3.png" alt="Description of your image">
</a>

## Login on your phone

Download the NextCloud app and you can connect to your server using that IP address just like you did in your browser.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.17.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.17.1.png" alt="Description of your image">
</a>

Select yes on the certificate, we trust it because its our certificate!

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.17.2.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.17.2.png" alt="Description of your image">
</a>

Then you can login.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.17.3.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.17.3.png" alt="Description of your image">
</a>

Now your connected, go back over to your app to use NextCloud.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.18.1.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.18.1.png" alt="Description of your image">
</a>

Then we can use the + button just like the site and upload pictures or create folders.

<a href="/images/EP8_nextcloud/Still 2024-12-30 112738_1.20.2.png" class="image-expand">
    <img src="/images/EP8_nextcloud/Still 2024-12-30 112738_1.20.2.png" alt="Description of your image">
</a>

## Closing comments

That is it, I hope you guys enjoyed! In a later episode we will cover Tailscale and how to access your NextCloud from outside your network. 

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)