# 1. BIOS & UEFI

## 1.1 What are they?

**Firmware** is software stored in nonvolatile memory on a device. Motherboard firmware starts hardware initialization before the operating system loads.

- **BIOS (Basic Input/Output System):** Traditional PC firmware with legacy boot methods.
- **UEFI (Unified Extensible Firmware Interface):** Modern firmware standard that commonly replaces legacy BIOS, supports modern boot features, and can provide a graphical setup interface.
- People often say “enter the BIOS” even when a modern PC actually uses UEFI.

**Easy picture:** Press power → firmware checks/initializes hardware → firmware finds a bootloader → the operating system starts.

## 1.2 Simplified boot sequence

1. Press the power button.
2. The PSU supplies stable power; the CPU begins executing firmware instructions.
3. Firmware initializes critical hardware and runs POST (Power-On Self-Test).
4. Firmware identifies an eligible boot device based on settings.
5. The bootloader starts (often from an **EFI System Partition** in a UEFI installation).
6. The bootloader loads Windows, Linux, or another OS.

> **POST:** Startup checks of essential hardware. Error LEDs, beep codes, or on-screen messages vary by manufacturer.

## 1.3 BIOS vs UEFI: key differences

| Feature | Legacy BIOS | UEFI |
|---|---|---|
| Era | Older PC firmware | Modern standard |
| Booting | Often uses MBR boot code | Typically loads an EFI bootloader |
| Partition style | Commonly MBR | Commonly GPT |
| Boot disk limits | MBR has ~2 TiB usable limit with 512-byte logical sectors | GPT supports much larger volumes |
| Secure Boot | Not a traditional BIOS feature | UEFI feature (when supported/enabled) |
| Interface | Often text-based | May be graphical or text-based |

**Important nuance:** GPT and UEFI are related but not the same thing. GPT is a disk partitioning scheme; UEFI is firmware. Some operating systems and hardware permit other combinations.

## 1.4 BIOS/UEFI settings worth knowing

- **Boot order:** Which boot entry/device to attempt first.
- **Secure Boot:** Checks signatures/trust of boot components according to the configured trust policy. It does **not** encrypt the disk.
- **TPM / firmware TPM:** Security feature used for protecting cryptographic keys and supporting features such as BitLocker.
- **Virtualization:** Intel VT-x / AMD-V (names depend on platform); needed for many virtualization workloads.
- **SATA configuration:** AHCI/RAID settings (options vary). Changing them after OS installation can stop the OS from booting.
- **XMP / EXPO:** Memory profile options for supported RAM/motherboard combinations; often enable speeds beyond default specifications.
- **Fan controls and hardware monitoring:** Fan curves, temperatures, voltages.
- **Date and time:** Check system clock configuration.

## 1.5 CMOS and RTC battery

- **CMOS** historically referred to memory used to keep firmware setup settings; modern boards can store settings in nonvolatile memory.
- The **RTC/CMOS battery** maintains the real-time clock when the PC is disconnected from power; on some systems it also supports retention of legacy configuration settings.
- Symptoms of a failing battery can include an incorrect clock or firmware warnings/settings resetting, depending on the device.
- A common desktop coin-cell type is **CR2032**, but verify your motherboard model first.

## 1.6 Firmware updates: rules for IT Support

1. Identify the **exact manufacturer, model, and board revision**.
2. Check the manufacturer's documentation, update notes, and supported CPU list.
3. Download firmware **only from an official, appropriate source**.
4. Follow the vendor's update procedure; use reliable power and don't interrupt the update.
5. Afterward, verify the version and review any settings that changed.

**Why update?** Compatibility, stability, bug fixes, and security updates. **Risk:** Wrong firmware or interrupted updates may leave the system unable to boot.

### Troubleshooting BIOS/UEFI

| Symptom | First checks |
|---|---|
| “No bootable device” | Is the drive detected? Correct boot entry/order? Bootloader intact? |
| PC fails POST after CPU upgrade | CPU socket/chipset/BIOS support and power connections |
| Clock repeatedly resets | RTC battery, firmware settings |
| Windows will not start after storage-mode change | Restore previous AHCI/RAID configuration; investigate driver support |
| Secure Boot-related message | Inspect UEFI boot mode, Secure Boot configuration, signed bootloader |

### Exam essentials

