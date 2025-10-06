# 🧰 Hardware Upgrade & Expansion Plan

## 📦 System Overview

**Host:** Dell PowerEdge R320 (1U Rackmount Server)  
**Use Case:** Proxmox VE 9.0 hypervisor running Security Onion and supporting services  
**Chassis:** 1U with 4 × 3.5″ hot-swap drive bays  
**Power:** Single PSUs  

---

## 🧠 Baseline Configuration (Before Upgrades)

| Component | Model / Spec | Notes |
|------------|---------------|------|
| CPU | Intel Xeon **E5-2407** (4C / 4T @ 2.2 GHz) | Entry-level Sandy Bridge CPU, no Hyper-Threading |
| RAM | 24 GB DDR3 ECC Registered | Factory configuration |
| Storage | 2 × 4 TB Seagate HDDs | Initially configured under RAID |
| Boot Drive | None (installed during upgrade) | Added Intel SSD later |
| RAID Controller | Dell PERC H310 | Confirmed LSI SAS2008 chipset, HBA-capable |
| NIC | Dual-port Intel 1 GbE | Connected to core switch |

---

## 🔧 Upgrades Performed

| Date | Component | Upgrade | Rationale |
|------|------------|----------|------------|
| 2025-10 | **CPU** | Upgraded to **Intel Xeon E5-2450 v2** (8C / 16T @ 2.5 GHz) | Doubled core count and added Hyper-Threading; improves VM concurrency |
| 2025-10 | **Memory** | Increased to **48 GB DDR3 ECC** | Ensures headroom for Security Onion and multiple containers |
| 2025-10 | **Boot Drive** | Added **Intel DC S3520 480 GB SSD** | Dedicated Proxmox OS disk; reliable enterprise SATA SSD |
| 2025-10 | **Storage Configuration** | Converted controller to **HBA mode** | Enables ZFS and direct disk passthrough |
| 2025-10 | **Storage Pool** | Created **ZFS mirror (2 × 4 TB)** | Provides redundancy for Security Onion log storage |

---

## 💡 Rationale for Component Choices

- **Xeon E5-2450 v2:** Balances low power draw (95 W TDP) with solid multi-core performance; compatible with the R320’s BIOS v2.9.0.  
- **Intel DC S3520 SSD:** Optimized for 24/7 workloads and consistent write endurance; ideal for Proxmox root.  
- **ZFS Mirror on 2 × 4 TB HDDs:** Offers fault tolerance and integrity checking for continuous packet capture/log data.  
- **48 GB RAM:** Provides sufficient memory for:
  - 1 × Security Onion VM (16 GB)
  - 1 × Elastic Stack node (12 GB)
  - Multiple lightweight containers (10–12 GB aggregate)
  - System & ARC cache (8–10 GB)

---

## 📈 Future Expansion Plan

| Bay | Planned Drive | Type | Purpose |
|------|---------------|------|----------|
| **Bay 1** | Intel DC S3520 480 GB | SSD | Boot / Proxmox OS |
| **Bay 2** | 4 TB HDD #1 | HDD | ZFS mirror member (data) |
| **Bay 3** | 4 TB HDD #2 | HDD | ZFS mirror member (data) |
| **Bay 4** | TBD (Future) | SSD or HDD | For expansion or hot-spare |

### 🧩 Planned Additions

- **Bay 4:**
  - Option 1 → *4 TB HDD* → convert ZFS mirror → RAIDZ1 (expand capacity).  
  - Option 2 → *Enterprise SATA SSD* → add VM-only storage pool (`fast-vm`).  

### 🪛 Other Potential Upgrades

| Target | Plan | Benefit |
|---------|------|----------|
| **NIC Expansion** | Add 2-port Intel i350 PCIe card | Enables dedicated Security Onion traffic capture |
| **10 GbE Upgrade** | Future SFP+ NIC + core switch upgrade | Allows full 10 Gbit data ingest to Security Onion |
| **Fans & Thermals** | Replace aging 1U fans with PWM-controlled models | Reduce noise and maintain airflow efficiency |
| **Remote Management** | Enable iDRAC Enterprise License | Full remote console and virtual media |

---

## 🧭 Summary

The R320 was originally a light-duty rack server; upgrades transformed it into a capable **home-lab hypervisor and network security node**.  
The next phase focuses on:
- Filling remaining drive bays strategically for redundancy or performance.  
- Incrementally upgrading NICs and cooling for better network analysis capability.  
- Maintaining low power draw while increasing storage reliability.

---

*Document last updated: 2025-10-06*  
