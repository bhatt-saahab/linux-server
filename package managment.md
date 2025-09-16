# Red Hat Package Manager (RPM) Notes

This document provides detailed notes on the Red Hat Package Manager (RPM), a powerful package management system used primarily in Red Hat-based Linux distributions like RHEL, CentOS, and Fedora. It covers key features, package types, the RPM database, naming conventions, and common commands with copyable examples.

- **`rpm`** = just installs a raw file (like double-clicking an `.exe`).
- **`yum`/`dnf`** = smart installers that also fetch and install dependencies automatically (like an app store).

---

## Overview of RPM

RPM (Red Hat Package Manager) is an open-source package management system designed for Red Hat-based Linux distributions but also used across various UNIX and Linux systems. It facilitates the installation, uninstallation, upgrading, querying, listing, and verification of software packages.

### Key Features

- **File Extension**: `.rpm` is the standard file extension for RPM packages.
- **Usage**: Manages software, documentation, and source code packages.
- **Package Types**:
    - **Binary RPM**: Contains precompiled applications or libraries.
    - **Source RPM (SRPM)**: Includes source code and build instructions for compiling software locally.
- **Architecture Types**:
    - `i386`: For 32-bit systems.
    - `x86_64`: For 64-bit systems.
    - `noarch`: Architecture-independent software (e.g., scripts, documentation).
- **Package Contents**:
    - Application binaries or libraries.
    - Documentation (e.g., man pages).
    - Configuration files.
    - SPEC file (`.spec`): Contains metadata, build instructions, and scripts for packaging.

---

## RPM Database

RPM maintains a database in `/var/lib/rpm` to track installed packages, their versions, and metadata. This database is essential for:

- Package verification.
- Querying installed packages.
- Managing dependencies and conflicts.

---

## RPM Package Naming Convention

RPM packages follow a structured naming convention. Example:

**httpd-2.4.6-93.el7.centos.x86_64.rpm**

- **httpd**: Package name (e.g., Apache HTTP Server).
- **2.4.6**: Package version.
- **93**: Release number (incremented for updates or rebuilds).
- **el7**: Target distribution and version (Enterprise Linux 7).
- **centos**: Distribution variant (CentOS).
- **x86_64**: Architecture (64-bit).
- **.rpm**: File format.

---

## Common RPM Commands

Below are common RPM commands categorized by function, with copyable examples. Each command includes a button to copy the command for easy execution.

### Querying Packages

### Check if a Package is Installed

- **Description**: Queries whether a specific package is installed.
- **Command**:
    
    ```bash
    rpm -q package-name
    
    ```
    
    Copy Command
    

### List All Installed Packages

- **Description**: Displays all packages installed on the system.
- **Command**:
    
    ```bash
    rpm -qa
    
    ```
    
    Copy Command
    

### Check Detailed Package Information

- **Description**: Provides detailed metadata about an installed package.
- **Command**:
    
    ```bash
    rpm -qi package-name
    
    ```
    
    Copy Command
    

### List Files in a Package

- **Description**: Lists all files installed by a package.
- **Command**:
    
    ```bash
    rpm -ql package-name
    
    ```
    
    Copy Command
    

### List Configuration Files of a Package

- **Description**: Lists configuration files associated with a package.
- **Command**:
    
    ```bash
    rpm -qc package-name
    
    ```
    
    Copy Command
    

### List Documentation Files

- **Description**: Lists documentation files (e.g., man pages) for a package.
- **Command**:
    
    ```bash
    rpm -qd package-name
    
    ```
    
    Copy Command
    

### Verify Package Integrity

- **Description**: Verifies the integrity of a package’s files against the RPM database.
- **Command**:
    
    ```bash
    rpm -V package-name
    
    ```
    
    Copy Command
    

### Query Which Package Owns a File

- **Description**: Identifies which package owns a specific file.
- **Command**:
    
    ```bash
    rpm -qf /path/to/file
    
    ```
    
    Copy Command
    

### Installing Packages

### Install a Package

- **Description**: Installs a new RPM package.
- **Command**:
    
    ```bash
    rpm -i package.rpm
    
    ```
    
    Copy Command
    

### Install with Verbose Output and Progress

- **Description**: Installs with verbose output and a progress bar.
- **Command**:
    
    ```bash
    rpm -ivh package.rpm
    
    ```
    
    Copy Command
    

### Upgrade or Install a Package

- **Description**: Upgrades an existing package or installs it if not present.
- **Command**:
    
    ```bash
    rpm -Uvh package.rpm
    
    ```
    
    Copy Command
    

### Install Ignoring Dependencies

