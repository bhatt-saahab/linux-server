In Linux, **permissions** define **who can access** a file or directory and **what actions** they can perform. This system ensures **security**, **accountability**, and **controlled access** for users and processes.

## What Are Linux File Permissions?

Linux uses a **three-tiered permission model** applied to:

- **User (Owner)**: The user who owns the file.
- **Group**: The group associated with the file.
- **Others**: All other users not in the owner or group categories.

Each tier can be assigned the following permissions:

- **r**: Read
- **w**: Write
- **x**: Execute

## Understanding the Permission String

To view permissions, use the command:

```bash
ls -l /path/to/file

```

### Example Output:

```bash
-rwxr-xr-- 1 armour infusec 1234 Jul 21 20:00 script.sh

```

### Breakdown of Permission String:

| Position | Symbol | Meaning |
| --- | --- | --- |
| 1 | `-` or `d` or `l` | File type (`-` for file, `d` for directory, `l` for symlink) |
| 2-4 | `rwx` | **Owner permissions**: Read, Write, Execute |
| 5-7 | `r-x` | **Group permissions**: Read, Execute |
| 8-10 | `r--` | **Others permissions**: Read only |

## Permission Meanings

| Permission | File Meaning | Directory Meaning |
| --- | --- | --- |
| **Read (r)** | Read file content | List directory contents (`ls`) |
| **Write (w)** | Modify file content | Create, delete, or rename files in directory |
| **Execute (x)** | Execute the file (e.g., scripts) | Access or traverse directory |

## File Type Characters

| Character | File Type |
| --- | --- |
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `p` | Named pipe |
| `s` | Socket |

## Setting Permissions

Permissions can be set using two methods: **Numeric (Octal)** and **Symbolic**.

### Numeric (Octal) Method

Permissions are represented as a **three-digit octal number** (e.g., `754`). Each digit corresponds to a user class (Owner, Group, Others).

### Permission Values:

| Symbol | Value | Meaning |
| --- | --- | --- |
| `r` | 4 | Read |
| `w` | 2 | Write |
| `x` | 1 | Execute |

### Calculation:

Add values for each entity:

- Example: `7 = 4 (r) + 2 (w) + 1 (x)` = `rwx`
- Example Permission: `754`
    - **Owner**: `7` = `rwx` (4+2+1)
    - **Group**: `5` = `r-x` (4+0+1)
    - **Others**: `4` = `r--` (4+0+0)

### Command:

```bash
chmod 754 filename  # Sets rwxr-xr--

```

### Symbolic Method

Uses letters and symbols to set permissions.

### Examples:

```bash
chmod u+x file        # Add execute permission for user
chmod g-w file        # Remove write permission for group
chmod o=r file        # Set read-only for others

```

## Special Permission Bits

Special bits provide additional control over file or directory behavior.

| Name | Symbol | Description | Use Case |
| --- | --- | --- | --- |
| **SUID** | `s` (user bit) | Run file with owner’s privileges | Executables like `passwd` |
| **SGID** | `s` (group bit) | Run with group privileges or inherit group for directories | Shared directories or group collaboration |
| **Sticky Bit** | `t` (others bit) | Restrict file deletion to owner only | Used on `/tmp` directory |

### Example:

Set sticky bit on a directory:

```bash
chmod +t /shared_dir

```

## Checking Permissions Examples

Use `ls -lh` to view permissions for files or directories:

```bash
ls -lh /dev/ | grep shm      # Check shared memory permissions
ls -lh / | grep tmp          # View /tmp directory permissions
ls -lh /home                 # List user directories with permissions
ls -lh /home/armour/         # View specific user’s files

```

# Linux Permission Assignment

Linux allows assigning permissions using **Symbolic** and **Numeric (Octal)** methods to control access for **Owner**, **Group**, and **Others**.

## Symbolic Method

The symbolic method uses **letters and symbols** for human-readable permission assignment.

### Syntax:

```bash
chmod [user_class][operation][permission] file.txt

```

### User Classes:

| Symbol | Class |
| --- | --- |
| `u` | User (Owner) |
| `g` | Group |
| `o` | Others |
| `a` | All (u + g + o) |

### Operations:

| Symbol | Operation |
| --- | --- |
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set exact permission |

### Permission Types:

| Symbol | Permission |
| --- | --- |
| `r` | Read |
| `w` | Write |
| `x` | Execute |

### Examples:

1. Add execute permission for the owner:
    
    ```bash
    chmod u+x file.txt
    
    ```
    
2. Remove write permission for others:
    
    ```bash
    chmod o-w file.txt
    
    ```
    
3. Set read and write permissions for the group:
    
    ```bash
    chmod g=rw file.txt
    
    ```
    

## Numeric (Octal) Method Recap

- Uses a **three-digit number** to represent permissions for **Owner**, **Group**, and **Others**.
- Example: `754` translates to:
    - **Owner**: `rwx` (7)
    - **Group**: `r-x` (5)
    - **Others**: `r--` (4)

### Command:

```bash
chmod 754 file.txt

```

## Key Notes

