Your sir told you to **make SSH connection first** because:

### **Why first SSH? (Simple reason)**

- You need to **connect to the remote machine** before you can do anything on it.
- Without SSH, you **can’t access** or control that server.
- It’s like **opening the door** before entering a room.

### **In short:**

> SSH is the first step to control or work on another system remotely.
> 

Once connected via SSH, you can:

- Run commands
- Upload/download files
- Configure servers

**Command:**

```bash
ssh username@IP_address

```

---

---

### **System & OS Information**

| **Task** | **Command** |
| --- | --- |
| Check current runlevel | `runlevel` |
| Check kernel version | `uname -r` |
| Check Linux distribution | `cat /etc/os-release` |

---

### **Disk & Filesystem**

| **Task** | **Command** |
| --- | --- |
| List all mounted filesystems | `df -h` |
| Check disk usage of current dir | `du -sh` |

---

### **Process Management**

| **Task** | **Command** |
| --- | --- |
| List all running processes | `ps aux` |
| Monitor real-time processes | `top` |
| (Better interface, if installed) | `htop` |

---

## **Linux Basic Commands**

### **Shell Prompt Formats**

| **Prompt Type** | **Example** | **Meaning** |
| --- | --- | --- |
| **Root user** | `[root@localhost ~]#` | Logged in as `root` (superuser) |
| **Normal user** | `[armour@localhost ~]$` | Logged in as normal user `armour` |
| **General Format** | `[username@hostname path]` | Standard shell prompt format |

---

### **System Identification**

| **Command** | **Description** |
| --- | --- |
| `hostname` | Displays the system’s hostname (computer's network name) |

### **Working with Directories**

| **Command** | **Description** |
| --- | --- |
| `pwd` | Shows the present working directory (full path) |

---

---

# **🎯 Getting Help With Commands in Linux**

> Displays help documentation about usage, options, and syntax for each command.
> 

---

## **1. Terminal Help Flags**

Most Linux commands support `--help` or `-h` for a quick summary of usage.

### **Examples:**

- **List directory options**
    
    ```bash
    ls --help
    
    ```
    
- **Incorrect but common misunderstanding**
    
    ```bash
    ls -h
    
    ```
    
    *(This shows human-readable sizes, not help)*
    
- **Help for `sudo`**
    
    ```bash
    sudo --help
    
    ```
    
- **Help for `vim`**
    
    ```bash
    vim -h
    
    ```
    
- **Help for `crunch`**
    
    ```bash
    crunch --help
    
    ```
    
- **Help for `ts` (from moreutils)**
    
    ```bash
    ts --help
    
    ```
    

---

## **2. Using `man` – The Manual Pages**

Use the `man` command to access **full documentation** for Linux commands.

### **Examples:**

```bash
man ls
man sudo
man vim
man crunch

```

> Tips:
> 
> - Press `q` to quit the manual.
> - Use arrow keys or `Space` to scroll.

---

## **3. Using `help` – For Shell Built-in Commands**

Some commands like `cd`, `echo`, and `exit` are **built into the shell**, not standalone programs.

To get help on them, use:

```bash
help

```

Or to get help for a specific command:

```bash
help cd
help exit
help echo

```

---

## ✅ Quick Summary

| **Purpose** | **Command** |
| --- | --- |
| Quick command help | `--help` / `-h` |
| Full manual page | `man <command>` |
| Help for shell built-ins | `help` |

---

---

# 📚 **Manual and Info Pages in Linux**

---

### 1. Display the manual page for `crunch`

```bash
man crunch

```

---

### 2. Show the info page for `crunch` (often more detailed)

```bash
info crunch

```

---

### 3. Open the main manual interface

```bash
man

```

---

### 4. Search manual pages for any command related to `mkdir`

```bash
man -k mkdir

```

---

### 5. Search **exactly** for `mkdir`

```bash
man kmkdir$""

```

*(Note: This seems like a typo or unusual command — typically, use quotes for exact match like:)*

```bash
man -k '^mkdir$'

```

---

### 6. Open the **section 2** manual for the `mkdir` system call

```bash
man 2 mkdir

```

---

### 7. Search and display information related to `passwd` and `ls` commands

```bash
man -k passwd
man 2 ls
info ls

```

*(Your original had `man-k p`*

---

---

# **📁 File and Directory Listing with `ls`**

The `ls` command is used to **list files and directories** in Linux/Unix.

---

## **✨ Basic `ls` Usage**

| **Command** | **Description** |
| --- | --- |
| `ls` | Lists files and directories in current folder. |
| `ls -1` | Lists **one file per line**. |

---

## **🧾 Long & Detailed Listing**

| **Command** | **Description** |
| --- | --- |
| `ls -l` | **Long format** listing (permissions, size, timestamp). |
| `ls -lh` | Long listing with **human-readable sizes** (e.g., KB, MB). |
| `ls -lha` | Includes **hidden files** (starting with `.`). |
| `ls -lhr` | Long, human-readable, and **reverse order**. |

---

## **⏰ Sorting by Time**

| **Command** | **Description** |
| --- | --- |
| `ls -lt` | Sorts files by **modification time (latest first)**. |
| `ls -lt --reverse` or `ls -ltr` | **Reverses** the time sorting (oldest first). |

---

## **📂 Recursive Listing**

| **Command** | **Description** |
| --- | --- |
| `ls -lhR` | Recursively lists all directories with **human-readable** sizes. |

---

## **⚠️ Hidden Files**

- Files starting with a dot (`.`) are **hidden**.
- Use `a` or `A` to include them in listing.

---

**Let me know** if you want this as a printable PDF cheat sheet!
