The `su` (switch user or substitute user) and `sg` (switch group) commands in Linux allow users to temporarily assume the identity of another user or group to perform tasks with their permissions. These commands are essential for administrative tasks, privilege escalation, and executing commands in a specific user or group context.

## Key Concepts

1. **su Command**:
    - Allows a user to switch to another user account or run commands as another user (typically the root user) without logging out.
    - Requires the target user’s password unless executed by the root user.
    - Can initiate a new shell session or execute a single command as the target user.
    - 
    
    ## If `user1` switches to `user2` with `su`
    
    - After giving **user2’s password**, `user1` becomes `user2`.
    - Now `user1` has **all powers of user2** (no more powers of `user1`).
    - It’s like **wearing user2’s ID card** 🪪 → you act as `user2`.
    
    ---
    
    ## 🔹 If `user1` switches to `root` with `su -`
    
    - After giving **root password**, `user1` becomes root.
    - Now `user1` has **full root powers** (superuser, can do anything).
    - It’s like **becoming the admin of the system** 🛠.
    
    ## 
    
2. **sg Command**:
    - Allows a user to execute commands with the privileges of a specified group.
    - Similar to `su` but focuses on group privileges rather than user accounts.
    - Requires the user to be a member of the target group or have appropriate permissions.
3. **Use Cases**:
    - `su`: Used for administrative tasks, such as managing system files or services as the root user.
    - `sg`: Used to run commands with group-specific permissions, such as accessing files restricted to a particular group.
4. **Related Tools**:
    - `sudo`: Often preferred over `su` for controlled privilege escalation.
    - Group membership management commands: `groups`, `newgrp`.

---

## Using the `su` Command

The `su` command allows switching to another user’s account or running commands as that user.

### Basic Syntax

- **Command**: `su [options] [username]`
    - If no username is specified, `su` defaults to switching to the root user.
    - Example: `su` (switches to root, prompts for root password).
    - Example: `su john` (switches to user `john`, prompts for john’s password).

### Common Options

- or `l` or `-login`: Starts a new login shell, initializing the environment as if the user logged in directly.
    - Example: `su - john` (starts a login shell as user `john`).
- `c` or `-command`: Executes a single command as the specified user and exits.
    - Example: `su -c "ls /root" john` (runs `ls /root` as user `john`).
- `s` or `-shell`: Specifies the shell to use for the session.
    - Example: `su -s /bin/bash john` (uses `/bin/bash` as the shell for `john`).

### Examples

- Switch to root user with a login shell:
    
    ```
    su -
    
    ```
    
- Switch to user `john` without changing the environment:
    
    ```
    su john
    
    ```
    
- Run a single command as root:
    
    ```
    su -c "systemctl restart apache2"
    
    ```
    

### Notes

- Without the  option, `su` keeps the current user’s environment variables, which may lead to unexpected behavior.
- Root can use `su` to switch to any user without a password; regular users need the target user’s password.

---

## Using the `sg` Command

The `sg` command allows running commands with the privileges of a specified group.

### Basic Syntax

- **Command**: `sg groupname [-c command]`
    - Executes a new shell or a specific command with the specified group’s privileges.
    - Example: `sg developers` (starts a new shell with `developers` group privileges).
    - Example: `sg developers -c "touch /shared/project.txt"` (runs the command with `developers` group privileges).

### Common Options

- `c`: Executes a single command with the specified group’s privileges.
    - Example: `sg developers -c "cat /shared/file.txt"`.

### Prerequisites

- The user must be a member of the target group (check with `groups` command).
- If the user is not a member, they need appropriate permissions (e.g., via `sudo`).

### Examples

- Start a shell with `developers` group privileges:
    
    ```
    sg developers
    
    ```
    
- Create a file with `developers` group ownership:
    
    ```
    sg developers -c "touch /shared/newfile.txt"
    
    ```
    

### Notes

- `sg` is less commonly used than `su` or `sudo` but is useful for group-specific tasks.
- The `newgrp` command is an alternative to `sg` for switching group contexts in a new shell.

---

## Viewing User and Group Information

To verify the context of users and groups:

- **Check Current User**:
    - Command: `whoami`
    - Example: `whoami` (displays the current effective user).
- **Check Current Groups**:
    - Command: `groups`
    - Example: `groups` (lists groups the current user belongs to).
- **Check Effective Group**:
    - Command: `id -g --name`
    - Example: `id -g --name` (displays the current effective group).

---

## Practical Examples

1. **As an Admin**:
    - Switch to root to install a package:
        
        ```
        su -c "yum install vim"
        
        ```
        
    - Restart a service as root:
        
        ```
        su -c "systemctl restart nginx"
        
        ```
        
2. **As a Developer**:
    - Access a group-restricted directory:
        
        ```
        sg developers -c "cd /shared/project && make"
        
        ```
        
    - Create a file with group permissions:
        
        ```
        sg developers -c "echo 'Code' > /shared/code.txt"
        
        ```
        

---

## Summary of Commands

| **Action** | **Command Example** | **Description** |
| --- | --- | --- |
| Switch to root user | `su -` | Start a login shell as root |
| Switch to another user | `su john` | Switch to user `john` (non-login shell) |
| Run command as another user | `su -c "ls /root" john` | Run `ls /root` as user `john` |
| Specify shell for su | `su -s /bin/bash john` | Switch to `john` using `/bin/bash` shell |
| Run command with group | `sg developers -c "touch /shared/file.txt"` | Run command with `developers` group privileges |
| Start shell with group | `sg developers` | Start a new shell with `developers` group privileges |
| Check current user | `whoami` | Display current effective user |
| Check current groups | `groups` | List groups the current user belongs to |

---

## Notes

- **Security Considerations**:
    - Use `su` cautiously, especially when switching to root, as it grants full access.
    - Prefer `sudo` for controlled privilege escalation in production environments.
    - Ensure group memberships are correctly configured before using `sg`.
- **Environment Preservation**:
    - Use `su -` for a clean login environment; plain `su` retains the current user’s environment.
- **Group Context**:
    - `sg` requires the user to be a member of the target group or have elevated privileges.
- **Alternatives**:
    - `sudo`: For fine-grained control and logging of commands.
    - `newgrp`: For switching group contexts in a new shell, similar to `sg`.
- Always verify the current user and group context after switching using `whoami` or `groups`.
