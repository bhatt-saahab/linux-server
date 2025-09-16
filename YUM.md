

# Yum Command Reference Notes

## General Yum Commands

**Displays Yum Version**

- **Command**: `yum version`
    - **Description**: Displays Yum version information.
    - **Example**:
        
        ```bash
        yum version
        
        ```
        

**List Enabled Repositories**

- **Command**: `yum repolist`
    - **Description**: Lists enabled repositories.
    - **Example**:
        
        ```bash
        yum repolist
        
        ```
        

**List All Repositories (Including Disabled)**

- **Command**: `yum repolist all`
    - **Description**: Lists all repositories, including disabled ones.
    - **Example**:
        
        ```bash
        yum repolist all
        
        ```
        

**List All Available Packages**

- **Command**: `yum list`
    - **Description**: Lists all available packages.
    - **Example**:
        
        ```bash
        yum list
        
        ```
        

**Count All Available Packages**

- **Command**: `yum list | wc -l`
    - **Description**: Counts the total number of available packages.
    - **Example**:
        
        ```bash
        yum list | wc -l
        
        ```
        

**List All Packages (Installed + Available)**

- **Command**: `yum list all`
    - **Description**: Lists all packages, both installed and available.
    - **Example**:
        
        ```bash
        yum list all
        
        ```
        

**Count All Packages (Installed + Available)**

- **Command**: `yum list all | wc -l`
    - **Description**: Counts the total number of all packages (installed and available).
    - **Example**:
        
        ```bash
        yum list all | wc -l
        
        ```
        

**List Installed Packages**

- **Command**: `yum list installed`
    - **Description**: Lists all installed packages.
    - **Example**:
        
        ```bash
        yum list installed
        
        ```
        

**Count Installed Packages**

- **Command**: `yum list installed | wc -l`
    - **Description**: Counts the total number of installed packages.
    - **Example**:
        
        ```bash
        yum list installed | wc -l
        
        ```
        

**List Available Packages**

- **Command**: `yum list available`
    - **Description**: Lists packages available for installation.
    - **Example**:
        
        ```bash
        yum list available
        
        ```
        

**Count Available Packages**

- **Command**: `yum list available | wc -l`
    - **Description**: Counts the total number of available packages.
    - **Example**:
        
        ```bash
        yum list available | wc -l
        
        ```
        

**List Recently Installed or Updated Packages**

- **Command**: `yum list recent`
    - **Description**: Lists recently installed or updated packages.
    - **Example**:
        
        ```bash
        yum list recent
        
        ```
        

**List Installed Packages Not in Enabled Repos**

- **Command**: `yum list extras`
    - **Description**: Lists installed packages not available from enabled repositories.
    - **Example**:
        
        ```bash
        yum list extras
        
        ```
        

**Check for Problems and Dependency Issues**

- **Command**: `yum check`
    - **Description**: Checks for problems such as dependency issues.
    - **Example**:
        
        ```bash
        yum check
        
        ```
        

**Check for Available Package Updates**

- **Command**: `yum check-update`
    - **Description**: Checks for available updates for installed packages.
    - **Example**:
        
        ```bash
        yum check-update
        
        ```
        

**Update All Installed Packages**

- **Command**: `yum update`
    - **Description**: Updates all installed packages to the latest version.
    - **Example**:
        
        ```bash
        yum update
        
        ```
        

**Upgrade All Installed Packages**

- **Command**: `yum upgrade`
    - **Description**: Same as `update` but may also remove obsolete packages.
    - **Example**:
        
        ```bash
        yum upgrade
        
        ```
        

---

## Package Search and Information

**Search for Packages by Keyword**

- **Command**: `yum search <package>`
    - **Description**: Searches for packages containing the specified keyword.
    - **Example**:
        
        ```bash
        yum search nmap
        
        ```
        

**Display Detailed Package Information**

- **Command**: `yum info <package>`
    - **Description**: Displays detailed information about a specific package.
    - **Examples**:
        
        ```bash
        yum info gzip.x86_64
        yum info python3
        yum info vim-enhanced.x86_64
        yum info vlc
        
        ```
        

**Find Package Providing a File or Feature**

- **Command**: `yum provides <file>`
    - **Description**: Shows which package provides a specific file or feature.
    - **Examples**:
        
        ```bash
        yum provides nmap
        yum provides vlc
        
        ```
        

---

## Package Installation, Update, and Removal

**Install a Package**

- **Command**: `yum install <package>`
    - **Description**: Installs one or more packages.
    - **Examples**:
        
        ```bash
        yum install python
        yum install curl
        yum install git
        yum install wget
        yum install vlc
        yum install net-tools.x86_64
        
        ```
        

**Install Packages Matching a Pattern**

- **Command**: `yum install <pattern>`
    - **Description**: Installs all packages matching the specified pattern.
    - **Examples**:
        
        ```bash
        yum install bash*
        yum install nmap*
        
        ```
        

**Install with Automatic Yes**

- **Command**: `yum install <package> -y`
    - **Description**: Installs a package without prompting for confirmation.
    - **Example**:
        
        ```bash
        yum install vlc -y
        
        ```
        

**Update a Specific Package**

- **Command**: `yum update <package>`
    - **Description**: Updates a specific package to the latest version.
    - **Examples**:
        
        ```bash
        yum update gzip
        yum update nmap
        
        ```
        

**Upgrade a Specific Package**

- **Command**: `yum upgrade <package>`
    - **Description**: Upgrades a specific package to the latest version.
    - **Examples**:
        
        ```bash
        yum upgrade nmap
        yum upgrade vim
        
        ```
        

**Remove a Package**

