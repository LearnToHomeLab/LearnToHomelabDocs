# How to Install Fail2Ban in 2025

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/JyAdPYkdqkM?si=9wm7pHwL5mWn0nCJ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Install Fail2Ban

Fail2Ban is a log-parsing application that helps protect Linux servers from malicious attacks, particularly brute-force attacks. It works by monitoring system logs for suspicious activity, such as repeated failed login attempts, and then automatically blocking the IP address of the attacker from accessing the server. This blocking is usually achieved by adding rules to the server's firewall (e.g., iptables). '

To install Fail2Ban:

```
sudo apt install fail2ban
```

We then need to start and enable the service:

```
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
```

We can ensure the service is running with:

```
sudo systemctl status fail2ban
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
    <p>You can skip to part 5 because the default install is fine, but if you would like to be more specific you can read the following configuration options for Fail2Ban</p>
</div>

</body>
</html>

## Basic Configuration

Fail2ban uses "jails" to define which services to monitor and how to respond to suspicious activity.

1.  Create a local configuration file:
    - Never edit the default `jail.conf` directly, as it may be overwritten during updates. Instead, copy it:
        
        ```
        sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
        ```
        
        Or, you can create/edit `/etc/fail2ban/jail.local` directly if it doesn’t exist.

2.  **Edit the configuration:**
    
    ```
    sudo nano /etc/fail2ban/jail.local
    ```
    
    - **Common settings to review:**
        - `ignoreip` — IPs to never ban (e.g., your own).
        - `bantime` — How long (in seconds) a ban lasts (e.g., 3600 for 1 hour).
        - `findtime` — Time window for counting failures (e.g., 600 for 10 minutes).
        - `maxretry` — Number of failures before ban (e.g., 3).
    - Example:
        
        ```
        [DEFAULT] 
        ignoreip = 127.0.0.1 
        bantime  = 3600 
        findtime = 600 
        maxretry = 3
        ```
        
3.  **Enable and configure a jail (e.g., SSH):**
    - In the same `jail.local` file, ensure you have:
        
        ```
        [sshd] 
        enabled = true 
        port    = ssh 
        filter  = sshd 
        logpath = /var/log/auth.log 
        maxretry = 3 
        bantime = 600 
        findtime = 600
        ```
        
    - This will protect SSH from brute-force attacks

4.  **Restart Fail2ban to apply changes:**
    
    ```
    sudo systemctl restart fail2ban
    ```
    

## Verify Fail2ban Operation

- Check the status of all jails:
    
    ```
    sudo fail2ban-client status
    ```
    
- Check the status of a specific jail (e.g., SSH):
    
    ```
    sudo fail2ban-client status sshd
    ```

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)