- Know **POST**, **boot order**, **Secure Boot**, **TPM**, **GPT**, **MBR**, and **RTC battery**.
- Secure Boot verifies trusted boot software; **BitLocker** provides disk/volume encryption.
- UEFI is firmware; GPT is a partition table format.

---

# 2. CPU (Central Processing Unit)

## 2.1 What does a CPU do?

The CPU executes program instructions, performs calculations, and coordinates work with memory and other hardware.

**Easy analogy:** CPU = worker; RAM = work desk; SSD = filing cabinet.

## 2.2 Essential CPU terms

| Term | Meaning |
|---|---|
| Core | Processing unit inside the CPU capable of executing instructions |
| Thread | A sequence of instructions; logical processors may expose hardware thread contexts |
| SMT / Hyper-Threading | Allows some cores to handle multiple hardware threads (availability varies) |
| Clock speed (GHz) | CPU cycles per second; **not** a complete performance comparison |
| Cache (L1/L2/L3) | Very fast small memory that keeps frequently needed data close to CPU |
| Architecture / ISA | Instruction set, e.g., x86-64 or ARM64 |
| TDP / processor power rating | Cooling/power design guidance; **not necessarily actual maximum electrical draw** |
| Integrated graphics (iGPU) | GPU built into certain processors; not all CPUs include one |
| Thermal throttling | CPU reduces performance/speed to keep temperatures within limits |

**Common trap:** More GHz does not automatically mean better performance; architecture, cores, cache, thermals, and workload matter.

## 2.3 CPU sockets and compatibility

- The **CPU socket** must be compatible with the specific processor.
- The **motherboard chipset** and **firmware version** must also support the CPU.
- Check the manufacturer's CPU support list before buying or replacing a processor.
- A matching socket alone is **not enough** to guarantee compatibility.

Examples of socket families: Intel **LGA** and AMD **AM4/AM5** (check actual generation/model). Some laptops have soldered CPUs that cannot be replaced individually.

## 2.4 Cooling, fans, and thermal paste

- A CPU cooler moves heat away from the processor.
- **Thermal paste** fills microscopic gaps between CPU and cooler; it does not replace proper heatsink contact.
- Ensure the cooler is secured and the fan/pump connects to the proper header.
- Do not touch socket pins or contacts; avoid excessive force.

### CPU troubleshooting

| Symptom | First checks |
|---|---|
| High temperature or shutdowns | Fan/pump, dust, cooler mounting, airflow, temperature readings |
| New CPU won't POST | Socket, supported CPU list, BIOS version, EPS CPU power |
| Slow under sustained load | Thermal throttling, power settings, background processes |
| No display | Monitor/cable, RAM, GPU, integrated-graphics availability; don't assume CPU failure |

### Exam essentials

- Distinguish **cores vs threads**, **cache vs RAM**, and **clock speed vs performance**.
- Know that overheating can produce throttling, freezing, or shutdowns.
- Check **socket + BIOS + chipset compatibility** before CPU replacement.

---

# 3. RAM (Random Access Memory)

## 3.1 What is RAM?

RAM stores data and instructions actively used by the CPU. Standard system RAM is **volatile**, so it loses its contents when power is removed.

**RAM vs SSD:** RAM = fast temporary workspace; SSD = persistent storage for files and installed programs.

## 3.2 RAM vocabulary

| Term | Meaning |
|---|---|
| DIMM | Common full-size desktop memory module |
| SO-DIMM | Smaller module common in many laptops and mini PCs |
| DDR4 / DDR5 | Different RAM generations; not interchangeable |
| Capacity (GB) | How much data RAM can hold |
| Data rate (MT/s) | Memory transfers per second, a useful speed measure |
| Latency (CL) | Timing measure; evaluate together with data rate |
| Single-/dual-channel | Memory-channel configurations; dual-channel can increase bandwidth |
| ECC RAM | Memory with error-correction capability; needs platform support |
| XMP / EXPO | Supported memory performance profiles, usually enabled in firmware |

**Be careful:** DDR3, DDR4, and DDR5 module notches and electrical standards differ. Never force a module into an incompatible slot.

## 3.3 Correct RAM installation

