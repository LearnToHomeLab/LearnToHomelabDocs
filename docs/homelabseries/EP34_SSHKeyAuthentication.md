# How to Enable Linux SSH Key Authentication 
<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/4Ll2ONlEfcs?si=x-VAtM8gHIjOsfm-" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Throughout this course, we have used a username and password to SSH into our machines. It is not a bad option, especially if you are leaving services private, BUT if you are exposing SSH over the public internet or want to follow best practice, we need to use SSH logins via key authentication. It will be impossible for a hacker to ever log in to your system remotely without that private SSH key.

First thing we need to do is create an encrypted key set on our computer (client), NOT the server. You will NEVER transfer your private key over the internet, it will always stay on your computer (however, if you want to keep a safe copy of it somewhere, you could put it on a USB drive for safekeeping). I do know some people upload them to their password vault as well, but I would be mindful of this practice. Remember, if you lose the key, you could still log in to your machine locally and upload a new key to access it remotely again if needed.

### Creating the SSH Key

You can leave the default settings when creating your SSH key as shown below, (you do not need to change anything)

<a href="/images/EP34_SSHKeyAuthentication/ssh key example.png" class="image-expand">
    <img src="/images/EP34_SSHKeyAuthentication/ssh key example.png" alt="Description of your image">
</a>

Open a new tab in your Windows CLI (command line) and paste the following command.:


```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Your SSH key on Windows is stored in the following location:

`
_C:\\Users\\your_username\\.ssh_
`
### Uploading the SSH

We will type the following command into that same CLI to upload the SSH key to our Linux Server:

Make sure you put the correct SSH key name, the username of the Linux machine you are connecting to, and its IP address.

```
type $env:USERPROFILE\.ssh\<your_ssh_key_name> | ssh <user>@<host_Ip_address> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

We can then check the following folder to ensure it is in there:

```
cd .ssh
```

Then open the authorized keys file:

```
nano authorized_keys
```

To go back to your root directory, you can do the following:

```
cd ~
```

We can then ensure our SSH key folder has the correct permissions with:

```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

### Disable SSH Password Authentication

We need to now disable password authentication so we only use the key to access our machine:

```
sudo nano /etc/ssh/sshd_config
```

We want to edit the following parameters in the config file found under the #Authentication section.

```
PasswordAuthentication no
PermitRootLogin no
```

You may also have another file where you need to set that parameter to _no_ as well, it can be changed here:

```
sudo nano /etc/ssh/sshd_config.d/50-cloud-init.conf
```

Then we need to restart SSH:

```
sudo systemctl restart ssh
```

Log out of our server and then try to log back in:

```
exit
```

Then SSH back in, and we should be taken back into our server automatically without being prompted for a password, thanks to our private key.

```
ssh <username>@<server_ip>
```


## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)