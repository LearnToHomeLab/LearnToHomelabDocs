# Welcome
LTH is glad to see you here! This free course focuses on beginners and newcomers to IT, Cyber Security, and Network Engineering prospects (and really anyone interested in IT or self-hosting services)!

[Our YouTube videos accompany this series; click here to find that series on YouTube!](https://youtube.com/playlist?list=PLAvgoEDVC5qFPNbsRBT-naqnsZwxIcqQ6&si=Pn6K2clYE_zLVs5C)
<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/K9gXMoPrPA0?si=i-yFKPqx8_fom9Xv" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Introduction
What does this course encompass and it is right for me is a question most of you are asking. You may even be asking yourself if you have enough knowledge to be successful in this course, and the answer is yes you do. 

The course "HomeLab" you are about to embark on was created so that even the most novice individual could follow. Please take the time to read through this page and every lesson page; there are lots of great details!

## What is a Homelab? 
An IT homelab is a personal setup where enthusiasts and professionals experiment with and learn about computer systems, networking, cybersecurity, and server management at home. Using hardware like old PCs, servers, or mini computers, homelabbers create virtual environments to explore IT concepts, test software, and develop skills in areas like virtualization, network security, and system administration. Homelabs mimic business IT environments, enabling hands-on practice with technologies like firewalls, cloud services, and automation tools, helping users advance their careers, troubleshoot, and stay current with industry trends.

## First things first
This course is about getting hands-on skills to pass an interview that will be an entry-level job for many of you. Although there are many high-level or "very knowledgeable" areas of focus throughout this course, experience is king. You also must understand that everyone puts in their "sweat equity" before they reach the top. If your family needs to support you or your spouse must start working while you transition or take a pay cut to get an entry-level role, that is sweat equity. The technical field is a very fast return on investment AS LONG AS you apply yourself. You should be qualified and take on responsibility for the position you want to be in. Do not get in that ugly mindset that you are worth some set amount of money, prove it. 

Lastly, before we get started, realize that this industry is COMPETITIVE, if you want to study, get a job, and sit back, this industry is not for you. I have been doing this for about ten years, and to this day, I spend around 10-20 hours a week bettering myself. 

## What you will learn

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
    /* You can add more styles as needed */
}
</style>
</head>
<body>

<div class="warning-box">
    <p>Some videos are not required to setup a successful home lab, use case will determine that, please read on.</p>
</div>

</body>
</html>

Below, you will find a breakdown of the network we are going to set up and some of the services. The image you are looking at in IT is called a topology. Topologies come in two forms: logical and physical. Any time we use the term logical, we refer to digital or how the computers will communicate or host services. Physical topologies show you how the devices are interconnected. 

In this case, our topology does both; we can see the arrows from the public internet down and imagine each arrow as being an ethernet cable connecting our homelab devices together. We can see for this course, we will use three servers, but realistically, if you do not want to or cannot afford to, you can simply use one server and host all your stuff on that. The other two servers will be used to teach a more professional and closer to an enterprise setup so to speak. Please take a moment to look at our topology for a high-level overview of what will be covered here. 

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
    <p>Throughout this course, during each episode, you will see the topology map with a red box. The content contained within the red box is what the lesson will be covering and what part of the home lab setup we are on.</p>
</div>

</body>
</html>
<a href="/images/start guide/course flow.png" class="image-expand">
    <img src="/images/start guide/course flow.png" alt="Description of your image">
</a>
Here is what that topology looks like in physical form without the stage 2 servers.
<a href="/images/EP2_switch/switch.png" class="image-expand">
    <img src="/images/EP2_switch/switch.png" alt="Description of your image">
</a>

Okay before we get down to the course content it is important to understand that there are certain things you are not **REQUIRED** to do. What do we mean by this? HomeLabs are about learning and catering towards what you want, however some people may expose things to the internet or use a virtual private network (VPN) that will allow them access to their internal resources externally. **In this course we will cover some of that but will NOT be making services public through the firewall. Best practice will be to use a VPN tunnel and that is what is covered in this course. Because of this, the Firewall video/device is not required.**

I know budget is always of concern for anyone, so again pay attention to what is required and what is not required below. By not having to setup a firewall, you can invest that money into a small form factor PC and install Proxmox on there. 

## Not required
1. Opnsense/PFsense Firewall (Episode - 3)
2. Stage 2, as indicated in the topology breakdown. A NAS backup and fail-over machine are solely for people learning more advanced technologies and capabilities. They are not required for the main purpose of this course.

## Order of Content
0. [Getting started (Intro video)](https://www.youtube.com/watch?v=K9gXMoPrPA0&list=PLAvgoEDVC5qFPNbsRBT-naqnsZwxIcqQ6&index=1) 
1. [Note taking](/homelabseries/EP1_notekeeping/)
2. [Installing your switch](/homelabseries/EP2_switch/)
3. [Firewall](/homelabseries/EP3_firewall/)
4. [Proxmox](/homelabseries/EP4_proxmox/)
5. [Setting up our first VM (Ubuntu)](/homelabseries/EP5_firstvmubuntu/)
6. [First Video Game Server (minecraft)](/homelabseries/EP6_firstvideogameserver)
7. [Setup Pi-Hole with Proxmox](/homelabseries/EP7_setuppihole)
8. [Setup NextCloud with Proxmox](/homelabseries/EP8_nextcloud)
9. [Setup Tailscale with Proxmox](/homelabseries/EP9_tailscale)
10. [Zabbix Server With Proxmox](/homelabseries/EP10_zabbixserver)
11. [Zabbix Agent Install on a VM](/homelabseries/EP11_zabbixagent)