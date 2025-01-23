# How to Install The Wazuh Server Dependency
In this episode we will cover how to install the Wazuh server "Agent". Wazuh is a free, open-source security platform that protects data from security threats. It combines Security Information and Event Management (SIEM) and Extended Detection and Response (XDR) capabilities. 

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/wC4EscsMwyk?si=t6s5KZRHHOx_jpxF" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Useful links/Information

1. If you want to understand how Wazuh works and all the components behind scenes read about it [here](https://documentation.wazuh.com/current/proof-of-concept-guide/index.html)

2. The quick start guide we are going to follow found [here](https://documentation.wazuh.com/current/quickstart.html)

3. How Wazuh Rules are formatted can be found [here](https://documentation.wazuh.com/current/user-manual/ruleset/rules/index.html)

4. Where to put Wazuh Rules can be found [here](https://documentation.wazuh.com/current/user-manual/ruleset/rules/default.html)

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
    <p>To note, we were unable to get the script to install when attempting to install the Wazuh Server when allocating less than 75Gigs of storage</p>
</div>

</body>
</html>

## Steps to Install Wazuh Server


Please see the below image on the configuration of the Proxmox VM we used to install the Wazuh Server. 

We recommend Ubuntu Server and that can be found [here](https://ubuntu.com/download/server) ***DO NOT FORGET TO ENABLE SSH DURING INSTALL***


<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.3.1.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.3.1.png" alt="Description of your image">
</a>


If you would like to read the latest information on what Wazuh believes you should have for a proper install, that can be found [here](https://documentation.wazuh.com/current/quickstart.html)

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.4.1.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.4.1.png" alt="Description of your image">
</a>

AFTER you created your VM please use your CLI of preference to SSH into your Wazuh Server VM.

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.5.1.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.5.1.png" alt="Description of your image">
</a>

Please paste the following install script ***(NOTE, this will change with new releases)*** you can find the latest script [here](https://documentation.wazuh.com/current/quickstart.html)

```
curl -sO https://packages.wazuh.com/4.10/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.6.1.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.6.1.png" alt="Description of your image">
</a>

After the install script completes, you will find your login information at the end of the install, please copy these somewhere for safe keeping.

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.1.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.1.png" alt="Description of your image">
</a>

Now you can login to your Wazuh Server by going to the following URL
```
https://server_ip:443
```

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.2.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.2.png" alt="Description of your image">
</a>

It really is that simple, now you just need to wait a couple minutes for Wazuh to finish setting everything up.

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.3.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.3.png" alt="Description of your image">
</a>

That is it! Here is the main dashboard for Wazuh Server!

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.4.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.4.png" alt="Description of your image">
</a>

## Change Wazuh to Dark Mode

Now I know all you IT / Computer and / HomeLab lovers desire dark mode! So here is how you do it!

Select the hamburger icon on the top left, go down to ***Dashboard Management / Dashboards Management / Advanced Settings //*** Scroll down to the appearance section 

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.5.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.5.png" alt="Description of your image">
</a>

Then all you have to do is turn on dark mode and click save changes.

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.6.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.6.png" alt="Description of your image">
</a>

Then you can click the Wazuh "W" logo on the top right to go back to the homepage, feel free to explore Wazuh Server or watch our next episode on installing the agent and configuration! 

<a href="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.7.png" class="image-expand">
    <img src="/images/EP15_wazuhserver/Still 2025-01-20 115204_1.7.7.png" alt="Description of your image">
</a>