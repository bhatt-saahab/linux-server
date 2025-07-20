


Contains key OS components:

- **System32** – Core system files (DLLs, EXEs, drivers).
- **WinSxS** – Side-by-side assemblies (Windows component store).
- **Temp** – Temporary files.
- **Logs** – System and installation logs.

### ➤ `C:\Program Files`

Default folder for **64-bit** applications on 64-bit Windows.

### ➤ `C:\Program Files (x86)`

Default folder for **32-bit** applications on 64-bit Windows.

### ➤ `C:\Users`

Stores **user profiles** as subfolders:

- **Default** – Template for new user profiles.
- **Public** – Shared user space.
- **YourUserName** – Personal files like:
    - Desktop
    - Documents
    - Downloads
    - AppData (hidden; for app data/configs)

### ➤ `C:\ProgramData`

Stores **application data shared** across all users.

(Hidden by default, often used for app settings/cache.)

### ➤ `C:\System Volume Information`

System-managed folder containing:

- Restore points
- Volume metadata
    
    (Restricted access)
    

### ➤ `C:\$Recycle.Bin`

Stores **deleted files for all users** (Recycle Bin contents).

---

### **➤ Linux Directory Structure**

| **Directory** | **Purpose** |
| --- | --- |
| `/` | **Root directory** – Top-level of the filesystem hierarchy |
| `/bin` | Essential user binaries (e.g. `ls`, `cp`, `mv`) – Required for boot |
| `/sbin` | Essential system binaries (e.g. `init`, `fsck`, `reboot`) – Admin tasks |
| `/lib` | Shared libraries needed by `/bin` and `/sbin` |
| `/lib64` | 64-bit specific shared libraries – On 64-bit systems |
| `/etc` | System-wide configuration files and startup scripts |
| `/dev` | Device files (e.g. `/dev/sda`, `/dev/null`) |
| `/proc` | Virtual filesystem for kernel/process info |
| `/var` | Variable data: logs (`/var/log`), mail, cache, spool |
| `/tmp` | Temporary files – Cleared on reboot |
| `/usr` | Secondary hierarchy for user apps/libraries (`/usr/bin`, `/usr/lib`) |
| `/boot` | Boot files (e.g. kernel, GRUB configs) |
| `/opt` | Optional add-on or third-party software |
| `/srv` | Service data (e.g. web, FTP servers) |
| `/home` | Home directories for regular users (e.g. `/home/alex`) |
| `/root` | Home directory for the **root** user |
| `/mnt` | Temporary mount point for manual mounts |
| `/media` | Auto-mounted removable media (e.g. USB, CDs) |

---

Let me know if you want this in **PDF** or **colorful infographic** format!

| Concept | Analogy |
| --- | --- |
| `/` | Like the **main building** of a company—everyone works in it. |
| `/root` | Like the **CEO's private office** inside that building—only the CEO (root user) can access it. |
