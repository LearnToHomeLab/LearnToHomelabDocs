# How to Setup Ceph on Proxmox and Perform Live VM Migration

In this video we will cover how to do live VM migration between Proxmox Nodes in a cluster using Ceph as the distributed data storage.

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/gg_6yAt661g?si=8cPM1Sxq5vvEpBYX" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Setting up a Ceph Storage Pool

Here are the following steps to create a ceph cluster:

1. Have dedicated storage for your ceph pool (ssd, HDD. CANNOT be the one you are already using because we are going to wipe it)


Ensure you have an extra SSD/HDD installed for your Ceph pool. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.1.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.1.png" alt="Description of your image">
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
    <p>The following commands will need to be done on EVERY node (cluster size dependent)</p>
</div>

</body>
</html>

Click on your node, go to Ceph, and click install Ceph.

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.2.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.2.png" alt="Description of your image">
</a>

We are going to use Reef (18.2) make sure you install the latest at the time you do this install and the No-Subcription option because we do not pay for Proxmox. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.3.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.3.png" alt="Description of your image">
</a>

On the next screen you will see a prompt during install, click enter for yes and wait for it to finish. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.4.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.3.4.png" alt="Description of your image">
</a>

When you see the following screen and the blue next button is now clickable, go to next.

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.4.1.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.4.1.png" alt="Description of your image">
</a>

Your install should do this by default but if not make sure it has the same network selected as the node, then click next. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.4.2.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.4.2.png" alt="Description of your image">
</a>

### Now we need to create the storage pool

Click on the node name, go to disks, select your dedicated storage device, and click wipe disk. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.5.1.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.5.1.png" alt="Description of your image">
</a>

Next go back to the ceph menu (click the drop down area next to the name ceph) and select OSD. Within OSD select the device you just wiped and click create. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.5.2.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.5.2.png" alt="Description of your image">
</a>

Next click the Pools menu below the OSD menu, click create on the top left, select the size of the pool based on how many nodes /OSD drives you have. We have two nodes and two drives so we are doing two. (leave PG autoscaler mode to on). 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.6.1.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.6.1.png" alt="Description of your image">
</a>

## How to Perform live migrations of VMs

So in order to perform a live migration your VM's storage has to be set to the Ceph pool storage. 

You will create a VM like any other VM BUT on the disks page you will select the storage option as your Ceph pool. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.1.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.1.png" alt="Description of your image">
</a>


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
    <p>You can edit old VM's and move their storage to the Ceph Pool so they can live migrate as well.</p>
</div>

</body>
</html>

### Removing local disk for live migration

Live migration will not work with a CD/DVD attached. You only need the CD/DVD attached for the initial install operating system file. 

1. Turn your machine off
2. Select the CD/DVD device under hardware
3. Click remove
4. Start your VM again. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.2.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.2.png" alt="Description of your image">
</a>

***Example of how live migration wont work with a local CD/DVD attached.***

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.3.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.3.png" alt="Description of your image">
</a>

***Example with the CD/DVD removed***

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.4.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.4.png" alt="Description of your image">
</a>

Now we can see live migraiton is possible with that CD/DVD removed and the VM running. Select the node you wish to move your VM to and click migrate. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.6.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.6.png" alt="Description of your image">
</a>

***Live feed of the migration***

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.7.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.7.png" alt="Description of your image">
</a>

We can now see the VM has moved to the other machine with virtually no down time. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.8.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.8.png" alt="Description of your image">
</a>

Now if you moved all your VM's to a different node you could go back and update your other node, take it off line for maintenance, fix a failing part, etc. without losing any uptime or having upset customers. 

<a href="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.9.png" class="image-expand">
    <img src="/images/EP21_ProxmoxCeph/Still 2025-02-18 105326_1.7.9.png" alt="Description of your image">
</a>

## Conclusion

That is it for this video, We covered:
1. How to wipe drives
2. How to create a Ceph Pool
3. How to live migrate VM's 
4. How to update other systems without disrupting the availability of our users.

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)