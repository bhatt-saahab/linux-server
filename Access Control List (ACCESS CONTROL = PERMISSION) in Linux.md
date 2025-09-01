---

Access Control Lists (ACLs) extend the standard Linux permission model by allowing fine-grained permissions to be assigned to multiple users and groups for files and directories, beyond the traditional owner-group-other permission scheme.

## Key Concepts

1. **Standard Permissions**:
    - Linux uses three permission sets for files/directories:
        - **User (owner)**: Permissions for the file/directory owner.
        - **Group**: Permissions for the group associated with the file/directory.
        - **Others**: Permissions for all other users.
    - Represented as read (`r`), write (`w`), and execute (`x`).
2. **Extended Permissions (ACLs)**:
    - Allow assigning specific permissions to multiple individual users and groups, beyond the standard model.
    - Provides more granular control over access.
3. **Supported Filesystems**:
    - Filesystems like `ext3`, `ext4`, and `XFS` support ACLs.
    - ACL support must be enabled when mounting the filesystem.

---

## Enabling ACL on a Filesystem

To use ACLs, the filesystem must be mounted with ACL support enabled.

### Steps to Enable ACL

1. **Mount Filesystem with ACL Support**:
    - Command: `mount -o acl /dev/sdX /mountpoint`
        - Example: `mount -o acl /dev/sda1 /data`
    - This enables ACL support temporarily for the current session.
2. **Make ACL Support Permanent**:
    - Edit the `/etc/fstab` file to include the `acl` option.
    - Example `/etc/fstab` entry:
        
        ```
        /dev/sdX /mountpoint ext4 defaults,acl 0 2
        
        ```
        
    - Example `/etc/fstab` with UUID:
        
        ```
        UUID=50705329-bc44-4c8c-a9c4-cf017a00404e / xfs defaults,acl 0 0
        UUID=e8b49578-4abd-4328-9199-9a670eec4376 /boot xfs defaults 0 0
        UUID=04173dec-b439-43a5-bfde-6aa5e2000083 none swap defaults 0 0
        
        ```
        
3. **Install ACL Tools**:
    - Ensure ACL utilities are installed to manage ACLs.
    - Command (for Red Hat-based systems): `yum install acl`
    - This installs tools like `getfacl` and `setfacl`.

---

## Viewing ACLs

To check the ACL entries for a file or directory:

- **Command**: `getfacl /path/to/file_or_directory`
    - Example: `getfacl /data2`
- **Recursive ACL Display**:
    - Command: `getfacl -R /path/to/directory`
    - Example: `getfacl -R /data`
- **Indicator in File Listings**:
    - A `+` in the `ls -l` output (e.g., `rw-rw-r--+`) indicates the presence of ACLs.
- **Alternative Command**:
    - `chacl -l filename`: Lists ACL entries (less common).

---

## Setting ACL Entries

Use the `setfacl` command with the `-m` (modify) option to add or update ACL entries.

### Add Permissions for a User

- **Command**: `setfacl -m u:username:permissions filename`
- **Example**: `setfacl -m u:armour:rwx /data2`
    - Grants read, write, and execute permissions to user `armour` for `/data2`.

### Add Permissions for a Group

- **Command**: `setfacl -m g:groupname:permissions filename`
- **Example**: `setfacl -m g:IT:rwx /data2`
    - Grants read, write, and execute permissions to the `IT` group for `/data2`.

### Recursive ACL Application

- **Command**: `setfacl -R -m u:username:permissions /directory`
- **Example**: `setfacl -R -m u:armour:rwx /data`
    - Applies permissions recursively to all files and subdirectories in `/data`.

---

## Default ACLs on Directories

Default ACLs ensure that new files and directories created within a directory inherit specific ACL permissions.

- **Command**: `setfacl -d -m u:username:permissions directory`
- **Example**: `setfacl -d -m u:armour:rwx /data2`
    - New files and directories in `/data2` will automatically inherit `rwx` permissions for user `armour`.

---

## Removing ACL Entries

Use the `setfacl` command with the `-x` or `-b` options to remove ACL entries.

### Remove a Specific ACL Entry

- **For a User**:
    - Command: `setfacl -x u:username /path`
    - Example: `setfacl -x u:armour /data`
- **For a Group**:
    - Command: `setfacl -x g:groupname /path`
    - Example: `setfacl -x g:EMP /data`
- **For a Default ACL**:
    - Command: `setfacl -d -x u:username /path`
    - Example: `setfacl -d -x u:armour /data`

### Remove All ACL Entries

- **Command**: `setfacl -b /path`
- **Example**: `setfacl -b /data2`
    - Removes all ACL entries and reverts to traditional owner-group-other permissions.
- **Recursive Removal**:
    - Command: `setfacl -R -b /path`
    - Example: `setfacl -R -b /data`

---

## Summary of ACL Commands

| **Action** | **Command Example** | **Description** |
| --- | --- | --- |
| View ACL | `getfacl filename` | Show ACL entries for a file or directory |
| Set ACL for user | `setfacl -m u:armour:rwx /data2` | Add `rwx` permissions for user `armour` |
| Set ACL for group | `setfacl -m g:IT:rwx /data2` | Add `rwx` permissions for group `IT` |
| Set default ACL on directory | `setfacl -d -m u:armour:rwx /data2` | Set default ACL for new files in `/data2` |
| Remove specific ACL entry | `setfacl -x u:armour /data2` | Remove ACL entry for user `armour` |
| Remove all ACL entries | `setfacl -b /data2` | Remove all ACLs and revert to standard permissions |
| Recursive set ACL | `setfacl -R -m u:armour:rwx /data` | Recursively apply ACL to directory and contents |
| List ACLs (alternative) | `chacl -l filename` | Alternative command to list ACL entries |

---

## Notes

- Always ensure the filesystem supports ACLs and is mounted with the `acl` option.
- Use `getfacl` to verify ACLs after making changes.
- The `+` in `ls -l` output is a quick way to identify files/directories with ACLs.
- Default ACLs are particularly useful for directories where consistent permissions are needed for new files.
- Be cautious when removing ACLs, as it may affect access for users or groups relying on those permissions.

---

These notes cover all the provided details in a structured, clear, and concise manner, ensuring no critical information is missed. Let me know if you need further clarification or additional details!
