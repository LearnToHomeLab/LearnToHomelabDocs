# Topic: How to setup a Pfsense/OPNsense firewall

## Introduction:
If you have found yourself here it is because you have a desire to install your own enterprise-grade firewall, and we will be doing exactly that. Overall, pfSense/OPNsense allows for a reliable network backbone, routing, VPN connections, security features, failover scenarios, and inter-VLAN routing. This tutorial is part 1 of our HomeLab series, teaching you how to maintain your own "enterprise" style network at home. The advantage of a homelab allows for real-world experience you can put on your resume and speak to in an interview when asked questions related to your technical expertise. 

## How to use this guide:
TechTouch Labs handles teaching very differently compared to other industry standards. This is because we believe they truly lack in teaching you. There will be very lengthy commands, and for the sake of time, go ahead and copy and paste those commands. HOWEVER, please read what the command does or you will never learn. Linux is notorious for using abbreviations, and without reading what it does, you will never understand what you are actually configuring.
## Topology
A network topology is the physical and logical arrangement of nodes and connections in a network:
<a href="/images/EP2_firewall/firewall_topology.png" class="image-expand">
    <img src="/images/EP2_firewall/firewall_topology.png" alt="Description of your image">
</a>

## Required Items:
The firewall being used in this guide: [firewall](https://tinyurl.com/ynvvvdrw) 
Alternative: [Beelink U59 dual ethernet](https://amzn.to/3PloqUa)
**or you can use any mini pc of your chosing and equip the USB 3.0 ports with a** [USB to ethernet adapter](https://amzn.to/4a8eXrT)

- [x] Firewall Appliance (this could be a mini PC with two ethernet ports)
- [x] USB thumb Drive

## Walkthrough/Commands:
The start of the tutorial:

Step 1:

Etcher allows us to create a bootable flash drive, this is how we will get OPNsense on to the firewall appliance. Download Etcher [here](https://etcher.balena.io/). 

## Step 1 Download OPNsense
Download either PFsense or OPNsense (the process will be the same but for the purpose of this tutorial we will be using OPNsense) and grab your file. For Opnsense leave all the download selections as shown in the image. For PFsense you will select Architecture: AMD64 (64-bit) Installer: DVD Image (ISO) Installer. 

1 - Go to either [Opnsense.org/Downloads](https://opnsense.org/download/) or [Pfsense.org/Downloads](https://www.pfsense.org/download/)
<a href="/images/EP2_firewall/opnsense_1.png" class="image-expand">
    <img src="/images/EP2_firewall/opnsense_1.png" alt="Description of your image">
</a>

2 - Next go to the folder where OPNsense or PFsense was downloaded <kbd>right click</kbd> details tab, and then copy the file name.
<a href="/images/EP2_firewall/opnsense_2.png" class="image-expand">
    <img src="/images/EP2_firewall/opnsense_2.png" alt="Description of your image">
</a>

3 - You will then use the following command to verify the SHA256 hash as seen in step 1 right below the download button. **!Remember, that SHA256 value will change with every update so verify it against what is currently showing on their website!**
```
certUtil -hashfile (the file path of your ISO file) SHA256
```
EXMAPLE: 
```
certUtil -hashfile C:\Users\TechTouch\Downloads\OPNsense-24.1-vga-amd64.img.bz2 SHA256
```
<a href="/images/EP2_firewall/opnsense_3.png" class="image-expand">
    <img src="/images/EP2_firewall/opnsense_3.png" alt="Description of your image">
</a>

Now move on to Step 2: Downloading Etcher and create a bootable USB flash drive. **You can use the navigation bar on the left to quickly get back up to the tab selection.**

## Step 2 Download Etcher (bootable USB application)

1 - Etcher allows us to create a bootable flash drive, this is how we will get OPNsense on to the firewall appliance. Download Etcher [here](https://etcher.balena.io/). 
<a href="/images/EP2_firewall/etcher_1.png" class="image-expand">
    <img src="/images/EP2_firewall/etcher_1.png" alt="Description of your image">
</a>
2 - Pick the correct download for your operating system.
<a href="/images/EP2_firewall/etcher_2.png" class="image-expand">
    <img src="/images/EP2_firewall/etcher_2.png" alt="Description of your image">
</a>
3 - Select *flash from file* 
<a href="/images/EP2_firewall/etcher_3.png" class="image-expand">
    <img src="/images/EP2_firewall/etcher_3.png" alt="Description of your image">
</a>
4 - Select your OPNsense or PFsense download. 
<a href="/images/EP2_firewall/etcher_4.png" class="image-expand">
    <img src="/images/EP2_firewall/etcher_4.png" alt="Description of your image">
</a>
5 - Now select the USB thumb drive. **!WARNING THIS WILL DELETE EVERYTHING ON THE THUMB DRIVE!**
<a href="/images/EP2_firewall/etcher_5.png" class="image-expand">
    <img src="/images/EP2_firewall/etcher_5.png" alt="Description of your image">
</a>
6 - You can now remove the thumb drive from your device and plug it into your firewall appliance **!MAKE SURE YOUR APPLIANCE IS CURRENTLY TURNED OFF!**
<a href="/images/EP2_firewall/etcher_6.png" class="image-expand">
    <img src="/images/EP2_firewall/etcher_6.png" alt="Description of your image">
</a>

## Step 3 (boot to OPNsense on your firewall client)
After you have plugged the USB drive into your firewall appliance turn it on while tapping the <kbd>Del</kbd> (delete) key until the BIOS comes up. 

1 - use your **arrow keys** and get to the BIOs tab, select your USB device, then move over to the exit tab, **save changes and exit.** 
<a href="/images/EP2_firewall/bios.png" class="image-expand">
    <img src="/images/EP2_firewall/bios.png" alt="Description of your image">
</a>

2 - After your device is booted you should see this screen with the IP address of your device. **!YOU WILL NEED TO BE DIRECTLY CONNECTED TO THIS DEVICE OVER ETHERNET AND THEN GO TO THAT IP ADDRESS!**

Take note: the below image shows (vtnet0) this is the port that is being used for the LAN interface, because your appliance has multiple ethernet switchports you may need to plug into each until you can access the website at that IP address.
<a href="/images/EP2_firewall/opnsense_start.png" class="image-expand">
    <img src="/images/EP2_firewall/opnsense_start.png" alt="Description of your image">
</a>

3 - After you have connected to that IP you will seen this screen. Simply follow the wizard. 
<a href="/images/EP2_firewall/opn_1.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_1.png" alt="Description of your image">
</a>
4 - We are going to use Cloudflare DNS servers, they are usually much faster than ones provided by your ISP. 
```
1.1.1.1
```
```
1.0.0.1
```
<a href="/images/EP2_firewall/opn_2.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_2.png" alt="Description of your image">
</a>
5 - Pick your respective time zone. 
<a href="/images/EP2_firewall/opn_3.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_3.png" alt="Description of your image">
</a>
6 - If your internet service provider (ISP) uses MAC address security and want to avoid calling their support to give them your new MAC address you can simply copy your older routers MAC into the MAD address field. If you get a static IP address from your ISP you will also input that here.
<a href="/images/EP2_firewall/opn_4.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_4.png" alt="Description of your image">
</a>
7 - Here you can pick whatever private IP range that you like, default is perfectly fine too. If you want a list of private IP ranges you can find that [here](https://en.wikipedia.org/wiki/Private_network). 
<a href="/images/EP2_firewall/opn_5.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_5.png" alt="Description of your image">
</a>
8 - Set a strong password here. 
<a href="/images/EP2_firewall/opn_6.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_6.png" alt="Description of your image">
</a>
9 - You are all done, go ahead and reload!
<a href="/images/EP2_firewall/opn_7.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_7.png" alt="Description of your image">
</a>
10 - <kbd>left click</kbd> and go to your dashboard.
<a href="/images/EP2_firewall/opn_8.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_8.png" alt="Description of your image">
</a>
11 - You are all set, Opnsense/Pfsense is now setup and ready for use! Future videos will dive more into OPNsense configuations based on setting up our homelab but you can find their documentation [here](https://docs.opnsense.org/index.html)
<a href="/images/EP2_firewall/opn_9.png" class="image-expand">
    <img src="/images/EP2_firewall/opn_9.png" alt="Description of your image">
</a>














































