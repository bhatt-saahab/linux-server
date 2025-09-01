---

# Part 1 — Rescue / Password Reset

## A) Show the GRUB menu (dual-boot)

1. Reboot.
2. When BIOS/UEFI splash appears, **hold `Shift`** (BIOS) or **tap `Esc`** (UEFI) to open **GRUB**.
3. **Use arrow keys** to highlight your OS.
    - For Kali steps below, highlight **Kali GNU/Linux** and press **`e`** (do **not** press Enter).

---

## B) Kali / Debian / Ubuntu (simplest)

### Quick root shell (for reset)

1. In GRUB edit screen, find the line starting with:
    
    ```
    linux /boot/vmlinuz-... root=UUID=... ro quiet splash
    
    ```
    
2. Replace the ending with:
    
    ```
    rw init=/bin/bash
    
    ```
    
3. Boot with **Ctrl+X** (or **F10**). You’ll land at:
    
    ```
    root@(none):/#
    
    ```
    
4. (Optional but useful to get full commands)
    
    ```bash
    mount -o remount,rw /
    mount -t proc /proc /proc
    mount -t sysfs /sys /sys
    mount -o bind /dev /dev
    mount -t devpts devpts /dev/pts
    export PATH=/usr/bin:/usr/sbin:/bin:/sbin
    
    ```
    
    (One-liner:)
    
    ```bash
    mount -o remount,rw / && mount -t proc /proc /proc && mount -t sysfs /sys /sys && mount -o bind /dev /dev && mount -t devpts devpts /dev/pts && export PATH=/usr/bin:/usr/sbin:/bin:/sbin
    
    ```
    
5. Reset password (if needed):
    
    ```bash
    passwd root
    sync
    
    ```
    
6. Continue boot or reboot:
    
    ```bash
    exec /sbin/init   # or: reboot -f
    
    ```
    

### Proper systemd rescue (alternative)

- Append **`systemd.unit=rescue.target`** (or **`emergency.target`**) instead of `init=/bin/bash` and boot.
    
    Use if you want a cleaner single-user mode with minimal services.
    

✅ **Note:** No `/sysroot`, no SELinux relabeling on Kali/Debian by default.

---

## C) CentOS / RHEL / Fedora (SELinux aware)

1. In GRUB edit screen, append:
    
    ```
    rd.break
    
    ```
    
    (drops to initramfs before full boot)
    
2. Make real root writable (it’s mounted at **/sysroot**):
    
    ```bash
    mount -o remount,rw /sysroot
    chroot /sysroot
    
    ```
    
3. Reset password:
    
    ```bash
    passwd root
    sync
    
    ```
    
4. **SELinux check** (important):
    
    ```bash
    getenforce
    
    ```
    
    - If **Enforcing** → create relabel flag:
        
        ```bash
        touch /.autorelabel
        
        ```
        
    - If **Permissive/Disabled** → skip relabel.
5. Exit twice and reboot:
    
    ```bash
    exit
    exit
    reboot
    
    ```
    

---

# Part 2 — Protect GRUB with a Password

## A) Kali / Debian (recommended workflow)

1. Generate a PBKDF2 hash:
    
    ```bash
    grub-mkpasswd-pbkdf2
    
    ```
    
    Copy the full `grub.pbkdf2.sha512...` hash.
    
2. Add a GRUB superuser (don’t edit `10_linux`; use `40_custom`):
    
    ```bash
    sudo nano /etc/grub.d/40_custom
    
    ```
    
    Add:
    
    ```bash
    set superusers="Armour"        # choose your name
    password_pbkdf2 Armour grub.pbkdf2.sha512.10000....   # paste full hash
    
    ```
    
3. Regenerate GRUB:
    
    ```bash
    sudo update-grub
    
    ```
    
4. Reboot and test: pressing **`e`** or **`c`** now asks for **Username: Armour** and the **plain password** you used to make the hash.

### (Optional) Require a password to boot a specific entry

- Create your own menuentry in `40_custom`:
    
    ```bash
    menuentry "Kali (locked)" --users Armour {
        linux  /boot/vmlinuz-... root=UUID=... ro quiet splash
        initrd /boot/initrd.img-...
    }
    
    ```
    
    Only user *Armour* can boot that entry.
    

---

## B) CentOS / RHEL (two good options)

### Method 1 — **grub2-setpassword** (easiest)

1. Set password interactively:
    
    ```bash
    sudo grub2-setpassword
    
    ```
    
    (Sets superuser **root** and writes **/boot/grub2/user.cfg** with the hash.)
    
2. Reboot and test.
    
    *(You usually do **not** need to rebuild grub.cfg; RHEL’s `00_header` auto-sources `user.cfg`.)*
    
3. Remove later (if needed):
    
    ```bash
    sudo rm -f /boot/grub2/user.cfg
    
    ```
    

### Method 2 — Manual (PBKDF2 + custom)

1. Generate hash:
    
    ```bash
    grub2-mkpasswd-pbkdf2
    
    ```
    
2. Add user lines (prefer `40_custom`):
    
    ```bash
    sudo nano /etc/grub.d/40_custom
    
    ```
    
    ```
    set superusers="bhatt"
    password_pbkdf2 bhatt grub.pbkdf2.sha512.10000....
    
    ```
    
