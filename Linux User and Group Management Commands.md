

## 1. **userdel** - Delete User Accounts

The `userdel` command removes a user account from the system.

- **Display last 3 lines of account-related files**:
    
    ```bash
    tail -v -n 3 /etc/passwd /etc/shadow /etc/group /etc/gshadow
    
    ```
    
    - Shows the last 3 lines of `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow` with file names.
- **Delete user `u15` without removing home directory or mail spool**:
    
    ```bash
    userdel u15
    
    ```
    
    - Removes user `u15` from system files but leaves their home directory and mail spool intact.
- **Delete user `u1` and remove home directory and mail spool**:
    
    ```bash
    userdel -r u1
    
    ```
    
    - The `r` option deletes the user’s home directory and mail spool along with the user account.
- **Forcefully delete user `u16` with home directory and mail spool**:
    
    ```bash
    userdel -f -r u16
    
    ```
    
    - The `f` option forces deletion even if the user is logged in or their home directory is in use.
    - The `r` option removes the home directory and mail spool.

---

## 2. **deluser** - Delete User Accounts (Debian-based Systems)

The `deluser` command is used on Debian-based systems to remove user accounts.

- **Remove user `u15` without deleting home directory**:
    
    ```bash
    deluser u15
    
    ```
    
    - Deletes user `u15` but retains their home directory.
- **Remove user `u1` and delete home directory and mail spool**:
    
    ```bash
    deluser --remove-home u1
    
    ```
    
    - The `-remove-home` option deletes the user’s home directory and mail spool.
- **Remove user `u16` with home directory and from all groups**:
    
    ```bash
    deluser --remove-home --remove-all-files u16
    
    ```
    
    - Deletes user `u16`, their home directory, and removes them from all groups they belong to.
- **Remove user `u17` from the `developers` group**:
    
    ```bash
    deluser u17 developers
    
    ```
    
    - Removes user `u17` from the supplementary group `developers`.
- **Forcefully remove user `u18`**:
    
    ```bash
    deluser --force u18
    
    ```
    
    - Forces removal of user `u18`, even if they are currently logged in.

---

## 3. **passwd** - Manage User Passwords

The `passwd` command manages user passwords and their status.

- **Search for `root` entries in account and group files**:
    
    ```bash
    grep root /etc/passwd /etc/shadow /etc/group /etc/gshadow
    
    ```
    
    - Searches for entries containing "root" in the specified files.
- **Change password for the current user**:
    
    ```bash
    passwd
    
    ```
    
    - Prompts the currently logged-in user to change their password.
- **Display last 4 lines of user and group files**:
    
    ```bash
    tail -v -n 4 /etc/passwd /etc/shadow /etc/group /etc/gshadow
    
    ```
    
    - Shows the last 4 lines of the specified files with file names.
- **Change password for user `u1`**:
    
    ```bash
    passwd u1
    
    ```
    
    - Changes the password for user `u1`.
- **Delete password for user `u1`**:
    
    ```bash
    passwd -d u1
    
    ```
    
    - Removes the password for `u1`, allowing passwordless login (if permitted by system policy).
- **Lock user `u1`’s password**:
    
    ```bash
    passwd -l u1
    
    ```
    
    - Locks the password for `u1`, disabling password-based login.
- **Unlock user `u1`’s password**:
    
    ```bash
    passwd -u u1
    
    ```
    
    - Unlocks the password for `u1`, enabling password-based login again.
- **Force password change on next login and unlock account**:
    
    ```bash
    passwd -f -u u1
    
    ```
    
    - Forces user `u1` to change their password on next login and unlocks their account.
- **Show password status for user `u9`**:
    
    ```bash
    passwd -S u9
    
    ```
    
    - Displays the password status for user `u9` (e.g., locked, unlocked, or no password).
- **Generate MD5 hash for password**:
    
    ```bash
    openssl passwd -1
    
    ```
    
    - Generates an MD5 hash for a password using OpenSSL.
- **Set encrypted password for user `user3`**:
    
    ```bash
    usermod -p '$1$JafiDMw0$Q6VF2IqPINwOG6CvmKV.V0' user3
    
    ```
    
    - Sets an encrypted MD5 password for `user3` using `usermod`.
- **Generate MD5 hash with custom salt**:
    
    ```bash
    openssl passwd -1 -salt asdfgh
    
    ```
    
    - Generates an MD5 hash with the custom salt `asdfgh`.
- **Generate DES crypt password with custom salt**:
    
    ```bash
    openssl passwd -crypt -salt asdfgh 123456
    
    ```
    
    - Generates a traditional DES crypt password for `123456` with the salt `asdfgh`.
- **Generate DES password hash**:
    
    ```bash
    openssl passwd 12345
    
    ```
    
    - Generates a DES password hash for the input `12345`.
- **View and edit `/etc/passwd`**:
    
    ```bash
    vim /etc/passwd
    
    ```
    
    - Opens `/etc/passwd` for manual inspection or editing of user records.
    - **Example line**:
        
        ```
        armour:nneW/qmjM5zmY:1000:1000:Armour:/home/armour:/bin/bash
        
        ```
        
        - Fields: `username:password:UID:GID:comment:home_directory:shell`.
- **View and edit `/etc/shadow`**:
    
    ```bash
    vim /etc/shadow
    
    ```
    
    - Opens `/etc/shadow` for manual inspection or editing of encrypted password fields.
    - **Example line**:
        
        ```
        armour:dJCqiFN5pbdy2::0:99999:7:::
        
        ```
        
        - Fields: `username:encrypted_password:last_change:min_days:max_days:warn_days:inactive_days:expire_date:reserved`.

---

