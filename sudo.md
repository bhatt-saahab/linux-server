# selected user ko ,sudo kuch power dena taki sudo ki power normal user use kar sake.

## Overview

The `sudo` command in Linux enables authorized users to execute commands with superuser (`root`) or another user’s privileges, as defined in the `/etc/sudoers` configuration file. Unlike `su`, which switches to another user’s session, `sudo` allows execution of specific commands without requiring a full session switch or the target user’s password, based on configured policies.

### Purpose

- **Controlled Privilege Escalation**: Allows users to run commands as `root` or other users securely.
- **Granular Permissions**: Configures specific commands, users, and hosts via `/etc/sudoers`.
- **Security**: Enhances system security by limiting access and logging actions.

---

(for debian based system)

Got it 👍 You wrote this for **RPM-based systems (CentOS/RedHat)**, but since **Kali is Debian-based (APT)** we need to adapt it.

Here’s the **Kali version** of your notes with equivalent commands:

---

# 🐉 Kali Linux – Installation and Package Management (APT-Based Systems)

---

## 🔍 Check if `sudo` is Installed

```bash
dpkg -l | grep sudo

```

- `dpkg -l` → lists installed packages
- `grep sudo` → filters only `sudo`

---

## 📦 Install `sudo` (if missing)

```bash
sudo apt update
sudo apt install sudo -y

```

---

## 📂 List Files Installed by `sudo` Package

```bash
dpkg -L sudo

```

---

## ⚙️ List `sudo` Configuration Files

```bash
dpkg -L sudo | grep etc

```

- Shows files under `/etc/` (like `/etc/sudoers`)

---

## 📖 List `sudo` Documentation Files

```bash
dpkg -L sudo | grep doc

```

---

# 📝 The `/etc/sudoers` File

- **Purpose**: Defines **who** can run **what** as **which user/group** on **which host**.
- **Safe Editing**: Always use `visudo` (to avoid breaking sudo).

```bash
sudo visudo
#it hlep to what we canged when we exit it ask there change in this line

```

👉 If you prefer `vim` or `nano`:

```bash
sudo EDITOR=vim visudo
sudo EDITOR=nano visudo

```

---

## 🔑 Key Sections of `/etc/sudoers`

### Root Privileges

```bash
root ALL=(ALL:ALL) ALL

```

- Root can run anything, anywhere, as anyone.

---

### Wheel / Sudo Group Privileges (Debian/Kali uses `sudo` group)

```bash
%sudo ALL=(ALL:ALL) ALL

```

- Any user in group `sudo` has full privileges.

---

### Specific User Privileges

```bash
armour ALL=(ALL:ALL) ALL
#user host =(kon se useer se run kar sakta he root,armour,emp1:optional group identity) allowed commands.
```

- User `armour` can run all commands as any user/group on any host.

---

### Group Privileges

```bash
%IT ALL=(ALL:ALL) ALL

%sudo ALL=(ALL)ALL #Debian / Ubuntu / Kali

%wheel ALL=(ALL)ALL # RedHat / CentOS / Fedora

#THIS DEFAULT GROUP IT HAVE ALL SUDO POWER , IF ANY USE IS MEMBER OF WHEEL GROUP IT ALSO LIKE SUDO .
```

- Members of `IT` group get full sudo access.

---

## ⚡ Syntax of Privilege Specification

```bash
USER HOST=(RUNAS_USER:RUNAS_GROUP) COMMANDS

```

- **USER** → user or `%group`
- **HOST** → host(s), often `ALL`
- **RUNAS_USER** → user to run as
- **RUNAS_GROUP** → group to run as (optional)
- **COMMANDS** → allowed commands

📌 Example:

```bash
emp1 ALL=(armour:EMP) /usr/sbin/fdisk

```

- `emp1` can run `fdisk` as **user `armour`** and **group `EMP`** on any host.

---

## 🔎 Viewing & Filtering `/etc/sudoers`

### Show Comment Lines

```bash
grep "^#" /etc/sudoers

```

### Show Non-Comment Lines

```bash
grep -v "^#" /etc/sudoers

```

### Show Active Config (no comments/blank lines)

```bash
grep -v "^#" /etc/sudoers | sed '/^$/d'

```