3. Rebuild GRUB:
    
    ```bash
    sudo grub2-mkconfig -o /boot/grub2/grub.cfg
    
    ```
    
4. Reboot and test.

---

## Quick Verification

- **Kali/Debian**
    
    ```bash
    head -30 /boot/grub/grub.cfg | grep -E 'superusers|password_pbkdf2|user.cfg'
    
    ```
    
- **RHEL/CentOS**
    
    ```bash
    ls -l /boot/grub2/user.cfg
    grep -n 'source \$prefix/user.cfg' /boot/grub2/grub.cfg
    head -30 /boot/grub2/grub.cfg | grep superusers
    
    ```
    

---

## What to type at GRUB prompt

- **Username:** exactly as set (e.g., `Armour` or `root` on RHEL with grub2-setpassword).
- **Password:** the **plain** password you chose (GRUB hashes it and compares to the stored PBKDF2).
    
    *You never type the long hash.*
    

---

### Tiny cheat card

- **Kali reset:** `rw init=/bin/bash` → `passwd root` → `exec /sbin/init`
- **RHEL reset:** `rd.break` → `mount -o remount,rw /sysroot` → `chroot /sysroot` → `passwd root` → *(if Enforcing)* `touch /.autorelabel` → reboot
- **Lock GRUB (Kali):** `grub-mkpasswd-pbkdf2` → edit `40_custom` → `update-grub`
- **Lock GRUB (RHEL):** `grub2-setpassword` *(or)* PBKDF2 + `40_custom` → `grub2-mkconfig`

If you want, I can turn this into a printable one-pager with command blocks.

### You said:

Add comment there it help to connect this

### ChatGPT said:

Got it 👍

Here’s your **Method 3: Using `grub2-setpassword`** with **comments added** so you can connect each step clearly:

---

## 🔐 Method 3: Protecting GRUB with Password (Recommended)

### 1️⃣ Set the GRUB password

```bash
grub-setpassword

```

➡️ This will ask you to enter and confirm a password.

➡️ It generates a **hashed password** (not plain text).

---

### 2️⃣ File created/updated

```
/boot/grub2/user.cfg

```

➡️ This file stores the hashed GRUB password.

➡️ It is automatically included when GRUB runs.

---

### 3️⃣ Confirm password is loaded in GRUB config

Open the main config file:

```bash
vim /boot/grub/grub.cfg

```

➡️ Inside, check for this line:

```bash
source ${prefix}/user.cfg

```

✅ This tells GRUB to read the `user.cfg` file where your password is stored.

---

### 4️⃣ Superuser configuration (for GRUB access)

The following should exist inside GRUB config (automatically handled, but check):

```bash
set superusers="root"          # GRUB admin user
export superusers              # Make it global
password_pbkdf2 root <HASH>    # GRUB password (hashed, from user.cfg)

```

---

### 5️⃣ Reboot & Test

➡️ Restart your system.

➡️ When you press `e` or try to edit GRUB entries, it will now **ask for the password**.

---

### 6️⃣ Remove password (if required later)

Just delete the file:

```bash
rm -f /boot/grub2/user.cfg

```

➡️ This removes GRUB password protection.

---

✅ **Summary (with link between steps):**

- `grub-setpassword` → creates **user.cfg** with hashed password
- `grub.cfg` → loads **user.cfg** (via `source ${prefix}/user.cfg`)
- `set superusers` & `password_pbkdf2` → ensure only **root (GRUB user)** can modify entries

---

# 🔒 Setting a Password on GRUB (Kali Linux)

---

### 1️⃣ Generate a GRUB Password Hash

Run this command as root:

```bash
grub-mkpasswd-pbkdf2

```

- It will ask you to type a new GRUB password twice.
- Output will look like this:

```
PBKDF2 hash of your password is grub.pbkdf2.sha512.10000.XXXXXXXXXXXXXXXX

```

👉 Copy the entire hash string.

---

### 2️⃣ Edit GRUB Configuration

Open `/etc/grub.d/40_custom`:

```bash
sudo nano /etc/grub.d/40_custom

```

Add this block at the bottom (replace with your hash):

```bash
set superusers="bhatt"
password_pbkdf2 bhatt grub.pbkdf2.sha512.10000.XXXXXXXXXXXXXXXX

```

- `bhatt` → GRUB username
- `password_pbkdf2` → secure password hash

---

### 3️⃣ Update GRUB

Run:

```bash
sudo update-grub

```

---

### 4️⃣ Test

- Reboot system.
- At GRUB menu, press **`e`** to edit boot entry.
- Now it will **ask for username + password**.
    - Username = `bhatt`
    - Password = the one you set in step 1.

---

✅ Now, nobody can boot into single-user mode and reset root password without the GRUB login.

---

⚠️ Note:

- Normal boot doesn’t ask for password, only **when editing entries or entering GRUB console**.
- If you want **full boot password protection**, that’s a different setup (locking menu entries).

---

👉 Do you want me to also show you the **difference between menu protection and full boot protection in GRUB** (so you can choose which to use in Kali)?