- **Description**: Installs a package while ignoring dependency checks (not recommended).
- **Command**:
    
    ```bash
    rpm --nodeps -ivh package.rpm
    
    ```
    
    Copy Command
    

### Removing Packages

### Remove a Package

- **Description**: Uninstalls a package from the system.
- **Command**:
    
    ```bash
    rpm -e package-name
    
    ```
    
    Copy Command
    

### Remove with Verbose Output

- **Description**: Uninstalls a package with verbose output.
- **Command**:
    
    ```bash
    rpm -evh package-name
    
    ```
    
    Copy Command
    

### Remove Ignoring Dependencies

- **Description**: Uninstalls a package while ignoring dependencies (not recommended).
- **Command**:
    
    ```bash
    rpm --nodeps -evh package-name
    
    ```
    
    Copy Command
    

---

## Use Cases

- **System Administration**: Install, update, or remove software packages efficiently.
- **Troubleshooting**: Verify package integrity or identify which package owns a file.
- **Software Development**: Build and distribute custom software using SRPMs.
- **System Auditing**: Query installed packages to ensure compliance or security.

---

## Advantages

- Robust package management for Red Hat-based systems.
- Supports both binary and source packages.
- Extensive querying capabilities for system analysis.
- Maintains a reliable database for tracking packages.

---

## Disadvantages

- Dependency management can be complex without tools like `yum` or `dnf`.
- Requires root privileges for most operations.
- Manual dependency resolution can be error-prone when using `-nodeps`.

---

# LibreOffice Installation and Management Commands

This guide provides structured commands for downloading, installing, managing, and extracting LibreOffice packages, as well as handling RPM packages and mounting ISO images. Commands are organized with clear headings, examples, and copy-paste-ready snippets.

## LibreOffice Installation

### Download LibreOffice 7.1.3 RPM Package

Download the LibreOffice 7.1.3 RPM package for x86_64 Linux.

**Command**:

```bash
wget https://mirrors.estointernet.in/tdf/libreoffice/stable/7.1.3/rpm/x86_64/LibreOffice_7.1.3_Linux_x86-64_rpm.tar.gz

```

**Copy & Run**:

```bash
wget https://mirrors.estointernet.in/tdf/libreoffice/stable/7.1.3/rpm/x86_64/LibreOffice_7.1.3_Linux_x86-64_rpm.tar.gz

```

### Extract the Downloaded Tarball

Extract the downloaded tarball to access the RPM packages.

**Command**:

```bash
tar -xvf LibreOffice_7.1.3_Linux_x86-64_rpm.tar.gz

```

**Copy & Run**:

```bash
tar -xvf LibreOffice_7.1.3_Linux_x86-64_rpm.tar.gz

```

### Install RPM Packages

Install all RPM packages in the extracted folder.

### Method 1: Install All RPMs

**Command**:

```bash
rpm -ivh *.rpm

```

**Copy & Run**:

```bash
rpm -ivh *.rpm

```

### Method 2: Alternative Installation

**Command**:

```bash
rpm -ivh .

```

**Copy & Run**:

```bash
rpm -ivh .

```

### List Installed LibreOffice and libobasis Packages

List installed LibreOffice and libobasis packages, output on one line with spaces.

### Method 1

**Command**:

```bash
rpm -qa | grep -E "libreoffice|libobasis" | tr "\n" " "

```

**Copy & Run**:

```bash
rpm -qa | grep -E "libreoffice|libobasis" | tr "\n" " "

```

### Method 2

**Command**:

```bash
rpm -qa | grep -E "libreoffice|libobasis" | tr -s "\n" " "

```

**Copy & Run**:

```bash
rpm -qa | grep -E "libreoffice|libobasis" | tr -s "\n" " "

```

### Remove Specific OpenOffice 4.1.7 Packages

Remove specified OpenOffice 4.1.7 packages by name.

**Command**:

