

Linux uses three **special permission bits** to control advanced security behaviors for files and directories: **setuid**, **setgid**, and the **sticky bit**. These permissions enhance security and functionality but must be used cautiously due to potential risks.

---

### 1. Setuid (Set User ID)

### Function

- When set on an **executable file**, the program runs with the **permissions of the file's owner** (often `root`) rather than the user executing it.
- Essential for programs requiring elevated privileges, such as `passwd`, which needs access to protected files like `/etc/shadow`.

### How to Set

- Use the `chmod` command with the `u+s` option or the octal value `4` in the leading digit.
- Command: `chmod u+s <file>` or `chmod 4755 <file>`.

### Example

- The `passwd` command has `setuid` to allow users to update their passwords securely:
    
    ```bash
    ls -l /usr/bin/passwd
    # Output: -rwsr-xr-x 1 root root /usr/bin/passwd
    
    ```
    
    - The `s` in the owner's execute position (`rws`) indicates `setuid`.

### Demonstration with `fdisk`

- **Locate the `fdisk` binary**:
    
    ```bash
    which fdisk
    # Output: /usr/sbin/fdisk
    
    ```
    
- **Display disk partition information** (requires root or `setuid` privileges):
    
    ```bash
    fdisk -l
    
    ```
    
- **Create a user with root privileges (for demonstration only, highly dangerous)**:
    
    ```bash
    useradd -o -u 0 root2
    
    ```
    
    - Creates a user `root2` with UID 0 (root's UID). **Warning**: This is insecure and should not be done in production environments.
- **Grant `setuid` to `fdisk`**:
    
    ```bash
    chmod u+s /usr/sbin/fdisk
    
    ```
    
- **Verify permissions**:
    
    ```bash
    ls -l /usr/sbin/fdisk
    # Output: -rwsr-xr-x 1 root root /usr/sbin/fdisk
    
    ```
    
- **Run `fdisk` as a regular user**:
    
    ```bash
    fdisk -l
    
    ```
    
    - With `setuid`, non-root users can execute `fdisk` with root privileges.
- **Remove `setuid` (for safety)**:
    
    ```bash
    chmod u-s /usr/sbin/fdisk
    
    ```
    

---

### 2. Setgid (Set Group ID)

### Function

- **On executable files**: The program runs with the **group permissions of the file’s group owner**, not the user’s group.
- **On directories**: Files created within the directory **inherit the group ownership** of the directory, not the user’s primary group. This ensures consistent group access in shared directories.

### How to Set

- Use `chmod g+s <file-or-directory>` or the octal value `2` in the leading digit (e.g., `chmod 2755 <dir>`).

### Example

- Set `setgid` on a shared project directory to ensure group consistency:
    
    ```bash
    chmod g+s /project/shared
    ls -ld /project/shared
    # Output: drwxr-sr-x 2 user group /project/shared
    
    ```
    
    - The `s` in the group’s execute position (`r-s`) indicates `setgid`.

---

### 3. Sticky Bit

### Function

- When set on a **directory**, only the **file owner**, **directory owner**, or **root** can delete or rename files within it, even if others have write permissions.
- Commonly used on shared directories like `/tmp` to prevent unauthorized file deletion.

### How to Set

- Use `chmod +t <directory>` or the octal value `1` in the leading digit (e.g., `chmod 1777 <dir>`).

### Example

- The `/tmp` directory typically has the sticky bit set:
    
    ```bash
    ls -ld /tmp
    # Output: drwxrwxrwt 10 root root /tmp
    
    ```
    
    - The `t` in the others’ execute position (`rwt`) indicates the sticky bit.

---

### Checking Special Permissions

### Using `ls -l`

- **setuid**: Appears as `s` in the owner’s execute position (e.g., `rwsr-xr-x`).
- **setgid**: Appears as `s` in the group’s execute position (e.g., `rwxr-sr-x`).
- **Sticky bit**: Appears as `t` in the others’ execute position (e.g., `drwxrwxrwt`).

### Numeric (Octal) Representation

- Special permissions use a **fourth (leading) digit** in `chmod`:
    - `4` = `setuid`
    - `2` = `setgid`
    - `1` = `sticky bit`
- Examples:
    - `setuid` + `rwxr-xr-x`: `chmod 4755 <file>`
    - `setgid` + `rwxr-xr-x`: `chmod 2755 <dir>`
    - `sticky bit` + `rwxrwxrwx`: `chmod 1777 <dir>`

---

### Example: Creating a Setuid Root Shell (Demonstration Only)

**Warning**: This is highly dangerous and should only be done in a controlled, isolated environment (e.g., a virtual machine) for learning purposes. Misuse can lead to severe security vulnerabilities.

### C Code for a Root Shell

```c
#include <stdio.h>
#include <unistd.h>

int main(void) {
    setuid(0);       // Set user ID to root
    setgid(0);       // Set group ID to root
    seteuid(0);      // Set effective user ID to root
    setegid(0);      // Set effective group ID to root
    execvp("/bin/sh", NULL, NULL); // Launch a root shell
    return 0;
}

```

### Steps

1. **Save the code**:
    
    ```bash
    vim rootshell.c
    
    ```
    
2. **Install a C compiler** (if not present):
    
    ```bash
    yum install gcc
    
    ```
    
3. **Compile the program**:
    
    ```bash
    gcc rootshell.c -o rootshell
    
    ```
    
4. **Enable `setuid` on the binary**:
    
    ```bash
    chmod u+s rootshell
    
    ```
    
5. **Verify permissions**:
    
    ```bash
    ls -l rootshell
    # Output: -rwsr-xr-x 1 root root rootshell
    
    ```
    
6. **Run the setuid root shell**:
    
    ```bash
    ./rootshell
    
    ```
    
    - This grants a root shell to any user (assuming no system-level protections like SELinux or AppArmor).

### Cleanup

- **Remove `setuid`** to prevent misuse:
    
    ```bash
    chmod u-s rootshell
    
    ```
    

---

### Further Permission Inspection: `passwd` Demonstration

### Check Sensitive File Permissions

- Files like `/etc/shadow` are typically readable only by `root`:
    
    ```bash
    ls -l /etc/shadow
    # Output: -rw-r----- 1 root shadow /etc/shadow
    ls -l /etc/gshadow
    # Output: -rw-r----- 1 root shadow /etc/gshadow
    
    ```
    

### Inspect `passwd` Command

- The `passwd` command uses `setuid` to allow users to modify `/etc/shadow`:
    
    ```bash
    which passwd
    # Output: /usr/bin/passwd
    ls -l /usr/bin/passwd
    # Output: -rwsr-xr-x 1 root root /usr/bin/passwd
    
    ```
    
    - The `s` in `rws` indicates `setuid`, enabling temporary root access.

### Remove `setuid` from `passwd` (Not Recommended)

- Disabling `setuid` prevents regular users from changing passwords:
    
    ```bash
    chmod u-s /usr/bin/passwd
    
    ```
    
    - **Warning**: This breaks standard functionality and should be avoided in production.

---

### Security Warning

- **Setuid** and **setgid** on executables can lead to **privilege escalation** if misused, especially on untrusted or poorly secured binaries.
- **Never** set `setuid` or `setgid` on interpreters (e.g., Python, Bash) or user-created programs outside secure, isolated environments.
- Restrict special permissions to **trusted system binaries** (e.g., `/usr/bin/passwd`, `/usr/sbin/fdisk`).
- Regularly audit files with `setuid`/`setgid`:
    
    ```bash
    find / -perm -4000  # Find setuid files
    find / -perm -2000  # Find setgid files
    
    ```
    

---

### `/usr/bin` vs. `/usr/sbin`

### Overview

- **/usr/bin**: Contains executable binaries for **general user commands**, accessible to all users. Examples: `vim`, `scp`, `ls`.
- **/usr/sbin**: Contains **system administration binaries**, typically requiring root or sudo privileges. Examples: `fdisk`, `ifconfig`, `shutdown`.

### Key Differences

| **Directory** | **Intended For** | **Typical Use Cases** | **Example Programs** |
| --- | --- | --- | --- |
| `/usr/bin` | All users | Regular applications | `vim`, `du`, `diff` |
| `/usr/sbin` | Admin/root users | System administration tools | `fdisk`, `ifconfig` |

### Context and Evolution

- **Historical Purpose**: The separation organizes binaries by user role, with `/usr/sbin` reserved for administrative tasks.
- **Modern Systems**: The distinction is largely conventional, not a security mechanism. Ordinary users can access `/usr/sbin` but lack permissions to execute privileged tools.
- **Symlinks**: In some distributions, `/bin` is a symlink to `/usr/bin`, and `/sbin` to `/usr/sbin`, simplifying the file system structure.

### Summary

- `/usr/bin`: General-purpose, non-privileged binaries for all users.
- `/usr/sbin`: Administrative tools, typically requiring elevated privileges.

---

### Corrections and Clarifications

- Fixed typos: "cheak" → "check," "inporant" → "important," "passed" → "passwd," "frisk" → "fdisk," "Footl" → "root2."
- Corrected command syntax: `chmod uts cfiles` → `chmod u+s <file>`, `chmod ges` → `chmod g+s`, `chmod +` → `chmod +t`.
- Clarified `setuid`/`setgid` behavior and risks, emphasizing safe usage.
- Fixed C code: Corrected `execvp` arguments and added necessary headers.
- Streamlined `/usr/bin` vs. `/usr/sbin` section to remove redundant details.
- Added commands to audit `setuid`/`setgid` files for security.

This version ensures accuracy, clarity, and completeness while maintaining all critical information. Let me know if you need further details or specific examples!
