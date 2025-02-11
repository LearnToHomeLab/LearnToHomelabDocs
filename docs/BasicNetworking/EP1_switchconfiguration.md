# How To Configure Cisco Switches (The Basics)

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/xwxfK4AuhaA?si=OEML82LYrxZ2ns8P" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


## Resources

Here is where you will go to download Packet Tracer: [download](https://www.netacad.com/resources/lab-downloads?courseLang=en-US)

**Here is the GitHub repo with all the Packet Tracer files we will use for the course** [Pkt files](https://github.com/LearnToHomeLab/BasicNetworkingLabs)

You will download them by selecting the episode:

<a href="/BasicNetworkingimages/EP1_BasicNetworking/This Repo holds content for Basic Cisco Netw.png" class="image-expand">
    <img src="/BasicNetworkingimages/EP1_BasicNetworking/This Repo holds content for Basic Cisco Netw.png" alt="Description of your image">
</a>

Then by clicking raw download, after that double click it in your downloads folder and it will open it automatically in Packet tracer:

<a href="/BasicNetworkingimages/EP1_BasicNetworking/LearnToHomeLab_Basi.png" class="image-expand">
    <img src="/BasicNetworkingimages/EP1_BasicNetworking/LearnToHomeLab_Basi.png" alt="Description of your image">
</a>

## Getting Started With Packet Tracer

1. To add multiple Items you hold down <kbd>ctrl</kbd> 
2. Click Options / Preferences / (Always show port Labels in Logical Workspace) AND (Align logical workspace objects) to keep things aligned.

## Network Overview 

Here is a our Topology 

<a href="/BasicNetworkingimages/EP1_BasicNetworking/nocables.png" class="image-expand">
    <img src="/BasicNetworkingimages/EP1_BasicNetworking/nocables.png" alt="Description of your image">
</a>

First things first we need to connect all our devices like shown below. 

1. Select the lightning bolt tab
2. Find the black straight cable called (copper straight through) and connect your devices like the image below

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
    <p>When in the Configuration area you cannot save your changes with wr BUT to force ANY command you can use 'do' before the command and it will work</p>
</div>

</body>
</html>

<a href="/BasicNetworkingimages/EP1_BasicNetworking/cabledtopology.png" class="image-expand">
    <img src="/BasicNetworkingimages/EP1_BasicNetworking/cabledtopology.png" alt="Description of your image">
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
    <p>Note that the green lights on your devices only signifies that the device is turned on. They do not confirm that the device is functioning properly.</p>
</div>

</body>
</html>


## Set Computer IPs
1. Double click on each pc (one at a time)
2. Select the **Desktop Tab**
3. Select **IP configuration** and assign the following IP addresses:
	1. PC_1 (192.168.50.101)
	2. PC_2 (192.168.50.102)
	3. Set the subnet mask as if it doesn't do it automatically (255.255.255.0)


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
    <p> You can configure multiple ports at one time with the following command: [Switch(config)]# interface range GigabitEthernet 0/1 - 10</p>
</div>

</body>
</html>

## COMMAND LINE INTERFACE (CLI) OVERVIEW:

COMMAND LINE INTERFACE (CLI) OVERVIEW:

|Mode Name|Capabilities|
|---|---|
|**User EXEC Mode**|- Basic monitoring commands (`show`, `ping`, `traceroute`).  <br>- Cannot modify configurations or restart devices.|
|**Privileged EXEC Mode**|- Full system access (`show running-config`, `debug`, `reload`).  <br>- Enter global configuration mode (`configure terminal`).|
|**Global Configuration Mode**|- Modify system-wide settings (hostname, passwords).  <br>- Enter submodes (interface, line, routing protocols).|
|**Setup Mode**|- Initial setup wizard for devices with no startup configuration.  <br>- Configures basic IP, hostname, and passwords.|
|**ROM Monitor (ROMMON)**|- Low-level troubleshooting (password recovery, IOS image restoration).  <br>- Accessed during boot failures.|

## Configure the Switches

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
    <p>Double click on either switch (you will need to do the following commands on both switches) and then click the CLI tab. </p>
</div>

</body>
</html>


**Hostname:**

The purpose of the hostname is to identify your device. Below are the commands to set the hostname. Typically, a hostname will include information about the device such as building number, room number, device model, etc.

    Switch>enable

Note: This will give you access to the Privileged EXEC mode. Notice that the ‘>’ prompt is replaced with a ‘#’.

    Switch#config t 

Note: This will give you access to the Configuration mode, allowing you to make changes to the device settings. 

    Switch(config)#hostname Switch_A

Note: This changes the hostname of the device you are configuring. Notice on the next line that the default name ‘Switch’ is replaced with the new hostname. 

    Switch_A(config)#exit

    Switch_A#

## Setting Passwords

**Passwords:** 

Passwords keep the device secure and ensures that only people who have the need to know can access the device. Typically, passwords will be unique and created by the infrastructure team (you and your peers) and will be changed periodically, or whenever someone loses the need to know. The following passwords will be the only passwords used on Cisco devices in this block, and will be consistently used for the remainder of this course. **It is critical that you type in the passwords correctly, or you may end up locking yourself out of the device. This may result with you having to restart and losing hours of work.** ***Note: when you are prompted to enter a password (for console, vty, enable secret, etc.) you will NOT see text appear when you type!*** For the remainder of this course, all your Cisco passwords should be as follows:

1. Enable Secret……………..enspass 
2. Console……..………….…..conpass 
3. VTY (Telnet)………….…….vtypass 

Enable Secret: 

	Switch_A#config t 
	Switch_A(config)#enable secret enspass 

Console: 

	Switch_A(config)#line console 0 
	Switch_A(config-line)#logging synchronous 

Note: IOS displays syslog messages to the console users at any time, even during the typing of a command. To avoid interruptions, add the ‘logging synchronous command’. 

    Switch_A(config-line)#password conpass 
	Switch_A(config-line)#login 

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
    <p>Note: It is important to include ‘login’ to the password configuration, if overlooked the password will not be prompted.</p>
</div>

</body>
</html>
 
	Switch_A(config-line)#exit 

VTY (Telnet/SSH):

	Switch_A(config)#line vty 0 ? 

Note: When configuring line vty always type line vty 0 ? to determine how many vty lines are on the device you are configuring. It will vary on each device model. 

	Switch_A (config)#line vty 0 15
	Switch_A(config-line)#logging synchronous 
	Switch_A(config-line)#password vtypass 
	Switch_A(config-line)#login 
	Switch_A(config-line)#exit

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
    <p>REMEMBER THAT YOU NEED TO DO ALL THE ABOVE COMMANDS TO THE B SWITCH TOO</p>
</div>

</body>
</html>



## SECURING PASSWORDS 

**Securing the passwords:** 

Passwords are good for security but not if they are compromised. Encrypting them will help prevent this. If left unencrypted, they will be visible to anyone accessing the device. The passwords are encrypted on a Cisco device by starting the password-encryption service as follows. 

    Switch_A#config t

	Switch_A(config)#service password-encryption 

Note: This encrypts all your passwords, making them unreadable to anyone accessing the device. Once the service is enabled, any passwords entered previously or afterwards will be encrypted. 

	Switch_A(config)#exit

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
    <p>Once the passwords are encrypted, they will be unintelligible to anyone accessing the device.</p>
</div>

</body>
</html>


## SETTING A BANNER 

Banners on networks are used to let someone logging in know that they are logging into a companies network. It serves the purpose of informing the user that if they do not have the need to know to access the device, there will be potential legal consequences if they proceed. Having this warning here makes it possible to hold people accountable for logging into devices they are not supposed to access. The banner must start and end with the same character called a delimiting character to let the device know the beginning and ending and cannot be used in the message. ‘#’ is used below as the character. 

    Switch_A#config t 
    Switch_A(config)#banner motd 

```
#You are accessing a LTH Company Network Switch, WARNING unauthorized access will be prosecuted!!!#
```

Note: The above syntax is a single command and is intended to be typed out in one line. 

    Switch_A(config)#exit

## CONFIGURING SWITCH INTERFACES 

Interfaces: Depending on the device, you will have either FastEthernet or GigabitEthernet Interfaces. Both will be configured with the same information but how you type it in for the initial configuration will vary slightly. To start with, let’s look at the interfaces in the switch. 

    Switch_A#show run 

Tapping the space bar will show everything loaded up as part of the IOS including the amount of interfaces.

**Trunk ports:**

    Switch_A#config t 
    Switch_A(config)#interface g0/1 
    Switch_A(config-if)#description Trunk to Switch_B 

Note: This will describe what the port is connected to. The description is purely for organizational purposes and does not affect functionality. 

    Switch_A(config-if)#switchport trunk encapsulation dot1q

Note: This command will tag traffic that passes through this interface using 802.1q. It is critical for future Labs to function. Trunk interfaces on Cisco switches also require that encapsulation is implemented before you enter the mode. 

    Switch_A(config-if)#switchport mode trunk 

Note: This assigns the interface as a Trunk port (for connections to other networking devices such as another Switch or a Router).

    Switch_A(config-if)#exit


**Access ports (Used):**

    Switch_A(config)#interface fa0/1
    Switch_A(config-if)#description Access to PC1 host 
    Switch_A(config-if)#switchport mode access 

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
    <p>This assigns the interface as an Access port (for connections to end-user equipment such as a PC, VoIP phone, or Printer)</p>
</div>

</body>
</html>

    Switch_A(config-if)#spanning-tree portfast 
Note: This command streamlines the normal Spanning-Tree Protocol process of preventing loops in the network by identifying this interface as only connecting to an end device, where a loop could not occur. 

    Switch_A(config-if)#exit 

**Access ports (Unused):**

    Switch_A(config)#interface fa0/1-(however many ports on your particular switch are not in use)
    Switch_A(config-if)#switchport mode access 
    Switch_A(config-if)#spanning-tree portfast 
    Switch_A(config-if)#shutdown 
Note: This will ‘turn off’ the interface, preventing anyone who plugs into it from accessing the network. 

IMPORTANT: Make sure you repeat these steps for all other unused ports on the device! 

    Switch_A(config-if)#exit 
    Switch_A(config)#exit

## VERIFYING CONFIGURATIONS 
Verify that everything is configured properly by following the steps below. 

    Switch_A#show run 

Note: This will show you the current running-configuration. Every change you make on a Cisco switch is live and ‘running’ on the device. You can look here to check the current settings on interfaces, banners, passwords, etc.

## CHANGING CONFIGURATIONS 

To change things such as hostname, banner, passwords, and descriptions you will simply retype the original commands with the correct information. To remove switchport trunk encapsulation dot1q, switchport mode trunk, switchport mode access, and spanning-tree portfast you will type **no** in front of the original command. 

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
    <p>Below is an example. Please do not actually perform this step as it is intended only to show how it would be done if necessary. </p>
</div>

</body>
</html>


    Switch_A#config t 
    Switch_A(config)#interface g3/3 
    Switch_A(config-if)#no description 
Note: This removes the description on interface g3/3. 

    Switch_A(config-if)#exit 
    Switch_A(config)#exit

## BACKING UP CONFIGURATIONS

Saving Configurations: Saving your configurations is crucial when working on equipment. If your device loses power with settings that are not properly saved, all of your configurations will be lost. First, we will see what the device looks like when it has not been saved.

    Switch_A#show start
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
    <p>This will show you the current startup-configuration. The settings you see here are what is currently saved to the device. This will also be the settings the device will boot up with if it is powered off and powered back on again. You have not saved anything yet, so you will see that is blank. If the device were to be shut off right now, you would lose all the work you have done up until this point.</p>
</div>

</body>
</html>


To save your configurations follow the steps below. Make sure you are consistently backing up your configurations! DO NOT wait until you have a device fully configured to save your configurations!!!!!!

    Switch_A#copy run start
or
    
    Cisco_Switch_A#wr

--------------------------------------

    Destination filename [startup-config]? (press enter)

Note: This command copies the 'running-configuration' to the 'startup-configuration'. By doing this you will ensure that the device will boot up with the configurations it is currently running. This is a command you should be doing often throughout the rest of labs. Without it, you could lose hours of work if you close a project or turn off your devices. (This command is the same as 'write memory').

To verify that the configurations saved we will type in the following.

    Cisco_Switch_A#show start

Note: Now that you have properly backed-up your configurations, you will see the same configurations as you would on your running-configuration (show run).

## TESTING CONNECTIVITY

Trouble shoot Switch 2 to allow the proper ping request to occur!

Double click onto PC1, follow the steps below to test the connection between PC1 and PC2.

1. Select the Desktop Tab
2. Select the Command Promt tile
3. ping PC 2
PC1> ping 192.168.50.102
