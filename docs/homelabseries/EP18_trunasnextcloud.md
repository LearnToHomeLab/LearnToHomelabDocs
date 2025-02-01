# NextCloud on TrueNas

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
    <p>This Article you are about to read is a stand alone tutorial but is also apart of our homelab series if you are following that. </p>
</div>

</body>
</html>

------------------------------------
## Warning 

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
    <p>If you are following this series from start to finish, this episode is a "repeat" in the manner that we have already covered NextCloud but this time we are hosting it on TrueNas and not Proxmox. 
The advantage you get here is your pictures are now saved within a RAID which gives you some fault tolerence to a failed drive so you don't lose your treasured pictures or vacations! </p>
</div>

</body>
</html>

(In reality, this is how I do it) but I wanted to share the Proxmox way for smaller homelabs or people with smaller budgets where they cannot afford multiple devices. 

***SO YOU CAN SKIP THIS EPISODE IF YOU ARE FOLLOWING THE COURSE AND WANTED TO USE THE PROXMOX WAY***

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/dClxLAW4SY0?si=GIKhNQbVT87LI8bN" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


## Installing NextCloud Steps

Go ahead and login to your TrueNas dashboard you can also learn how to install TrueNas from our previous episode [here](/homelabseries/EP17_truenasscale)

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.1.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.1.png" alt="Description of your image">
</a>

Select the "Apps" tab on the right and then click on "Check Available apps"

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.2.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.2.png" alt="Description of your image">
</a>

next search for (NextCloud) and select it. 

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.3.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.3.png" alt="Description of your image">
</a>

Click the blue isntall button.

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.4.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.4.png" alt="Description of your image">
</a>

Now a lot of this CAN be left the same but we have a couple things WE MUST FILL OUT. 

1. (Application name) give your NextCloud Container a name.
2. (Admin User) Create a username to login to NextCloud with.
3. (Admin Password) Set the password you are going to use to login.
4. (Host) This will be the IP address of your TrueNas machine, you can see the IP address of your TrueNas machine in your browsers URL. The example like ours is 192.168.50.221.
5. (Redia Password) Create a password.
6. (Database Password) Create a password.
7. (CPU) You can raise or lower how much of the CPU you want this NextCloud container to have access to.
8. (Memory in MB) You can raise or lower how much of the RAM you want this NextCloud container to have access to, ***more is better.***

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.5.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.5.png" alt="Description of your image">
</a>

**Second screenshot of the settings page settings that need to be changed as explained in the numbered list above.**

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.6.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.6.png" alt="Description of your image">
</a>

**Last screenshot of the settings page, select install.**

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.7.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.3.7.png" alt="Description of your image">
</a>

Wait until you see the status shown as running. You can then access your NextCloud instance by clicking the WebUI button.

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.4.1.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.4.1.png" alt="Description of your image">
</a>

If you need to delete your NextCloud Container you can also select it on the far left and an actions box will open, click that for options like delete.

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.4.2.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.4.2.png" alt="Description of your image">
</a>

After selecting the WebUI botton you will be on the login page, go ahead and put in the admin credentials you just created a minute ago. 

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.4.4.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.4.4.png" alt="Description of your image">
</a>

We can create new folders like the (TestFolder) shown below by clicking the (New) botton at the top. 

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.1.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.1.png" alt="Description of your image">
</a>

When you are in that folder you can click the new button in the middle of the screen to add pictures and documents. 

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.2.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.2.png" alt="Description of your image">
</a>

After images are within the folder you can see the new button is moved to the top. 

You can also add people from up top to access the whole folder or you can give people permissions for each file by selecting the icons on the far right of the image. 

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.3.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.3.png" alt="Description of your image">
</a>

You can share folders with others by sending them a link or controlling what users can access a folder. 

remember if you do not have tailscale setup, only users on the local network of the NAS will have access. 

<a href="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.4.png" class="image-expand">
    <img src="/images/EP18_trunasnextcloud/Still 2025-01-30 171223_1.5.4.png" alt="Description of your image">
</a>


## Conclusion

It is that simple, what did you think? 

I honestly love how simple it is to run your own personal Cloud for images/Documents! I hope you guys subscribe to our YouTube Channel for more content!




