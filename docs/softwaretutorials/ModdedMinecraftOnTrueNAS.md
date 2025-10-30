# Setup a Modded Minecraft Server on TrueNAS Scale with CurseForge

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/m7Kn8D47JsM?si=1V31jOStKzlr0ar-" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Setup a TrueNAS SMB Share (if you don’t have one)

If you do NOT have a TrueNAS SMB share setup and connected to your local computer VIA the file explorer, please watch our video here first. Specifically from the timestamps 00:00 - 06:21 (you do not need to follow the rest of setting up Jellyfin.

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/mLXMLJVp1kA?si=nd8sQK8dG2lVc1Yo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

After completing the SMB share continue on with the following: 

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
    <p>Now open File Explorer on your machine (windows shortcut <kbd>&#8862; + E</kbd> and create a folder on your SMB Share called “Minecraft”</p>
</div>

</body>
</html>


## Installing Modded Minecraft With CurseForge Overview

Due to CurseForge being one of the oldest and most popular Minecraft modded methods, this is the one we are going to use in this video. This method is virtually the same for all other modded platforms as shown at the beginning of this article.

1.  You will need to download the CurseForge app [here](https://www.curseforge.com/download/app)
2.  The mods for your forge server can be found [here](https://www.curseforge.com/minecraft/search?page=1&pageSize=20&sortBy=relevancy)
3.  We are going to use this pack found [here](https://www.curseforge.com/minecraft/modpacks/all-the-mods-10)

## Setting up Modded Minecraft on TrueNAS

### Pick your Mod Pack from CurseForge

The first thing we need to do is pick what modpack we are going to install, we are going to use this one [here](https://www.curseforge.com/minecraft/modpacks/all-the-mods-10).

We have four main things we need to pay attention to when picking our modded Minecraft pack:

1.  Select the files tab to see the files for the modpack.
2.  The pack files (this is what we will download to add to the server)
3.  What version of Minecraft this pack supports.
4.  What Mod Loader we will need to select in TrueNAS.


<a href="/images/ModdedMinecraftOnTrueNAS/all the mods 10 overview.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/all the mods 10 overview.png" alt="Description of your image">
</a>

Now select your pack (option 2 as shown above). You will be brought to virtually the same screen as shown below but we have an _additional files_ tab, this is where we get the SERVER side files:

<a href="/images/ModdedMinecraftOnTrueNAS/files all the mods 10 overview.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/files all the mods 10 overview.png" alt="Description of your image">
</a>

Under this tab, go ahead and download the server side files:

<a href="/images/ModdedMinecraftOnTrueNAS/server files all the mods 10 overview.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server files all the mods 10 overview.png" alt="Description of your image">
</a>

## Setup a Minecraft Server on TrueNAS

Go ahead and log into your TrueNAS machine

<a href="/images/ModdedMinecraftOnTrueNAS/truenas login page.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/truenas login page.png" alt="Description of your image">
</a>

Select your _apps_ Tab on the far left and then _discover apps_ on the top right. Search for “Minecraft” and select the _Minecraft Server (Java)_ version.

Either click install/install another instance if you already have a version of Minecraft running:

<a href="/images/ModdedMinecraftOnTrueNAS/install minecraft on truenas.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/install minecraft on truenas.png" alt="Description of your image">
</a>

### Modded Minecraft TrueNAS Server Settings

Now this is the super important step! We need to ensure that all our settings are correct or our modded Minecraft server will not boot.

Here are the steps (all steps assume you are typing the settings in, I am giving you the title of the box at which you need to fill in):

1.  Application name
2.  timezone
3.  EULA (check the box)
4.  Image Selector (if you install an older modpack that requires an older java version, you may need to google what version of java you need to set this to).
5.  Type (this information is found on your modpacks page, in our case the mod loader is NeoForge).
6.  Version (this is the version of Minecraft required by the modpack, i.e. 1.21.1).
<a href="/images/ModdedMinecraftOnTrueNAS/server steps 1 through 6.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server steps 1 through 6.png" alt="Description of your image">
</a>

7.  RCON Password (set a password for RCON).

<a href="/images/ModdedMinecraftOnTrueNAS/server steps 7.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server steps 7.png" alt="Description of your image">
</a>

8.  Additional Environment Variables (this page will differ on your modpack potentially but for CurseForge we will need to use two variables, “CF_PAGE_URL” AND “CF_API_KEY”. The page URL will be for your modpack, and the API key will come from your CurseForge profile found [here](https://console.curseforge.com/?#/api-keys))
9.  We are going to add two more variables called “INIT_MEMORY” and “MAX_MEMORY” where in our case of this modpack are going to be set to 16 gigabytes.

<a href="/images/ModdedMinecraftOnTrueNAS/iserver steps 8 through 9.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server steps 8 through 9.png" alt="Description of your image">
</a>

10. Set Host IP’s to the default under the Network Configuration **(you will need to change the ports if you already have other Minecraft servers running on your TrueNAS machine):**

<a href="/images/ModdedMinecraftOnTrueNAS/server steps 10.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server steps 10.png" alt="Description of your image">
</a>

11. Under **Storage Configuration**, type (set to Host Path), enable ACL, and set your Host Path to a folder on your SMB share called Minecraft, which you created in an earlier step).
12. ACL Options (check Force Flag)
<a href="/images/ModdedMinecraftOnTrueNAS/server steps 11 through 12.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server steps 11 through 12.png" alt="Description of your image">
</a>

13. CPU (set CPU to however many cores you want, we recommend 4 cores for the mod pack used in this example).
14. Memory (set the memory to between 12 - 16 gigabytes but it must match whatever you set for the variables in step 9).
15. Click Save/update.

<a href="/images/ModdedMinecraftOnTrueNAS/server steps 13 through 15.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/server steps 13 through 15.png" alt="Description of your image">
</a>

If your server starts to deploy, you can go ahead and stop it on the far right

<a href="/images/ModdedMinecraftOnTrueNAS/stop the minecraft deployment.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/stop the minecraft deployment.png" alt="Description of your image">
</a>

Now open the SMB share with the location of your Minecraft Server folder and delete any files in there

<a href="/images/ModdedMinecraftOnTrueNAS/delete smb minecraft folder contents.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/delete smb minecraft folder contents.png" alt="Description of your image">
</a>

Now go to your downloads folder and grab the server files you downloaded from CurseForge, right click on them, and extract all

<a href="/images/ModdedMinecraftOnTrueNAS/extract cruseforge server files.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/extract cruseforge server files.png" alt="Description of your image">
</a>

Now open that unzipped folder, see the highlighted items, these are the items we are going to copy into the Minecraft folder on our TrueNAS SMB Share

<a href="/images/ModdedMinecraftOnTrueNAS/open the unzipped server files folder for curseforge.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/open the unzipped server files folder for curseforge.png" alt="Description of your image">
</a>

Now go back over to your TrueNAS dashboard and boot your Minecraft server with the files above inside that folder.

<a href="/images/ModdedMinecraftOnTrueNAS/start the minecraft server.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/start the minecraft server.png" alt="Description of your image">
</a>

After it starts we can go over to the _Workloads_ section and _View Logs_ well its booting up to ensure we have no issues, if we do, we can take those error codes and ask something like ChatGPT what the issue is to help us get it running.

<a href="/images/ModdedMinecraftOnTrueNAS/view logs.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/view logs.png" alt="Description of your image">
</a>

## Adding the Modpack to CurseForge

Now that we have handled the server side of the modded Minecraft server we need to handle our client side. Open the CurseForge app and select Minecraft:

<a href="/images/ModdedMinecraftOnTrueNAS/curseforge minecraft mods.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/curseforge minecraft mods.png" alt="Description of your image">
</a>

Search for the same modpack you want to use, and click install, let it install. After it is installed you will see it under the _My Modpacks_ Tab seen in the image below:

<a href="/images/ModdedMinecraftOnTrueNAS/find client side modpack.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/find client side modpack.png" alt="Description of your image">
</a>

Hover over it, it will say play, select that and it will ask you to login to your Minecraft account if you have not done so before:

<a href="/images/ModdedMinecraftOnTrueNAS/select play minecraft.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/select play minecraft.png" alt="Description of your image">
</a>

After you login, at the top of the launcher you should see your modded Minecraft version and a play button:

<a href="/images/ModdedMinecraftOnTrueNAS/click play with the modpack selected.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/click play with the modpack selected.png" alt="Description of your image">
</a>

Wait for Minecraft to boot, go to your multiplayer tab, and then put in the IP and port number of your server and connect to your new Modded Minecraft server on TrueNAS!

<a href="/images/ModdedMinecraftOnTrueNAS/input IP and your port for minecraft.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/input IP and your port for minecraft.png" alt="Description of your image">
</a>

There you have it, your very own Modded Minecraft Server!

<a href="/images/ModdedMinecraftOnTrueNAS/logged into modded minecraft on TrueNAS.png" class="image-expand">
    <img src="/images/ModdedMinecraftOnTrueNAS/logged into modded minecraft on TrueNAS.png" alt="Description of your image">
</a>

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)