# 🗂️ **Copying Files and Directories with `cp`**

The `cp` command is used to **copy files or directories**.

### 📌 **Basic Syntax:**

```bash
cp [options] source destination

```

---

### 🎯 **Useful Options:**

| Option | Description |
| --- | --- |
| `-v` | Verbose (shows the process) |
| `-r` | Recursive (for directories) |
| `-i` | Prompt before overwrite |
| `-u` | Copy only when source is newer |

---

### 📁 **Examples:**

### 🔹 Copying a file:

```bash
cp anaconda-ks.cfg anaconda-ks.cfg.back

```

✅ *Creates a backup of the file.*

---

### 🔹 Copy a file to Desktop:

```bash
cp /etc/passwd /root/Desktop/

```

---

### 🔹 ❌ Incorrect: (multiple paths merged)

```bash
cp /etc/passwd /etc/hosts /var/log/messages /root/Desktop/

```

✅ **Corrected:**

```bash
cp /etc/passwd /etc/hosts /var/log/messages /root/Desktop/

```

---

### 🔹 Copy a directory with verbosity:

```bash
cp -vr /var/log /root/Desktop/d1/

```

---

### 🔹 Copy all `.conf` files to a folder:

```bash
cp -vr /etc/*.conf /root/Desktop/conf/

```

---

# 🔄 **Moving and Renaming with `mv`**

The `mv` command is used to **move** or **rename** files and directories.

### 📌 **Basic Syntax:**

```bash
mv [options] source destination

```

---

### 🎯 **Common Uses:**

| Task | Example |
| --- | --- |
| ✅ Rename file | `mv anaconda-ks.cfg anacondal` |
| ✅ Move file to dir | `mv a.txt d9/` |
| ✅ Move multiple files | `mv file[0-2] /root/Desktop/` |
| ✅ Move using pattern | `mv [hd]ella /root/Desktop/` |

---

### 🔹 Examples:

### ✅ Move file to directory:

```bash
mv ca /root/Desktop/

```

---

### 🔹 Move with wildcards:

```bash
mv hel? /root/Desktop/
mv file[0-2] /root/Desktop/
mv [hd]ella /root/Desktop/

```

---

### ❌ Incorrect use of mv (with misplaced options/syntax):

```bash
mv -vX /root/d2/     # ❌ '-X' is invalid option
mv (*.txt,*.pdf) /root/Desktop/  # ❌ Invalid shell syntax

```

✅ **Correct (using brace expansion):**

```bash
mv *.txt *.pdf /root/Desktop/

```

---

### ✅ **Tips:**

- Always use `i` to avoid accidental overwrite:
    
    ```bash
    mv -i old.txt new.txt
    
    ```
    
- Use `v` to see what is being moved:
    
    ```bash
    mv -v *.log /var/log/
    
    ```
    

---

Let me know if you want a printable PDF or visual flashcards for this topic!
