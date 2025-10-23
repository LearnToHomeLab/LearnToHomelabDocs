# I Made My Mikrotik AP Fully Managed by OPNsense – No More DHCP Chaos

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/5POELZHOsuU?si=xoPyL1WdjRbpvzye" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## WinBox Mikrotik AP Overview

Please see the image below, this will show you all sections (tabs) you need to have open, in order to perform the tasks found in this video.

<a href="/images/MikrotikAPManagedByOPNsense/Mikrotik overview.png" class="image-expand">
    <img src="/images/MikrotikAPManagedByOPNsense/Mikrotik overview.png" alt="Description of your image">
</a>

## Configuring your Mikrotik Wireless Access Point to get DHCP leases from your root DHCP server (OPNsense)

1.  Login to your Mikrotik Access point with a direct Ethernet Connection to your PC with the MAC address found on the sticker on the bottom of the access point (the login credentials will be found there too)
2.  We are going to open the bridge tab
3.  Under the bridge menu, go to the ports tab.
4.  Add all interfaces under here, you should just need to add ether 1 to BRIDGE if you have the default config setup.
5.  Go to the interfaces list window
6.  Under the interfaces window ensure the interfaces list tab has LAN set to bridge and WAN set to ether 1 (because we have the internet access connected to Ethernet 1)
7.  Open DHCP Client under IP →DHCP Client
8.  Create/Set the DHCP client to the interface bridge
9.  Open DHCP Server under: IP Tab → DHCP Server
10. Disable the DHCP server
11. Go to the Networks tab under the DHCP server window and disable that too
12. Open the address list under IP → Addresses (verify that you get the correct network for your homes network)
13. Configure Wi-Fi networks and settings under the Wi-Fi tab. (Here you can double click and set the SSID, band, channel width, passphrase, authentication type, under the configuration, channel, and security tabs)

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)