- **Command**: `yum remove <package>`
    - **Description**: Removes/uninstalls a package.
    - **Examples**:
        
        ```bash
        yum remove nmap
        yum remove gnome*
        
        ```
        

**Remove Packages Matching a Pattern**

- **Command**: `yum remove <pattern>`
    - **Description**: Removes all packages matching the specified pattern.
    - **Example**:
        
        ```bash
        yum remove nmap*
        
        ```
        

**Reinstall a Package**

- **Command**: `yum reinstall <package>`
    - **Description**: Reinstalls an already installed package.
    - **Example**:
        
        ```bash
        yum reinstall vlc
        
        ```
        

**Downgrade a Package**

- **Command**: `yum downgrade <package>`
    - **Description**: Downgrades a package to an earlier version.
    - **Examples**:
        
        ```bash
        yum downgrade nmap
        yum downgrade vlc
        
        ```
        

**Downgrade with Skip Broken Dependencies**

- **Command**: `yum downgrade <package> --skip-broken`
    - **Description**: Downgrades a package while skipping broken dependencies.
    - **Example**:
        
        ```bash
        yum downgrade vlc --skip-broken
        
        ```
        

---

## Package Dependency Management

**List Package Dependencies**

- **Command**: `yum deplist <package>`
    - **Description**: Lists dependencies required by a package.
    - **Example**:
        
        ```bash
        yum deplist vlc
        
        ```
        

**Find Package Providing a File or Feature**

- **Command**: `yum provides <file>`
    - **Description**: Shows which package provides a specific file or feature (repeated for clarity).
    - **Examples**:
        
        ```bash
        yum provides nmap
        yum provides vlc
        
        ```
        

---

## Cache Management

**Clean All Cached Data**

- **Command**: `yum clean all`
    - **Description**: Removes all cached package data and metadata.
    - **Example**:
        
        ```bash
        yum clean all
        
        ```
        

**Update Metadata Cache**

- **Command**: `yum makecache`
    - **Description**: Generates and updates metadata cache.
    - **Example**:
        
        ```bash
        yum makecache
        
        ```
        

**Manually Delete DNF Cache**

- **Command**:
    
    ```bash
    rm -rf /var/cache/dnf
    
    ```
    
    - **Description**: Manually deletes the DNF cache directory (used on newer systems).
    - **Example**:
        
        ```bash
        cd /var/cache/dnf
        rm -rf /var/cache/dnf
        
        ```
        

---

## Yum Package History and Sync

**Show Transaction History**

- **Command**: `yum history`
    - **Description**: Shows the transaction history of package operations.
    - **Example**:
        
        ```bash
        yum history
        
        ```
        

**Sync Packages to Repository Versions**

- **Command**: `yum distro-sync`
    - **Description**: Synchronizes installed packages to the exact versions in enabled repositories.
    - **Example**:
        
        ```bash
        yum distro-sync
        
        ```
        

**List Available Languages for Yum**

- **Command**: `yum langavailable`
    - **Description**: Lists available languages for Yum.
    - **Example**:
        
        ```bash
        yum langavailable
        
        ```
        

---

## Yum Groups Commands

**List All Package Groups**

- **Command**: `yum groups` or `yum groups list`
    - **Description**: Lists all available package groups.
    - **Examples**:
        
        ```bash
        yum groups
        yum groups list
        
        ```
        

**Show Information About a Group**

- **Command**: `yum group info <group>`
    - **Description**: Shows information about a specific package group.
    - **Example**:
        
        ```bash
        yum group info "System Tools"
        
        ```
        

**Install a Package Group**

- **Command**: `yum groups install <group>`
    - **Description**: Installs a package group.
    - **Examples**:
        
        ```bash
        yum groups install "System Tools"
        yum groups install "Development Tools"
        yum groups install "Compute Node"
        
        ```
        

**Remove a Package Group**

- **Command**: `yum groups remove <group>`
    - **Description**: Removes a package group.
    - **Examples**:
        
        ```bash
        yum groups remove "System Tools"
        yum groups remove "Compute Node"
        
        ```
        

**Summary of a Package Group**

- **Command**: `yum groups summary <group>`
    - **Description**: Provides a summary of a package group.
    - **Example**:
        
        ```bash
        yum groups summary "Compute Node"
        
        ```
        

**Mark a Group as Installed**

- **Command**: `yum groups mark install <group>`
    - **Description**: Marks a package group as installed.
    - **Example**:
        
        ```bash
        yum groups mark install "Console Internet Tools"
        
        ```
        

**Mark a Group as Removed**

- **Command**: `yum groups mark remove <group>`
    - **Description**: Marks a package group as removed.
    - **Example**:
        
        ```bash
        yum groups mark remove "Console Internet Tools"
        
        ```
        

---

## CentOS 6 Specific Group Commands

**List Package Groups (CentOS 6)**

- **Command**: `yum grouplist`
    - **Description**: Lists package groups in CentOS 6 format.
    - **Example**:
        
        ```bash
        yum grouplist
        
        ```
        

**Install a Group (CentOS 6)**

- **Command**: `yum groupinstall <group>`
    - **Description**: Installs a package group in CentOS 6 format.
    - **Examples**:
        
        ```bash
        yum groupinstall "System Administration Tools"
        yum groupinstall Haskell
        
        ```
        

**Remove a Group (CentOS 6)**

- **Command**: `yum groupremove <group>`
    - **Description**: Removes a package group in CentOS 6 format.
    - **Example**:
        
        ```bash
        yum groupremove Haskell
        
        ```
        

---

## Example Workflow: Installing and Managing Vim

1. **Search for Vim Packages**:
    
    ```bash
    yum search vim
    
    ```
