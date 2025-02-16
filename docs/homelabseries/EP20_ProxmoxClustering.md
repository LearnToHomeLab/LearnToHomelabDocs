# How to Setup a Proxmox Cluster
In this episode we will cover how to setup a Proxmox Cluster and in the next video I will cover setting up Ceph pool storage for live migrations of VMs. 

## What is Clustering? 

Allows you to manage multiple Proxmox nodes from a single interface
        
Enables manual migration of VMs and containers between nodes
        
Does not automatically provide failover or resource management

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/G90Ro1rDLCU?si=PMH0mj7bf6vhrXJ9" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


## Setting up your Proxmox Cluster

1. First you you need to do is ensure you have TWO Proxmox Nodes setup. 

2. The orinal node CAN have VMs on it but the SECOND Node CANNOT!

3. If you need to learn how to install Proxmox on a machine please check out our 4th episode in this series [here](https://www.learntohomelab.com/homelabseries/EP4_proxmox/)

-------------------------------------------------------

We are going to start with your first machine (or your machine that has VMs already on it)

Go to datacenter, cluster, and click create cluster.

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.1.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.1.png" alt="Description of your image">
</a>

Name your cluster and ensure the IP matches your current nodes IP which can be found in your URL bar, then click create.

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.2.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.2.png" alt="Description of your image">
</a>

Wait for TASK OK then click exit on the top right.

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.3.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.3.png" alt="Description of your image">
</a>

Select join information at the top.

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.4.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.4.png" alt="Description of your image">
</a>

Copy the join information and then LOGIN to your SECOND node.

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.5.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.5.png" alt="Description of your image">
</a>

On your second node go to datacenter, cluster, and join cluster. 

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.6.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.6.png" alt="Description of your image">
</a>

Paste the join information, type the password in for your FIRST NODES root login, and ensure your cluster network IP matches your current nodes URL and that the peer IP is correct for your FIRST NODE. 

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.7.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.7.png" alt="Description of your image">
</a>

After you click join cluster you may need to wait 1-3 minutes for the two machines to communicate before it will let you login. Refresh your browser and then login.

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.8.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.3.8.png" alt="Description of your image">
</a>

There you have it, a Proxmox Cluster that will allow you to manage your machines from one interface. 

<a href="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.4.1.png" class="image-expand">
    <img src="/images/EP20_ProxmoxClustering/Still 2025-02-16 102109_1.4.1.png" alt="Description of your image">
</a>

## Conclusion

In the next episode we will cover how to create a Ceph Pool and get our cluster ready for live migrations. 

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)



