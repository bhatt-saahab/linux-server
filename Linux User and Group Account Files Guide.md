Here's your topic **"User and Group Management in Linux"** rewritten in an **attractive, clear, and complete format** with colorful formatting using emojis and headings for easy study:

---

## 🧑‍💻 **User and Group Management in Linux**

Linux is a **multi-user OS**, meaning multiple users can operate the system simultaneously. Managing users and groups ensures secure and organized access to system resources.

---

### 👤 **Users in Linux**

A **user account** defines:

- Who can log in
- What files and commands the user can access

### 📦 Components of a User Account:

| 🔹 **Component** | 🔍 **Description** |
| --- | --- |
| 👤 Username | Unique name identifying the user (e.g., `sachin`, `admin`) |
| 🆔 UID | **User ID**: Unique number assigned to each user |
| 🔸 `0` = root |  |
| 🔸 `1–999` = system users |  |
| 🔸 `1000+` = normal users |  |
| 👥 GID | **Group ID**: Primary group the user belongs to |
| 🏠 Home Directory | Default directory for the user (e.g., `/home/sachin`) |
| 💻 Shell | Default command-line interface (e.g., `/bin/bash`) |
| 🔐 Password | Encrypted, stored in `/etc/shadow` |

---

### 📂 **Important System Files for User Management**

| 📁 **File** | 🧾 **Purpose** |
| --- | --- |
| `/etc/passwd` | Stores user info: username, UID, GID, home, shell |
| `/etc/shadow` | Stores encrypted passwords & password aging data |
| `/etc/group` | Stores group names, GIDs, and members |
| `/etc/gshadow` | Secure file for group passwords and admin group privileges |
| `/etc/login.defs` | Default config settings for user account creation |

---

### 🧑‍🤝‍🧑 **Types of User Accounts**

1. 🛠️ **System Accounts**
    
    For system processes and services (e.g., `nobody`, `daemon`)
    
2. 👨‍💼 **Regular User Accounts**
    
    For actual users to log in and use the system
    
3. 📦 **Service Accounts**
    
    For software, daemons, and applications with limited permissions
    

---

### ⚙️ **What is a Daemon in Linux?**

A **daemon** is a **background process** that performs essential system functions without direct user input.

- Runs silently in the background
- Often ends with **`d`**, like:
    - `sshd` – SSH service
    - `cron` – Task scheduler
    - `systemd` – System manager

---

✅ **Summary:**

- Linux user & group management is central to system security.
- Accounts are defined using `UID`, `GID`, and configuration files like `/etc/passwd` and `/etc/shadow`.
- **Daemons** automate and support core OS tasks.

---

---

## 1. /etc/passwd - Linux User Account File

The `/etc/passwd` file stores basic user account information on Linux systems. Each line represents a single user in a colon-separated format, accessible to all users but editable only by root.

### Format of /etc/passwd

Each line follows the format: `username:x:UID:GID:comment:home_directory:shell`