1. Shut down, unplug AC, and follow ESD precautions.
2. Confirm **DDR generation, module type, capacity, and motherboard support**.
3. Open the slot latch(es) as designed.
4. Align the module notch with the slot key.
5. Press straight down until fully seated and the retention mechanism engages.
6. For two modules, check the board manual for the correct paired slots (often A2/B2, **not always**).
7. Boot and verify detected capacity and stability.

## 3.4 What happens with insufficient RAM?

- Too many browser tabs/apps may consume available memory.
- The OS uses a **page file/swap** on storage, which is normally much slower than RAM.
- You may experience slow switching, pauses, or heavy disk activity.

### RAM troubleshooting

| Symptom | First checks |
|---|---|
| PC won't POST after installing RAM | Reseat, correct slots, generation/support, test one module at a time |
| Only half the memory detected | Seating, failed module/slot, platform capacity limitations |
| Random crashes / blue screens | Memory diagnostics, overclock/profile settings, module stability |
| System sluggish with many apps | RAM usage and page-file activity in Task Manager |

**Windows tools:** Task Manager → **Performance → Memory**; run **Windows Memory Diagnostic** (`mdsched.exe`). A clean test does not guarantee RAM is fault-free.

### Exam essentials

- DIMM vs SO-DIMM; DDR4 vs DDR5; volatile RAM vs nonvolatile storage.
- RAM compatibility includes **generation, motherboard limits, and supported configuration**.
- Memory faults can look like general instability or intermittent crashes.

---

# 4. Storage: HDD, SSD, SATA, M.2 & NVMe

## 4.1 What is storage?

Storage keeps the OS, applications, and personal data **when power is off**.

### Compare the main types

| Type | Technology | Strength | Limitation |
|---|---|---|---|
| HDD | Spinning magnetic disks | Economical bulk storage | Slower, moving parts |
| SATA SSD | Flash memory, SATA interface | Fast vs HDD, common upgrade | Limited by SATA interface |
| NVMe SSD | Flash memory, NVMe protocol over PCIe | High throughput, low latency | Compatibility/heat/cost vary |

## 4.2 Understand the naming (very important)

- **HDD or SSD** describes the storage technology.
- **2.5-inch / 3.5-inch / M.2** describes form factor or physical shape.
- **SATA / PCIe** describes the connection/interface.
- **NVMe** is a protocol commonly used by SSDs connected over PCIe.

**Important:** **M.2 does not automatically mean NVMe.** M.2 SSDs can use SATA or PCIe/NVMe depending on the drive and slot. Always check the specifications.

### Examples

- 3.5-inch SATA HDD → desktop hard disk using SATA data + SATA power.
- 2.5-inch SATA SSD → SSD using SATA data + SATA power.
- M.2 NVMe SSD → SSD in an M.2 slot using PCIe lanes and NVMe.
- M.2 SATA SSD → M.2-shaped SSD using the SATA interface; works only with compatible M.2 slots.

## 4.3 SATA vs NVMe

| Topic | SATA SSD | NVMe SSD |
|---|---|---|
| Data connection | SATA | PCIe |
| Common form factor | 2.5-inch; sometimes M.2 | M.2; sometimes add-in card or U.2/U.3 |
| Typical maximum interface example | SATA III: 6 Gb/s signaling (~550 MB/s practical sequential speeds) | Depends on PCIe generation and lane count |
| Best use | General desktop/laptop upgrades | Fast OS, applications, large file and demanding workloads |

**Do not memorize one universal NVMe speed.** It varies with PCIe generation, available lanes, drive model, and workload.

## 4.4 Partition styles and file systems

- **MBR:** Older partitioning scheme; with 512-byte logical sectors, traditionally limited to about **2 TiB** per disk and four primary partition entries (without extended partitions).
- **GPT:** Modern partitioning scheme that supports many partitions and very large disks; standard choice for modern UEFI OS installs.
- **NTFS:** Common Windows file system with permissions and other advanced features.
- **exFAT:** Common for removable drives shared among operating systems; no native NTFS-style ACL model.
- **FAT32:** Broad compatibility, but individual file size is limited to **4 GiB − 1 byte**.
- **ext4:** Common Linux file system.

**Formatting vs partitioning:** Partitioning divides a disk into logical regions; formatting creates a file system within a partition/volume.

## 4.5 Storage health and maintenance

