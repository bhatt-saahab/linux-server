

![LVM Diagram](https://access.redhat.com/webassets/avalon/d/Red_Hat_Enterprise_Linux-9-Configuring_and_managing_logical_volumes-en-US/images/31bd96635c4120abe3e771a423f61cd6/basic-lvm-volume-components.png)


Logical Volume Manager (LVM)** is a flexible and dynamic storage management framework for Linux (and some Unix-like systems). It abstracts physical storage devices into logical volumes, allowing administrators to manage disk storage more efficiently than traditional fixed partitioning.


## Key Components

1. **Physical Volumes (PVs)**: Physical storage devices (e.g., disks or partitions) initialized for use by LVM.
2. **Volume Groups (VGs)**: Pools of storage created by combining one or more PVs.
3. **Logical Volumes (LVs)**: Virtual partitions created from VGs, behaving like regular disk partitions but with enhanced flexibility.

---

## Essential Features

- **Dynamic Resizing**: Resize LVs and VGs online without downtime.
- **Snapshot Support**: Create read-only or read-write snapshots for consistent backups or testing.
- **Thin Provisioning**: Overcommit storage by creating volumes larger than available physical space, allocating space dynamically.
- **Caching**: Use fast storage (e.g., SSDs) as a cache to improve performance of slower disks.
- **RAID Support**: Supports RAID levels 0, 1, 4, 5, 6, and 10 for redundancy and performance.
- **Mirroring and Striping**: Provides data redundancy and improved I/O performance.
- **Volume Movement**: Move LVs across PVs without downtime.
- **LVM Profiles & Configurations**: Manage specific setups with configuration profiles.
- **JSON Reporting**: Command outputs in JSON format for automation.
- **Historical Logical Volumes**: Track and manage thin snapshots and volumes removed from dependency chains.
- **Multihost Volume Management**: Cluster LVM supports shared VGs across multiple hosts for high availability.

---

## Use Cases

- Simplified management and resizing of file systems in enterprise servers.
- Flexible storage for virtualized environments and containerized workloads.
- Efficient disk space utilization with thin provisioning.
- Data protection and backup consistency using snapshots.
- High availability solutions with cluster-wide volume management.
- Performance improvement with caching and RAID features.

---

## Summary Table of LVM Features

| **Feature** | **Description** |
| --- | --- |
| Physical Volumes (PVs) | Base physical storage devices (e.g., disks or partitions). |
| Volume Groups (VGs) | Pools combining multiple PVs as unified storage. |
| Logical Volumes (LVs) | Flexible virtual partitions used by the OS and applications. |
| Dynamic Resizing | Resize volumes and groups without downtime. |
| Snapshots | Create point-in-time copies for backups and testing. |
| Thin Provisioning | Overcommit storage, allocate space as needed. |
| RAID Support | Supports RAID levels 0, 1, 4, 5, 6, 10 for performance and redundancy. |
| Caching | Use SSDs or fast disks as caches for slower disks. |
| Volume Movement | Move volumes across physical drives without downtime. |
| JSON Output | Native command output in JSON for automation. |
| Cluster LVM | Manage shared volumes across multiple hosts for high availability. |

---

## LVM Setup and Management Steps

### 1. Install LVM

Install the LVM package if not already installed.

**On Debian/Ubuntu:**

```bash
sudo apt install lvm2

```

- **Explanation**: Installs the `lvm2` package, which provides LVM tools.

**On RHEL/CentOS:**

```bash
sudo yum install lvm2

```

- **Explanation**: Installs the `lvm2` package on RHEL-based systems.

---

### 2. Create Physical Volumes (PVs)

Initialize physical disks or partitions for LVM use.

**Identify available disks:**

```bash
lsblk

```

- **Explanation**: Lists block devices to identify available disks (e.g., `/dev/sdb`, `/dev/sdc`).

**Initialize disks as PVs:**

```bash
sudo pvcreate /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf

```

- **Explanation**: Initializes specified disks as PVs for LVM. Replace `/dev/sdb`, etc., with actual disk names.

**Verify PVs:**

```bash
pvs

```

- **Explanation**: Displays a summary of all PVs.

```bash
pvdisplay

```

- **Explanation**: Provides detailed information about PVs.

---

### 3. Create a Volume Group (VG)

Combine PVs into a VG to create a unified storage pool.

**Create a VG named `vg_data`:**

```bash
sudo vgcreate vg_data /dev/sdb /dev/sdc /dev/sdd /dev/sde

```

- **Explanation**: Creates a VG named `vg_data` using the specified PVs.

**Verify VG:**

```bash
vgs

```

- **Explanation**: Displays a summary of all VGs.

```bash
vgdisplay

```

- **Explanation**: Provides detailed information about VGs.

---

### 4. Create Logical Volumes (LVs)

Carve out LVs from the VG to act as virtual partitions.

**Create a 60GB LV named `lv_storage`:**

```bash
sudo lvcreate -L 60G -n lv_storage vg_data

```

- **Explanation**: Creates an LV named `lv_storage` with a size of 60GB in the `vg_data` VG.

**Create an LV using all free space:**

```bash
sudo lvcreate -l 100%FREE -n lv_storage2 vg_data

```

- **Explanation**: Creates an LV named `lv_storage2` using all available space in `vg_data`.

**Verify LVs:**

```bash
lvs

```

- **Explanation**: Displays a summary of all LVs.

```bash
lvdisplay

```

- **Explanation**: Provides detailed information about LVs.

---

### 5. Format and Mount the Logical Volume

Prepare the LV for use by formatting and mounting it.

**Format with ext4:**

```bash
sudo mkfs.ext4 /dev/vg_data/lv_storage

```

- **Explanation**: Formats the LV `lv_storage` with the ext4 filesystem.

**Format with xfs:**

```bash
sudo mkfs.xfs /dev/vg_data/lv_storage2

```

- **Explanation**: Formats the LV `lv_storage2` with the xfs filesystem.

**Create a mount point and mount:**

```bash
sudo mkdir /mnt/storage
sudo mount /dev/vg_data/lv_storage /mnt/storage

```

- **Explanation**: Creates a directory `/mnt/storage` and mounts the LV `lv_storage` to it.

---

### 6. Resizing Logical Volumes

LVM allows dynamic resizing of LVs (increase or decrease size).

### Extend LV (Increase Size)

**Add a new PV to the VG:**

```bash
sudo vgextend vg_data /dev/sdf

```

- **Explanation**: Adds a new PV (`/dev/sdf`) to the `vg_data` VG to increase available space.

**Increase LV size by 10GB:**

```bash
sudo lvextend -L +10G /dev/vg_data/lv_storage

```

- **Explanation**: Extends the LV `lv_storage` by an additional 10GB.

**Resize filesystem (ext4 example):**

```bash
sudo resize2fs /dev/vg_data/lv_storage

```

- **Explanation**: Updates the ext4 filesystem to use the new LV size.

**Verify new size:**

```bash
df -h /mnt/storage

```

- **Explanation**: Displays the disk usage and size of the mounted LV.

### Shrink LV (Reduce Size)

**Unmount the volume:**

```bash
sudo umount /mnt/storage

```

- **Explanation**: Unmounts the LV to safely resize it.

**Check and shrink filesystem:**

```bash
sudo e2fsck -f /dev/vg_data/lv_storage
sudo resize2fs /dev/vg_data/lv_storage 15G

```

- **Explanation**:
    - `e2fsck -f`: Checks the filesystem for errors before resizing.
    - `resize2fs`: Shrinks the ext4 filesystem to 15GB.

**Reduce LV size:**

```bash
sudo lvreduce -L 15G /dev/vg_data/lv_storage

```

- **Explanation**: Reduces the LV size to 15GB. Warning: Ensure the filesystem is resized first to avoid data loss.

**Remount the volume:**

```bash
sudo mount /dev/vg_data/lv_storage /mnt/storage

```

- **Explanation**: Remounts the LV after resizing.

---

### 7. Resizing Logical Volumes with `lvresize`

The `lvresize` command can resize LVs and optionally the filesystem in one step.

**Resize LV to 90GB with filesystem:**

```bash
sudo lvresize --size 90G --resizefs /dev/vg_data/lv_storage

```

- **Explanation**: Resizes the LV to 90GB and automatically resizes the filesystem.

**Resize LV to 40GB with filesystem:**

```bash
sudo lvresize --size 40G --resizefs /dev/vg_data/lv_storage

```

- **Explanation**: Resizes the LV to 40GB and automatically resizes the filesystem.

**Resize LV to 75GB without filesystem:**

```bash
sudo lvresize --size 75G /dev/vg_data/lv_storage

```

- **Explanation**: Resizes the LV to 75GB without resizing the filesystem (manual resize needed).

**Resize LV to 25GB without filesystem:**

```bash
sudo lvresize --size 25G /dev/vg_data/lv_storage

```

- **Explanation**: Resizes the LV to 25GB without resizing the filesystem (manual resize needed).

**Resize another LV (`lv1`) to 50GB without filesystem:**

```bash
sudo lvresize -L 50G /dev/vg1/lv1

```

- **Explanation**: Resizes the LV `lv1` in VG `vg1` to 50GB without resizing the filesystem.

**Resize `lv1` to 100GB without filesystem:**

```bash
sudo lvresize -L 100G /dev/vg1/lv1

```

- **Explanation**: Resizes the LV `lv1` in VG `vg1` to 100GB without resizing the filesystem.

---

### 8. Removing LVM Components

Remove LVs, VGs, or PVs when no longer needed.

### Remove Logical Volume

```bash
sudo umount /mnt/storage
sudo lvremove /dev/vg_data/lv_storage
lvdisplay

```

- **Explanation**:
    - `umount`: Unmounts the LV to ensure it’s not in use.
    - `lvremove`: Deletes the specified LV.
    - `lvdisplay`: Verifies the LV has been removed.

### Remove Volume Group

```bash
sudo vgremove vg_data
vgdisplay

```

- **Explanation**:
    - `vgremove`: Deletes the specified VG.
    - `vgdisplay`: Verifies the VG has been removed.

### Remove Physical Volume

```bash
sudo pvremove /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf
pvdisplay

```

- **Explanation**:
    - `pvremove`: Removes the PV configuration from the specified disks.
    - `pvdisplay`: Verifies the PVs have been removed.

---

### 9. Checking LVM Status

Monitor and inspect LVM components.

**Show logical volumes:**

```bash
lvs

```

- **Explanation**: Displays a summary of all LVs.

**Show volume groups:**

```bash
vgs

```

- **Explanation**: Displays a summary of all VGs.

**Show physical volumes:**

```bash
pvs

```

- **Explanation**: Displays a summary of all PVs.

---

### 10. Additional Disk Management Commands

Commands often used alongside LVM for disk inspection and management.

**List disks:**

```bash
fdisk -l | grep sd

```

- **Explanation**: Lists disk information, filtering for devices starting with `sd` (e.g., `/dev/sdb`).

**Manage disk partitions:**

```bash
sudo fdisk /dev/sdb

```

- **Explanation**: Opens an interactive interface to manage partitions on `/dev/sdb`.

**Check LVM package installation:**

```bash
rpm -qa | grep lvm

```

- **Explanation**: Lists installed RPM packages related to LVM (RHEL-based systems).

**View LVM package details:**

```bash
rpm -qi lvm2

```

- **Explanation**: Displays detailed information about the `lvm2` package.

---

## Notes on Corrections and Improvements

- Removed "Copy" and "Run" lines as requested.
- Corrected typos (e.g., `e.u, S5Ds` to `e.g., SSDs`, `150N` to `JSON`, `mare` to `more`).
- Fixed command syntax errors (e.g., `lvresize/dev/vod_data` to `lvresize /dev/vg_data`).
- Standardized command formatting for consistency (e.g., added `sudo` where appropriate).
- Organized content into logical sections for better readability.
- Ensured all provided commands and features were included without omission.

---

# RAID in Linux

**RAID (Redundant Array of Independent Disks)** is a technology that combines multiple physical disk drives into a single logical unit to enhance performance, provide redundancy, or both. In Linux, RAID is commonly managed using the `mdadm` tool for software RAID.

---

## Common RAID Levels in Linux

| **RAID Level** | **Description** | **Minimum Drives** | **Fault Tolerance** | **Use Case** |
| --- | --- | --- | --- | --- |
| **RAID 0** | Disk striping without redundancy | 2 | None (failure causes data loss) | High-speed data access (e.g., video editing) |
| **RAID 1** | Disk mirroring | 2 | 1 drive failure | Critical systems, OS boot drives |
| **RAID 5** | Block-level striping with distributed parity | 3 | 1 drive failure | File servers, general-purpose storage |
| **RAID 6** | Like RAID 5 but with double parity | 4 | 2 drive failures | High-capacity, fault-tolerant storage |
| **RAID 10** | Striped mirrors (combination of RAID 1 and 0) | 4 | 1 drive failure per mirror set | High performance and redundancy |

---

## Software RAID Setup Using `mdadm`

### Prerequisites

- Install `mdadm` if not already installed:
    
    ```bash
    sudo apt install mdadm    # On Debian/Ubuntu
    sudo yum install mdadm    # On RHEL/CentOS
    
    ```
    
    - **Explanation**: Installs the `mdadm` package, which provides tools for managing software RAID arrays.
- Identify available disks:
    
    ```bash
    lsblk
    
    ```
    
    - **Explanation**: Lists block devices to identify disks (e.g., `/dev/sdb`, `/dev/sdc`) available for RAID.

### Create RAID Arrays

**Create RAID 0 (Striping):**

```bash
sudo mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdb /dev/sdc

```

- **Explanation**: Creates a RAID 0 array named `/dev/md0` using two disks (`/dev/sdb`, `/dev/sdc`) for striping, improving performance but offering no redundancy.

**Create RAID 1 (Mirroring):**

```bash
sudo mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdb /dev/sdc

```

- **Explanation**: Creates a RAID 1 array named `/dev/md1` using two disks for mirroring, providing redundancy by duplicating data.

**Create RAID 5 (Striping with Parity):**

```bash
sudo mdadm --create /dev/md5 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd

```

- **Explanation**: Creates a RAID 5 array named `/dev/md5` using three disks, with data and parity striped across all drives for fault tolerance and performance.

**Create RAID 10 (Striped Mirrors):**

```bash
sudo mdadm --create /dev/md10 --level=10 --raid-devices=4 /dev/sdb /dev/sdc /dev/sdd /dev/sde

```

- **Explanation**: Creates a RAID 10 array named `/dev/md10` using four disks, combining mirroring and striping for both redundancy and performance.

---

### Format and Mount RAID Array

**Format the RAID array (e.g., with ext4):**

```bash
sudo mkfs.ext4 /dev/md0

```

- **Explanation**: Formats the RAID array `/dev/md0` with the ext4 filesystem. Replace `/dev/md0` with the appropriate RAID device.

**Create a mount point and mount:**

```bash
sudo mkdir /mnt/raid
sudo mount /dev/md0 /mnt/raid

```

- **Explanation**: Creates a directory `/mnt/raid` and mounts the RAID array `/dev/md0` to it for use.

---

## Managing and Checking RAID Status

**Check RAID array status:**

```bash
cat /proc/mdstat

```

- **Explanation**: Displays the current status of all RAID arrays, including active devices and their state.

```bash
sudo mdadm --detail /dev/md0

```

- **Explanation**: Provides detailed information about the specified RAID array (`/dev/md0`), including health, size, and status.

**Stop and remove RAID array:**

```bash
sudo mdadm --stop /dev/md0
sudo mdadm --remove /dev/md0

```

- **Explanation**:
    - `-stop`: Stops the RAID array, making it inactive.
    - `-remove`: Removes the RAID array configuration. Ensure the array is unmounted first.

**Save RAID configuration to persist through reboots:**

```bash
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
sudo update-initramfs -u

```

- **Explanation**:
    - `-detail --scan`: Appends the RAID configuration to `/etc/mdadm/mdadm.conf` to ensure the array is recognized after reboot.
    - `update-initramfs -u`: Updates the initial ramdisk to include RAID configuration for boot-time assembly.

---

## Notes on Corrections and Improvements

- Corrected typos (e.g., `rebpots` to `reboots`, `mdadm-create` to `mdadm --create`, `level-0` to `-level=0`).
- Removed redundant sections (e.g., repeated "Managing and Checking RAID Status").
- Added a step to format and mount the RAID array for completeness.
- Standardized command formatting with `sudo` where appropriate and corrected syntax errors (e.g., `-stop/dev/md0` to `-stop /dev/md0`).
- Included explanations for each command to clarify their purpose.
- Ensured all provided information was included without omission, with additional clarity for practical use.

---

These notes provide a comprehensive guide to setting up and managing RAID in Linux using `mdadm`. For further details or specific configurations, refer to the `mdadm` man page (`man mdadm`) or let me know if you need additional clarification!