```bash
rpm -evh openoffice-writer-4.1.7-9800.x86_64 \
openoffice-ogltrans-4.1.7-9800.x86_64 \
openoffice-xsltfilter-4.1.7-9800.x86_64 \
openoffice-en-US-calc-4.1.7-9800.x86_64 \
openoffice-calc-4.1.7-9800.x86_64 \
openoffice-images-4.1.7-9800.x86_64 \
openoffice-brand-draw-4.1.7-9800.x86_64 \
openoffice-ooofonts-4.1.7-9800.x86_64 \
openoffice-ure-4.1.7-9800.x86_64 \
openoffice-en-US-impress-4.1.7-9800.x86_64 \
openoffice-core05-4.1.7-9800.x86_64 \
openoffice-core06-4.1.7-9800.x86_64 \
openoffice-4.1.7-9800.x86_64 \
openoffice-brand-math-4.1.7-9800.x86_64 \
openoffice-brand-en-US-4.1.7-9800.x86_64 \
openoffice-graphicfilter-4.1.7-9800.x86_64 \
openoffice-oolinguistic-4.1.7-9800.x86_64 \
openoffice-impress-4.1.7-9800.x86_64 \
openoffice-en-US-help-4.1.7-9800.x86_64 \
openoffice-en-US-writer-4.1.7-9800.x86_64 \
openoffice-core03-4.1.7-9800.x86_64 \
openoffice-core07-4.1.7-9800.x86_64 \
openoffice-math-4.1.7-9800.x86_64 \
openoffice-brand-base-4.1.7-9800.x86_64 \
openoffice-brand-impress-4.1.7-9800.x86_64 \
openoffice-javafilter-4.1.7-9800.x86_64 \
openoffice-pyuno-4.1.7-9800.x86_64 \
openoffice-en-US-4.1.7-9800.x86_64 \
openoffice-en-US-draw-4.1.7-9800.x86_64 \
openoffice-en-US-res-4.1.7-9800.x86_64 \
openoffice-core02-4.1.7-9800.x86_64 \
openoffice-draw-4.1.7-9800.x86_64 \
openoffice-brand-calc-4.1.7-9800.x86_64 \
openoffice-onlineupdate-4.1.7-9800.x86_64 \
openoffice-core01-4.1.7-9800.x86_64 \
openoffice-en-US-math-4.1.7-9800.x86_64 \
openoffice-core05-4.1.7-9800.x86_64 \
openoffice-brand-writer-4.1.7-9800.x86_64 \
openoffice-gnome-integration-4.1.7-9800.x86_64 \
openoffice4.1.7-redhat-menus-4.1.7-9800.noarch \
openoffice-en-US-base-4.1.7-9800.x86_64 \
openoffice-base-4.1.7-9800.x86_64

```

**Copy & Run**:

```bash
rpm -evh openoffice-writer-4.1.7-9800.x86_64 openoffice-ogltrans-4.1.7-9800.x86_64 openoffice-xsltfilter-4.1.7-9800.x86_64 openoffice-en-US-calc-4.1.7-9800.x86_64 openoffice-calc-4.1.7-9800.x86_64 openoffice-images-4.1.7-9800.x86_64 openoffice-brand-draw-4.1.7-9800.x86_64 openoffice-ooofonts-4.1.7-9800.x86_64 openoffice-ure-4.1.7-9800.x86_64 openoffice-en-US-impress-4.1.7-9800.x86_64 openoffice-core05-4.1.7-9800.x86_64 openoffice-core06-4.1.7-9800.x86_64 openoffice-4.1.7-9800.x86_64 openoffice-brand-math-4.1.7-9800.x86_64 openoffice-brand-en-US-4.1.7-9800.x86_64 openoffice-graphicfilter-4.1.7-9800.x86_64 openoffice-oolinguistic-4.1.7-9800.x86_64 openoffice-impress-4.1.7-9800.x86_64 openoffice-en-US-help-4.1.7-9800.x86_64 openoffice-en-US-writer-4.1.7-9800.x86_64 openoffice-core03-4.1.7-9800.x86_64 openoffice-core07-4.1.7-9800.x86_64 openoffice-math-4.1.7-9800.x86_64 openoffice-brand-base-4.1.7-9800.x86_64 openoffice-brand-impress-4.1.7-9800.x86_64 openoffice-javafilter-4.1.7-9800.x86_64 openoffice-pyuno-4.1.7-9800.x86_64 openoffice-en-US-4.1.7-9800.x86_64 openoffice-en-US-draw-4.1.7-9800.x86_64 openoffice-en-US-res-4.1.7-9800.x86_64 openoffice-core02-4.1.7-9800.x86_64 openoffice-draw-4.1.7-9800.x86_64 openoffice-brand-calc-4.1.7-9800.x86_64 openoffice-onlineupdate-4.1.7-9800.x86_64 openoffice-core01-4.1.7-9800.x86_64 openoffice-en-US-math-4.1.7-9800.x86_64 openoffice-core05-4.1.7-9800.x86_64 openoffice-brand-writer-4.1.7-9800.x86_64 openoffice-gnome-integration-4.1.7-9800.x86_64 openoffice4.1.7-redhat-menus-4.1.7-9800.noarch openoffice-en-US-base-4.1.7-9800.x86_64 openoffice-base-4.1.7-9800.x86_64

```

## Extract RPM Package Files Without Installing

