
This episode is an update to episode 13 AND 14 due to Homarr's source code being redone. 

## What we will cover

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Informative Section</title>
<style>
.informative-section {
    background-color: #8CD2F4; /* light blue background color */
    color: black; /* Text color to contrast with dark background */
    padding: 20px; /* Padding inside the box */
    border-radius: 10px; /* Rounded corners */
    display: flex;
    align-items: center;
}
.circle-emoji {
    width: 50px;
    height: 30px;
    border-radius: 50%;
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-right: 15px;
    font-size: 20px;
    color: #231F20; /* Dark gray color for the exclamation mark */
}
</style>
</head>
<body>

<div class="informative-section">
    <div class="circle-emoji">!</div>
    <p>This episode is good for FRESH INSTALLS AND those who are UPGRADING from the old Homarr Dashboard</p>
</div>

</body>
</html>

1. Creating a new VM for the new Homarr Dashboard
2. How to create an API key for Proxmox usage stats.
3. How to install the new 1.0 Homarr dashboard
4. How to upgrade from the old dashboard to the new dashboard. 
5. How to add trusted certificates to your dashboard
6. How to edit old Proxmox intergrations
7. How to create new Proxmox intergrations in the Homarr Dashboard

## Getting started

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Rv9Ob8M2QQI?si=XkpT897yZ-2OllqL" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Fresh Install Users

Create a new Ubuntu Server VM in Proxmox with the following:

1. OS: Ubuntu Server
2. 2gb of ram
3. 2 vcores, 
4. 32gb of storage. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.5.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.5.1.png" alt="Description of your image">
</a>

***During install ensure you enable SSH!***

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.7.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.7.1.png" alt="Description of your image">
</a>

On your new VM we need to install Docker and Homarr with the following commands:

SSH into your NEW homarr VM using the following command:

```
ssh <username>@<VM_ipaddress>
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.1.png" alt="Description of your image">
</a>


Adding the GPG keys and Docker repo:

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.2.png" alt="Description of your image">
</a>


Install the Latest Package:

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.3.png" alt="Description of your image">
</a>


Ensure Docker is running after Install, you will get a response like this.

  
```

sudo docker run hello-world

```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.4.png" alt="Description of your image">
</a>

  
<details>
<summary>If Docker hello fails do the following</summary>

if you do not get a response try

```

systemctl status docker.service

```

  

If that shows failed messages, try the following

```

sudo systemctl daemon-reload

sudo systemctl restart docker

```

Then try to see its status once again:

```

systemctl status docker.service

```

<a href="/images/EP13_homarr/docker status_1.3.2.png" class="image-expand">

    <img src="/images/EP13_homarr/docker status_1.3.2.png" alt="Description of your image">

</a>
</details>
  

### Install Docker Compose

Install Docker Compose with: 

```

sudo apt install docker-compose

```

Verify that docker compose is installed

```

docker compose version

```

### Install Homarr

Then create a docker compose file:

```

nano docker-compose.yml

```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.5.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.5.png" alt="Description of your image">
</a>


Copy the following file config in there for your Homarr docker compose file.

```
#---------------------------------------------------------------------#
#     Homarr - A simple, yet powerful dashboard for your server.      #
#---------------------------------------------------------------------#
services:
  homarr:
    container_name: homarr
    image: ghcr.io/homarr-labs/homarr:latest
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # Optional, only if you want docker integration
      - ./homarr/appdata:/appdata
    environment:
      - SECRET_ENCRYPTION_KEY=51564af476c9eecd2efb30ed980a4b2e768efb7a558676859e2e1fbd04ce15a0
    ports:
      - '7575:7575'
```
To get out of the above editor you will do the following:
To exit: <kbd>ctrl + X</kbd> 

To confirm save: <kbd>y</kbd>

To confirm the file name you are saving to: <kbd>enter</kbd>

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.6.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.6.png" alt="Description of your image">
</a>


Then run the following to start it:

```

sudo docker compose up -d

```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.7.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.7.png" alt="Description of your image">
</a>

Then to login to your machine you will type the following into your browser to access the panel:

```
ip_address:7575
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.12.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.12.1.png" alt="Description of your image">
</a>


### Creating a Proxmox API Key

#### make new API key

1. Navigate to the Proxmox portal, click on Datacenter
2. Expand Permissions, click on Groups
3. Click the Create button

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.1.png" alt="Description of your image">
</a>

4. Name the group something informative, like api-users

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.2.png" alt="Description of your image">
</a>

