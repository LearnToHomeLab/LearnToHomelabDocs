# Installing Your First VM (Ubuntu) on Proxmox
This episode will go over basic linux commands, how to setup your first virtual machine (VM) inside Proxmox, and important things to know and understand when operating inside of the Linux terminal. 

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
    <p>This is a beginner friendly course so we understand many of you may find this lesson to be a review but these fundamental concepts are very important for beginners.</p>
</div>

</body>
</html>

## What is Linux? 
Linux is an operating system, just like Windows or macOS, but it's built on an entirely different philosophy and foundation. Here's an explanation in simple terms:

Operating System: An operating system is the software that manages all the hardware resources of a computer and provides the base upon which other software can operate. It handles tasks like managing files, running applications, and controlling hardware.

Open Source: Unlike Windows or macOS, which are owned and developed by specific companies (Microsoft and Apple, respectively), Linux is open source. This means its source code is freely available for anyone to view, modify, and distribute.

Variety of Distributions: Instead of a single version like Windows or macOS, Linux comes in many different flavors called "distributions" or "distros." Each distro packages the Linux kernel (the core of the operating system) along with various software applications and utilities. Examples of popular Linux distros include Ubuntu, Fedora, and Debian.

Customization: Linux is highly customizable. Users can choose different desktop environments (the look and feel of the graphical interface), install software packages tailored to their needs, and configure the system to their liking.

Command Line Interface (CLI): While Linux does have graphical user interfaces (GUIs) like other operating systems, it also emphasizes the use of the command line interface (CLI). This means users can interact with the system and perform tasks by typing commands rather than clicking on icons.

Stability and Security: Linux is known for its stability and security. It's widely used in servers, supercomputers, and other critical systems where reliability and security are paramount.

Community Support: Linux has a vibrant and active community of users and developers who provide support, contribute to development, and create software that runs on the platform.

In summary, Linux is an open-source operating system known for its flexibility, customization options, stability, and security. It's used by a wide range of people, from casual home users to large corporations and organizations, and it offers an alternative to proprietary operating systems like Windows and macOS.
## Linux Distributions
We covered Linux distros earlier but I wanted to go more in depth of what that actually means. 

UNIX distributions, including both Debian-based (e.g., Ubuntu) and non-Debian-based (e.g., Fedora, CentOS), typically adhere to a set of common command-line utilities and shell commands. These commands are often part of the POSIX (Portable Operating System Interface) standard, which defines a set of standards for ensuring compatibility between UNIX-like operating systems.

However, while many commands are shared across UNIX distributions, there can be some variations and differences in the way certain commands are implemented or the additional options they support. These differences may arise due to:

Package Management: Different distributions use different package managers for installing, updating, and managing software packages. For example, Debian-based distributions use apt or apt-get, while non-Debian-based distributions like Fedora use dnf or yum.

Filesystem Hierarchy: The organization of system files and directories may vary slightly between distributions, which can affect the paths used in commands or the locations of configuration files.

Init Systems: Different distributions may use different init systems (such as systemd, Upstart, or SysVinit), which can impact how services are managed and controlled.

Default Shell: While most UNIX distributions use the Bash shell (Bourne Again Shell) as the default shell, some may use alternatives like Zsh (Z Shell) or Dash. While the core set of commands remains the same, the behavior or features of the shell may differ slightly.

Despite these differences, the majority of basic commands and utilities (such as ls, cd, mkdir, rm, etc.) are consistent across UNIX distributions, allowing users to transfer their skills and knowledge between different systems with relative ease. Additionally, online documentation and resources specific to each distribution can help users navigate any differences and effectively use the system.
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
    <p>Throughout this course we are going to use Debian based distros, which also hapen to be the most popular across the industry. I HIGHLY recommend you stick within the Debian bubble. </p>
</div>

</body>
</html>

## Path selection (beginners vs familiar with Linux)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Warning Box Example</title>
<style>
.warning-box {
    background-color: #8B0000; /* Light red background color */
    border-left: 6px solid #f44336; /* Red border on the left side */
    padding: 10px; /* Padding inside the box */
    margin-bottom: 20px; /* Margin at the bottom to separate from other content */
    /* You can add more styles as needed */
}
</style>
</head>
<body>