### Download an RPM Package

Download an example RPM package (httpd).

**Command**:

```bash
wget http://repo.okay.com.mx/centos/7/x86_64/release/httpd-2.4.35-2.el7.x86_64.rpm

```

**Copy & Run**:

```bash
wget http://repo.okay.com.mx/centos/7/x86_64/release/httpd-2.4.35-2.el7.x86_64.rpm

```

### Convert RPM Package to cpio Archive

Convert an RPM package to a cpio archive for extraction.

**Command**:

```bash
rpm2cpio dhcp-server-4.4.2-15.b1.el9.x86_64.rpm

```

**Copy & Run**:

```bash
rpm2cpio dhcp-server-4.4.2-15.b1.el9.x86_64.rpm

```

### Extract Files from RPM Package Using cpio

Extract files from the RPM package.

**Command**:

```bash
rpm2cpio dhcp-server-4.4.2-15.b1.el9.x86_64.rpm | cpio -idmv

```

**Copy & Run**:

```bash
rpm2cpio dhcp-server-4.4.2-15.b1.el9.x86_64.rpm | cpio -idmv

```

**Example: Extract Files from httpd RPM Package**:

```bash
rpm2cpio httpd-2.4.35-2.el7.x86_64.rpm | cpio -idmv

```

**Copy & Run**:

```bash
rpm2cpio httpd-2.4.35-2.el7.x86_64.rpm | cpio -idmv

```

## Mount an ISO Image

### Download a CentOS Stream ISO Image

Download the CentOS Stream 9 boot ISO image.

**Command**:

```bash
wget https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/iso/CentOS-Stream-9-latest-x86_64-boot.iso

```

**Copy & Run**:

```bash
wget https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/iso/CentOS-Stream-9-latest-x86_64-boot.iso

```

### Verify File Type of the ISO Image

Check the file type to confirm it’s an ISO image.

**Command**:

```bash
file CentOS-Stream-9-latest-x86_64-boot.iso

```

**Copy & Run**:

```bash
file CentOS-Stream-9-latest-x86_64-boot.iso

```

### Mount the ISO Image

Mount the ISO image to the `/mnt` mount point.

**Command**:

```bash
mount -t iso9660 CentOS-Stream-9-latest-x86_64-boot.iso /mnt

```

**Copy & Run**:

```bash
mount -t iso9660 CentOS-Stream-9-latest-x86_64-boot.iso /mnt

```

### Unmount the ISO Image

Unmount the ISO image from the `/mnt` mount point.

**Command**:

```bash
umount /mnt

```

**Copy & Run**:

```bash
umount /mnt

```

### Copy ISO Image to Remote Server via SCP

Copy an ISO image to a remote server using SCP.

**Command**:

```bash
scp /root/CentOS-7-x86_64-Minimal-1611.iso root@192.168.1.35:/root/

```

**Copy & Run**:

```bash
scp /root/CentOS-7-x86_64-Minimal-1611.iso root@192.168.1.35:/root/

```

### Mount ISO Image from Another Directory

Mount an ISO image located in a different directory.

**Command**:

```bash
mount -t iso9660 /root/Documents/CentOS-7-x86_64-Minimal-1611.iso /mnt

```

**Copy & Run**:

```bash
mount -t iso9660 /root/Documents/CentOS-7-x86_64-Minimal-1611.iso /mnt

```

### Unmount the ISO Image

Unmount the ISO image from the `/mnt` mount point.

**Command**:

```bash
umount /mnt

```

**Copy & Run**:

```bash
umount /mnt

```

# **Yum (Yellowdog Updater, Modified) Notes**

## **Overview**

Yum is a powerful package management tool for RPM-based Linux distributions such as CentOS, RHEL, and Fedora. It simplifies package installation, updating, removal, and dependency resolution from local or remote repositories. Modern systems are transitioning to DNF (Dandified Yum) for improved performance and dependency handling.

### **Key Features of Yum**

- **Automatic Dependency Resolution**: Automatically installs required dependencies.
- **Remote and Local Repository Support**: Downloads packages from online mirrors or local media/repositories.
- **Group Package Management**: Supports installing, removing, or querying related package groups.
- **Rollback Functionality**: Allows undoing package updates (available in some versions).
- **Replaced by DNF**: DNF is preferred in newer systems for faster performance and better dependency resolution.

---

## **Setting Up a Local Repository from DVD/ISO (CentOS 9)**

### **Steps**

1. **Mount DVD or ISO to a Local Directory**
    
    Mount the CentOS 9 DVD or ISO to a local directory for accessing packages.
    
    ```bash
    mount /dev/sr0 /mnt
    mkdir /centos9
    cp -vr /mnt/* /centos9
    
    ```
    
