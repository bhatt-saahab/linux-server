---

# 🎯 **Wildcards (Globbing Patterns) in Linux**

Wildcards (also called *globbing patterns*) are symbols used to match filenames and paths based on specific patterns.

---

| 🔣 **Symbol** | 📝 **Description** | 🎯 **Example** | ✅ **Matches** |
| --- | --- | --- | --- |
| `*` | Matches **any number of characters** (including none) | `ls ca*` | `car`, `carpet`, `ca` |
| `?` | Matches **exactly one character** | `ls hel?` | `help`, `hell` |
| `[x-y]` | Matches a **single character in the range x to y** | `ls file[0-2]` | `file`, `file1`, `file2` |
| `[abc]` | Matches **one character from the set** (e.g. `a`, `b`, or `c`) | `ls [hd]ello` | `hello`, `dello` |
| `[^...]` | Matches **any character NOT in the set** | `ls file[^1]` | `file2`, `file3` (not `file1`) |
| `{a,b,...}` | Matches **any comma-separated pattern** | `ls *.{txt,pdf}` | `doc.txt`, `manual.pdf` |

---

## 📦 **Sample Files**

```
car  carpet  ca  help  hell  file  file1  file2  hello  dello  file3  doc.txt  manual.pdf

```

---

### 🧪 **Test Examples with Commands**

🔹 `ls ca*`

✅ Matches: `car`, `carpet`, `ca`

🧠 Uses `*` to match anything after "ca".

🔹 `ls hel?`

✅ Matches: `help`, `hell`

🧠 Uses `?` to match one character after "hel".

🔹 `ls file[0-2]`

✅ Matches: `file`, `file1`, `file2`

🧠 Uses `[0-2]` to allow only digits 0 through 2.

🔹 `ls [hd]ello`

✅ Matches: `hello`, `dello`

🧠 Matches either `h` or `d` at the start.

🔹 `ls file[^1]`

✅ Matches: `file2`, `file3`

🧠 Excludes filenames with `file1`.

🔹 `ls *.{txt,pdf}`

✅ Matches: `doc.txt`, `manual.pdf`

🧠 Matches both `.txt` and `.pdf` files.

---

## 🧠 **Tips**

- Wildcards expand only filenames **in the current directory**.
- Always use quotes (`"*.txt"`) to prevent shell from expanding patterns when necessary.
- Wildcards are powerful for **batch operations**, such as deleting or moving multiple files.

---

✅ **Best Used In:**

File searches, script automation, backups, and managing large directories.

---

Let me know if you want this as a **PDF or printable colorful sheet**.
