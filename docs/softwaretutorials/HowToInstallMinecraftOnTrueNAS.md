# MineCraft on TrueNas

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/w_Qbzbc0bWA?si=pwEfwIQCZd5ZEPDQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


Hey all, in today’s video, I am going to cover setting up ANY version of Minecraft on TrueNas (Minecraft Vanilla, Spigot, Bucket, Paper, Folia, Fabric, Forge, NeoForge, CurseForge, Modrinth, Feed the Beast, Pufferfish, etc., etc.)

## Installing Minecraft

1.  Log in to your TrueNas machine. If you have not set up TrueNas before, check out our video [here](https://www.youtube.com/watch?v=xHseIdxtugk&t=1s&ab_channel=LearnToHomeLab)
2.  Click the _apps_ page on the left!
<a href="/images/HowToInstallMinecraftOnTrueNAS/2 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/2 image.png" alt="Description of your image">
</a>
3.  Click _Discover Apps_ on the top right (the blue button).
<a href="/images/HowToInstallMinecraftOnTrueNAS/3 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/3 image.png" alt="Description of your image">
</a>
4.  In the search bar, type _Minecraft_!
<a href="/images/HowToInstallMinecraftOnTrueNAS/4 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/4 image.png" alt="Description of your image">
</a>
5.  Select Minecraft Server _Java_ or _Bedrock_ (Bedrock is the cross-platform one, where Java is PC only but many find it to be a better, more original experience to original Minecraft).
6.  Select _install_!
<a href="/images/HowToInstallMinecraftOnTrueNAS/6 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/6 image.png" alt="Description of your image">
</a>
    
## Application Settings
    
1.  Name your Minecraft server
2.  Select your time zone
3.  Check the EULA agreement box
4.  Select your Image
5.  Select your Type
6.  Select your Game Mode
7.  Name your Server!

<a href="/images/HowToInstallMinecraftOnTrueNAS/7 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/7 image.png" alt="Description of your image">
</a>

------------------
<ol start="8">
8. Add a Recon Password!
</ol>

<a href="/images/HowToInstallMinecraftOnTrueNAS/8 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/8 image.png" alt="Description of your image">
</a>

<ol start="9">
9.  Scroll down to _Network Configuration_
</ol>

<ol start="10">
10. Select _Host IP_ under the <em>Host IP</em> section.!
</ol>
<a href="/images/HowToInstallMinecraftOnTrueNAS/10 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/10 image.png" alt="Description of your image">
</a>

<ol start="11">
11. Scroll down to <em>Resource Configuration</em>
</ol>

<ol start="12">
12. Set the CPU and RAM count for your machine
</ol>

<ol start="13">
13. Select Install!
</ol>

<a href="/images/HowToInstallMinecraftOnTrueNAS/13 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/13 image.png" alt="Description of your image">
</a>

## Launch Minecraft

1.  Launch Minecraft
2.  Go to _Multiplayer_
3.  Select _direct connection_
4.  Type in your TrueNAS Machine IP and the port _25535 (For Java Vanilla)_

There you have it, a Minecraft server setup in just a few minutes!

## Editing Minecraft Server Files

1.  On the _Apps_ page you will select the CLI under the app details!
<a href="/images/HowToInstallMinecraftOnTrueNAS/editing 1 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/editing 1 image.png" alt="Description of your image">
</a>

2.  Within the CLI, you will type
    
    ```
    ls
    ```
    
This gives you a list of files to edit!

<a href="/images/HowToInstallMinecraftOnTrueNAS/editing 2 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/editing 2 image.png" alt="Description of your image">
</a>

<ol start="3">
3.  We will use Nano to edit the <em>server.properties</em> location.
</ol>
```
nano server.properties
```
    

Within there, you can find important information, such as port numbers, depending on the version you installed, and other server information you may want to change.

<a href="/images/HowToInstallMinecraftOnTrueNAS/editing 3 image.png" class="image-expand">
    <img src="/images/HowToInstallMinecraftOnTrueNAS/editing 3 image.png" alt="Description of your image">
</a>

That is it, I hope you guys enjoyed this tutorial, and stay tuned for more projects coming to the channel soon!

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)