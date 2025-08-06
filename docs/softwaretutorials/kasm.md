# Kasm

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/0oZLQZclnQs?si=j6HKS-eOJ-RwgywD" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

We will be using the following documentation to install KASM [here](https://kasmweb.com/docs/latest/index.html)

## Installing KASM

First, we are going to create a VM on Proxmox with at least their minimum requirements:

|     |     |
| --- | --- |
| **CPU** | 2 cores |
| **Memory** | 4GB |
| **Storage** | 50GB (SSD) |

Next, we are going to use their install script:

```
cd /tmp
curl -O https://kasm-static-content.s3.amazonaws.com/kasm_release_1.17.0.7f020d.tar.gz
tar -xf kasm_release_1.17.0.7f020d.tar.gz
sudo bash kasm_release/install.sh
```

After that, we can log in to KASM in our browser:

- Log in to the Web Application running on port 443

```
https://<WEBAPP_SERVER>:443
```

- The Default usernames are **admin@kasm.local** and **user@kasm.local**.

After installation, you will be presented with the passwords needed to log in just like the below screenshot:

<a href="/images/kasm/kasmpasswords.png" class="image-expand">
    <img src="/images/kasm/kasmpasswords.png" alt="Description of your image">
</a>

Super simple, I know! Take the time to look around Kasm or follow the video below if you are done watching ours!

After our tutorial, if you would like to go into more depth, you can check out KASMs video [here](https://www.youtube.com/watch?v=14JUXZITV1E&ab_channel=KasmWorkspaces)
