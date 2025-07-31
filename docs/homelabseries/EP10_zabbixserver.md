# Zabbix Server Install
Zabbix is an open-source monitoring tool that monitors IT infrastructure, including: 
Networks, Servers, Virtual machines (VMs), Cloud services, Applications, Databases, and Websites

In this episode we will cover how to setup the server side of Zabbix and in the followin episode/article we will show you the agent side.

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Ax3h24kXR1M?si=EnQw5wDNpi3ImpXW" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Our Homelab Topology

<a href="/images/EP10_zabbixserver/Untitled Diagram.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Untitled Diagram.png" alt="Description of your image">
</a>

## The Order of Commands

<a href="/images/EP10_zabbixserver/_second picture of zabbix steps.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/_second picture of zabbix steps.png" alt="Description of your image">
</a>

## List of commands used
If you do not care about the screenshots, here is a list of commands used!
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
    <p>Some commands MAY change usually just step 2 based on the current version of Zabbix. All other commands should work though.</p>
</div>

</body>
</html>

## Install zabbix Commands:

Link to Zabbix's site and the commands can be found [here](https://www.zabbix.com/download?zabbix=7.0&os_distribution=ubuntu&os_version=22.04&components=server_frontend_agent&db=mysql&ws=apache)

```
sudo -s
```

```
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu22.04_all.deb
```

```
dpkg -i zabbix-release_latest_7.0+ubuntu22.04_all.deb
```


```
apt update
```

```
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```
### Install SQL server

installs mySQL
```
sudo apt-get install mysql-server
```
Starts mySQL on boot
```
sudo systemctl start mysql
```
start it
```
service mysql start
```
then do
```
mysql
```




### Create the database
```
sudo mysql
```
Formats the database type to a the format Zabbix can understand (utf8mb4)
```
create database zabbix character set utf8mb4 collate utf8mb4_bin;
```
With this one the `password` section is where you assign your database password
```
create user zabbix@localhost identified by 'password';
```
Giving your user access to read and write to this database
```
grant all privileges on zabbix.* to zabbix@localhost;
```
Set trust for the database
```
set global log_bin_trust_function_creators = 1;
```
Exit mySQL
```
quit;
```

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
    <p>wait a couple minutes after doing the following command, the script takes awhile to work. You won't see any output for a couple minutes</p>
</div>

</body>
</html>
```
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

Go back into mySQL
```
mysql
```


```
set global log_bin_trust_function_creators = 0;
```

```
quit;
```

then go into the following config file and update the section (DBPassword=) section with the password you set earlier. It will be under the Database user=Zabbix section.

```
nano /etc/zabbix/zabbix_server.conf
```

Start the services with the following commands:
```
systemctl restart zabbix-server zabbix-agent apache2
```

```
systemctl enable zabbix-server zabbix-agent apache2
```

Now you can go to your Zabbix servers URL with the following format:

```
http://host_machine_ip/zabbix
```

## Walkthrough

Create a virutal machine for your Zabbix server. We used 2 cores, 2gb of RAM, and 20gb of storage on an Ubuntu Linux ISO 22.04 Jammy. [Here is the ISO](https://releases.ubuntu.com/22.04/?_gl=1*19ip6hm*_gcl_au*MTE4NTIyOTI0MS4xNzA3MTMxMDQx&_ga=2.149898549.2084151835.1707729318-1126754318.1683186906)

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.3.2.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.3.2.png" alt="Description of your image">
</a>

First go to Zabbix's site and grab the current version of Zabbix you are downloading, this is very important specifically for step 2 as shown under the order of commands section. Go [here](https://www.zabbix.com/download)

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.3.1.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.3.1.png" alt="Description of your image">
</a>

Now go ahead and login (SSH) to your freshly created VM for the Zabbix Server

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.4.1.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.4.1.png" alt="Description of your image">
</a>

Perform the following commands:

------------------------------------

```
sudo -s
```

```
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu22.04_all.deb
```

```
dpkg -i zabbix-release_latest_7.0+ubuntu22.04_all.deb
```


```
apt update
```

```
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

Install SQL server

-----------------------------------

installs mySQL
```
sudo apt-get install mysql-server
```
Starts mySQL on boot
```
sudo systemctl start mysql
```
start it
```
service mysql start
```
then do
```
mysql
```

Create the mySQL database:

----------------------------
```
sudo mysql
```
Formats the database type to a the format Zabbix can understand (utf8mb4)
```
create database zabbix character set utf8mb4 collate utf8mb4_bin;
```
With this one the `password` section is where you assign your database password
```
create user zabbix@localhost identified by 'password';
```
Giving your user access to read and write to this database
```
grant all privileges on zabbix.* to zabbix@localhost;
```
Set trust for the database
```
set global log_bin_trust_function_creators = 1;
```
Exit mySQL
```
quit;
```
--------------------

At this point we are going to execute the following command, you will notice no response after inputting the command and entering the password for the zabbix user you just created 7 command ago.
That is normal, give the script a couple minutes to do its thing.

```
zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```


<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.4.2.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.4.2.png" alt="Description of your image">
</a>

Now perform the following commands after the CLI comes back from being blank.

```
mysql
```


```
set global log_bin_trust_function_creators = 0;
```

```
quit;
```

We need to now edit the following config file, open it with:

```
nano /etc/zabbix/zabbix_server.conf
```

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.6.1.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.6.1.png" alt="Description of your image">
</a>

Look for the DBuser=zabbix section and edit the DBPassword= section with the password you just set earlier.

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.6.2.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.6.2.png" alt="Description of your image">
</a>

It will look like this when you are done. You can then save and exit with <kbd>ctrl + X</kbd> then click <kbd>Y</kbd> and lastly to save it click <kbd>enter</kbd>

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.6.3.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.6.3.png" alt="Description of your image">
</a>

Now perform the following commands to start the Zabbix server and all its needed counterparts.

```
systemctl restart zabbix-server zabbix-agent apache2
```

```
systemctl enable zabbix-server zabbix-agent apache2
```

Now go to your browser and we need to login with the following format:

```
http://host_machine_ip/zabbix
```

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.7.1.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.7.1.png" alt="Description of your image">
</a>

You will be presented with the following landing page, click next. 

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.8.1.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.8.1.png" alt="Description of your image">
</a>

Make sure everything has a green ok so you know you did it right.

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.8.2.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.8.2.png" alt="Description of your image">
</a>

Ensure you add the database user password you just set in that config file so Zabbix's panel can access it.

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.8.3.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.8.3.png" alt="Description of your image">
</a>

Set your server name and timezone

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.1.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.1.png" alt="Description of your image">
</a>

ensure all settings have been filled out or go back and fix them

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.2.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.2.png" alt="Description of your image">
</a>

login, remember the login for username and password is case sensitive! it is Admin NOT admin.

User: Admin

Pass: zabbix

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.3.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.3.png" alt="Description of your image">
</a>

You are in, stay tuned for next episode on how to setup an agent on your servers, VMs, firewalls, etc!

<a href="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.4.png" class="image-expand">
    <img src="/images/EP10_zabbixserver/Still 2025-01-05 093020_1.9.4.png" alt="Description of your image">
</a>

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)