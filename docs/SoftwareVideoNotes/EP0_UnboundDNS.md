# Unbound DNS and Network Wide ad blocking!

## Overview

This article will cover the benefits of using OPNsense + Unbound + Blocklists and how it can be a faster, better, and more streamlined approach to network-wide ad blocking over Pi-Hole.

## Benefits

Using Unbound DNS with ad-blocking offers several benefits over Cloudflare DNS:
1. Enhanced privacy: Unbound eliminates the need for a third-party upstream DNS service, ensuring no single DNS server has your full DNS history. This prevents companies like Cloudflare from collecting and potentially selling your data.

2. Recursive resolution: Unbound resolves DNS queries recursively, starting with root servers, which improves privacy through qname minimisation. This process reveals less information about your browsing habits to higher-level DNS servers.

3. Local control: By running Unbound locally, you have complete control over your DNS resolver, without relying on external services. This allows for customization and reduces dependence on third-party infrastructure.

4. Improved caching: Unbound's efficient caching algorithm and pre-fetching capabilities can lead to faster DNS resolution times for frequently accessed domains.

5. Reduced tracking: By eliminating third-party DNS providers, you limit the ability of companies to track your online activities through DNS requests.

6. DNSSEC validation: Unbound supports DNSSEC, which helps protect against DNS spoofing and cache poisoning attacks.

7. Compatibility with ad blocking: Unbound can be easily integrated with ad-blocking solutions like Pi-hole, providing a comprehensive solution for both privacy and ad filtering

## Check out our video on this topic

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src=" " frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Guide to setup Unbound DNS + Ad Blocking

1. First you need to login to your OPNsense machine and go to *Services / Unbound DNS / General*
2. Next you need to click *Enable Unbound* and click *Apply*

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.1.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.1.png" alt="Description of your image">
</a>

1. Next, we need to go into *Services / Unbound DNS / Blocklist*
2. Select *Enable* to turn Block lists on.
3. Select *Type of DNSBL* and your desired blocklist; in our case, we are going to use (Steven Back List).
4. Click Apply.

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.3.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.3.png" alt="Description of your image">
</a>

Now we need to change our DNS settings in TWO locations as shown in the following two screenshots. Now that Unbound is handling our DNS requests, we are removing Cloudflare from the picture.

We are going to assign our OPNsense machines IP address to our DNS records now that it is handling the requests.

The two locations you need to assign your OPNsense machines IP address to are:

1. Services / ISC DHCPv4 / [LAN]
2. System / Settings / General

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.4.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.4.png" alt="Description of your image">
</a>

AND

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.5.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.5.png" alt="Description of your image">
</a>

## Getting User Stats for Unbound

We can verify Unbound is working with ad blocking by enabling Unbound DNS under:

1. Reporting / Unbound DNS

and selecting *Go to the reporting configuration.

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.6.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.6.png" alt="Description of your image">
</a>

On this screen you will select *Enable local gather of Statistics*

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.7.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.3.7.png" alt="Description of your image">
</a>

## Clearing our DNS records on Windows

DNS across your network will reset to our new DNS IP within 5-20 minutes WITHOUT you doing anything but to quickly verify your setup is correct, you can do the following commands on your host before verifying it works. 

1. 
```
ipconfig /flushdns
```
2. 
```
ipconfig /renew
```

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.4.1.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.4.1.png" alt="Description of your image">
</a>

We are going to run a ad blocking test from AdminForge which can be found [here](https://test.adminforge.de/adblock.html)

You can see we already have a 41% block rate with a single block list, adding more can increase that number!

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.5.1.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.5.1.png" alt="Description of your image">
</a>

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
    <p>Remember, the more blocklists you add, the higher the chance it could affect your browsing experience or prevent you from accessing sites you would like to.</p>
</div>

</body>
</html>

We can go over to the *Reporting / Unbound DNS* page, then click the *details* tab and verify we are getting blocks. If you are, then you have set everything up correctly!

<a href="/images/EP0_unbounddns/Still 2024-12-26 191805_1.5.2.png" class="image-expand">
    <img src="/images/EP0_unbounddns/Still 2024-12-26 191805_1.5.2.png" alt="Description of your image">
</a>
