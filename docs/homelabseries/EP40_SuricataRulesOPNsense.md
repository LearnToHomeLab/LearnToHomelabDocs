# Enabling Suricata Rules on OPNsense Firewall
Hey guys, in this video I will cover how to enable Suricata Rules in your OPNsense firewall. 

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/FKOIyv0okC4?si=X79eCYYruEaUS6EP" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Do you need to enable your IPS? (Suricata on OPNsense)?

Well the short answer is no, especially if you have no port forwarding or open ports. However, this does not mean your normal network traffic is not susceptible to vulnerabilities that Suricata can investigate. ALL traffic coming in and out of your network Suricata will perform inspection on, so it can still be useful and at the end of the day it is another layer of security for your network and data.

## Backup Your OPNSense Firewall First

[Check out the threat lists here if you would like to see what they block](https://rules.emergingthreats.net/open/suricata-7.0.3/rules/)

Before you make changes to your Firewall, always make sure you download a copy of your settings first:

1.  Log in to your OPNsense machine
2.  Select **System**
3.  Select **Configuration**
4.  Select **Backups**
5.  Select **Download Configuration**

## Enable Emerging Threats (ET) Open Rules in Suricata (Free IDS/IPS Rules)

## Steps to install and Enable Suricata Rules:

1.  **Log into your OPNsense Web GUI.**
2.  Navigate to **Services > Intrusion Detection > Administration.**
3.  If Suricata is not enabled, check the **Enable** box at the top to activate it.
4.  Check the box next to “IPS Mode” too.
5.  Under the **Download** tab, find the **Rule Sets** section.
6.  Locate the **Emerging Threats Open** options and check the box to enable each ruleset (remember the more you enable the more resources your router uses). Here is a list of common ones you could enable:
    
    | **Category Name** | **Description / Purpose** | **Why Enable?** |
    | --- | --- | --- |
    | **emerging-exploit** | Rules detecting exploit attempts against vulnerabilities | Captures common attack vectors to patchable software |
    | **emerging-malware** | Known malware communication and payload signatures | Blocks malware command and control, payloads |
    | **emerging-scan** | Detects network scanning activities | Early indication of attackers probing your network |
    | **emerging-phishing** | Identifies phishing URLs and traffic | Helps prevent credential theft and social engineering attacks |
    | **emerging-dos** | Denial-of-service attacks and traffic | Detects volumetric or targeted DoS attacks |
    | **emerging-attack_response** | Responses by attackers post-exploitation | Helps spot attacker lateral movement or persistence |
    | **emerging-botcc (if available)** | Botnet command & control activity | Prevents infected hosts from communicating with attackers |
    | **emerging-web_server** | Web server-specific attacks | Protects vulnerable web applications |
    | **emerging-ftp/smtp/dns/pop3** | Protocol-specific attack and abuse patterns | Covers common attack vectors via standard services |
    | **emerging-snmp** | SNMP protocol abuse and attacks | Detects common misuses of network infrastructure |
    | **emerging-sql** | SQL Injection and Database Attacks | Protects backend databases |
    
7.  Click **Enable selected** at the top of the page.
8.  Next, go to the **rules** tab and click **Rules** to enable them all.
9.  Next, go to the **Schedule** tab so we can have the rules auto-update weekly.Set the following:  

    Minutes: 0

    Hours: 0 

    Day of the month: 1

    Months: *

    Days of the week: *

10. Save and apply all changes.

## Verify Emerging Threats is Working

1.  We will need to enable SSH under /system/settings/administration
2.  Login to our Opnsense machine over SSH (select windows key, type cmd, and then SSH from your terminal)
3.  After logging in to your OPNsense machine, Select option 8 for shell
4.  run the following command:
    
    ```
    curl http://testmynids.org/uid/index.html
    ```
    
5.  Check the logs under /services/intrusion detection/administration/alerts (on your OPNsense dashboard)
6.  turn off SSH under /system/administration (in your OPNsense dashboard)

Suricata will now monitor traffic using free, community-maintained ET Open threat signatures.

---

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)