✔ Steps:

1. `grep -v "^#"` → remove comment lines
2. `sed '/^$/d'` → remove blank lines

---

Here’s how to create new users in **Kali (Debian-based):**

---

## 👤 Create a New User

```bash
sudo adduser emp1

```

- This will:
    - Create user `emp1`
    - Ask for password
    - Create home directory `/home/emp1`

---

## 👥 Add User to a Group (e.g., `sudo`)

If you want `emp1` to have **sudo privileges**:

```bash
sudo usermod -aG sudo emp1

```

- `aG` → append to group
- `sudo` → group with admin rights in Debian/Kali

---

## 👀 Verify User & Groups

Check which groups a user belongs to:

```bash
groups emp1

```

---

## 🔄 Switch Between Users

```bash
su - emp1

```

- `su -` → starts login shell as `emp1`

---

## 🗑️ Delete a User (if needed)

Without removing home folder:

```bash
sudo deluser emp1

```

With home folder:

```bash
sudo deluser --remove-home emp1

```

---

👉 Suggestion for practice:

- Keep your main user `bhatt` as admin.
- Create 2–3 test users (`emp1`, `emp2`, `armour`) and one test group (`IT`).
- Then, edit `/etc/sudoers` with different privileges for each.

---

Do you want me to prepare a **step-by-step sudoers practice lab** for you (like tasks: user1 can only run `ls`, user2 can run `fdisk`, group IT can run all)?

## (red hat system)

Installation and Package Management (RPM-Based Systems)

### Check if Sudo is Installed

```bash
rpm -q | grep sudo

```

### Install Sudo (if missing)

```bash
sudo yum install sudo

```

### List Files Installed by Sudo Package

```bash
rpm -ql sudo

```

### List Sudo Configuration Files

```bash
rpm -qc sudo

```

### List Sudo Documentation Files

```bash
rpm -qd sudo

```

---

## The `/etc/sudoers` File

- **Purpose**: Controls who can run specific commands as which users or groups on designated hosts.
- **Editing**: Must be edited using `visudo` to prevent syntax errors and ensure file integrity.
    
    ```bash
    visudo
    
    ```
    
    - Specify editor (e.g., Vim):
        
        ```bash
        EDITOR=vim visudo
        
        ```
        

### Key Sections of the `/etc/sudoers` File

### User and Group Privileges

- **Root Privileges**:
    
    ```bash
    root ALL=(ALL) ALL
    
    ```
    
    - Root can run any command on any host as any user.
- **Wheel Group Privileges**:
    
    ```bash
    %wheel ALL=(ALL) ALL
    
    ```
    
    - Members of the `wheel` group have full sudo access.
- **Specific User Privileges**:
    
    ```bash
    armour ALL=(ALL) ALL
    
    ```
    
    - User `armour` can run all commands as any user on any host.
- **Group Privileges**:
    
    ```bash
    %IT ALL=(ALL) ALL
    
    ```
    
    - Members of the `IT` group have full sudo access.

### Syntax of Privilege Specification

```bash
USER HOST=(RUNAS_USER:RUNAS_GROUP) COMMANDS

```

- **USER**: User or group (e.g., `%groupname`) granted access.
- **HOST**: Host(s) where the rule applies (`ALL` for any host).
- **RUNAS_USER**: User identity to assume (e.g., `root`, `armour`).
- **RUNAS_GROUP**: Optional group identity to assume.
- **COMMANDS**: Allowed commands or command aliases.
- **Example**:
    
    ```bash
    emp1 ALL=(armour:EMP) /usr/sbin/fdisk
    
    ```
    
    - User `emp1` can run `/usr/sbin/fdisk` as user `armour` and group `EMP` on any host.

---

## Viewing and Filtering `/etc/sudoers`

- **Show Comment Lines**:
    
    ```bash
    grep "^#" /etc/sudoers
    
    ```
    
- **Show Non-Comment Lines**:
    
    ```bash
    grep -v "^#" /etc/sudoers
    
    ```
    
