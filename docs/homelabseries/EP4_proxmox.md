# Topic Proxmox Installation Guide

## Introduction:

In this episode, we will cover the installation of Proxmox on your server, mini-PC, SBC, etc. (whatever you have chosen to use as your device to host your services). 

## Topology
<a href="/images/EP3_proxmox/topology_proxmox.png" class="image-expand">
    <img src="/images/EP3_proxmox/topology_proxmox.png" alt="Description of your image">
</a>

## Required Items:
The Proxmox machine being used in this guide: [N95 mini pc](https://amzn.to/49Ul82n) (I highly recommend you go with something that has 16gb of RAM or more) Servers are RAM heavy, the more you have the better!.
Recommended: [Beelink Mini PC SER5](https://amzn.to/3vdgbTe)
Alternative: [Beelink U59 dual ethernet](https://amzn.to/3PloqUa)

- [x] Proxmox Appliance (some type of PC that you are okay with running 24/7)

- [x] USB thumb Drive
## Downloading Proxmox (bootable USB):
The start of the tutorial:
Go to Proxmox.com and download the latest ISO installer [here](https://www.proxmox.com/en/downloads). 
Note: copy the SHA256SUM to a .txt file to compare against in a later step. 
<a href="/images/EP3_proxmox/p1.png" class="image-expand">
    <img src="/images/EP3_proxmox/p1.png" alt="Description of your image">
</a>
Next go to where the file is downloaded <kbd>right click</kbd>, **properties**.
<a href="/images/EP3_proxmox/p2.png" class="image-expand">
    <img src="/images/EP3_proxmox/p2.png" alt="Description of your image">
</a>
Copy and paste the location of the file into the same .txt document. 
<a href="/images/EP3_proxmox/p3.png" class="image-expand">
    <img src="/images/EP3_proxmox/p3.png" alt="Description of your image">
</a>
Use the following command with your respective version of Proxmox to validate the integrity of the file against their good known hash.
EXAMPLE:
```
certUtil -hashfile C:\Users\learn\Downloads\proxmox-ve_8.1-2.iso SHA256
```
Use:
```
certUtil -hashfile (your file path here) SHA256
```
<a href="/images/EP3_proxmox/p4.png" class="image-expand">
    <img src="/images/EP3_proxmox/p4.png" alt="Description of your image">
</a>
Now open etcher (was previously downloaded in EP 1 how to install OPNsense or PFsense firewall). You can also download etcher from [here](https://etcher.balena.io/#download-etcher).
<a href="/images/EP3_proxmox/p5.png" class="image-expand">
    <img src="/images/EP3_proxmox/p5.png" alt="Description of your image">
</a>
After you clicked **flash from file** select your Proxmox .iso, then select open. 
<a href="/images/EP3_proxmox/p6.png" class="image-expand">
    <img src="/images/EP3_proxmox/p6.png" alt="Description of your image">
</a>
Now click **select target** and then choose the USB drive you want to write to. **!REMEMBER THIS WILL DELETE EVERYTHING ON THE USB DRIVE!**
<a href="/images/EP3_proxmox/p7.png" class="image-expand">
    <img src="/images/EP3_proxmox/p7.png" alt="Description of your image">
</a>
Now click flash and wait for Etcher to finish creating the bootable USB device. 
<a href="/images/EP3_proxmox/p8.png" class="image-expand">
    <img src="/images/EP3_proxmox/p8.png" alt="Description of your image">
</a>

## Installing Proxmox on Server/Mini PC

After that has completed, plug the USB device into your mini pc/server/SBC, whatever you are going to use to as your virtualization host **WHILE IT IS TURNED OFF**. Then turn the device on while continuously clicking your delete key until the BIOS appears. 
<a href="/images/EP3_proxmox/p9.png" class="image-expand">
    <img src="/images/EP3_proxmox/p9.png" alt="Description of your image">
</a>
Use your arrow keys and move over to the boot tab, under boot option #1 select the USB device with Proxmox on it.
<a href="/images/EP3_proxmox/p10.png" class="image-expand">
    <img src="/images/EP3_proxmox/p10.png" alt="Description of your image">
</a>
Use the arrow keys again and go to the **save and exit** tab and select **save changes and exit**. 
<a href="/images/EP3_proxmox/p11.png" class="image-expand">
    <img src="/images/EP3_proxmox/p11.png" alt="Description of your image">
</a>
Now allow for your device to boot, you will see the Proxmox graphical user interface (GUI) appear. Follow the install instructions, it is very basic, time zone, password, where you want to install to, etc. **!STOP ON THE LAST PAGE WHERE IT SAYS ISNTALLATION SUCCESSFUL!** read the next step. 
<a href="/images/EP3_proxmox/p12.png" class="image-expand">
    <img src="/images/EP3_proxmox/p12.png" alt="Description of your image">
</a>
When you get to the last step as seen below, when you select **reboot** you need to remove the USB device right after or it will take you back to the installation wizard.
<a href="/images/EP3_proxmox/p14.png" class="image-expand">
    <img src="/images/EP3_proxmox/p14.png" alt="Description of your image">
</a>
Now we have successfully installed Proxmox, go to your web browser and go to the IP address listed from your Proxmox device. In our case the IP is 192.168.1.50.216:8006.
<a href="/images/EP3_proxmox/p15.png" class="image-expand">
    <img src="/images/EP3_proxmox/p15.png" alt="Description of your image">
</a>
You will use **root** as the username, and then you will use whatever password you created during the setup wizard.
<a href="/images/EP3_proxmox/p16.png" class="image-expand">
    <img src="/images/EP3_proxmox/p16.png" alt="Description of your image">
</a>
You have now succesfully installed Proxmox for server and container virtualization! Please move to EP 5 where we will cover setting up a your first virtual machine.
<a href="/images/EP3_proxmox/p17.png" class="image-expand">
    <img src="/images/EP3_proxmox/p17.png" alt="Description of your image">
</a>
