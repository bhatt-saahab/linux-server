---

---

## 🟢 **1. Creating Files with `touch`**

Used to **create one or more empty files**.

### 📌 **Basic Usage**

```bash
touch f1.txt
touch file1

```

➡️ Creates files `f1.txt` and `file1` in the **current directory**.

### 📌 **Multiple Files**

```bash
touch f2.txt f3.txt f4.txt

```

➡️ Creates **3 files** in one go.

### 📌 **Special File Names**

| File Type | Command | Description |
| --- | --- | --- |
| Space | `touch "ARMOUR INFOSEC"` | Filename with spaces (must use quotes) |
| Hyphen | `touch ARMOUR-INFOSEC` | Hyphens are allowed |
| Underscore | `touch ARMOUR_INFOSEC` | Underscores are allowed |

### 📌 **Specific Location**

```bash
touch /tmp/f6.txt /root/d1/f7.txt

```

➡️ Creates files at **specific paths**

⚠️ `/root/` may require **sudo/root permissions**

---

## 🔵 **2. Viewing File Contents with `cat`**

### 📌 **Display Single File**

```bash
cat f1.txt

```

➡️ Shows content of `f1.txt`

### 📌 **Display Multiple Files**

```bash
cat anaconda-ks.cfg initial-setup-ks.cfg

```

➡️ Concatenates and shows contents of both files

### 📌 **Create File with Keyboard Input**

```bash
cat > f1.txt

```

➡️ Creates or **overwrites** `f1.txt`

➡️ Type content → `Ctrl + D` to save and exit

---

## 🟣 **3. Creating Directories with `mkdir`**

### 📌 **Basic Creation**

```bash
mkdir d1
mkdir d2 d3 d4

```

➡️ Creates directories `d1`, `d2`, `d3`, and `d4`

### 📌 **Nested Directories with `p`**

```bash
mkdir -p d5/dd2
mkdir -p d6/dd3/s1/s2/s3

```

➡️ `-p` creates **parent folders if not present**

---

## 🔴 **4. Removing Directories with `rmdir` and `rm`**

### 📌 **Removing Empty Directories**

```bash
rmdir d3/d4/
rmdir -p d1/d2/d3/d4/d5/

```

➡️ Removes empty directories and parent dirs if empty

### ⚠️ **Caution: Deleting Files & Folders**

| Command | Purpose |
| --- | --- |
| `rm f1.txt` | Delete single file |
| `rm -f f2.txt` | Force delete file |
| `rm -f f3.txt f4.txt f5.txt` | Delete multiple files |
| `rm -vf f6.txt` | Verbose + force delete |
| `rm -vf A*` | Delete all files starting with "A" |
| `rm -vf *.txt` | Delete all `.txt` files |
| `rm -rfv d6/*` | Recursive + force delete contents of d6 |

🚫 **Danger Zone**

```bash
rm -rf /
rm -rf

```

⚠️ Can **erase your entire system** — NEVER run this unless you absolutely know what you're doing!

---

## ✅ **Quick Recap Table**

| Command Type | Example | Action |
| --- | --- | --- |
| Create File | `touch file.txt` | Creates an empty file |
| View File | `cat file.txt` | Shows file content |
| Create Folder | `mkdir dir1` | Creates a folder |
| Nested Folders | `mkdir -p a/b/c` | Creates full path |
| Remove File | `rm -f file.txt` | Force remove |
| Remove Folder | `rm -rf folder/` | Remove folder & contents |

---

Let me know if you want this in **PDF, diagram, or printable format**!