5. Click on the Permissions "folder"
6. Click Add -> Group Permission

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.3.png" alt="Description of your image">
</a>

- Path: /
- Group: group from Step 4 above
- Role: PVEAuditor
- Propagate: Checked

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.4.png" alt="Description of your image">
</a>

7. Expand Permissions, click on Users
8. Click the Add button
    - User name: something informative like api
    - Realm: Proxmox VE authentication server
    - Password: create a secure password for the user
    - Confirm Password: re-enter the password
    - Group: group from Step 4 above

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.5.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.5.png" alt="Description of your image">
</a>

9. Expand Permissions, click on API Tokens
10. Click the Add button
    - User: user from Step 8 above
    - Token ID: something informative like the application or purpose like homarr
    - Privilege Separation: unchecked

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.6.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.6.png" alt="Description of your image">
</a>

11. Copy the Secret that is shown below because it is only shown once

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.7.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.7.png" alt="Description of your image">
</a>

12. Go back to the "Permissions" menu
13. Click Add -> API Token Permission

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.8.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.8.png" alt="Description of your image">
</a>

    - Path: /
    - API Token: select the API token created in Step 10
    - Role: PVE Auditor
    - Propagate: Checked

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.9.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.14.9.png" alt="Description of your image">
</a>


### Adding your Certificate 

Now we need to grab the Proxmox certificate.

1. Select the node where your Homarr Dashboard is located. 
2. Select Certificates
3. Select the pve-root-ca.pem certificate
4. Click View certificate

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.22.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.22.1.png" alt="Description of your image">
</a>

Next we need to copy the contents to a notepad and then save the file as
`certificate_name.crt`

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.23.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.23.1.png" alt="Description of your image">
</a>

Pasting it into Notepad

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.24.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.24.1.png" alt="Description of your image">
</a>

Saving it as a .crt file name

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.25.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.25.1.png" alt="Description of your image">
</a>

Now go over to your Homarr dashboard and on the top right click / your username bubble / Manage

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.1.png" alt="Description of your image">
</a>

Next go to:
1. Tools
2. Certificates
3. (top right) select add certificate
4. Add your saved certifcate 
5. Click add.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.2.png" alt="Description of your image">
</a>

`showing the certificate added`

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.3.png" alt="Description of your image">
</a>

You should now see a valid certificate

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.4.png" alt="Description of your image">
</a>



### Adding Proxmox Stats Integration

Now we can go over to the Apps page and create a new app (this must be done before adding the integration)

Click new app

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.1.png" alt="Description of your image">
</a>

1. Now you can give it whatever name you want.
2. Search for the icon related to what you are connecting (in our case Proxmox)
3. grab the IP(URL) address of the Proxmox Node we want to see stats from.
4. Click create

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.2.png" alt="Description of your image">
</a>

Now go to the integrations tab:
1. New integration
2. Search and select Proxmox

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.3.png" alt="Description of your image">
</a>

***This is where people struggle because this is the major change from the old Homarr panel***

We are going to go grab the correct information from Proxmox for the username, token ID, API key, and realm. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.4.png" alt="Description of your image">
</a>

Over on Proxmox:

1. Go to the data center at the top
2. Go to API Token
3. We will see the username
4. We will see the Token name

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.1.png" alt="Description of your image">
</a>

Go back over to Homarr and fill out that respective information in the username and token ID field. Remember you also need to paste your API key you created under the (make a new API key) section. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.2.png" alt="Description of your image">
</a>

Lastly we just need to get the realm. 

Your realms are found under datacenter / realms. We are going ot be using PVE so our real will be PVE. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.3.png" alt="Description of your image">
</a>

like so:

Then test connection and connect.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.4.png" alt="Description of your image">
</a>

Click the Homarr logo at the top left to go back to your main dashboard OR (Boards on the far right, then select your dashboard from there)

