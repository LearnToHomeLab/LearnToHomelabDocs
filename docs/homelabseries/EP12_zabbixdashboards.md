# How to create Dashboards in Zabbix

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/y-0MNSrWXSo?si=BLRAnK7bNHz7aF_v" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Introduction
This is going to be a more basic article because what dashboards you want, how many you want, and the types of machines/services you are monitoring vary widely. 

In short, this article will familiarize you with how to create dashboards, grab device information, and the importance of classifying devices by catergories or customers for easy dashboard creation. 

## Getting started

Firs go ahead and login to your Zabbix Dashboard/Monitoring service website. Selecting the Dashboard menu on the far left will present you with the following screen.

You can view all your dashboards by selecting the all dashboards found on the top right of this page. When editing a dashboard you will be able to save on the top right. 

<a href="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.1.png" class="image-expand">
    <img src="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.1.png" alt="Description of your image">
</a>

After selecting all dashboards you can see a list of all your dashboards. It is best practice to make dashboards for specific customers, job types (network engineers monitoring all the switches and routers for example) etc. You want to try
and avoid have cluttered or overwhelming dashboards.

<a href="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.2.png" class="image-expand">
    <img src="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.2.png" alt="Description of your image">
</a>

After selecting create a new dashboard on the top right, you can select anywhere in the menu to create a widget and will be presented with the following screen. 

The type of dashboard you pick is how the information will be presented, graphs, tables, pictures, etc. 

Host groups is a grouping of devices you should have created when adding agents, for example, you should have a group for a specific customer or all your routers/switches. This allows you to pull all their info in quickly. 

Hosts are a more refined search where you can select certain devices of a group. 

(do not select add just yet)

<a href="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.3.png" class="image-expand">
    <img src="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.3.png" alt="Description of your image">
</a>

Before selecting add you will be presented with a screenn like below, this screen depends on what type of widget you created but you are provided a list of resources you can choose to monitor. This will take trial and error though. Some selections may
not reveal any information because the agent is unable to pull that type of data (it is service dependent). 

<a href="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.4.png" class="image-expand">
    <img src="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.4.png" alt="Description of your image">
</a>

That is it, here is a quick and basic example of what your newly created dashboard could look like. Super simple, super easy to do! 

<a href="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.5.png" class="image-expand">
    <img src="/images/EP12_zabbixdashboards/Still 2025-01-09 175014_1.3.5.png" alt="Description of your image">
</a>

## Closing thoughts

Join our discord and share screenshots of your custom made dashboards [Discord](https://discord.gg/6MsHSJWZpH)

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)