- **SMART:** Drive health/diagnostic information; useful, but not a guarantee of future reliability.
- **TRIM:** Lets an OS inform supported SSDs that blocks are no longer needed, helping manage flash storage.
- **Backup:** Protect important data **before** working on a questionable drive.
- **RAID is not a backup:** RAID can improve availability/performance, but does not protect against deletion, ransomware, fire, or all controller failures.
- SSDs do not need traditional HDD defragmentation; Windows performs appropriate drive optimization automatically.

### Storage troubleshooting

| Symptom | First checks |
|---|---|
| Drive missing in BIOS/UEFI | Power/cable, port/slot support, seating, drive health |
| Drive in BIOS but not File Explorer | Disk Management, partition, formatting, assigned drive letter |
| Very slow HDD | Disk health, free space, background I/O; back up if failure suspected |
| NVMe drive disappears under load | Temperature, firmware, seating, hardware/slot problems |
| “No bootable device” | Boot order, drive detection, bootloader / OS installation |
| Clicking HDD | **Back up immediately if possible**; minimize further use; consider professional recovery |

**Data safety:** Initializing, formatting, or deleting partitions may destroy access to data. Check which disk you're working on first.

### Exam essentials

- Recognize **HDD vs SSD**, **SATA vs NVMe**, **M.2 vs 2.5-inch**.
- Understand **GPT vs MBR** and basic **NTFS/exFAT/FAT32** use cases.
- Know why backups matter before troubleshooting a failing disk.

---

# 5. How These Components Work Together

```text
Power button
    |
    v
Motherboard / power delivery
    |
    v
CPU starts BIOS/UEFI firmware
    |
    v
POST and hardware initialization (including RAM)
    |
    v
Firmware selects bootloader on storage drive
    |
    v
Operating system loads from SSD/HDD into RAM
    |
    v
CPU runs OS and application instructions
```

**One-sentence memory trick:** **UEFI starts the computer; the CPU executes; RAM holds active work; storage remembers it after power-off.**

---

# 6. Windows Commands for IT Support

Open **PowerShell** (commands shown here are read-only unless noted).

```powershell
# Motherboard information
Get-CimInstance Win32_BaseBoard | Select-Object Manufacturer, Product, Version

# Firmware vendor and version
Get-CimInstance Win32_BIOS | Select-Object Manufacturer, SMBIOSBIOSVersion

# CPU name, core count, logical processor count
Get-CimInstance Win32_Processor | Select-Object Name, NumberOfCores, NumberOfLogicalProcessors

# Physical RAM sticks and reported speed/capacity
Get-CimInstance Win32_PhysicalMemory | Select-Object BankLabel, Capacity, Speed, Manufacturer

# Installed physical drives (disk model and bus type)
Get-PhysicalDisk | Select-Object FriendlyName, MediaType, BusType, Size, HealthStatus

# Windows-visible disks and partition styles
Get-Disk | Select-Object Number, FriendlyName, PartitionStyle, Size

# System information including BIOS mode (GUI)
msinfo32

# Disk Management (GUI)
diskmgmt.msc

# Memory diagnostic (requires a restart to test)
mdsched.exe
```

> Some fields may be blank, approximate, or incorrectly reported by firmware and drivers. Cross-check manufacturer documentation where needed.

---

# 7. Hands-on Practice Checklist

## BIOS / UEFI
- [ ] Open System Information (`msinfo32`) and identify BIOS Mode.
- [ ] Find your motherboard firmware version.
- [ ] Enter UEFI setup using the manufacturer-recommended key or Windows advanced startup.
- [ ] Identify the boot order **without changing it**.
- [ ] Locate Secure Boot, TPM, and virtualization settings (do not change without a reason).

## CPU
- [ ] Identify CPU model and socket from official specifications.
- [ ] Find the core count and logical processor count in Windows.
- [ ] Observe CPU utilization in Task Manager.
- [ ] Read CPU temperature with a reliable monitoring tool or firmware interface.

## RAM
- [ ] Find total installed RAM and current utilization in Task Manager.
- [ ] Check module count and speed.
- [ ] Determine whether the system uses DDR4 or DDR5 from official specs.
- [ ] Check the motherboard manual for supported capacity and slot order.