- **Permissions ensure security** by controlling access to files and directories.
- Use **symbolic method** for human-readable changes or **numeric method** for precise control.
- **Special bits** (SUID, SGID, Sticky Bit) add advanced functionality for specific use cases.
- Always verify permissions with `ls -lh` to ensure correct access control.

# `chown` Command in Linux

The `chown` command in Linux is used to **change the owner and/or group** of files or directories. Below is a detailed, organized, and comprehensive set of notes covering all aspects of the `chown` command based on the provided information.

---

## Table of Contents

1. [Purpose](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
2. [Basic Syntax](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
3. [Options](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
4. [Common Usage Examples](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
    - [Changing Owner Only](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
    - [Changing Owner and Group Together](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
    - [Changing Group Only](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
    - [Working with Multiple Files and Patterns](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)
5. [Key Notes](https://www.notion.so/Linux-Permissions-239add49374d80c08b71c643d1130f3c?pvs=21)

---

## Purpose

- The `chown` command is used to **modify the ownership** (user and/or group) of files and directories in Linux.
- It allows system administrators to assign ownership to specific users or groups and is essential for managing permissions and access control.

---

## Basic Syntax

```bash
chown [OPTIONS] NEW_OWNER[:NEW_GROUP] FILE ...

```

- **NEW_OWNER**: The username or User ID (UID) to set as the new owner.
- **NEW_GROUP**: The group name or Group ID (GID) to set as the new group (optional).
- **FILE ...**: The file(s) or directory/directories to modify.
- The colon (`:`) is used to separate the owner and group in the command.

---

## Options

- **`R`**: Recursively changes ownership for directories and their contents (files and subdirectories).
- **`f`**: Suppresses most error messages, useful for scripting or when errors are expected but not critical.

---

## Common Usage Examples

### Changing Owner Only

1. **Change the owner of a single file**:
    
    ```bash
    chown armour demo
    
    ```
    
    - Sets the owner of the file `demo` to the user `armour`.
2. **Change the owner of a specific file**:
    
    ```bash
    chown root log/messages
    
    ```
    
    - Sets the owner of the file `log/messages` to the user `root`.
3. **Recursively change the owner of a directory and its contents**:
    
    ```bash
    chown -R armour log/
    
    ```
    
    - Changes the owner of the directory `log/` and all its contents to `armour`.
    - Alternative syntax (same effect, `R` position is flexible):
        
        ```bash
        chown armour -R log/
        
        ```
        
4. **Recursively change owner with error suppression**:
    
    ```bash
    chown armour -f -R log/
    
    ```
    
    - Changes the owner of `log/` and its contents to `armour`, suppressing error messages.
5. **Change the owner of multiple files**:
    
    ```bash
    chown armour boot.log cron firewalld
    
    ```
    
    - Sets the owner of the files `boot.log`, `cron`, and `firewalld` to `armour`.
6. **Change the owner of files matching a pattern**:
    - All `.log` files in the current working directory (CWD):
        
        ```bash
        chown armour *.log
        
        ```
        
    - All files starting with `maillog`:
        
        ```bash
        chown root maillog*
        
        ```
        
    - All files ending with `.old`:
        
        ```bash
        chown armour *.old
        
        ```
        
    - All files starting with `X`:
        
        ```bash
        chown armour X*
        
        ```
        

---

### Changing Owner and Group Together

1. **Set both owner and group for a directory**:
    
    ```bash
    chown armour:armour log/
    
    ```
    
    - Sets the owner and group of `log/` to `armour`.
2. **Recursively set owner and group for a directory and its contents**:
    
    ```bash
    chown armour:armour -R log/
    
    ```
    
    - Changes the owner and group of `log/` and all its contents to `armour`.
    - Alternative syntax (same effect, `R` position is flexible):
        
        ```bash
        chown -R armour:armour log/
        
        ```
        

---

### Changing Group Only

1. **Change the group of a directory (owner unchanged)**:
    
    ```bash
    chown :armour log/
    
    ```
    
    - Sets the group of `log/` to `armour` without modifying the owner.
2. **Recursively change the group of a directory and its contents**:
    
    ```bash
    chown -R :armour log/
    
    ```
    
    - Changes the group of `log/` and all its contents to `armour` without modifying the owner.
    - Alternative syntax (same effect):
        
        ```bash
        chown :armour -R log/
        
        ```
        
3. **Recursively set group to a different group (e.g., `infosec`)**:
    
    ```bash
    chown -R :infosec log/
    
    ```
    
    - Changes the group of `log/` and its contents to `infosec` without modifying the owner.

---

### Working with Multiple Files and Patterns

- The `chown` command supports **wildcards** () for pattern matching:
    - `.log`: Matches all files with a `.log` extension.
    - `maillog*`: Matches all files starting with `maillog`.
    - `.old`: Matches all files ending with `.old`.
    - `X*`: Matches all files starting with `X`.
- Example commands:
    
    ```bash
    chown armour *.log
    chown root maillog*
    chown armour *.old
    chown armour X*
    
    ```
    

---
