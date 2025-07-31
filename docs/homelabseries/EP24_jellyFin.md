## Introduction
In this video we will cover 

1. How to setup a SMB share on Truenas

2. How to Install JellyFin on your TrueNas machine

3. How to connect JellyFin to your SMB Share.

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/mLXMLJVp1kA?si=W0NgkkqPExEx0Rx1" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Creating an SMB Share on TrueNas

If you have not setup TrueNas before, please see our previous video on how to do that [here](/homelabseries/EP17_truenasscale)

That video will also cover how to setup a storage pool which is required before this tutorial. 

Login to TrueNas and perform the following:

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.3.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.3.1.png" alt="Description of your image">
</a>

## Create a Dataset

Next You need to go to the datasets tab then select "Add dataset on the top right:

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.3.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.3.2.png" alt="Description of your image">
</a>

Then perform the following: Name your dataset, give it the SMB preset, and ensure your SMB name is descriptive like (smbshare), then slick save.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.4.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.4.1.png" alt="Description of your image">
</a>

## SMB Share

Next we need to go to the Shares Tab and ensure the SMB share was created and enabled. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.5.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.5.1.png" alt="Description of your image">
</a>

## Create local Group

Next go to Credentials / Local Groups

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.7.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.7.1.png" alt="Description of your image">
</a>

Click "Add" on the top right:

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.8.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.8.1.png" alt="Description of your image">
</a>

Next you need to give the group a name, allow samba authentication, and save it. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.9.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.9.1.png" alt="Description of your image">
</a>

## Create a Local User

We now need to go to the local users tab in the same area.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.10.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.10.1.png" alt="Description of your image">
</a>

Click add on the top right as well

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.10.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.10.2.png" alt="Description of your image">
</a>

Now to create a user we need to do the following. 

1. Assign a name

2. create a username

3. (and 4) assign a passward

5. Turn off "Create a New Primary Group"

6. Assign the local group you made earlier

7. Assign the local group you made earlier

8. Set the home directory to your JellyFin SMB Share directory.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.11.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.11.1.png" alt="Description of your image">
</a>

Then go all the way to the bottom and click save.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.12.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.12.1.png" alt="Description of your image">
</a>

## Enable SMB on TrueNas

Next we need to go to System Settings / Services

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.14.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.14.1.png" alt="Description of your image">
</a>

Ensure the following settings are on.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.15.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.15.1.png" alt="Description of your image">
</a>

## SMB Share ACL's

Next we need to ensure the SMB file share access control lists are enabled/configured. Go back to the Shares tab and click the "Shield" icon on the right to edit your ACL's.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.16.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.16.1.png" alt="Description of your image">
</a>

We are going to use a pre-made ACL (nsf4_open) then click continue.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.16.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.16.2.png" alt="Description of your image">
</a>

Just do a click glance but the settings should all be correct, you can then save the access control list. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.17.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.17.1.png" alt="Description of your image">
</a>

## Connecting to our SMB share on Windows

To connect to an SMB share on Windows you will do the following

```
\\<IP_address of SMB server>\<smb_share_filename>
```

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.19.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.19.1.png" alt="Description of your image">
</a>

You will be prompted with the following screen, input the credentials of the local user you created for your SMB share. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.20.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.20.1.png" alt="Description of your image">
</a>

Now you need to create some folders to organize the movies, pictures, and documents. This will allow you to have categories within JellyFin to browse through. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.20.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.20.2.png" alt="Description of your image">
</a>

## Installing JellyFIn Media Server

To Install JellyFin head over to the "Apps" Tab and then select Discover Apps on the top right.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.21.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.21.1.png" alt="Description of your image">
</a>

Search for JellyFin and click on it

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.21.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.21.2.png" alt="Description of your image">
</a>

Select Install

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.21.3.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.21.3.png" alt="Description of your image">
</a>

Then you will be prompted with the settings for installation menu of JellyFin. 

1. You will need to assign the application name

2. Assign the IP address for the JellyFin Server (this will be the same IP as seen in your browser URL if you are installing this on TrueNas)

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.22.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.22.1.png" alt="Description of your image">
</a>

Next scroll down until you see "Additional Storage" This is where you will connect the SMB share we setup earlier. 

1. Select the SMB share type.

2. Mount Path can be named whatever you want! /SMB just keeps it simple.

3. Server IP (same as before, the IP of TrueNas like seen in your URL bar)

4. The SAME name as your created JellyFin SMB share.

5. The name of the local user you created earlier. 

6. The Password of that user you created earlier. 

Then click save and wait for your VM to have the status of deployed.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.22.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.22.2.png" alt="Description of your image">
</a>

After your VM is running, click the web portal icon button. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.24.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.24.1.png" alt="Description of your image">
</a>

Select your language and click next. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.24.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.24.2.png" alt="Description of your image">
</a>

Create a user to login to JellyFin with, then click next. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.25.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.25.1.png" alt="Description of your image">
</a>

Then Select content type, movies, and add your folders you created on your SMB share earlier. Remember that your share will be under the /SMB directory. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.26.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.26.1.png" alt="Description of your image">
</a>

*Showing the /SMB directory*

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.27.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.27.1.png" alt="Description of your image">
</a>

*Then in there we can see the folders we created earlier.*

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.27.2.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.27.2.png" alt="Description of your image">
</a>

Then scroll to the bottom and select Ok.

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.28.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.28.1.png" alt="Description of your image">
</a>

Login to JellyFin with your JellyFin account you created earlier. 

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.29.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.29.1.png" alt="Description of your image">
</a>

Then that is it, you are in! enjoy watching and streaming your content!

<a href="/images/EP24_jellyFin/Still 2025-03-03 084826_1.30.1.png" class="image-expand">
    <img src="/images/EP24_jellyFin/Still 2025-03-03 084826_1.30.1.png" alt="Description of your image">
</a>


## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)