## Storage
- [ ] Identify your HDD(s) and SSD(s).
- [ ] Find whether each uses SATA or NVMe/PCIe.
- [ ] Open Disk Management and identify partitions **without deleting anything**.
- [ ] Find whether your OS disk uses GPT or MBR.
- [ ] Verify that important files have a backup.

---

# 8. Troubleshooting Scenarios (Interview Practice)

**Scenario 1 — A PC powers on, but the screen stays black.**  
Check the display/cable/input, POST diagnostics, RAM seating, GPU/display output, and power cables. Do not assume the CPU is broken.

**Scenario 2 — A PC started crashing after adding RAM.**  
Check compatibility, seat the modules properly, disable unstable memory profiles, test one module at a time, and run diagnostics.

**Scenario 3 — After an OS reinstall, the SSD appears in BIOS but not Windows Explorer.**  
Check Disk Management for a missing drive letter, unallocated space, or an unmounted/unformatted partition. **Confirm no needed data exists before modifying partitions.**

**Scenario 4 — A computer reports no boot device.**  
Check drive detection and UEFI boot order first. Then investigate EFI boot files, operating system installation, and drive condition.

**Scenario 5 — CPU performance suddenly drops during gaming or stress tests.**  
Check temperatures, cooler installation, fan operation, airflow, power restrictions, and thermal throttling.

---

# 9. Quick Review Questions

1. What is the difference between BIOS and UEFI?
2. What does POST stand for?
3. Is Secure Boot the same as drive encryption?
4. What is the difference between UEFI and GPT?
5. What is the function of the RTC/CMOS battery?
6. Why doesn't a CPU socket match guarantee CPU compatibility?
7. What is the difference between CPU cores and logical processors?
8. What is CPU thermal throttling?
9. Why is RAM called volatile memory?
10. What is the difference between DIMM and SO-DIMM?
11. Can DDR4 fit in a DDR5 slot?
12. What is dual-channel RAM?
13. Does M.2 always mean NVMe?
14. What is the difference between SATA and PCIe/NVMe?
15. What is the FAT32 maximum individual file size?
16. What is the difference between GPT and MBR?
17. What does SMART do?
18. What should you do before investigating a failing storage drive?
19. Why might a disk appear in firmware but not File Explorer?
20. Which component runs software, which stores active data, and which keeps files after shutdown?

<details>
<summary><strong>Short answers — open after trying the questions</strong></summary>

1. BIOS is older PC firmware; UEFI is the modern firmware standard.
2. Power-On Self-Test.
3. No; Secure Boot checks boot trust, while encryption protects data at rest.
4. UEFI is firmware; GPT is a partition scheme.
5. Maintains the real-time clock when external power is absent.
6. Chipset and firmware must support the exact CPU too.
7. Cores are processing units; logical processors are execution contexts exposed to the OS.
8. Reducing performance to control temperature.
9. It loses normal working data when power is removed.
10. Desktop-sized vs compact memory modules.
11. No.
12. A memory configuration using two channels to increase bandwidth.
13. No, some M.2 drives use SATA.
14. SATA is an older storage interface; NVMe is a protocol for PCIe-connected storage.
15. 4 GiB − 1 byte.
16. Older vs modern partitioning scheme, with GPT supporting larger disks and more partitions.
17. Reports storage device diagnostic/health data.
18. Protect or back up important data before risky steps.
19. Partition, file system, mounting, or drive-letter issues.
20. CPU executes; RAM temporarily holds active data; SSD/HDD persists data.

</details>

---

# 10. Last-minute Cheat Sheet

| If you see this term... | Remember this... |
|---|---|
| UEFI | Modern boot firmware |
| POST | Early startup hardware checks |
| Secure Boot | Trusted boot verification, **not encryption** |
| GPT | Modern disk partitioning |
| CPU core | Processing unit inside the CPU |
| CPU cache | Very fast small memory near/on CPU |
| Thermal throttling | Performance reduction to limit heat |
| RAM | Volatile working memory |
| DIMM | Common desktop RAM module |
| SO-DIMM | Common compact/laptop RAM module |
| DDR4 vs DDR5 | Not physically interchangeable |
| HDD | Magnetic spinning disk |
| SSD | Solid-state flash storage |
| SATA | Storage interface |
| M.2 | Physical slot/module form factor |
| NVMe | Storage protocol over PCIe |
| SMART | Drive health information |
| Backup | Separate recoverable copy of data |

