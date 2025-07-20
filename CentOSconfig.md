

## **Prerequisites**

### **Minimum System Requirements**

- **[🧠] RAM:** 2 GB *(4 GB Recommended)*
- **[💽] Disk Space:** 20 GB *(40 GB Recommended)*

### **Tools Needed**

- **[🔌] USB Drive:** 8 GB or more
- **[📦] ISO File:** Download from [centos.org](https://www.centos.org/download/)
- **[📝] Partition Plan:** Prepare ahead (see below)

---

## **Step 1: Download CentOS Stream 9 ISO**

**[🌐] URL:** https://www.centos.org/download/cr

- Select **CentOS Stream 9 DVD ISO**
- Click **Download** and save it on your system

---

## **Step 2: Create Bootable USB**

### **Tools to Use:**

- **[🪟] Windows:** Rufus
- **[🐧] Linux/macOS:** `dd` or **Etcher**

### **Linux Example using `dd`:**

```bash
sudo dd if=CentOS-Stream-9-*.iso of=/dev/sdX bs=4M status=progress && sync

```

> [⚠️**] Replace /dev/sdX with your actual USB device (not a partition like /dev/sdX1)**
> 

---

## **Step 3: Boot & Start Installation**

1. **[🔁] Reboot your system with USB plugged in**
2. **[**⚙️**] Enter Boot Menu:** Press **F12**, **ESC**, or **F2**
3. **[📀] Select USB Drive as boot option**
4. **[🚀] Choose "Install CentOS Stream 9"**

---

## **Step 4: Installation Options**

1. **[🗣️] Language:** Select your preferred language
2. **[💾] Installation Destination:** Select your target disk
3. **[🛠️] Partitioning:** Choose **Custom Partitioning** and configure:
    - `/boot` – 1 GB (ext4)
    - `swap` – Equal to RAM (e.g., 2–4 GB)
    - `/` (root) – Rest of space (xfs recommended)

---

## **Step 5: Post-Installation Setup**

### **[🔐] First Login & Update System**

```bash
dnf update -y

```

### **[📦] Enable EPEL (Extra Packages for Enterprise Linux)**

```bash
dnf install epel-release -y

```

### **[🛠️] Install Basic Utilities**

```bash
dnf install -y wget curl vim git net-tools

```

---

Let me know if you'd like a **printable PDF version** or **graphics-based note** too!
