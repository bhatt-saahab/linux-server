

The **chmod** (change mode) command in Linux modifies permissions for files and directories. It supports two methods: **Symbolic** and **Numeric (Octal)**, allowing fine-grained control over access permissions.

---

## 1. Symbolic Method

### Permissions

- **r** = read
- **w** = write
- **x** = execute

### Scope

- **u** = user/owner
- **g** = group
- **o** = others
- **a** = all (u + g + o)

### Common Symbolic Usage

Below are examples of chmod commands using the symbolic method for the file `password-armour` or directory `log/`. The commands modify permissions by adding (+), removing (-), or setting (=) specific permissions.

1. **Add write for others**:
    
    ```bash
    chmod o+w password-armour
    
    ```
    
2. **Remove write from others**:
    
    ```bash
    chmod o-w password-armour
    
    ```
    
3. **Add read, write for group**:
    
    ```bash
    chmod g+rw password-armour
    
    ```
    
4. **Remove write from group**:
    
    ```bash
    chmod g-w password-armour
    
    ```
    
5. **Add execute for owner**:
    
    ```bash
    chmod u+x password-armour
    
    ```
    
6. **Set owner permission to read, write, execute**:
    
    ```bash
    chmod u+rwx password-armour
    
    ```
    
7. **Remove all permissions from owner**:
    
    ```bash
    chmod u-rwx password-armour
    
    ```
    
8. **Add all permissions for everyone (u, g, o)**:**Equivalent** (shorthand):
    
    ```bash
    chmod ugo+rwx password-armour
    
    ```
    
    ```bash
    chmod a+rwx password-armour
    
    ```
    
9. **Remove all permissions for all users**:
    
    ```bash
    chmod a-rwx password-armour
    
    ```
    
10. **Set owner: rwx, group: rw, others: r**:
    
    ```bash
    chmod u+rwx,g+rw,o+r password-armour
    
    ```
    
11. **Set group permission to read, write (removes execute if present)**:
    
    ```bash
    chmod g=rw password-armour
    
    ```
    
12. **All users: read, write only**:
    
    ```bash
    chmod a=rw password-armour
    
    ```
    
13. **Owner & group: rwx, others: r**:
    
    ```bash
    chmod u=rwx,g=rwx,o=r password-armour
    
    ```
    
14. **Add execute for all users (shorthand)**:
    
    ```bash
    chmod +x password-armour
    
    ```
    
15. **Directory: All users get rwx**:
    
    ```bash
    chmod a+rwx log/
    
    ```
    

---

## 2. Numeric (Octal) Method

### Permissions Values

- **4** = read (r)
- **2** = write (w)
- **1** = execute (x)
- **0** = no permissions

Combine values for each scope (user, group, others) by adding them:

- **7** = rwx (4 + 2 + 1)
- **6** = rw- (4 + 2)
- **5** = r-x (4 + 1)
- **4** = r-- (4)
- **0** = --- (none)

### Order

Permissions are specified in the order: **user (u), group (g), others (o)**.

### Common Numeric Usage

Below are examples of chmod commands using the numeric method for the file `password-armour`, directory `log/`, or specific files.

1. **Only owner: rwx; no one else has permissions**:
    
    ```bash
    chmod 700 password-armour
    
    ```
    
2. **Owner: rwx, group: r, others: r**:
    
    ```bash
    chmod 744 password-armour
    
    ```
    
3. **Owner: rwx, group: rx, others: rx (typical for scripts/programs)**:
    
    ```bash
    chmod 755 password-armour
    
    ```
    
4. **All have rwx (not recommended for security)**:
    
    ```bash
    chmod 777 password-armour
    
    ```
    
5. **No one has any access**:
    
    ```bash
    chmod 000 password-armour
    
    ```
    
6. **Directory: Owner: rwx, group/others: rx**:
    
    ```bash
    chmod 755 log/
    
    ```
    
7. **Verbosely & recursively set rwx for all under log/**:
    
    ```bash
    chmod -vR 777 log/
    
    ```
    
8. **Verbosely & recursively set rwxr-xr-x for all under log/**:
    
    ```bash
    chmod -vR 755 log/
    
    ```
    
9. **Verbosely set owner: rwx, others: none for all .log files**:
    
    ```bash
    chmod -v 700 *.log
    
    ```
    
10. **Set 744 permissions on listed files**:
    
    ```bash
    chmod 744 messages boot.log cron firewalld
    
    ```
    

---

## Tips

- **Verify Permissions**: Use `ls -l` to check permissions before and after applying `chmod`.
- **Symbolic vs. Numeric**:
    - **Symbolic**: Clearer for ad-hoc, specific changes (e.g., adding execute for owner only).
    - **Numeric**: Common in scripts for setting precise permissions in one command.
- **Recursive Use**: Use `chmod -R` for directories, but double-check to avoid unintended changes.
- **Security Note**: Avoid overly permissive settings (e.g., `777`) to prevent unauthorized access.

---

## Key Points

- **chmod** modifies file and directory permissions using **symbolic** (r, w, x; u, g, o) or **numeric** (octal) methods.
- **Symbolic Method**: Flexible for adding/removing specific permissions; uses `+`, , `=` operators.
- **Numeric Method**: Concise, using octal values (0–7) to set permissions for user, group, and others.
- **Recursive Flag (-R)**: Applies changes to directories and their contents; use cautiously.
- **Verbose Flag (-v)**: Displays changes made for confirmation.
- **Security**: Always verify changes with `ls -l` and avoid overly permissive settings like `777`.

---

**Note**: All details from the provided input have been included, with typos corrected (e.g., "exefute" → "execute," "wrlle" → "write," "0 = others" → "o = others"). The notes are structured for clarity and completeness. If you need further clarification, examples, or a specific chmod command tailored to a scenario, let me know!