<div class="warning-box">
    <p>If you are new and unfamiliar with Linux please read the Linux section, if you want to continue on with installing your virtual machine (VM) then please click the "installing your VM" section under the table of contents.</p>
</div>

</body>
</html>

## Linux For beginners (navigation)
Learn more Linux commands
> To get Linux practice please checkout [Linux Journey](https://linuxjourney.com/)
> To learn more linux commands please see [Digital Oceans Linux Examples](https://www.digitalocean.com/community/tutorials/linux-commands)
{.is-info}

**Linux Commands**

Linux and specifically Linux Server is administrated (controlled) primarily through the Command Line interface (CLI), being able to understand and navigate your way through the CLI is critical for the remainder of this course. 

For the simplicity and timeliness of this episode, I am going to cover how to navigate within the Linux CLI but futher episodes and articles will explain commands before they are used. 

Navigation commands: 
Here are some common CLI (Command-Line Interface) commands used in Debian-based Linux distributions like Debian itself, Ubuntu, and Linux Mint:

The CLI has three major indicators in red, your username, in yellow the device you are currently connected to, and then a symbol of ~$ or ~#.

When you see the $ symbol in the Linux CLI, it typically indicates that the shell prompt is in the regular user mode. This means you're logged in as a regular user and have limited permissions.

When you see the # symbol in the Linux CLI, it indicates that the shell prompt is in the root or superuser mode. This means you have administrative privileges and can perform tasks that require elevated permissions, such as installing software or modifying system configurations.
<a href="/images/EP4_firstvmubuntu/ubuntu_user.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/ubuntu_user.png" alt="Description of your image">
</a>

---
| Command Syntax        | Description                                                      | Example                       |
|-----------------------|------------------------------------------------------------------|-------------------------------|
| apt update            | Updates the local package index.                                 | apt update                    |
| apt upgrade           | Upgrades installed packages to their latest versions.            | apt upgrade                   |
| apt install <package> | Installs a package.                                              | apt install firefox           |
| apt remove <package>  | Removes a package.                                               | apt remove firefox            |
| apt search <keyword>  | Searches for a package.                                          | apt search editor             |
| dpkg -i <package.deb> | Installs a .deb package.                                         | dpkg -i package.deb           |
| dpkg -l               | Lists installed packages.                                        | dpkg -l                       |
| ls                    | Lists files and directories.                                     | ls                            |
| ls -l                 | Lists files in long format, including permissions and details.  | ls -l                         |
| ls -a                 | Lists all files, including hidden files.                         | ls -a                         |
| cd <directory>        | Changes to the specified directory.                               | cd Documents                  |
| cd ..                 | Moves up one directory.                                          | cd ..                         |
| cd ~ or cd            | Changes to the home directory.                                    | cd ~                          |
| mkdir <directory_name>| Creates a new directory.                                         | mkdir project                 |
| rm <file>             | Deletes a file.                                                  | rm file.txt                   |
| rm -r <directory>     | Deletes a directory and its contents recursively.                 | rm -r folder                  |
| nano <filename>       | Opens a file in the nano editor.                                 | nano example.txt              |
| vim <filename>        | Opens a file in the vim editor.                                  | vim example.txt               |
| sudo <command>        | Executes a command with superuser privileges.                    | sudo apt update               |
| man <command>         | Shows the manual page for the specified command.                 | man ls                        |
| pwd                   | Prints the current working directory.                            | pwd                                     |
| cp <source> <destination> | Copies files or directories.                                   | cp file.txt /path/to/destination       |
| mv <source> <destination> | Moves or renames files or directories.                         | mv file.txt /path/to/destination       |
| touch <filename>      | Creates an empty file.                                           | touch newfile.txt                      |
| cat <filename>        | Displays the contents of a file.                                 | cat file.txt                           |
| grep <pattern> <filename> | Searches for a pattern in a file.                               | grep "search term" file.txt            |
| find <directory> <options> | Searches for files or directories.                            | find /path/to/search -name "*.txt"     |
| chmod <permissions> <filename> | Changes permissions of a file or directory.                   | chmod 755 script.sh                    |
| chown <user>:<group> <filename> | Changes ownership of a file or directory.                    | chown user:group file.txt              |
| df                    | Displays disk space usage.                                       | df -h                                   |
| du                    | Displays disk usage of files and directories.                    | du -sh /path/to/directory              |
| top                   | Displays real-time system information.                           | top                                     |
| ps                    | Displays information about active processes.                      | ps aux                                  |
| kill <PID>            | Terminates a process using its process ID.                       | kill 1234                              |
| history               | Displays the command history.                                    | history                                 |
| tar <options> <archive_name> <files/directories> | Creates or extracts tar archives.                    | tar -cvf archive.tar file1 file2       |
| gzip <filename>       | Compresses files.                                                 | gzip file.txt                          |
| unzip <filename>      | Extracts files from a zip archive.                               | unzip archive.zip                      |
| wget <URL>            | Downloads files from the internet.                               | wget http://example.com/file.txt       |
| curl <URL>            | Transfers data to or from a server.                              | curl -O http://example.com/file.txt    |
---
I know that table may feel overwhelming, but fear not. Throughout this course we will go over the commands as we use them. Again, please feel free to practice using [Linux Journey](https://linuxjourney.com/).
  
> Alright  if you are ready, lets get started! (Click the Installing VM tab)
{.is-info}

  
## Installing your VM 
Alright, you should be somewhat familiar with the Linux CLI now.
  
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
  Node: (select whatever Proxmox server or mini PC you want to install to (our case it is pve still).
  VM Id: does not matter (you can leave default).
  Name: (Describe what you are installing on the Ubuntu server (Wiki.Js, ARK server, Minecraft, Zabbix, etc).

---

 -OS Tab:
  ISO image: select the ubuntu file we just uploaded.

---

 -System Tab:
  All settings can stay default here.

---

 -Disk Tab:
  Disk Size (GiB): (set based on the requirement of whatever software we are installing) i.e Wiki.Js reccomends at least 1gig of storage and Ubuntu Server requires 20gigs so we should have no less than 22gigs. (I would reccomend going up at least 5gigs for small installs and at least double for other applications where you know you will be uploading lots of content i.e. mods, pictures, user accounts, etc. 

---

 -CPU Tab:
  Again, this will be based on the requirements of what you are installing. Wiki.js requires 2 cores and so does Ubuntu Server so we will select 2 cores. 

---

 -Memory Tab: 
  Again, based on system requirements. Wiki.js wants 2gig of ram, Ubuntu Server reccomends 4gigs of ram but you can honestly get away with 1-2 depending on what you are installing. In our case for Wiki.js we are going to keep 2gigs.

---

 -Network Tab:
  This can stay default.

---

 -Confirm Tab: 
  Please check over all your settigns and click *finish*. 

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
6. We can leave this default becasue most of you will be using DHCP. 
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
9. In the case of Proxmox we are creating a virtual machine, and during the setup of our Proxmox VM we set the disk drive size, meaning our VM can only see the virtualized partitioned disk drive (this prevents you from over writing any other VM disk partitons on your server). You are good to go ahead and use the WHOLE disk drive in this case.
<a href="/images/EP4_firstvmubuntu/9_use_entire_disk.png" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/9_use_entire_disk.png" alt="Description of your image">
</a>
10. This is just giving you a breakdown of that paritioned disk and how much space is going to each resource.
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
  
Now all you need to do is add this VM in Solarwinds Putty and connect to it over SSH:
<a href="/images/EP4_firstvmubuntu/2024-03-30_13-28-45.gif" class="image-expand">
    <img src="/images/EP4_firstvmubuntu/2024-03-30_13-28-45.gif" alt="Description of your image">
</a> 
  
Using SSH is important for future videos because it allows you to copy and paste content into your CLI and important data from your local machine to your VM.
  
