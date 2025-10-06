## 🖥️ Baseline Configuration (Before Upgrades)

| Component        | Specification                                            |
|------------------|-----------------------------------------------------------|
| **Model**        | Dell PowerEdge R320                                        |
| **CPU**          | Intel Xeon E5-2407 (4 cores / 4 threads @ 2.2 GHz)         |
| **RAM**          | 8 GB ECC DDR3 (2 × 4 GB module)                             |
| **Storage**       | 2 × 4 TB HDDs (of 4 possible drive bays)                    |
| **Drive Bays**   | 4 × 3.5″ hot-swappable or cabled SAS/SATA slots :contentReference[oaicite:5]{index=5} |
| **Network**      | Dual gigabit Ethernet (integrated NICs)                    |
| **Firmware**     | BIOS v2.9.0                                                |

---

## ⚙️ Upgraded Configuration (Current Setup)

| Component        | Specification                                               |
|------------------|--------------------------------------------------------------|
| **CPU**          | Intel Xeon E5-2450 v2 (8 cores / 16 threads @ 2.50 GHz, turbo 3.30 GHz) |
| **RAM**          | 48 GB ECC DDR3 (3 × 16 GB modules)                             |
| **Primary Storage (OS)** | 480 GB Intel DC SSD                                     |
| **Secondary Storage (Logs/VMs)** | 2 × 4 TB HDDs (you can still populate 2 more bays)     |
| **Drive Bays**   | 4 × 3.5″ cabled SAS/SATA slots :contentReference[oaicite:6]{index=6} |
| **Network**      | Dual Intel gigabit NICs (bridge + monitoring)                |
| **Cooling & Power** | Stock Dell cooling with redundancy                          |
| **Firmware**     | BIOS v2.9.0 (verified or updated for CPU compatibility)      |

---

## 🧩 Proxmox VE 9.0 Installation

This section documents the full installation and configuration of **Proxmox VE 9.0** on the **Dell PowerEdge R320** platform, verified against official Proxmox and Dell sources.

---

### 🛠️ Pre-Install Checks

Before installing, confirm these baseline settings:

- **Disable Secure Boot** in BIOS (Proxmox will not boot with Secure Boot on).  
- **Controller Mode:** ensure your storage controller is set to **HBA / Non-RAID** so disks appear as raw devices.  
- **Boot Mode:** set to **UEFI** (CSM Off optional).  
- **Boot Order:** USB first, then HDD/SSD.  
- **Keyboard / Monitor:** connected locally (or via iDRAC virtual console).

---

### 🔧 Controller / Mode Setup (Switching to HBA / Non-RAID)

Most R320 units ship with a Dell PERC RAID controller. To allow Proxmox or ZFS to manage drives directly:

1. Reboot the server and watch for the RAID prompt (`Ctrl + R` or `Ctrl + H`).  
2. Enter the **RAID Controller Configuration Utility**.  
3. Navigate to  
   **Controller Management → Advanced Controller Management**.  
4. Select **Switch to HBA Mode** (or similar).  
5. Delete all existing **Virtual Disks / RAID Volumes** if prompted — they must be removed before switching modes.  
6. Confirm and reboot.  
7. After reboot, each physical disk will appear independently (e.g. `/dev/sda`, `/dev/sdb`, `/dev/sdc`).

> 📝 Reference: [Dell Support KB — Switching Controller to HBA Mode](https://www.dell.com/support/manuals/en-us/poweredge-rc-h730/perc9ugpublication/switching-the-controller-to-hba-mode)

---

### 💻 BIOS & Boot Menu Keys (Dell PowerEdge R320)

| Key | Function |
|------|-----------|
| **F2** | Enter **System Setup / BIOS** (permanent settings) |
| **F10** | Launch **Lifecycle Controller / System Services** |
| **F11** | Open **Boot Manager / One-Time Boot Menu** |
| **F12** | PXE / Network Boot (if enabled) |

---

### 🔧 Installation Media

- **Proxmox VE Version:** 9.0 (Debian Bookworm-based)  
- **Download:** [proxmox.com/downloads](https://www.proxmox.com/en/downloads)  
- **Bootable USB:** 4 GB or larger, written with **Rufus** using:  
  - Partition scheme → **GPT**  
  - Target system → **UEFI (non-CSM)**  
  - File system → **FAT32**

Insert the USB stick, power on, and press **F11** to enter the *One-Time Boot Menu* → select the USB device.

---

### ⚙️ Installation Steps

1. **Start Installer** → select *Install Proxmox VE*.  
2. **Accept License Agreement.**  
3. **Target Disk:** choose the **480 GB Intel DC S3520 SSD** (`sda`).  
   - Filesystem: **ext4** (recommended for single disk; ZFS optional).  
4. **Location / Timezone:** `America/Los_Angeles`, keyboard `US`.  
5. **Create root password** and enter admin email.  
6. **Configure Network:**
