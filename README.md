## 🖥️ Baseline Configuration (Before Upgrades)

| Component        | Specification                                            |
|------------------|-----------------------------------------------------------|
| **Model**        | Dell PowerEdge R320                                        |
| **CPU**          | Intel Xeon E5-2407 (4 cores / 4 threads @ 2.2 GHz)         |
| **RAM**          | 8 GB ECC DDR3 (1 × 8 GB module)                             |
| **Storage**       | 2 × 4 TB HDDs (of 4 possible drive bays)                    |
| **Drive Bays**   | 4 × 3.5″ hot-swappable or cabled SAS/SATA slots :contentReference[oaicite:5]{index=5} |
| **Network**      | Dual gigabit Ethernet (integrated NICs)                    |
| **Firmware**     | BIOS v2.9.0                                                |

---

## ⚙️ Upgraded Configuration (Current Setup)

| Component        | Specification                                               |
|------------------|--------------------------------------------------------------|
| **CPU**          | Intel Xeon E5-2450 v2 (8 cores / 16 threads @ 2.50 GHz, turbo 3.30 GHz) |
| **RAM**          | 48 GB ECC DDR3 (6 × 8 GB modules)                             |
| **Primary Storage (OS)** | 480 GB Intel DC SSD                                     |
| **Secondary Storage (Logs/VMs)** | 2 × 4 TB HDDs (you can still populate 2 more bays)     |
| **Drive Bays**   | 4 × 3.5″ hot-swappable/cabled SAS/SATA slots :contentReference[oaicite:6]{index=6} |
| **Network**      | Dual Intel gigabit NICs (bridge + monitoring)                |
| **Cooling & Power** | Stock Dell cooling with redundancy                          |
| **Firmware**     | BIOS v2.9.0 (verified or updated for CPU compatibility)      |
