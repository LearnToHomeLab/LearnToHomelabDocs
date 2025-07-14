## Move Proxmox VMs & Containers to a New Storage Drive

**The reasons are long so you can skip this part if you want BUT:**

**Reasons why you may need to do this:**

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
    <p>
    upgrading to a larger or faster drive, running out of space, performance boost by migrating to SSDs or NVMe, replacing aging or failing hardware, decommissioning or removing a drive, reconfiguring storage pools or RAID setups, drive failure or errors, consolidating or organizing storage, centralizing VMs and containers for easier management, separating workloads based on performance or redundancy needs, cleaning up temporary or test storage, migrating to network or shared storage for HA or live migration, expanding a cluster with shared storage, preparing for server maintenance or upgrades, freeing up disks for replacement or reinstallation, optimizing backup and restore workflows, improving disaster recovery plans, balancing resource allocation across cluster nodes, capacity expansion for better scalability, hardware upgrade or replacement, disaster recovery, consolidation or optimization of resources.
    </p>
</div>

</body>
</html>

---------

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/2pky63gridE?si=xQwIRRmXCbYaxbSn" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

To migrate a Proxmox VM's disk from Ceph storage to local storage, follow these steps:

# Moving Proxmox VM Storage

1.  **Prepare the VM**
    - Shut down the VM (optional but recommended for stability).
    - Navigate to: `VM → Hardware → Hard Disk (e.g., scsi0)`.
2.  **Initiate Storage Move**
    - Click the **"Disk Action"** dropdown → Select **"Move Storage"**.
<a href="/images/EP39_MovingProxmoxVMStorage/image1.png" class="image-expand">
    <img src="/images/EP39_MovingProxmoxVMStorage/image1.png" alt="Description of your image">
</a>
    - In the pop-up:
        - **Target Storage**: Select your local storage (e.g., `local`, `local-lvm`).
<a href="/images/EP39_MovingProxmoxVMStorage/image2.png" class="image-expand">
    <img src="/images/EP39_MovingProxmoxVMStorage/image2.png" alt="Description of your image">
</a>
    - **Delete Source**: Check this to remove the original Ceph disk after migration.
    - Click **"Move Disk"**.
3.  **Monitor Progress**
    
    - Track the migration in the Proxmox task log.
    - Verify success in `Hardware → Hard Disk`; the disk path should now show the local storage.
    - You may also see an unused disk line item, go ahead and click that and remove/delete it. You should now be able to go back to the ceph cluster and remove it or see that it has already been removed.
<a href="/images/EP39_MovingProxmoxVMStorage/image3.png" class="image-expand">
    <img src="/images/EP39_MovingProxmoxVMStorage/image3.png" alt="Description of your image">
</a>
    - Shown below is the VM still displayed on the Ceph pool if you do not remove it, as shown in the image above. Note that a Ceph pool cannot be destroyed or changed until all container and VM disk images are removed.
<a href="/images/EP39_MovingProxmoxVMStorage/image4.png" class="image-expand">
    <img src="/images/EP39_MovingProxmoxVMStorage/image4.png" alt="Description of your image">
</a>
    
# Moving Container storage
    
Containers are slightly different and are required to be turned off. After the container is turned off, you will need to go to the resources tab (instead of the hardware tab found on the VMs). All other steps are the exact same as a virtual machine outside of the location where the container files are stored.

<a href="/images/EP39_MovingProxmoxVMStorage/image5.png" class="image-expand">
    <img src="/images/EP39_MovingProxmoxVMStorage/image5.png" alt="Description of your image">
</a>

# Common errors

If you get the following error:

## VM is locked (snapshot) (500)

<a href="/images/EP39_MovingProxmoxVMStorage/image6.png" class="image-expand">
    <img src="/images/EP39_MovingProxmoxVMStorage/image6.png" alt="Description of your image">
</a>

You may need to perform the following tasks WITHIN the Proxmox Shell CLI (not the container or VM CLI, the main Proxmox node CLI):

## Step-by-Step Solution

1.  **Identify the locked VM**
    - Note the VM ID (e.g., `100`) from Proxmox's web interface or run:
        
        ```
        qm list
        ```
        
2.  **Unlock the VM via CLI**
    - For KVM virtual machines (most common):
        
        ```
        qm unlock <VMID>
        ```
        
        Example for VM ID `100`:
        
        ```
        qm unlock 100
        ```
        
3.  **Verify unlock success**
    - Check the VM status:
        
        ```
        qm config <VMID>
        ```
        
        You should also see on the far left of your screen that the VM no longer has a lock icon next to its name.

## failed to update VM 119: unable to delete 'cephbackup:vm-119-disk-0' - volume is still in use (snapshot?) (500)

Make sure your VM is turned off first!

1.  **Unlock the VM**  
    First, release the snapshot lock:
    
    ```
    qm unlock <VMID>
    ```
    
    **Force-delete orphaned snapshots**  
    If the snapshot metadata exists but the underlying storage is missing:
    
    ```
    qm delsnapshot <VMID> <snapshot-name> --force
    ```
    
    Replace `<snapshot-name>` with the actual snapshot name (e.g., `BeforeDiskUpgrade`). The `--force` The flag bypasses missing storage checks.


## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)