# DNF Package Manager

DNF (Dandified Yum) is the next-generation package manager for RPM-based Linux distributions such as Fedora, Red Hat Enterprise Linux (RHEL) 8+, CentOS Stream, Rocky Linux, and others. It replaces the older YUM package manager, offering improved performance, better dependency resolution, and a modernized codebase.

## Key Features

- Installs, updates, and removes software packages with automatic dependency management
- Uses RPM packages and repositories
- Supports package groups for managing collections of related packages
- Maintains history of transactions for rollbacks and auditing
- Offers plugin system to extend functionality
- Compatible command syntax with YUM for ease of transition

**`rpm`** → installs a single package file (no dependency handling) ⚠️

**`dnf`** → high-level package manager (auto-resolves dependencies, updates, repos) ✅

## Basic Usage

- **Update all packages**:
    
    ```bash
    dnf update
    
    ```
    
- **Install a package**:
    
    ```bash
    dnf install <package>
    
    ```
    
- **Remove a package**:
    
    ```bash
    dnf remove <package>
    
    ```
    
- **Search for packages**:
    
    ```bash
    dnf search <keyword>
    
    ```
    
- **Show package info**:
    
    ```bash
    dnf info <package>
    
    ```
    
- **List all packages**:
    
    ```bash
    dnf list
    
    ```
    
- **List installed packages**:
    
    ```bash
    dnf list installed
    
    ```
    
- **List available packages**:
    
    ```bash
    dnf list available
    
    ```
    
- **List packages with available updates**:
    
    ```bash
    dnf list updates
    
    ```
    
- **List packages with available upgrades**:
    
    ```bash
    dnf list upgrades
    
    ```
    
- **List recently added packages**:
    
    ```bash
    dnf list recent
    
    ```
    
- **List installed packages not found in enabled repos**:
    
    ```bash
    dnf list extras
    
    ```
    
- **Check for problems in the package database**:
    
    ```bash
    dnf check
    
    ```
    
- **Clean package cache**:
    
    ```bash
    dnf clean all
    
    ```
    
- **View transaction history**:
    
    ```bash
    dnf history
    
    ```
    
- **Manage package groups**:
    - List available package groups:
        
        ```bash
        dnf group list
        
        ```
        
    - Install a package group:
        
        ```bash
        dnf group install "<group>"
        
        ```
        
    - Remove a package group:
        
        ```bash
        dnf group remove "<group>"
        
        ```
        

## Advanced Commands

- **Upgrade all packages (removes obsolete ones)**:
    
    ```bash
    dnf upgrade
    
    ```
    
- **Undo a specific transaction**:
    
    ```bash
    dnf history undo <transaction_id>
    
    ```
    
- **Roll back system state to a specific transaction**:
    
    ```bash
    dnf history rollback <transaction_id>
    
    ```
    
- **Show information about a specific package group**:
    
    ```bash
    dnf group info "<group>"
    
    ```
    
- **List dependencies for a specified package**:
    
    ```bash
    dnf deplist <package>
    
    ```
    
- **Find which package provides a specified file**:
    
    ```bash
    dnf provides <file>
    
    ```
    
- **List enabled repositories**:
    
    ```bash
    dnf repolist
    
    ```
    
- **List all repositories (including disabled)**:
    
    ```bash
    dnf repolist all
    
    ```
    
- **Add a new repository**:
    
    ```bash
    dnf config-manager --add-repo <url>
    
    ```
    
- **Disable a repository**:
    
    ```bash
    dnf config-manager --disable <repo>
    
    ```
    
- **Enable a repository**:
    
    ```bash
    dnf config-manager --enable <repo>
    
    ```
    
- **Remove all orphaned packages**:
    
    ```bash
    dnf autoremove
    
    ```
    
- **Show DNF version information**:
    
    ```bash
    dnf version
    
    ```
    

## Command Summary

| Command | Description |
| --- | --- |
| `dnf update` | Update all installed packages to the latest version |
| `dnf upgrade` | Upgrade all packages, removing obsolete ones if needed |
| `dnf install <package>` | Install specified package(s) |
| `dnf remove <package>` | Remove specified package(s) and unnecessary dependencies |
| `dnf search <keyword>` | Search for packages matching the keyword |
| `dnf info <package>` | Show detailed info about a package |
| `dnf list` | List all available and installed packages |
| `dnf list installed` | List installed packages |
| `dnf list available` | List packages available for installation |
| `dnf list updates` | List packages with available updates |
| `dnf list extras` | List installed packages not found in enabled repos |
| `dnf check` | Check for problems in the package database |
| `dnf clean all` | Clean package cache |
| `dnf history` | Show history of package transactions |
| `dnf history undo <transaction_id>` | Undo a specific transaction by its ID |
| `dnf history rollback <transaction_id>` | Roll back system state to a specific transaction |
| `dnf group list` | List all available package groups |
| `dnf group info "<group>"` | Show information about a specific package group |
| `dnf group install "<group>"` | Install a package group |
| `dnf group remove "<group>"` | Remove a package group |
| `dnf deplist <package>` | List dependencies for a specified package |
| `dnf provides <file>` | Find which package provides a specified file |
| `dnf repolist` | List enabled repositories |
| `dnf repolist all` | List all repositories, including disabled ones |
| `dnf config-manager --add-repo <url>` | Add a new repository |
| `dnf config-manager --disable <repo>` | Disable a repository |
| `dnf config-manager --enable <repo>` | Enable a repository |
| `dnf autoremove` | Remove all orphaned packages no longer needed |
| `dnf version` | Show DNF version information |

## Configuration Files

- **Global configuration**: `/etc/dnf/dnf.conf`
- **Repository definitions**: `/etc/yum.repos.d/`

## Additional Resources

- Fedora DNF Documentation
- DNF Command Reference