- **Show Active Configuration (Exclude Comments and Empty Lines)**:
    
    ```bash
    cat /etc/sudoers | grep -v "^#" | sed '/^$/d'
    
    ```
    
    - Alternative (more efficient, without `cat`):
        
        ```bash
        grep -v "^#" /etc/sudoers | sed '/^$/d'
        
        ```
        
    - Steps:
        1. `grep -v "^#"` removes lines starting with `#`.
        2. `sed '/^$/d'` deletes empty lines.

---

## Default Security and Environment Settings

The `/etc/sudoers` file includes `Defaults` directives to configure security and environment behavior:

1. `Defaults !visiblepw`: Prevents `sudo` from running if password input cannot be hidden.
2. `Defaults always_set_home`: Sets `$HOME` to the target user’s home directory.
3. `Defaults match_group_by_gid`: Matches groups by GID for consistency.
4. `Defaults always_query_group_plugin`: Ensures group plugins are queried.
5. `Defaults env_reset`: Clears environment variables, preserving only those in `env_keep`.
6. `Defaults env_keep = "COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS"`: Preserves listed environment variables.
7. `Defaults env_keep += "MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE"`: Adds more variables to preserve.
8. `Defaults env_keep += "LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES"`: Further environment variables.
9. `Defaults env_keep += "LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE"`: Additional variables.
10. `Defaults env_keep += "LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY"`: Final preserved variables.
11. `Defaults secure_path = /sbin:/bin:/usr/sbin:/usr/bin`: Restricts `PATH` to trusted directories.

---

## Useful Sudo Commands

### Check Allowed Commands (Current User)

- List commands the current user can run:
or
    
    ```bash
    sudo -l
    
    ```
    
    ```bash
    sudo --list
    
    ```
    

### Run Commands as Root

- Check user ID as `root`:
    
    ```bash
    sudo id
    
    ```
    
- List disk partitions as `root`:
    
    ```bash
    sudo fdisk -l
    
    ```
    

### Run Commands as Another User

- Check user ID as `armour`:
    
    ```bash
    sudo -u armour id
    
    ```
    
- Create directory as `armour`:
    
    ```bash
    sudo --user=armour mkdir d1
    
    ```
    
- Check identity as `infosec`:
    
    ```bash
    sudo -u infosec whoami
    
    ```
    

### Run Commands as Another User and Group

- Check ID as user `armour` and group `IT`:
    
    ```bash
    sudo -u armour -g IT id
    
    ```
    
- Create directory as user `infosec` and group `IT`:
    
    ```bash
    sudo --user=infosec --group=IT mkdir /tmp/d2
    
    ```
    

### Background Command Execution

- Run command as `infosec` in the background:
    
    ```bash
    sudo -b --user=infosec id
    
    ```
    

### Start Login Shell as Another User

- Start a login shell as `infosec`:
or
    
    ```bash
    sudo --user=infosec --login
    
    ```
    
    ```bash
    sudo --user=infosec -i
    
    ```
    

### List Files and Directories as Another User

- List files in `/home/it1/` as user `it1`:
    
    ```bash
    sudo -u it1 ls -lh /home/it1/
    
    ```
    

---

## Managing Sudo Privileges via Groups

### Add User to `wheel` Group (Enable Sudo Access)

- Using `gpasswd`:
    
    ```bash
    gpasswd -a armour wheel
    
    ```
    
- Using `usermod`:
    
    ```bash
    usermod -aG wheel it1
    
    ```
    

### Remove User from `wheel` Group

```bash
gpasswd -d armour wheel

```

### List Members of `wheel` Group

```bash
gpasswd wheel

```

---

## Environment Security Defaults Summary

- **`env_reset`**: Clears the environment, preserving only whitelisted variables (`env_keep`).
- **`always_set_home`**: Sets `$HOME` to the target user’s home directory.
- **`secure_path`**: Restricts the `PATH` environment to trusted directories (`/sbin:/bin:/usr/sbin:/usr/bin`).
- **`visiblepw`**: Prevents `sudo` from running if password input cannot be hidden, enhancing security.

---

## Summary

The `sudo` command is a critical tool for Linux system administration, providing controlled privilege escalation through the `/etc/sudoers` file. It supports granular permissions, secure environment management, and flexible command execution as different users or groups. Proper configuration and use of `visudo` ensure safe and effective privilege management, making `sudo` essential for secure system operations.
