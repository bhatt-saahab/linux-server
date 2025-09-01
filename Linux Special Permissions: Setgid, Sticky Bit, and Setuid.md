

## 1. Setgid (Set-Group-ID)

**Definition**:

Setgid is a special permission that serves two primary functions:

- **On Files**: When set on an executable file, it runs with the permissions of the file's group owner, not the user's primary group (similar to Setuid for users).
- **On Directories**: Ensures that new files or subdirectories created within inherit the group ownership of the parent directory, not the user’s primary group. This is crucial for collaboration in shared directories.

### Key Features

- **Purpose**: Facilitates group-based collaboration and privilege escalation for executables.
- **Identification**: In `ls -l` output, SGID appears as an `s` in the group execute position (e.g., `drwxrwsr-x` for directories or `rwxr-sr-x` for files).
- **Numeric (Octal) Mode**: Uses `2` as the leading digit in `chmod` commands (e.g., `chmod 2777` sets SGID + full permissions).

### Commands and Examples

1. **Set full permissions on a directory**:
    
    ```bash
    chmod 777 /data/
    
    ```
    
    Grants read, write, and execute permissions for all (owner, group, others).
    
2. **Create directories and files (as a regular user)**:
    
    ```bash
    mkdir a1
    touch f1
    
    ```
    
3. **Set SGID on a directory** (ensures group inheritance):
    
    ```bash
    chmod g+s /data/
    
    ```
    
    Verify with:
    
    ```bash
    ls -lh
    
    ```
    
    Output shows `s` in group execute position (e.g., `drwxrwsr-x`).
    
4. **Create test directories/files after setting SGID**:
    
    ```bash
    mkdir a2
    touch f2
    
    ```
    
    New files/directories inherit the group of `/data/`.
    
5. **Remove SGID**:
    
    ```bash
    chmod g-s /data/
    
    ```
    
    Verify with:
    
    ```bash
    ls -lh
    
    ```
    
6. **Set SGID and permissions using octal notation**:
    
    ```bash
    chmod 2777 /data/
    
    ```
    
    Sets SGID (`2`) + full permissions (`777`). Verify:
    
    ```bash
    ls -lh
    
    ```
    
7. **Change group ownership**:
    
    ```bash
    chgrp u1 /data/
    
    ```
    
    Set SGID again:
    
    ```bash
    chmod g+s /data/
    
    ```
    
8. **Employee group practice**:
    
    ```bash
    mkdir emp
    chgrp EMP emp/
    chmod 770 emp/
    chmod g+s emp/
    
    ```
    
    Ensures new files in `emp/` inherit the `EMP` group.
    
9. **Set SGID on an executable** (e.g., custom root shell):
    
    ```bash
    chmod g+s rootshell
    
    ```
    
    Runs `rootshell` with group owner’s permissions.
    

### Practical Impact

- **Shared Folders**: SGID ensures consistent group ownership for files in collaborative directories, supporting team workflows.
- **Executable Files**: SGID allows group-based privilege escalation (less common than on directories).

### Security Caution

- Using `chmod 2777` (SGID + full permissions) on critical directories can introduce security risks in multi-user systems by granting excessive access.

---

## 2. Sticky Bit

**Definition**:

The sticky bit is a special permission, typically set on directories, that restricts file deletion or renaming to the file owner, directory owner, or root, even if others have write permissions. Commonly used in shared directories like `/tmp`.

### Key Features

- **Purpose**: Prevents unauthorized deletion/renaming in shared directories.
- **Identification**: In `ls -l` output, appears as `t` (if execute is allowed) or `T` (if execute is not allowed) in the others’ execute position (e.g., `drwxrwxrwt`).
- **Numeric (Octal) Mode**: Uses `1` as the leading digit in `chmod` commands (e.g., `chmod 1777` sets sticky bit + full permissions).

### Commands and Examples

1. **Set full permissions on a directory**:
    
    ```bash
    chmod 777 /data/
    
    ```
    
2. **Check permissions**:
    
    ```bash
    ls -lh | grep data
    
    ```
    
3. **Add sticky bit**:
    
    ```bash
    chmod o+t /data/
    
    ```
    
    Verify (`t` in others’ execute position):
    
    ```bash
    ls -lh | grep data
    
    ```
    
4. **Remove sticky bit**:
    
    ```bash
    chmod o-t /data/
    
    ```
    
    Verify:
    
    ```bash
    ls -lh | grep data
    
    ```
    
5. **Set sticky bit with octal notation**:
    
    ```bash
    chmod 1777 /data/
    
    ```
    
    Sets sticky bit (`1`) + full permissions (`777`). Verify:
    
    ```bash
    ls -lh | grep data
    
    ```
    
6. **Reset to remove sticky bit**:
    
    ```bash
    chmod 0777 /data/
    
    ```
    
    Verify:
    
    ```bash
    ls -lh | grep data
    
    ```
    
7. **Set all special bits (SUID, SGID, sticky bit)**:
    
    ```bash
    chmod 7777 /data/
    
    ```
    
    Sets SUID (`4`), SGID (`2`), sticky bit (`1`) + full permissions (`777`). Verify (`rwsrwsrwt`):
    
    ```bash
    ls -lh | grep data
    
    ```
    

### Notes

- **Octal Notation for Special Bits**:
    - `4` = Setuid
    - `2` = Setgid
    - `1` = Sticky bit
