# How to Install Proxmox Statistics on The Homarr Dashboard

Here is the example of what we will be covering:

<a href="/images/EP14_homarr/2025-01-16 10_21_15-Default Board • Homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/2025-01-16 10_21_15-Default Board • Homarr.png" alt="Description of your image">
</a>


## Follow the steps on your own

If you would like to follow the 13 steps on your own [here](https://homarr.dev/docs/integrations/hardware/) is a link to Homarrs documentation. 

## Before getting started

1. Make sure you login to your Homarr dashboard like we setup in the previous episode.

2. Make sure you login to your Proxmox Machine to create the API key required for stats to be shown in Homarr.

## Step by Step Instructions

1. Navigate to the Proxmox portal, click on Datacenter

2. Expand Permissions, click on Groups

3. Click the Create button

4. Name the group something informative, like api-users (our case we did ytlearngroup)

<a href="/images/EP14_homarr/steps1-4.png" class="image-expand">
    <img src="/images/EP14_homarr/steps1-4.png" alt="Description of your image">
</a>

5. Click on the Permissions "folder"

Click Add -> Group Permission

<a href="/images/EP14_homarr/steps 5.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 5.png" alt="Description of your image">
</a>

6. 

    Path: /

    Group: group from Step 4 above

    Role: PVEAuditor

    Propagate: Checked

<a href="/images/EP14_homarr/steps 6.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 6.png" alt="Description of your image">
</a>

7. Expand Permissions, click on Users

8. Click the Add button

    User name: something informative like api

    Realm: Proxmox VE authentication server

    Password: create a secure password for the user

    Confirm Password: re-enter the password

    Group: group from Step 4 above
<a href="/images/EP14_homarr/steps 7-8.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 7-8.png" alt="Description of your image">
</a>

9. Expand Permissions, click on API Tokens

10. Click the Add button

    User: user from Step 8 above

    Token ID: something informative like the application or purpose like homarr

    Privilege Separation: unchecked

<a href="/images/EP14_homarr/steps 9-10.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 9-10.png" alt="Description of your image">
</a>

11. Copy the Secret that is shown in Step 10 because it is only shown once. 

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
    <p>NOTICE THIS IS THE STEP WHERE YOU CAN GRAB THE CORRECT INTEGRATION KEY FORMAT!</p>
</div>

</body>
</html>

You will copy the TokenID into a notepad ADD an <kbd>=</kbd> sign and then paste the secret key after that.

```
<User>@pve!<Token ID>=<Secret>
```

Exmaple:

```
ytuser@pve!homarr=5b5467-0260-48ab-a8f5-03753d332145
```

<a href="/images/EP14_homarr/Steps 11.png" class="image-expand">
    <img src="/images/EP14_homarr/Steps 11.png" alt="Description of your image">
</a>

12. Go back to the "Permissions" menu

    Click Add -> API Token Permission

<a href="/images/EP14_homarr/steps 12.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 12.png" alt="Description of your image">
</a>

13. 

    Path: /

    API Token: select the API token created in Step 10

    Role: PVE Auditor

    Propagate: Checked

    <a href="/images/EP14_homarr/steps 13.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 13.png" alt="Description of your image">
</a>

## Adding your API to Homarr's Dashboard

Open your Homarr Dashboard

Select the Writing / edit icon.

<a href="/images/EP14_homarr/steps 1 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 1 homarr.png" alt="Description of your image">
</a>

Then the Add tile button

<a href="/images/EP14_homarrsteps 2 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 2 homarr.png" alt="Description of your image">
</a>

Then select "Apps"

<a href="/images/EP14_homarr/steps 3 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 3 homarr.png" alt="Description of your image">
</a>

You will then need to grap the IP address of your server and paste it to internal and external.

<a href="/images/EP14_homarr/steps 4 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 4 homarr.png" alt="Description of your image">
</a>

Move over to the integrations tab and this is where you will select your integration as Proxmox and paste your Proxmox API key you made a minute ago. Then select "Save".

<a href="/images/EP14_homarr/steps 5 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 5 homarr.png" alt="Description of your image">
</a>

After that you will need to add a Widget like you just added an app.

<a href="/images/EP14_homarr/steps 6 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 6 homarr.png" alt="Description of your image">
</a>

Scroll down until you find System Health Monitoring and add it.

<a href="/images/EP14_homarr/steps 7 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 7 homarr.png" alt="Description of your image">
</a>

Find the newly placed widget on your Dashboard, click the gear icon on the top right to edit it.

<a href="/images/EP14_homarr/steps 8 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 8 homarr.png" alt="Description of your image">
</a>

Lastly, change your settings to match the below screenshot, save, and wait a couple minutes for your data to appear and that is it. (9)

<a href="/images/EP14_homarr/steps 9 homarr.png" class="image-expand">
    <img src="/images/EP14_homarr/steps 9 homarr.png" alt="Description of your image">
</a>

## Closing thoughts

That is it, if you have any other questions do not forget to hop in our discord! 

