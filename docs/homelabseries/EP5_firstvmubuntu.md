# Installing Your First VM (Ubuntu) on Proxmox
This episode will go over how to setup your first virtual machine (VM) inside Proxmox.

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Informative Section</title>
<style>
.informative-section {
    background-color: #283593; /* Dark blue background color */
    color: white; /* Text color to contrast with dark background */
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
    color: #283593; /* Dark blue color for the exclamation mark */
}
</style>
</head>
<body>

<div class="informative-section">
    <div class="circle-emoji">!</div>
    <p>This is a beginner-friendly course, so we understand many of you may find this lesson to be a review, but these fundamental concepts are very important for beginners when using Proxmox.</p>
</div>

</body>
</html>
--------------------
<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/RJdRgJFiupo?si=PcHcDpMwlQiwQjQv" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Installing your VM 
  
Step 1. head over to [https://ubuntu.com/download/server](https://ubuntu.com/download/server) and download Ubuntu Server 22.x (x= whatever the latest version is). 
<a href="/images/EP4_firstvmubuntu/ubuntu_server_website_step_1.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/ubuntu_server_website_step_1.png" alt="Description of your image">
</a>
Step 2. After you have downloaded it, navigate to the IP address of your server or mini PC where you installed Proxmox on it. You should be presented with a screen like this:
<a href="/images/EP4_firstvmubuntu/2024-03-30_11_46_38-pve_-_proxmox_virtual_environment.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/2024-03-30_11_46_38-pve_-_proxmox_virtual_environment.png" alt="Description of your image">
</a>
Step 3. Select your server (our case pve), then local (pve), and ISO images. Upload your Ubuntu Server .iso image there. 
<a href="/images/EP4_firstvmubuntu/step_3_iso_image_proxmox.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/step_3_iso_image_proxmox.png" alt="Description of your image">
</a>
Step 4. Select *iso images*, *upload*, *select file*, and *upload*. After exit out of the pop up. 
<a href="/images/EP4_firstvmubuntu/step_4_proxmox.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/step_4_proxmox.png" alt="Description of your image">
</a>
Step 5. We can now select *create a vm*, and follow the install process.
<a href="/images/EP4_firstvmubuntu/2024-03-30_12-11-22.gif" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/2024-03-30_12-11-22.gif" alt="Description of your image">
</a>

## VM settings for Proxmox
Settings:

---

 -General Tab.
  Node: (select whatever Proxmox server or mini-PC you want to install to (our case, it is still pve).
  VM Id: does not matter (you can leave default).
  Name: (Describe what you install on the Ubuntu server (Wiki.Js, ARK server, Minecraft, Zabbix, etc).

---

 -OS Tab:
  ISO image: select the ubuntu file we just uploaded.

---

 -System Tab:
  All settings can stay default here.

---

 -Disk Tab:
    Disk Size (GiB): (set based on the requirement of whatever software we are installing), i.e., Wiki.Js recommends at least 1gig of storage, and Ubuntu Server requires 20gigs, so we should have no less than 22gigs. (I would recommend going up at least 5 gigs for small installs and at least double for other applications where you know you will be uploading lots of content, i.e., mods, pictures, user accounts, etc. 

---

 -CPU Tab:
  Again, this will be based on the requirements of what you are installing. Wiki.js requires 2 cores and Ubuntu Server so that we will select 2 cores. 

---

 -Memory Tab: 
  Again, based on system requirements. Wiki.js wants 2 gigs of RAM. Ubuntu Server recommends 4 gigs of RAM, but you can get away with 1-2, depending on your installation. In our case, for Wiki.js, we are going to keep 2gigs.

---

 -Network Tab:
  This can stay default.

---

 -Confirm Tab: 
  Please check over all your settings and click *finish*. 

---
## Installing Ubuntu Server on your Proxmox VM

1. Now we can boot the new virtual machine by selecting the console tab and then start now.
<a href="/images/EP4_firstvmubuntu/1_console_start.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/1_console_start.png" alt="Description of your image">
</a>
2. Select the top option, install Ubuntu Server. 
<a href="/images/EP4_firstvmubuntu/2_install_ubuntu_server.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/2_install_ubuntu_server.png" alt="Description of your image">
</a>
3. Now Select your language. 
<a href="/images/EP4_firstvmubuntu/3_select_language.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/3_select_language.png" alt="Description of your image">
</a>
4. Pick your Keyboard layout/variant.
<a href="/images/EP4_firstvmubuntu/4_pick_language_layout.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/4_pick_language_layout.png" alt="Description of your image">
</a>
5. We are selecting the Ubuntu Server 
<a href="/images/EP4_firstvmubuntu/5_select_ubuntu_server.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/5_select_ubuntu_server.png" alt="Description of your image">
</a>
6. We can leave this default because most of you will use DHCP. 
<a href="/images/EP4_firstvmubuntu/6_configure_interface.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/6_configure_interface.png" alt="Description of your image">
</a>
7. We can skip this because we are not using a proxy. 
<a href="/images/EP4_firstvmubuntu/7_skip_click_done.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/7_skip_click_done.png" alt="Description of your image">
</a>
8. Our Ubuntu server is testing the mirror (a way to grab updates), after the mirror connection is confirmed you can select done. 
<a href="/images/EP4_firstvmubuntu/8_checking_mirror.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/8_checking_mirror.png" alt="Description of your image">
</a>
9. In the case of Proxmox, we are creating a virtual machine, and during the setup of our Proxmox VM, we set the disk drive size, meaning our VM can only see the virtualized partitioned disk drive (this prevents you from overwriting any other VM disk partitions on your server). You are good to go ahead and use the WHOLE disk drive in this case.
<a href="/images/EP4_firstvmubuntu/9_use_entire_disk.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/9_use_entire_disk.png" alt="Description of your image">
</a>
10. This is just giving you a breakdown of that partitioned disk and how much space is going to each resource.
<a href="/images/EP4_firstvmubuntu/10_file_overview.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/10_file_overview.png" alt="Description of your image">
</a>
11. Your name can be set to the same as the username. The username and password is what will be used when we SSH into this (VM SO DO NOT FORGET THEM!). Setting the server name is very important, this is how your VM will appear to all other devices on your network, make is something memorable that explains what this VM is. 
<a href="/images/EP4_firstvmubuntu/11_set_your_username_nad_password.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/11_set_your_username_nad_password.png" alt="Description of your image">
</a>
12. You can skip this and select *done*. 
<a href="/images/EP4_firstvmubuntu/12_skip_for_now_click_continue_.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/12_skip_for_now_click_continue_.png" alt="Description of your image">
</a>

> 13. This part is so important, make sure you click <kbd>enter</kbd> on your keyboard and there is a 'X' in the openssh box. This allows us to SSH into your server. 
{.is-warning}
<a href="/images/EP4_firstvmubuntu/13_install_ssh.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/13_install_ssh.png" alt="Description of your image">
</a> 
14. You can skip all this content. 
<a href="/images/EP4_firstvmubuntu/14_skip_this.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/14_skip_this.png" alt="Description of your image">
</a> 
15. Wait for the VM to finish installing.
<a href="/images/EP4_firstvmubuntu/15_installing_system.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/15_installing_system.png" alt="Description of your image">
</a> 
16. Reboot now after that is complete. 
<a href="/images/EP4_firstvmubuntu/16_reboot_system.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/15_installing_system.png" alt="Description of your image">
</a> 
17. Now you can login to your VM with the credentials you made earlier, this will allow you to see the IP address of your VM so we can use Putty and SSH to control it.
<a href="/images/EP4_firstvmubuntu/17_log_in.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/17_log_in.png" alt="Description of your image">
</a> 
  
1. If you are on Windows 11 or newer we reccomend using Windows command line (CLI) to SSH into your machines, this allows you to copy and paste. 
2. You can also login with SSH on Linux. 
3. If you are on Windows 10 or prior we reccomend using [Putty](https://www.putty.org/)

The command to use SSH in the CLI is:
```
ssh username@server_ip_address
```

Example:
```
ssh learn@192.168.1.1
```

<a href="/images/EP4_firstvmubuntu/windows11clissh.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/windows11clissh.png" alt="Description of your image">
</a> 
  
Using SSH is important for future videos because it allows you to copy and paste content into your CLI and important data from your local machine to your VM.
  