- `chmod 1777` is common for `/tmp` (sticky bit + full permissions).
- `chmod 7777` (SUID + SGID + sticky bit) is rarely needed and potentially insecure.

---

## 3. Setuid (Set-User-ID)

**Definition**:

Setuid is a special permission that allows an executable to run with the privileges of its file owner (often root), regardless of the executing user. Critical for commands like `passwd` that require temporary elevated privileges.

### Key Features

- **Purpose**: Enables privilege escalation for specific tasks (e.g., modifying `/etc/shadow` via `passwd`).
- **Identification**: In `ls -l` output, appears as `s` in the owner’s execute position (e.g., `rwsr-xr-x`).
- **Numeric (Octal) Mode**: Uses `4` as the leading digit in `chmod` commands (e.g., `chmod 4755` sets SUID + permissions).

### Commands and Examples

1. **Locate an executable** (e.g., `fdisk`):
    
    ```bash
    which fdisk
    
    ```
    
2. **Display disk partitions** (requires root or SUID):
    
    ```bash
    fdisk -l
    
    ```
    
3. **Create a user with root privileges** (demonstration only, highly dangerous):
    
    ```bash
    useradd root1 -o -u 0
    
    ```
    
4. **Grant SUID to `fdisk`**:
    
    ```bash
    chmod u+s /usr/sbin/fdisk
    
    ```
    
    Verify (`s` in owner’s execute position):
    
    ```bash
    ls -lh /usr/sbin/fdisk
    
    ```
    
5. **Run `fdisk` as a regular user**:
    
    ```bash
    fdisk -l
    
    ```
    
6. **Remove SUID**:
    
    ```bash
    chmod u-s /usr/sbin/fdisk
    
    ```
    
7. **Set SUID with octal notation**:
    
    ```bash
    chmod 4755 /usr/sbin/fdisk
    
    ```
    
    Sets SUID (`4`) + permissions (`755`).
    
8. **Restore standard permissions**:
    
    ```bash
    chmod 0755 /usr/sbin/fdisk
    
    ```
    

### Custom Setuid Root Shell

1. **Create C code for a root shell**:
    
    ```c
    #include <stdio.h>
    int main(void) {
        setuid(0);
        setgid(0);
        seteuid(0);
        setegid(0);
        execvp("/bin/sh", NULL, NULL);
    }
    
    ```
    
2. **Install C compiler**:
    
    ```bash
    yum install gcc
    
    ```
    
3. **Compile the program**:
    
    ```bash
    gcc rootshell.c -o rootshell
    
    ```
    
4. **Enable SUID**:
    
    ```bash
    chmod u+s rootshell
    
    ```
    
5. **Run the root shell**:
    
    ```bash
    ./rootshell
    
    ```
    
    Grants root access (assuming no system protections).
    

### Security Warning

- **Risks**: SUID on executables can lead to unintended privilege escalation. Restrict SUID to trusted system binaries. Avoid setting SUID on interpreters or user-created programs outside secure environments.
- **Example**: Misconfigured SUID binaries can allow any user to gain root access, compromising system security.

### Passwd Demonstration

1. **Check sensitive file permissions**:
    
    ```bash
    ls -lh /etc/shadow
    ls -lh /etc/gshadow
    
    ```
    
2. **Inspect `passwd` SUID**:
    
    ```bash
    which passwd
    ls -lh /usr/bin/passwd
    
    ```
    
    Output shows `s` in owner’s execute position (e.g., `-rwsr-xr-x`), allowing users to modify `/etc/shadow`.
    
3. **Remove SUID from `passwd`** (not recommended):
    
    ```bash
    chmod u-s /usr/bin/passwd
    
    ```
    
    Prevents standard users from changing passwords.
    

---

## /usr/bin vs. /usr/sbin

- **/usr/bin**:
    - Contains user commands and executables for general use (e.g., `vim`, `scp`).
    - Intended for all users, no administrative privileges required.
- **/usr/sbin**:
    - Contains system administration binaries (e.g., `fdisk`, `ifconfig`, `shutdown`).
    - Primarily for root or users with `sudo` privileges.

---

## Summary of Special Permissions

| Permission | Octal | Symbol | Purpose | Common Use Case |
| --- | --- | --- | --- | --- |
| Setuid | 4 | `s` (owner) | Runs executable as file owner | `passwd`, `sudo` |
| Setgid | 2 | `s` (group) | Runs executable as group owner or inherits group for directories | Shared directories, group collaboration |
| Sticky Bit | 1 | `t` (others) | Restricts deletion/renaming in directories | `/tmp`, shared folders |

### Combined Example

- `chmod 7777 /data/` sets SUID, SGID, sticky bit, and full permissions (`rwsrwsrwt`).
- Use cautiously, as this combination is rarely needed and can be insecure.

---

## Security Best Practices

- **Minimize Special Permissions**: Only apply SUID, SGID, or sticky bit when necessary.
- **Restrict Write/Execute**: Avoid `777` permissions with special bits to prevent unauthorized access.
- **Audit Regularly**: Check for unexpected SUID/SGID binaries using `find / -perm /6000`.
- **Isolate Environments**: Test SUID/SGID programs in secure, isolated systems to avoid risks.

---

These notes cover all provided details, organized for clarity and practical use. Let me know if you need further clarification or specific examples!
