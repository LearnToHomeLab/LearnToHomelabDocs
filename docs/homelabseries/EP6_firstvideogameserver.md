# Setting up your first Video Game Server (Minecraft Example)! 
Hey guys, in this episode we are going to cover setting up any SteamCMD based video game server using LinuxGSM and PlayitGG. In this example we are going to cover this topic with a Minecraft server. I personally love this project, and I got into
computers more than 13 years ago now because of video game server hosting, it is what sparked the passion of computers for me!

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
    <p>Do not forget, on the right side of the screen are subject topics to easily move throughout this walkthrough!</p>
</div>

</body>
</html>

## Grabbing everything you need to get started
First you need to access [PlayIt.GG](https://playit.gg/).
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.1.png" alt="Description of your image">
</a>
    
You can find [LinuxGSM](https://linuxgsm.com).
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.2.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.2.png" alt="Description of your image">
</a>

Next, if you do not remember your VMs IP address you will need to login into your Proxmox Machine, login to the VM, and then grab it.
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.3.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.3.png" alt="Description of your image">
</a>

IP on VM:
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.4.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.4.png" alt="Description of your image">
</a>

## Getting your Ubuntu Server up to date (step by step)
1. SSH into your server TWICE to perform the following commands (later there will be a case where we need two SSH sessions open).
```
ssh username@server_ip_address
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.5.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.5.png" alt="Description of your image">
</a>

2. Get ubuntu to reach out and find new dependencies to install.
```
sudo apt upgrade
```
3. AND Update those out of date dependencies.
```
sudo apt update
``` 
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.6.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.6.png" alt="Description of your image">
</a>


## Installing LinuxGSM Minecraft Server
Now we can start installing our video game server, in this example it is a Minecraft Bedrock Edition. The commands can be found [here](https://linuxgsm.com/servers/mcbserver/)
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.7.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.7.png" alt="Description of your image">
</a>

Now we need to create the user. 
*You will notice I just clicked enter and bypassed all the user info.*
```
add user mcbserver
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.8.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.8.png" alt="Description of your image">
</a>

Currently out of our TWO SSH windows that are open, you are going to see that I login to user MCBserver in the LEFT window.
```
su - mcbserver
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.9.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.9.png" alt="Description of your image">
</a>

Now we are going to request the LinuxGSM client contents IN THE LEFT SSH TAB.
```
curl -Lo linuxgsm.sh https://linuxgsm.sh && chmod +x linuxgsm.sh && bash linuxgsm.sh mcbserver
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.10.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.10.png" alt="Description of your image">
</a>

Now we can see we are missing some files because our VM was unable to locate them and we are missing the Unzip utility tool, we need to install those now. 
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.11.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.11.png" alt="Description of your image">
</a>
IN THE RIGHT SSH TAB we are going to type the following:

The following commands will allow our VM to find the missing files, download them, and unzip them
```
sudo add-apt-repository universe
sudo add-apt-repository multiverse
sudo dpkg --add-architecture i386
sudo apt update
```
AND
```
sudo apt-get install unzip
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.12.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.12.png" alt="Description of your image">
</a>

Now we can request those missing files found two pictures ago
```
sudo apt update; sudo apt install bsdmainutils bzip2 jq lib32gcc-s1 lib32stdc++6 libsdl2-2.0-0:i386 netcat bigz unzip
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.13.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.13.png" alt="Description of your image">
</a>

Now in our LEFT SSH tab we can continue where we left off, now that we have all the correct packages:
```
./mcbserver install
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.14.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.14.png" alt="Description of your image">
</a>

We can see after installing our (mcb =Minecraft bedrock) server, we get all green files now, so we know it worked.
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.15.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.3.15.png" alt="Description of your image">
</a>

The most important area of LinuxGSM is knowing where to find your configuration files, they will always be stated under the (./(game_server_type) details) after typing the following command
and the status of your server (if it is running or stopped).
```
./mcbserver details
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.1.png" alt="Description of your image">
</a>
To edit this configuration file, we are going to use nano.
```
nano /home/mcbserver/serverfiles/server.properties
```
Here is what ours looks like, we are going to use our arrow keys to go down to *server-port* and change it to [4356]

After that to exit, you will type <kbd>Ctrl</kbd> + <kbd>X</kbd> then type <kbd>Y</kbd> at the next prompt to confirm changes and lastly to save it you will click <kbd>Enter</kbd>

<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.2.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.2.png" alt="Description of your image">
</a>

Then we can confirm our changes by typing the following command and confirming the change
```
./mcbserver details
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.3.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.3.png" alt="Description of your image">
</a>

Now we are done, and we can start our Minecraft server with the following command, you will now see it started properly when the status shows a green started indicator
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.5.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.4.5.png" alt="Description of your image">
</a>

## Installing PlayitGG
Now we have gotten LinuxGSM out of the way, we are going to install PlayitGG in the RIGHT SSH window and leave the left window open.

On PlayitGG's site we are going to copy the following command into our RIGHT SSH window. 
```
curl -SsL https://playit-cloud.github.io/ppa/key.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/playit.gpg >/dev/null
echo "deb [signed-by=/etc/apt/trusted.gpg.d/playit.gpg] https://playit-cloud.github.io/ppa/data ./" | sudo tee /etc/apt/sources.list.d/playit-cloud.list
sudo apt update
sudo apt install playit
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.5.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.5.1.png" alt="Description of your image">
</a>

After that is done, to start the PlayitGG service, we need to simply type the following command
```
playit
```
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.5.3.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.5.3.png" alt="Description of your image">
</a>

You will then be prompted with the following screen; you will need to do <kbd>Ctrl</kbd> + <kbd>left click</kbd> to follow the link.
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.1.png" alt="Description of your image">
</a>

Now you are going to wait 1-5 minutes for the PlayitGG servers to find your tunnel calling out to it.
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.2.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.2.png" alt="Description of your image">
</a>

Going to the next page you will be prompted with a screen like such, we are going to select the tunnel type for bedrock edition
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.3.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.3.png" alt="Description of your image">
</a>

Then on that same Tunnels page we need to change our port to [4356] just like we did in the LinuxGSM config file.
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.4.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.8.4.png" alt="Description of your image">
</a>

## How do you restart your server if your Proxmox Machine restarts or any of your stuff needs an update? 
So, if your Proxmox machine needs an update, your VM needs an update, etc. You will need to restart your services. 

PlayitGG is super simple, just type the following command and it will start right up.
```
playit
```

Now to start your Minecraft server backup, update it, or make changes you will need to again open another SSH tab because we do not want to stop the PlayitGG service and do the following.

1. Login to your VM:
2. Change users 
```
su mcbserver
```
3. Change to your users directory 
```
cd ~
```
Then you will be able to perform the LinuxGSM commands like ./mcbserver details, start, stop, update, etc. 
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.9.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.9.1.png" alt="Description of your image">
</a>

## Logging into your Video Game server with friends

Now the information to connect to your server will be found on the Tunnels page. Remember though, if you are a local user (within the home network your Video game server is hosted) you can use that VMs IP address and the port number [4356], anyone outside
your network will need to use the information like shown below found on the PlayitGG tunnels page.
<a href="/images/EP6_gameserver/Still 2024-12-19 121524_1.8.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 121524_1.8.1.png" alt="Description of your image">
</a>

Typed into Minecraft it will look like this
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.10.1.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.10.1.png" alt="Description of your image">
</a>

Would you look at that, you are in! Potentially your first video game server setup EVER, congrats! 
<a href="/images/EP6_gameserver/Still 2024-12-19 153947_1.10.2.png" class="image-expand">
    <img src="/images/EP6_gameserver/Still 2024-12-19 153947_1.10.2.png" alt="Description of your image">
</a>
