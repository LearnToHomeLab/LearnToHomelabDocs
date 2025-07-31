# How to Install The Pterodactyl Game Panel in One Click!

Pterodactly is an amazing game panel that has been around for the last ten years, I have been keeping my eye on this project and really think it is worth the spotlight at this point. 

Check the project out [here](https://pterodactyl.io/)


<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/T8Eu_5xi-Wo?si=AOsPIXB7tlJ0HBYW" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## What you need to get started

1. Create a VM or have Ubuntu Server installed on a machine ready to go.

2. Head over to the Pterodactyl-Installer script [here](https://github.com/pterodactyl-installer/pterodactyl-installer)

## How to Install Petrodactyl

Create a VM with whatever specs you can afford, it should be at least the minimum shown below. Reminder: All your game servers will have to share whatever resources you allocate. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.4.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.4.1.png" alt="Description of your image">
</a>

SSH into your VM with the following command:

```
ssh <username>@<ip_address>
```

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.1.png" alt="Description of your image">
</a>

Then, put yourself in root mode with

```
sudo su
```

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.2.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.2.png" alt="Description of your image">
</a>

Then paste the install scrip which can be found [here](https://github.com/pterodactyl-installer/pterodactyl-installer) 

```
bash <(curl -s https://pterodactyl-installer.se)
```

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.3.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.3.png" alt="Description of your image">
</a>

You will then see a list of options; select #2 so we can install the game panel and wings. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.4.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.4.png" alt="Description of your image">
</a>

You will then be prompted with the “Database name” field; anything in ( ) will mean that is the default answer. We will leave the defaults for the database name and username and then make our own password. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.6.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.6.png" alt="Description of your image">
</a>

Next, you will click the link shown in the CLI using <kbd> ctrl + left click </kbd> and find your timezone, then paste your timezone into the CLI. It can also be found [here](https://www.php.net/manual/en/timezones.php)

<a href="/images/EP25_Pterodactylinstall/timezones_1.5.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/timezones_1.5.1.png" alt="Description of your image">
</a>

Next, you need to add a valid email address; this is used to create your account, receive emails, and find users within the panel. They will ask for that twice. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.7.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.7.png" alt="Description of your image">
</a>

Next, you will create an admin account. Fill out all the relevant information. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.8.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.8.png" alt="Description of your image">
</a>

Next, we need to set the FQDN (if this server will be seen over a public IP); if not, you will use the IP address of your machine / VM for the domain name, which will allow you to access it in your browser. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.9.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.5.9.png" alt="Description of your image">
</a>

Next, click enter for “no” on (Do you want to automatically configure a UFW (FireWall)). If this were public facing, you would want to select “Y” for yes. 

<a href="/images/EP25_Pterodactylinstall/no ufw_1.5.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/no ufw_1.5.1.png" alt="Description of your image">
</a>

Next, confirm that your settings look correct, and then type “Y” for yes to continue with the installation. Wait a couple of minutes for everything to finish. After that, you will see a question asking to send anonymous data; that is up to you, but we typed no and then clicked enter to finish the installation.  

<a href="/images/EP25_Pterodactylinstall/check settings_1.5.2.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/check settings_1.5.2.png" alt="Description of your image">
</a>

Next, you should be prompted to perform the Wings installation on the following screen. Go ahead and type your FQDN or IP address into your browser and log in with the admin credentials you created earlier.  

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.7.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.7.1.png" alt="Description of your image">
</a>

Next, return to your command prompt and type “Y” to continue the wings installation. You will be prompted with a few questions asking: 

1. Do you want to  auto-configuring the UFW. If this machine is public-facing, you will want to say yes; if the server is not public-facing, you can say no. 

2. We will also type no to auto-setup the database for hosts. 

3. You will also say no to setting up Let’s Encrypt unless this is public-facing.  

4. type “Y” for yes to continue with the installation.

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.10.2.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.10.2.png" alt="Description of your image">
</a>

Next, you will see a link in the CLI to their documentation on how to finish setting up Wings. Click that. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.11.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.11.1.png" alt="Description of your image">
</a>

Next, we will create a node in the panel by selecting the gear icon on the top right, then select locations (create a new location and name it whatever you want). Finally, go back to the nodes tab and click Create New at the top right. Read through this step carefully, but it is self-explanatory. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.18.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.18.1.png" alt="Description of your image">
</a>

Next, after your node is created, we need to assign IP addresses and port numbers to it. You can add a maximum of 1000 port number ranges at a time. For example, ports 1000-2000 would be a range. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.23.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.23.1.png" alt="Description of your image">
</a>

Next, under the nodes tap, if you click your node and then the configurations tab, you will be presented with the config file we need to add to our server in the CLI. That will be done by doing. 

```
nano /etc/pterodactyl/config.yml
```

Then, paste it into the empty file. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.27.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.27.1.png" alt="Description of your image">
</a>

To exit the file, you will type <kbd> ctrl + X </kbd>, then type <kbd>y</kbd> to save and <kbd>enter</kbd> to exit.

*Here is what it looks like in the folder*

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.29.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.29.1.png" alt="Description of your image">
</a>


Next you will need to start wings with the following command and ensure you do not get any errors. 

```
sudo wings --debug
```

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.31.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.31.1.png" alt="Description of your image">
</a>

Next, we can set wings to run in the background by typing the following command.

```
sudo systemctl enable --now wings
```

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.35.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.35.1.png" alt="Description of your image">
</a>

## Create your first server.

Go to your servers tab in the game panel, select Create New at the top right, and follow the instructions, which are again self-explanatory. Specifically, “Nest Configuration” is where you will set the type of game you are trying to create. Side note: Also, pay close attention to the “Startup Configuration” because that is where you will set important things like the amount of RAM your server can use. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.36.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.36.1.png" alt="Description of your image">
</a>

Next, wait for your game server to install. After a few minutes, you can try reloading your browser, and the installing banner should be gone. 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.38.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.38.1.png" alt="Description of your image">
</a>

Next, click the “Pterodactyl” word at the top right of the panel; you will then see your game server on the main page. Click it and then click Start at the top right. Wait for your server to start and you are good to go!

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.39.2.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.39.2.png" alt="Description of your image">
</a>

You are finally done, go ahead and try logging on to your game server! 

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.42.1.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.42.1.png" alt="Description of your image">
</a>

We are in!

<a href="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.42.2.png" class="image-expand">
    <img src="/images/EP25_Pterodactylinstall/Still 2025-03-06 133057_1.42.2.png" alt="Description of your image">
</a>

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)