| Field No. | Field Name | Description |
| --- | --- | --- |
| 1 | username | Login name (e.g., `root`, `armour`) |
| 2 | x | Placeholder indicating password is in `/etc/shadow` |
| 3 | UID | User ID (`0` for root, `1000+` for normal users) |
| 4 | GID | Primary group ID |
| 5 | comment | GECOS field (user's real name or other info) |
| 6 | home_directory | Default login directory (e.g., `/home/armour`) |
| 7 | shell | Default shell (e.g., `/bin/bash`, `/sbin/nologin`) |

> 🔵 Note: The x in the password field ensures passwords are securely stored in /etc/shadow. System or service accounts often use /sbin/nologin to prevent shell access.
> 

### Example Entry Breakdown

Example: `root:x:0:0:root:/root:/bin/bash`

| Field | Value | Description |
| --- | --- | --- |
| Username | `root` | Superuser account |
| Password | `x` | Password stored in `/etc/shadow` |
| UID | `0` | User ID for root |
| GID | `0` | Group ID for root |
| Comment | `root` | GECOS (optional description) |
| Home Dir | `/root` | Home directory |
| Shell | `/bin/bash` | Default login shell |

### Sample /etc/passwd Entries

| User | UID | GID | Comment | Home Directory | Shell |
| --- | --- | --- | --- | --- | --- |
| daemon | 2 | 2 | daemon | /sbin | /sbin/nologin |
| sshd | 74 | 74 | Privilege-separated SSH | /usr/share/empty.sshd | /usr/sbin/nologin |
| apache | 48 | 48 | Apache | /usr/share/httpd | /sbin/nologin |
| armour | 1000 | 1000 | Armour Infosec | /home/armour | /bin/bash |

> 🟢 Note: System accounts (e.g., daemon, sshd, apache) typically have low UIDs (<1000) and use /sbin/nologin for security. User accounts start at UID 1000+.
> 

### Viewing /etc/passwd

| Command | Description |
| --- | --- |
| `cat /etc/passwd` | Show all entries |
| `awk -F: '$3>=1000 {print $1}' /etc/passwd` | Show human users (UID ≥ 1000) |
| `grep '^username:' /etc/passwd` | Search for a specific user |

> 🟡 Note: The corrected awk command removes erroneous syntax ($365534) and uses proper filtering for human users.
> 

### Editing /etc/passwd

| Command | Description |
| --- | --- |
| `sudo vim /etc/passwd` | Open file safely with root privileges |
| `sudo cp /etc/passwd /etc/passwd.bak` | Backup before editing |
| `sudo vipw` | Use safe editor to prevent corruption |

> 🔴 Warning: Never delete or corrupt /etc/passwd, as it can render the system unbootable. Avoid manual edits; prefer useradd, usermod, or userdel.
> 

> 🟢 Best Practice: Assigning UID 0 to non-root users grants superuser privileges and is a security risk. Always use vipw for safe editing.
> 

---

## 2. /etc/shadow - Secure User Passwords File

The `/etc/shadow` file stores encrypted user passwords and password aging policies. It is readable only by root and is critical for system authentication.

### Format of /etc/shadow

Each line follows the format: `username:encrypted_password:last_change:min:max:warn:inactive:expire:unused`

| Field No. | Field Name | Description |
| --- | --- | --- |
| 1 | username | Login name |
| 2 | encrypted_password | Password hash or placeholder (`*`, `!`, `!!`) |
| 3 | last_change | Days since Jan 1, 1970 when password was last changed |
| 4 | min | Minimum days before password can be changed |
| 5 | max | Maximum days a password is valid |
| 6 | warn | Days before expiry to warn user |
| 7 | inactive | Days after expiry until account is disabled |
| 8 | expire | Account expiration date (days since epoch) |
| 9 | unused | Reserved for future use |

> 🔵 Note: A password field of *, !, or !! disables password-based login, often used for system accounts.
> 

### Password Hash Types

The encrypted password field uses the format: `$type$salt$hashed_password`

| Type Prefix | Algorithm | Notes |
| --- | --- | --- |
| `$1$` | MD5 | Insecure, avoid in modern systems |
| `$2a$` | Blowfish | Used in some BSD systems |
| `$2$` | Eksblowfish | Variant of Blowfish |
| `$5$` | SHA-256 | Common in older systems |
| `$6$` | SHA-512 | Default on most modern systems |

> 🟢 Note: SHA-512 ($6$) is the recommended hash algorithm for security. MD5 ($1$) is deprecated due to vulnerabilities.
> 

### Example Entry Breakdown

Example: `daemon:*:17110:0:99999:7:::`

| Field | Value | Description |
| --- | --- | --- |
| Username | `daemon` | System user |
| Password | `*` | No login allowed |
| Last Change | `17110` | Days since epoch (e.g., `date -d "1970-01-01 +17110 days"`) |
| Min Age | `0` | Can change password any time |
| Max Age | `99999` | Password never expires |
| Warn | `7` | Warn 7 days before expiration |
| Inactive | (empty) | Not set |
| Expire | (empty) | Not set |
| Unused | (empty) | Reserved |

### Useful Commands

| Command | Description |
| --- | --- |
| `chage -l username` | View password aging settings |
| `chage -M 90 -W 7 -m 1 username` | Set password policy (max 90 days, warn 7 days, min 1 day) |
| `grep PASS /etc/login.defs` | View password policy defaults |
| `grep ENCRYPT_METHOD /etc/login.defs` | Check encryption algorithm (e.g., SHA-512) |

> 🟡 Note: The corrected grep command uses ENCRYPT_METHOD instead of SHA for accuracy in checking the encryption algorithm.
> 

> 🟢 Best Practice: Regularly review /etc/login.defs to ensure secure password policies (e.g., SHA-512, reasonable max age).
> 

---

## 3. /etc/group - Linux Group Account File

The `/etc/group` file defines group memberships, used to manage permissions and access controls for users collectively.

### Format of /etc/group

Each line follows the format: `group_name:x:GID:user_list`

| Field No. | Field Name | Description |
| --- | --- | --- |
| 1 | group_name | Name of the group (e.g., `wheel`, `sshd`) |
| 2 | x | Placeholder for encrypted group passwords (rarely used) |
| 3 | GID | Group ID, a unique numeric identifier |
| 4 | user_list | Comma-separated list of group members (can be empty) |

> 🔵 Note: Group passwords are rarely used and are typically stored in /etc/gshadow if needed.
> 

### Example Entries

| Group Name | GID | Members |
| --- | --- | --- |
| root | 0 | (empty) |
| daemon | 2 | (empty) |
| sshd | 74 | (empty) |
| apache | 48 | (empty) |
| armour | 1000 | armour |

### Breakdown of Entry: `armour:x:1000:armour`

| Field | Value | Description |
| --- | --- | --- |
| Group Name | `armour` | Name of the group |
| Password | `x` | Placeholder (unused) |
| GID | `1000` | Group ID |
| Members | `armour` | User(s) in this group |

> 🟢 Note: Users can belong to multiple supplementary groups, listed in the user_list field.
> 

### Viewing /etc/group

| Command | Description |
| --- | --- |
| `cat /etc/group` | View full group list |
| `getent group groupname` | View specific group |
| `groups username` | View groups for a specific user |

### Editing /etc/group

| Command | Description |
| --- | --- |
| `sudo vim /etc/group` | Edit with root privileges |
| `sudo cp /etc/group /etc/group.bak` | Backup before editing |
| `sudo vigr` | Use safe editor to prevent corruption |

> 🟢 Best Practice: Use groupadd, groupmod, or groupdel instead of manual edits to avoid errors.
> 

---

## 4. /etc/gshadow - Secure Group Access File

The `/etc/gshadow` file stores secure group account information, including group passwords, administrators, and members. It complements `/etc/group` with additional security controls and is readable only by root.

### Format of /etc/gshadow

Each line follows the format: `group_name:encrypted_password:administrators:members`

| Field No. | Field Name | Description |
| --- | --- | --- |
| 1 | group_name | Name of the group |
| 2 | encrypted_password | Password used with `newgrp` (rarely used) |
| 3 | administrators | Comma-separated list of group admins |
| 4 | members | Comma-separated list of regular group members |

### Group Password Field

| Value | Meaning |
| --- | --- |
| `!` or `!!` | Group password not set or disabled (default) |
| (empty) | Password not used; group accessible by members/admins |
| Encrypted string | Set with `gpasswd` for use with `newgrp` |

> 🔵 Note: If /etc/gshadow is deleted, group passwords are temporarily stored in /etc/group.
> 

### Administrators Field

- Lists users who can:
    - Add/remove members using `gpasswd`.
    - Change the group password.
    - Manage the group without root privileges.
- If empty, only the user matching the group name is considered the admin.

> 🟢 Note: Administrators provide a way to delegate group management without requiring root access.
> 

### Members Field

- Lists supplementary group members (beyond the primary GID).
- Comma-separated, can be empty.

### Viewing /etc/gshadow

| Command | Description |
| --- | --- |
| `sudo cat /etc/gshadow` | Display contents (root only) |
| `sudo vigr -s` | Use safe editor to prevent corruption |

> 🟡 Note: Use vigr -s to edit /etc/gshadow to avoid sync issues with /etc/group.
> 

> 🔴 Warning: Avoid setting group passwords unless necessary (e.g., for newgrp). Manual edits should be avoided; use gpasswd for changes.
> 

---

## Security Notes

| Note Type | Description |
| --- | --- |
| 🔴 Warning | Never delete or corrupt `/etc/passwd` or `/etc/shadow`, as it can make the system unbootable. |
| 🔴 Warning | Only root should access `/etc/shadow` and `/etc/gshadow` to prevent unauthorized access. |
| 🟢 Best Practice | Use tools like `vipw`, `vigr`, `useradd`, `usermod`, `groupadd`, or `gpasswd` to avoid manual edit errors. |
| 🟢 Best Practice | Regularly back up files (e.g., `sudo cp /etc/passwd /etc/passwd.bak`) before editing. |
| 🟡 Note | Ensure `/etc/login.defs` is configured with secure defaults (e.g., SHA-512 for password hashing). |
| 🟡 Note | Avoid assigning UID 0 to non-root users to prevent unauthorized superuser access. |

> 🔵 Final Note: Always verify changes in a test environment before applying to production systems to avoid disruptions.
>