2. **Install createrepo_c (CentOS 9) or createrepo (CentOS 7)**
    
    Install the tool to generate repository metadata. Use `createrepo_c` for CentOS 9 or `createrepo` for CentOS 7.
    
    ```bash
    rpm -ivh createrepo_c-*.rpm
    
    ```
    
    *For CentOS 7*:
    
    ```bash
    rpm -ivh createrepo-*.rpm
    
    ```
    
3. **Create Repository Metadata**
    
    Generate metadata for the local repository.
    
    ```bash
    ls -lh | grep repodata
    createrepo -v /centos9/AppStream/Packages/
    
    ```
    
    To output metadata to a different directory:
    
    ```bash
    createrepo -v /centos9/AppStream/Packages/ -o /tmp
    
    ```
    
4. **Configure Yum Repository File**
    
    Create a repository configuration file at `/etc/yum.repos.d/centos9.repo`.
    
    ```bash
    [centos9]
    name=CentOS 9 DVD
    baseurl=file:///centos9/AppStream/Packages
    gpgcheck=0
    
    ```
    
5. **Clean Yum Cache and Update Repository Lists**
    
    Clear the Yum cache and refresh repository metadata.
    
    ```bash
    yum clean all
    rm -rf /var/cache/yum
    yum repolist all
    
    ```
    
6. **Install Packages from Local Repository**
    
    Install packages using the local repository.
    
    ```bash
    yum install python3.12
    yum install firefox
    yum install httpd
    
    ```
    

---

## **Yum Repository Configuration Fields**

### **Fields Description**

| **Field** | **Description** |
| --- | --- |
| `[baseos]` | Repository ID, unique identifier used internally by Yum/DNF. |
| `name` | Human-readable name (e.g., `CentOS Stream $releasever - BaseOS`). `$releasever` expands to the OS version (e.g., 9). |
| `metalink` | URL providing a dynamic list of mirror URLs for package downloads (e.g., `https://mirrors.centos.org/metalink?repo=centos-baseos-$stream&arch=$basearch&protocol=https,http`). `$stream` is the CentOS Stream version, `$basearch` is the system architecture (e.g., x86_64). |
| `gpgkey` | Location of the GPG public key for package signature verification (e.g., `file:///etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial`). |
| `gpgcheck` | Enables (1) or disables (0) GPG signature verification for packages. |
| `repo_gpgcheck` | Enables (1) or disables (0) GPG checking for repository metadata (e.g., repomd.xml). |
| `metadata_expire` | Time interval for checking updated repository metadata (e.g., `6h` for 6 hours). |
| `countme` | Optional field to enable repository usage statistics (1 to enable). |
| `enabled` | Enables (1) or disables (0) the repository. |

### **Example Repository Configuration**

```bash
[baseos]
name=CentOS Stream $releasever - BaseOS
metalink=https://mirrors.centos.org/metalink?repo=centos-baseos-$stream&arch=$basearch&protocol=https,http
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
gpgcheck=1
repo_gpgcheck=0
metadata_expire=6h
countme=1
enabled=1

```

---

## **Popular Third-Party Repositories**

### **Repository Details**

| **Repository** | **Description** | **Install Command** |
| --- | --- | --- |
| **EPEL** | Extra packages by Fedora project | `yum install epel-release.noarch` |
| **Remi** | Updated PHP and related packages | `rpm -ivh https://rpms.remirepo.net/enterprise/remi-release-9.rpm` |
| **RPM Fusion** | Multimedia packages | `yum install https://mirrors.ustc.edu.cn/rpmfusion/free/el/rpmfusion-free-release-9.noarch.rpm` |
| **ELRepo** | Kernel and hardware drivers | `rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org` |
|  |  | `yum install https://www.elrepo.org/elrepo-release-9.el9.elrepo.noarch.rpm` |
| **IUS** | Updated popular packages | `rpm -ivh https://repo.ius.io/ius-release-el7.rpm` |
|  |  | `yum install https://repo.ius.io/ius-release-el7.rpm` |

---

## **Summary**

Yum is a robust package management tool for RPM-based Linux distributions, offering features like dependency resolution, repository support, and group package management. Setting up a local repository from a DVD/ISO involves mounting the media, generating metadata with `createrepo`, and configuring a Yum repository file. Third-party repositories like EPEL, Remi, and RPM Fusion extend package availability. While Yum is being replaced by DNF in modern systems, it remains widely used in CentOS, RHEL, and Fedora environments. Always ensure proper repository configuration and use trusted sources for security.