On the top right click the pencil icon to edit your dashboard (it won't look like ours below)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.29.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.29.1.png" alt="Description of your image">
</a>

Now you will notice all your icons have three dots on the top right and your board is now editable.

There will be a <kdb>+</kbd> icon on the top right, click that and then select new item.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.1.png" alt="Description of your image">
</a>

Under the items we need to select (System Health Monitoring) and click add to board

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.2.png" alt="Description of your image">
</a>

Now on our dashboard page we will see that new section with no data, click the three dots on the right and click edit item.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.3.png" alt="Description of your image">
</a>

From the integrations drop down menu select the integration we just created, and click save changes.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.4.png" alt="Description of your image">
</a>

Now you can see we have the Proxmox stats on our dashboard!

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.31.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.31.1.png" alt="Description of your image">
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
    <p>The fresh install tutorial is now over</p>
</div>

</body>
</html>

## Upgrade path for old users

### Create a new Homarr VM

Create a new Ubuntu Server VM in Proxmox with the following:

1. OS: Ubuntu Server
2. 2gb of ram
3. 2 vcores, 
4. 32gb of storage. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.5.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.5.1.png" alt="Description of your image">
</a>

***During install ensure you enable SSH!***

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.7.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.7.1.png" alt="Description of your image">
</a>

On your new VM we need to install Docker and Homarr with the following commands:

SSH into your NEW homarr VM using the following command:

```
ssh <username>@<VM_ipaddress>
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.1.png" alt="Description of your image">
</a>


Adding the GPG keys and Docker repo:

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.2.png" alt="Description of your image">
</a>


Install the Latest Package:

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.3.png" alt="Description of your image">
</a>


Ensure Docker is running after Install, you will get a response like this.

  
```

sudo docker run hello-world

```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.4.png" alt="Description of your image">
</a>

  
<details>
<summary>If Docker hello fails do the following</summary>

if you do not get a response try

```

systemctl status docker.service

```

  

If that shows failed messages, try the following

```

sudo systemctl daemon-reload

sudo systemctl restart docker

```

Then try to see its status once again:

```

systemctl status docker.service

```

<a href="/images/EP13_homarr/docker status_1.3.2.png" class="image-expand">

    <img src="/images/EP13_homarr/docker status_1.3.2.png" alt="Description of your image">

</a>
</details>
  

### Install Docker Compose

Install Docker Compose with: 

```

sudo apt install docker-compose

```

Verify that docker compose is installed

```

docker compose version

```

### Install Homarr

Then create a docker compose file:

```

nano docker-compose.yml

```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.5.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.5.png" alt="Description of your image">
</a>


Copy the following file config in there for your Homarr docker compose file.

```
#---------------------------------------------------------------------#
#     Homarr - A simple, yet powerful dashboard for your server.      #
#---------------------------------------------------------------------#
services:
  homarr:
    container_name: homarr
    image: ghcr.io/homarr-labs/homarr:latest
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # Optional, only if you want docker integration
      - ./homarr/appdata:/appdata
    environment:
      - SECRET_ENCRYPTION_KEY=51564af476c9eecd2efb30ed980a4b2e768efb7a558676859e2e1fbd04ce15a0
    ports:
      - '7575:7575'
```
To get out of the above editor you will do the following:
To exit: <kbd>ctrl + X</kbd> 

To confirm save: <kbd>y</kbd>

To confirm the file name you are saving to: <kbd>enter</kbd>

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.6.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.6.png" alt="Description of your image">
</a>


Then run the following to start it:

```

sudo docker compose up -d

```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.7.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.11.7.png" alt="Description of your image">
</a>

Then to login to your machine you will type the following into your browser to access the panel:

```
ip_address:7575
```

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.12.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.12.1.png" alt="Description of your image">
</a>

### Exporting your old dashboard

login to your OLD Homarr Dashboard, click the username top right, clicked manage, under settings go to tools, migrate to 1.0

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.15.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.15.1.png" alt="Description of your image">
</a>

here is how you get to that menu:

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.16.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.16.1.png" alt="Description of your image">
</a>

Select export data (copy your encryption key to your notes!!!!) and ensure you also select keep on the top right of your browser if it tries to block it.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.17.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.17.1.png" alt="Description of your image">
</a>

Going over to your fresh VM you just created, click (import from Homarr before 1.0)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.18.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.18.1.png" alt="Description of your image">
</a>

After selecting your .zip file you will be presented with the screen below. We are not changing ANY of the settings, simply click (confirm import and continue)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.18.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.18.3.png" alt="Description of your image">
</a>

Now paste that encryption key so Homarr and unzip your old dashboard.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.18.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.18.4.png" alt="Description of your image">
</a>

We wont be changing any of the settings here but you can turn off (send anonymous analytics) if you want.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.19.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.19.2.png" alt="Description of your image">
</a>

You will be presented with the following screen, we are going to select (go to default-large board)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.19.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.19.3.png" alt="Description of your image">
</a>

You may then be prompted to login, you will do this with the credentials of your old dashboard (because now its really your new dashboard)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.19.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.19.4.png" alt="Description of your image">
</a>

Now we are going to select (configure server-wide home dashboard) this is where we will set the default dashboard when you login.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.20.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.20.1.png" alt="Description of your image">
</a>

Find your old dashboards, click the three dots, then select (set as your home board)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.20.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.20.2.png" alt="Description of your image">
</a>

Now you have your dashboard back! 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.20.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.20.3.png" alt="Description of your image">
</a>

### Adding your Certificate 

Now we need to grab the Proxmox certificate.

1. Select the node where your Homarr Dashboard is located. 
2. Select Certificates
3. Select the pve-root-ca.pem certificate
4. Click View certificate

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.22.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.22.1.png" alt="Description of your image">
</a>

Next we need to copy the contents to a notepad and then save the file as
`certificate_name.crt`

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.23.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.23.1.png" alt="Description of your image">
</a>

Pasting it into Notepad

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.24.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.24.1.png" alt="Description of your image">
</a>

Saving it as a .crt file name

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.25.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.25.1.png" alt="Description of your image">
</a>

Now go over to your Homarr dashboard and on the top right click / your username bubble / Manage

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.1.png" alt="Description of your image">
</a>

Next go to:
1. Tools
2. Certificates
3. (top right) select add certificate
4. Add your saved certifcate 
5. Click add.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.2.png" alt="Description of your image">
</a>

`showing the certificate added`

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.3.png" alt="Description of your image">
</a>

You should now see a valid certificate

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.26.4.png" alt="Description of your image">
</a>



### Adding Proxmox Stats Integration

Now we can go over to the Apps page and create a new app (this must be done before adding the integration)

Click new app

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.1.png" alt="Description of your image">
</a>

1. Now you can give it whatever name you want.
2. Search for the icon related to what you are connecting (in our case Proxmox)
3. grab the IP(URL) address of the Proxmox Node we want to see stats from.
4. Click create

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.2.png" alt="Description of your image">
</a>

Now go to the integrations tab:
1. New integration
2. Search and select Proxmox

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.3.png" alt="Description of your image">
</a>

***This is where people struggle because this is the major change from the old Homarr panel***

We are going to go grab the correct information from Proxmox for the username, token ID, API key, and realm. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.27.4.png" alt="Description of your image">
</a>

Over on Proxmox:

1. Go to the data center at the top
2. Go to API Token
3. We will see the username
4. We will see the Token name

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.1.png" alt="Description of your image">
</a>

Go back over to Homarr and fill out that respective information in the username and token ID field. Remember you also need to paste your API key you created under the (make a new API key) section. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.2.png" alt="Description of your image">
</a>

Lastly we just need to get the realm. 

Your realms are found under datacenter / realms. We are going ot be using PVE so our real will be PVE. 

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.3.png" alt="Description of your image">
</a>

like so:

Then test connection and connect.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.28.4.png" alt="Description of your image">
</a>

Click the Homarr logo at the top left to go back to your main dashboard OR (Boards on the far right, then select your dashboard from there)

On the top right click the pencil icon to edit your dashboard (it won't look like ours below)

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.29.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.29.1.png" alt="Description of your image">
</a>

Now you will notice all your icons have three dots on the top right and your board is now editable.

There will be a <kdb>+</kbd> icon on the top right, click that and then select new item.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.1.png" alt="Description of your image">
</a>

Under the items we need to select (System Health Monitoring) and click add to board

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.2.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.2.png" alt="Description of your image">
</a>

Now on our dashboard page we will see that new section with no data, click the three dots on the right and click edit item.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.3.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.3.png" alt="Description of your image">
</a>

From the integrations drop down menu select the integration we just created, and click save changes.

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.4.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.30.4.png" alt="Description of your image">
</a>

Now you can see we have the Proxmox stats on our dashboard!

<a href="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.31.1.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/Still 2025-02-23 111731_1.31.1.png" alt="Description of your image">
</a>

## Updating Homarr 1.0

To update, navigate to the directory with the *docker-compose.yaml* located. (This will need to be done using the sudo command or becoming the super user with *sudo su*)

Stop Homarr using 

```
docker compose down
```

Pull the newest image of Homarr using 

```
docker compose pull
```

Start Homarr again using the below command. (-d for detached mode - start in background)

```
docker compose up -d 
```

Delete the old image using (Warning: this also removes you other unused images - not just Homarr)

```
docker image prune
``` 

<a href="/images/EP22_homarr1.0upgrade/homarr update.png" class="image-expand">
    <img src="/images/EP22_homarr1.0upgrade/homarr update.png" alt="Description of your image">
</a>

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)