## 4. **groupadd** - Create New Groups

The `groupadd` command creates new groups on the system.

- **Display help information**:
    
    ```bash
    groupadd --help
    groupadd -h
    
    ```
    
    - Shows help information for the `groupadd` command.
- **Create group `IT`**:
    
    ```bash
    groupadd IT
    
    ```
    
    - Creates a group named `IT`.
- **Create group `EMP`**:
    
    ```bash
    groupadd EMP
    
    ```
    
    - Creates a group named `EMP`.
- **Create group `SELES`**:
    
    ```bash
    groupadd SELES
    
    ```
    
    - Creates a group named `SELES`.
- **Create group `demo` with GID 1030**:
    
    ```bash
    groupadd -g 1030 demo
    
    ```
    
    - Creates a group named `demo` with the specified GID `1030`.
- **Create group `demo2` with duplicate GID 1030**:
    
    ```bash
    groupadd -g 1030 -o demo2
    
    ```
    
    - The `o` option allows creating `demo2` with a non-unique GID `1030`.
- **Create group `demo3` with encrypted password**:
    
    ```bash
    groupadd -p Sevs2NnMDrR52 demo3
    
    ```
    
    - Creates group `demo3` with the encrypted password `Sevs2NnMDrR52`.
- **Create group `demo4` with encrypted password**:
    
    ```bash
    groupadd -p '$1$lsPUtmoT$B.yzyVcDquljgIQaRk1YW.' demo4
    
    ```
    
    - Creates group `demo4` with the encrypted password.
- **Create system group `sysgrp`**:
    
    ```bash
    groupadd -r sysgrp
    
    ```
    
    - Creates a system group named `sysgrp` with a GID in the system range.

---

## 5. **groupmod** - Modify Existing Groups

The `groupmod` command modifies group attributes.

- **Display help information**:
    
    ```bash
    groupmod --help
    
    ```
    
    - Shows help information for the `groupmod` command.
- **Change GID of group `demo` to 1028**:
    
    ```bash
    groupmod -g 1028 demo
    
    ```
    
    - Changes the GID of the `demo` group to `1028`.
- **Change GID of group `demo` to 1030 (non-unique)**:
    
    ```bash
    groupmod -g 1030 demo
    
    ```
    
    - Changes the GID of `demo` to `1030`, allowing non-unique GID with `o` (if needed).
- **Rename group `demo` to `DEMO1`**:
    
    ```bash
    groupmod -n DEMO1 demo
    
    ```
    
    - Renames the group `demo` to `DEMO1`.
- **Set encrypted password for group `demo`**:
    
    ```bash
    groupmod -p Sevs2NnMDrR52 demo
    
    ```
    
    - Sets the encrypted password for the `demo` group to `Sevs2NnMDrR52`.

---

## 6. **groupdel** - Delete Groups

The `groupdel` command deletes groups from the system.

- **Display help information**:
    
    ```bash
    groupdel --help
    groupdel -h
    
    ```
    
    - Shows help information for the `groupdel` command.
- **Delete group `demo`**:
    
    ```bash
    groupdel demo
    
    ```
    
    - Deletes the group `demo` from the system.

---

## 7. **gpasswd** - Manage Group Membership and Passwords

The `gpasswd` command manages group passwords and membership.

- **Display help information**:
    
    ```bash
    gpasswd --help
    gpasswd -h
    
    ```
    
    - Shows help information for the `gpasswd` command.
- **Show group membership for users**:
    
    ```bash
    groups root
    groups armour
    groups u1
    
    ```
    
    - Displays the groups that `root`, `armour`, and `u1` belong to.
- **Set password for group `HR`**:
    
    ```bash
    gpasswd HR
    
    ```
    
    - Sets a password for the `HR` group.
- **Add user `armour` to group `IT`**:
    
    ```bash
    gpasswd -a armour IT
    
    ```
    
    - Adds user `armour` to the `IT` group.
- **Add user `armour` to group `EMP`**:
    
    ```bash
    gpasswd -a armour EMP
    
    ```
    
    - Adds user `armour` to the `EMP` group.
- **Add user `u1` to group `IT`**:
    
    ```bash
    gpasswd -a u1 IT
    
    ```
    
    - Adds user `u1` to the `IT` group.
- **Add user `u1` to group `mgr26mgr`**:
    
    ```bash
    gpasswd -a u1 mgr
    
    ```
    
    - Adds user `u1` to the `mgr` group.
- **Add user `armour` to group `demo2`**:
    
    ```bash
    gpasswd -a armour demo2
    
    ```
    
    - Adds user `armour` to the `demo2` group.
- **Add multiple users to group `SELES`**:
    
    ```bash
    gpasswd -M armour,u1,u2,u4 SELES
    
    ```
    
    - Adds users `armour`, `u1`, `u2`, and `u4` to the `SELES` group.
- **Add multiple users to group `admin1`**:
    
    ```bash
    gpasswd -M u2,u3,u4 admin1
    
    ```
    
    - Adds users `u2`, `u3`, and `u4` to the `admin1` group.
- **Set password for group `armour`**:
    
    ```bash
    gpasswd armour
    
    ```
    
    - Sets a password for the `armour` group.
- **Remove user `armour` from group `SELES`**:
    
    ```bash
    gpasswd -d armour SELES
    
    ```
    
    - Removes user `armour` from the `SELES` group.
- **Remove user `armour` from group `root`**:
    
    ```bash
    gpasswd -d armour root
    
    ```
    
    - Removes user `armour` from the `root` group.

---

These notes cover all the provided commands and their details, organized systematically to ensure clarity and completeness. Let me know if you need further clarification or additional details!
