## How to Enable and use The Linux Firewall (UFW)

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/B8ClCMHRW-s?si=XGYOWlU6q5cemkNy" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

**UFW (Uncomplicated Firewall) controls network traffic between your Ubuntu machine and other devices.** It primarily filters incoming and outgoing connections to and from your machine, NOT internal communication on the machine.

There is one thing we need to be mindful of when enabling the UFW: accidentally blocking our services’ communication. We first need to grab a list of the services running on our machine and what port they are using, so we can add those to our firewall list.

We will use the following command to grab a list of ports we need to add to our firewall, We will pay attention to the _local address: port_ column. This column does not show ALL the ports you need to add, just gives you a list of ports so you can work through them and decide what you may need to add to your firewall.

```
sudo ss -lntup
```

Now we do not want to lose our SSH access, so we need to ensure the UFW has SSH permissions first. You will type “y” when prompted.

```
sudo ufw allow OpenSSH
sudo ufw enable
```

We can verify UFW is running now by using the following command

```
sudo ufw status
```

Here are a list of common firewall rules you may need to use or come across often. 

|     |     |     |     |
| --- | --- | --- | --- |
| **Command** | **Description** | **Command** | **Description** |
| `sudo ufw enable` | Enable the firewall | `sudo ufw disable` | Disable the firewall |
| `sudo ufw status` | Show firewall status | `sudo ufw status verbose` | Show detailed firewall status |
| `sudo ufw status numbered` | Show rules with numbers | `sudo ufw allow [port]` | Allow traffic on a port |
| `sudo ufw deny [port]` | Deny traffic on a port | `sudo ufw allow [port]/[proto]` | Allow port with protocol (e.g., tcp) |
| `sudo ufw allow from [IP]` | Allow all traffic from an IP | `sudo ufw allow from [IP] to any port [port] proto [proto]` | Allow from IP to specific port/proto |
| `sudo ufw allow in on [iface] to any port [port]` | Allow a port on a specific interface | `sudo ufw delete allow [port]` | Delete the allow rule for a port |
| `sudo ufw delete [number]` | Delete the rule by number | `sudo ufw default deny incoming` | Set the default policy to deny incoming |
| `sudo ufw default allow outgoing` | Set the default policy to allow outgoing | `sudo ufw reload` | Reload UFW to apply changes |
| `sudo ufw reset` | Reset UFW and remove all rules | `sudo ufw logging on` | Enable UFW logging |
| `sudo ufw show added` | Show added rules | `sudo ufw --help` | Show help and available commands |


Ultimately, how you use the UWF will be on a case-by-case basis based on the services you are running. I hope this short and quick tutorial gives you an overview and idea of how the UFW works. It is a great tool and highly recommended to use; it just adds another layer of security to your infrastructure. 

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)