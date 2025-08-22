# Linux User Management Tutorial 2025

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/B832XYN46UM?si=S_1SQAmkWEQpBz-s" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Checkout this series here   
Check out videos in this playlist [here](https://www.youtube.com/playlist?list=PLAvgoEDVC5qGxD1JIioyofs2IL7XKUnkT)


## 1. Users and Groups

Linux manages system access through users and groups. Each user has a unique user ID (UID) and belongs to one or more groups identified by group IDs (GID). Permissions to files and processes are controlled by this system, ensuring security and access control on multi-user systems.

Example:

- Users have home directories typically in `/home/username`.
- Groups organize multiple users for easier permission management.

## 2. root

The root user (UID 0) is the superuser with unlimited access to the system. Normal users should avoid working as root to prevent accidental system damage. Instead, tools like `sudo` allow trusted users to run specific commands as root safely.

Command example:

- Run a command as root using sudo:
    
    ```
    sudo apt update
    ```
    
- Switch to root shell (less recommended):
    
    ```
    sudo su
    ```
    
- Switch back to normal user:
    
    ```
    su <username>
    ```
    

## 3. /etc/passwd

`/etc/passwd` is a system file listing all the user accounts. Each line represents a user account, containing fields such as username, UID, GID, user information, home directory, and login shell. It is readable by all users but does not contain password hashes.

View `/etc/passwd` contents:

```
cat /etc/passwd
```

The **general format** of `/etc/passwd` is:

```
username : password_placeholder : UID : GID : comment/gecos : home_directory : login_shell
```

Each field is broken down in the table below, with root as an example:

| **Field #** | **Value** | **Name / Field Description** | **Meaning in This Context** |
| --- | --- | --- | --- |
| 1   | `root` | **Username** | The login name of the account. This is the superuser account. |
| 2   | `x` | **Password placeholder** | Indicates the actual hashed password is stored in `/etc/shadow` (for security), not here. |
| 3   | `0` | **UID (User ID)** | Unique ID for the user. `0` means this account is the root superuser with full system permissions. |
| 4   | `0` | **GID (Group ID)** | Primary group ID. `0` refers to the `root` group from `/etc/group`. |
| 5   | `root` | **Comment / GECOS field** | A descriptive field, often the real name or account description. Here it’s simply “root.” |
| 6   | `/root` | **Home directory** | The root user’s personal home folder, where configs and files are stored. |
| 7   | `/bin/bash` | **Login shell** | The default shell program started when this account logs in — here, the GNU Bash shell. |

## 4. /etc/shadow

`/etc/shadow` stores encrypted passwords and account expiration information for users. It is readable only by root or users with proper privileges to protect password security.

View with root privilege:

```
sudo cat /etc/shadow
```

To understand what each section means for the shadow folder see the table below:

| **Field Number** | **Value** | **Meaning** |
| --- | --- | --- |
| 1   | root | Username — the account name. |
| 2   | *  | Password field — here `*` means the account is **locked** or has **no valid password** set. |
| 3   | 20134 | Last password change date — number of days since **Jan 1, 1970** (Unix epoch). |
| 4   | 0   | Minimum days before password can be changed — 0 means the password can be changed any time. |
| 5   | 99999 | Maximum days password is valid before requiring change — 99999 means password never expires. |
| 6   | 7   | Warning period — number of days before expiration to warn the user to change the password. |
| 7   | (empty) | Inactivity period — days after password expires before account is disabled (empty means disabled immediately or no inactivity setting). |
| 8   | (empty) | Account expiration date — number of days since Jan 1, 1970, when the account is disabled (empty means no expiration). |
| 9   | (empty) | Reserved field — currently unused. |

## 5. /etc/group

`/etc/group` lists all groups on the system and their members, making it easier to see which users belong to each group.

View `/etc/group`:

```
cat /etc/group
```

The general format of each line in `/etc/group` is:

```
group_name : password_placeholder : GID : member_list
```

## 6. User Management Tools

Linux provides several command-line tools to manage users and groups:

- Add a user:
    
    ```
    sudo useradd username
    ```
    
- Delete a user:
    
    ```
    sudo userdel username
    ```
    
- Modify a user (e.g., change username or home directory):
    
    ```
    sudo usermod -l newname oldname
    ```
    
- Add a group:
    
    ```
    sudo groupadd groupname
    ```
    
- Add user to group:
    
    ```
    sudo usermod -aG groupname username
    ```
    
- List user groups:
    
    ```
    groups username
    ```

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)