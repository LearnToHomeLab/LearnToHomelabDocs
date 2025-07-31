# How to Push Wazuh Alerts to Your Discord Server

In this episode we will cover how to push Wazuh Alerts to your Discord server! I think this integration is super useful because 99% of us probably already use Discord. Why monitor a Wazuh Dashboard when you can monitor your network through Discord? 


<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/NcXIl3VsHHY?si=BahQXNm_w4iKsuR7" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Example of Discord Alerts

Here is an example of what we are going to do in this episode: 

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.1.1.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.1.1.png" alt="Description of your image">
</a>

## Create a Discord Webhook

1. Open Discord.
2. Go to the server you want to use to monitor Wazuh.
3. Create a text channel.

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.1.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.1.png" alt="Description of your image">
</a>

1. <kbd>right click</kbd> on your server
2. Go to server settings.
3. Select the integrations page.

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.2.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.2.png" alt="Description of your image">
</a>

Click on Create a webhook. 

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.3.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.3.png" alt="Description of your image">
</a>

1. Click New Webhook.
2. Name your webhook but to something like WazuhAlerts.
3. Select the text channel for your Wazuh alerts we created a second ago. 
4. Copy the Webhook to a notepad, we will paste it in a configuration file in a minute. 

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.4.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.4.png" alt="Description of your image">
</a>

## Configure Wazuh's Dashboard Integration settings

Login to your Wazuh dashboard and go to the following location:

(Server Manangement / Settings)

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.5.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.5.png" alt="Description of your image">
</a>

On the top right click (edit configuration)

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.6.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.6.png" alt="Description of your image">
</a>

We are going to paste the following code BELOW the tags ``<global> </global>``

```
 <integration>
     <name>custom-discord</name>
     <hook_url>https://discord.com/api/webhooks/XXXXXXXXXXX</hook_url>
     <alert_format>json</alert_format>
 </integration>
```
Then paste your Discords Webhook in the ``<hook_url> </hook_url>`` tags.

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.7.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.7.png" alt="Description of your image">
</a>

1. Click Save.
2. Restart Manager.

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.8.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.8.png" alt="Description of your image">
</a>

## SSH into your Wazuh Dashboard Machine

Next we need to SSH into your Wazuh Dashboard Machine/VM (etc.) to configure the following settings. 

```
ssh username@ip_address
```

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.9.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.9.png" alt="Description of your image">
</a>

After you login perform the following commands:

```
sudo su
```

then go to the config section for integrations: 
```
cd /var/ossec/integrations
```

We can use the following command to see a list of files in there
```
ls -l
```

We need to grab the following discord integrations for this custom Discord notifications here:

```
wget https://raw.githubusercontent.com/maikroservice/wazuh-integrations/main/discord/custom-discord
```
and
```
wget https://raw.githubusercontent.com/maikroservice/wazuh-integrations/main/discord/custom-discord.py
```

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.10.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.10.png" alt="Description of your image">
</a>

We can then verify they are downloaded. We can also see they are white because they don't have the proper permissions yet. 
```
ls -l
```

Then we need to ensure they have the proper permissions to execute:
```
sudo chmod 750 /var/ossec/integrations/custom-*
sudo chown root:wazuh /var/ossec/integrations/custom-*
```

Now we can verify they are correct one more time (and that they have turned green instead of white becuase they have the right perms now.)
```
ls -l
```

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 114021_1.3.11.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 114021_1.3.11.png" alt="Description of your image">
</a>

Now because this is a python script we need to install the proper pip:
(You may get a "Running as pip as the root user..." error but its fine, do not worry about it.)
```
# debian / ubuntu
sudo apt-get install python3-pip
pip3 install requests
```

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.4.1.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.4.1.png" alt="Description of your image">
</a>

Lastly, we need to restart Wazuhs controls:

```
/var/ossec/bin/wazuh-control restart
```
<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.12.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.12.png" alt="Description of your image">
</a>

....

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.11.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.3.11.png" alt="Description of your image">
</a>

## Verify Discord Alerts

Next we can go to our Discord channel and see the service restarted with a confirmation alert:

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.4.3.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.4.3.png" alt="Description of your image">
</a>

I am going to attempt to SSH into one of our Machines with the Wazuh Agent installed and type the wrong password to mimic failed login attempts from a malicious actor.

We will see that we get notified in Discord for these failed attempts within just a few seconds. 

<a href="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.5.1.png" class="image-expand">
    <img src="/images/EP19_wazuhdiscordalerts/Still 2025-02-03 110900_1.5.1.png" alt="Description of your image">
</a>

## Conclusion

That is it! I hope you guys enjoyed, if you would like to learn more please see the links down below. 

[How to setup Discord Webhooks](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks)

[Wazuh external integration configurations](https://documentation.wazuh.com/current/user-manual/manager/integration-with-external-apis.html)

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)