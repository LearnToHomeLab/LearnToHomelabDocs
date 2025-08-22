# Linux Permissions Tutorial 2025

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/7hA7QBnozmE?si=VUR5G3EGAxBNggi5" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## 1. File Permissions

Linux files have permissions defining who can read, write, or execute them. Permissions are split into three sets:

- **User** (owner)
- **Group** (group members)
- **Others** (everyone else)

Permissions appear in the format:  
`-rwxr-xr-x`

- The first character indicates file type (`-` for file, `d` for directory).
- Then three sets of `rwx` refer to user, group, and others.
- `r` = read, `w` = write, `x` = execute, `-` = no permission.

Instead of typing rwx you can also use numbers based on the table below:

| Number | Permission |
| --- | --- |
| 4   | Read |
| 2   | Write |
| 1   | Execute |

Example:

```
ls -l example.txt
```

## 2. Chmod Modifying Permissions

Use `chmod` to add (`+`), remove (`-`), or set permissions directly (numeric mode).

- Add executable permission to the user:
    
    ```
    chmod u+x myfile.txt
    ```
    
- Remove executable permission from the group:
    
    ```
    chmod g-x myfile.txt
    ```
    
- Set exact permissions with numeric mode (e.g., `755`):
    
    ```
    chmod 755 myfile.txt
    ```
    
    - 7 = read+write+execute (4+2+1) for user
    - 5 = read+execute (4+1) for group and others

## 3. Ownership Permissions

Files are owned by a user and a group. To view ownership:

```
ls -l myfile.txt
```

Change ownership with `chown`:

- Change owner:
    
    ```
    sudo chown alice myfile.txt
    ```
    
- Change owner and group:
    
    ```
    sudo chown alice:developers myfile.txt
    ```
    
- Change group only:
    
    ```
    sudo chgrp developers myfile.txt
    ```
    

## 4. Umask

`umask` controls the **default** permissions for newly created files or directories by masking **out permissions (meaning we are SUBTRACTING permissions)**. A `umask` of `0022` removes write permission for group and others by default.

Here is a table on how permissions work. The top table is more traditional for chmod, well the second table is usually what is used with Umask.

| Number | Permission |
| --- | --- |
| 4   | Read |
| 2   | Write |
| 1   | Execute |

| Read | Write | Execute | Total Value | Symbolic Equivalent: |
| --- | --- | --- | --- | --- |
| 0   | 0   | 0   | **0** |     |
| 0   | 0   | **1** | **1** | **x** |
| 0   | **2** | 0   | **2** | **w** |
| 0   | **2** | **1** | **3** | **wx** |
| **4** | 0   | 0   | **4** | **r** |
| **4** | 0   | **1** | **5** | **rx** |
| **4** | **2** | 0   | **6** | **rw** |
| **4** | **2** | **1** | **7** | **rw** |

<a href="/images/EP4_LinuxPermissions/linux_permissions.drawio.png" class="image-expand">
    <img src="/images/EP4_LinuxPermissions/linux_permissions.drawio.png" alt="Description of your image">
</a>

View your current mask:

```
umask
```

Set a new mask (temporary for session):

```
umask 027
```

This means new files will have permissions masked accordingly (e.g., 750 for directories).

### Set Permanent Umask for One User

Edit the user's shell startup files in their home director

Example if you are logged in as the root user controlling accounts:

```
sudo nano /home/<user>/.bashrc (.profile, .bash_profile)
```

these may include:

- `~/.bashrc` (For Bash shell, most common)
    
    ```
    sudo nano ~/.bashrc
    ```
    
- `~/.profile` (For login shells)
    
    ```
    sudo nano ~/.profile
    ```
    
- `~/.bash_profile` (Sometimes preferred in Bash)
    
    ```
    sudo nano ~/.bash_profile
    ```
    

Add the following line to the end of one of these files:

```
umask 027   # Example, pick your required umask value
```

After saving, the new umask will apply for all new shells and logins by that user. It affects only newly created files and directories, not existing ones. The change takes effect at the next login or when the terminal is restarted

## 5. Setuid (Set User ID)

The setuid bit allows users to run an executable with the permissions of the file owner (usually root). It is indicated by `s` in the user execute permission place.

Example: Check setuid bit on `passwd`:

```
ls -l /usr/bin/passwd
```

Set the setuid bit:

```
sudo chmod u+s <program you want to allow executible permissions>
```

## 6. Setgid (Set Group ID)

The setgid bit allows users to run an executable with the permissions of the group owner or lets files created in a directory inherit the directory’s group. It appears as `s` in the group execute position.

Set setgid on a directory:

```
sudo chmod g+s </shared-directory full path>
```

Files created inside inherit the group ownership of the directory.

## 7. Process Permissions

Processes run with the permissions of the user who started them. Permissions determine if a process can read/write/execute files or access system resources. To check a process’s user, use:

```
ps -u username
```

You can also check process capabilities related to security policies, but generally, processes inherit file permissions from their user identity.

## 8. The Sticky Bit

When set on a directory, the sticky bit prevents users from deleting or renaming files owned by others within that directory. It appears as a `t` in the others’ execute bit position.

Example directory with sticky bit:

```
ls -ld /tmp
```

Set sticky bit on a directory:

```
sudo chmod +t /shared-directory
```

This ensures only file owners (or root) can delete or rename files inside.

## Checkout this series here   
Check out videos in this playlist [here](https://www.youtube.com/playlist?list=PLAvgoEDVC5qGxD1JIioyofs2IL7XKUnkT)

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)