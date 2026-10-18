
**Level:** Beginner to Intermediate  
## 1. Computer Hardware Fundamentals

Hardware is the collection of physical components in a computer.
![[parts of computers.png]]

| Component | Function | Common issues |
|---|---|---|
| CPU | Executes instructions | Overheating, failure to POST |
| Motherboard | Connects components | No power, faulty ports |
| RAM | Temporary working memory | Crashes, freezing, POST errors |
| SSD/HDD | Stores files and OS | Slow PC, boot failure |
| PSU | Converts AC to regulated DC | No power, unexpected shutdown |
| GPU | Generates graphics | No display, visual artifacts |
| Cooling | Removes heat | Overheating, throttling |
| RTC/CMOS battery | Maintains clock and some firmware settings | Clock/configuration resets |

## 2. Motherboard

The **motherboard** is the main printed circuit board (PCB).
### Components to identify
- **CPU socket:** Must match the CPU platform.
- **DIMM slots:** Hold desktop RAM.
- **PCIe slots:** Support GPUs, NICs, and expansion cards.
- **M.2 slots:** May support NVMe or SATA SSDs (check the board specification).
- **SATA ports:** Connect compatible SATA storage.
- **24-pin ATX:** Main motherboard power connector.
- **4/8-pin EPS CPU:** CPU power input.
- **VRM:** Regulates voltages for chips.
- **Front-panel header:** Case power/reset switches and LEDs.
- **UEFI/BIOS firmware:** Initializes hardware and controls boot settings.

### Common faults

| Symptom | Possible cause | Technician check |
|---|---|---|
| No power | PSU, power switch, motherboard | Outlet, cables, front-panel connections |
| Fans run, blank screen | RAM, GPU, CPU, firmware | POST LEDs/beeps, display connection |
| USB port fails | Device, port, driver, controller | Try known-good device and alternate port |
| Drive missing | Storage, connector, firmware | BIOS detection, cables, drive health |
| Clock loses time | RTC battery | Replace appropriate battery if indicated |

> **Remember:** Fans spinning does not prove POST succeeded.

## 3. CPU (Central Processing Unit)
The CPU carries out instructions and calculations.

| Term | Meaning |
|---|---|
| Core | Physical execution core |
| Thread | Logical execution stream |
| Clock speed | Operating frequency (GHz) |
| Cache | Very fast memory on/near CPU |
| TDP | Thermal design rating, not necessarily maximum draw |
| Thermal throttling | Automatic performance reduction due to heat |
| Integrated graphics | GPU included in some CPUs |

**Troubleshooting:** Check temperatures, fan operation, dust, heatsink installation, and BIOS/CPU compatibility. Thermal paste may need replacement when reinstalling a heatsink.
## 4. RAM (Random Access Memory)
RAM temporarily holds active data and is **volatile** (data is lost without power).
- **DDR4 and DDR5** are different and not interchangeable.
- **DIMM** is common in desktops; **SO-DIMM** in many laptops.
- Capacity is measured in GB; transfer speed commonly in MT/s.
- **Dual-channel** can increase memory bandwidth.
- **ECC** can detect/correct certain errors on supported platforms.
### Typical symptoms
- Blue-screen errors (BSOD)
- Random freezing/restarts
- Application crashes
- Memory-related POST/beep codes
### Safe RAM test procedure
1. Shut down and unplug the PC.
2. Apply electrostatic discharge (ESD) precautions.
3. Reseat removable modules.
4. Test modules individually using supported slots.
5. Run **Windows Memory Diagnostic** (`mdsched.exe`) or **MemTest86**.
6. Check motherboard compatibility and memory settings.
## 5. Storage: HDD, SATA SSD, NVMe SSD

| Feature | HDD | SATA SSD | NVMe SSD |
|---|---|---|---|
| Technology | Spinning magnetic disks | Flash | Flash |
| Typical interface | SATA | SATA | PCIe (NVMe) |
| Performance | Lower | Medium | Higher |
| Moving parts | Yes | No | No |

### Useful diagnostics
- **Disk Management** (`diskmgmt.msc`)
- **Device Manager** (`devmgmt.msc`)
- **Event Viewer** (`eventvwr.msc`)
- **CrystalDiskInfo** (supported SMART indicators)
- Manufacturer diagnostic utilities

> **Important:** Back up critical data before stress-testing or repairing a drive that may be failing.

---

# 6. Power Supply Unit (PSU)
 **What does a PSU do?**
  A desktop PSU converts wall **AC power** into regulated **DC voltage rails** needed by the computer.

```text
Wall outlet (AC; usually 220–240 V in Egypt)
                  |
                  v
          Power Supply Unit
     (conversion and regulation)
                  |
                  v
        +12 V / +5 V / +3.3 V
                  |
                  v
       Motherboard and devices
```

## PSU voltage rails

| Rail | Typical uses |
|---|---|
| +12 V | CPU/GPU voltage regulation, fans, motors |
| +5 V | USB and various electronic circuits |
| +3.3 V | Motherboard logic and other electronics |
| +5 VSB | Standby and soft-power functions |
| -12 V | Some legacy circuits |

> Modern CPU/GPU circuitry steps voltage down locally using voltage regulators.

## PSU connectors

| Connector | Where used |
|---|---|
| 24-pin ATX | Motherboard main power |
| 4+4-pin EPS | CPU power input |
| 6+2-pin PCIe | Compatible GPU power input |
| 12V-2x6 | Supported high-power GPUs |
| 15-pin SATA power | SATA drives and certain peripherals |
| 4-pin Molex | Older accessories |

**Safety:** EPS CPU and 8-pin PCIe GPU connectors are not interchangeable. **Modular PSU cables are not universally compatible across PSU models**, even if plugs appear to fit.

## Wattage basics

Electrical power:

$$P=V\times I$$

- **P**: Power (W)
- **V**: Voltage (V)
- **I**: Current (A)

**Example:** A 12 V device drawing 5 A uses **60 W**.

For sizing, estimate CPU + GPU + all other components, then choose a reliable PSU with suitable headroom, supported connectors, and enough capacity for peak/transient loads. Follow GPU and PSU manufacturer recommendations.

### Practice example

| Component group | Example power |
|---|---:|
| CPU | 65 W |
| GPU | 180 W |
| Other components | 60 W |
| **Estimated total** | **305 W** |

Using **30% headroom** as a *learning example*: 305 × 1.3 = **396.5 W**, rounded up to a standard suitable PSU capacity (e.g. 450 W), *provided the actual GPU/PSU specifications and transient demands permit it*. This is not a universal rule.

## PSU efficiency and 80 PLUS

Efficiency = DC output power / AC input power.

Example: A PSU delivering **400 W** at **80% efficiency** draws **500 W** from the wall and dissipates approximately **100 W** as heat.

Common 80 PLUS tiers: Standard, Bronze, Silver, Gold, Platinum, Titanium.

**Note:** Better efficiency does *not automatically* mean better build quality or protection.

## PSU protections

| Code | Meaning |
|---|---|
| OVP | Over Voltage Protection |
| UVP | Under Voltage Protection |
| OCP | Over Current Protection |
| OPP | Over Power Protection |
| SCP | Short Circuit Protection |
| OTP | Over Temperature Protection |

---

## 7. Power Supply Troubleshooting

| Symptom                 | Possible causes                         | Initial investigation                     |
| ----------------------- | --------------------------------------- | ----------------------------------------- |
| Absolutely no power     | Outlet, cable, switch, PSU, motherboard | Test known-good external power path       |
| Sudden power-off        | PSU, overheating, other hardware        | Check temps, logs, power connections      |
| Restarts under GPU load | Power delivery, GPU, thermal issue      | Review loads, cabling, temps              |
| Clicking/odd sound      | Fan, relay, damaged part                | Identify source safely                    |
| Burning smell/smoke     | Electrical fault                        | Disconnect power immediately              |
| Fans spin; no display   | GPU, RAM, CPU, board, PSU               | Check POST diagnostics                    |
| Intermittent startup    | Loose cable, power button, PSU, board   | Inspect connectors and isolate components |

### Procedure: Desktop will not power on

1. Verify power at the outlet and check the power cable/power strip.
2. Confirm the PSU's external power switch is correctly set (if present).
3. Look for standby lights and POST indicators; note whether fans start.
4. Turn off and **unplug** the PC before opening it.
5. Check the 24-pin ATX, CPU EPS, and power-button header connections.
6. Remove nonessential peripherals and try a supported minimal configuration.
7. If equipped and trained, use an appropriate PSU tester; preferably substitute a **known-good compatible PSU**.
8. Confirm stable startup and document the result.

### Essential PSU safety

- **Never open the PSU enclosure.** Capacitors can retain dangerous energy after unplugging.
- Never reseat internal power connections while energized.
- Never bypass electrical protections.
- A simple PSU tester or unloaded voltage reading cannot conclusively verify reliability under load.
- If there is smoke, sparking, damaged insulation, or a burning smell, disconnect safely and stop troubleshooting.

## 8. BIOS/UEFI and Boot Process

```text
Power button
     |
Power sequencing
     |
CPU executes firmware
     |
POST / hardware initialization
     |
UEFI selects boot device
     |
OS bootloader
     |
Operating system
```

Know these settings:

- Boot order and device selection
- UEFI vs Legacy/CSM
- Secure Boot and TPM
- SATA/AHCI configuration
- Virtualization (Intel VT-x / AMD-V)
- Memory profiles (XMP/EXPO)
- Firmware version and vendor update procedure

**Diagnostic distinction:**

- **No power:** System does not turn on.
- **No POST:** Powers on but fails hardware initialization.
- **No boot:** Completes POST but cannot load an operating system.

## 9. Windows Hardware Diagnostic Tools

| Tool | Run command | Use |
|---|---|---|
| System Information | `msinfo32` | System model, firmware, hardware |
| Device Manager | `devmgmt.msc` | Hardware/drivers |
| Disk Management | `diskmgmt.msc` | Disk/partition setup |
| Event Viewer | `eventvwr.msc` | Errors and logs |
| Reliability Monitor | `perfmon /rel` | Failure timeline |
| Memory Diagnostic | `mdsched.exe` | RAM testing |
| DirectX Diagnostic | `dxdiag` | Display/audio details |
| Task Manager | `taskmgr` | Resource usage |

### PowerShell examples

**Basic computer information**

```powershell
Get-ComputerInfo |
  Select-Object CsManufacturer, CsModel, BiosBIOSVersion
```

**CPU**

```powershell
Get-CimInstance Win32_Processor |
  Select-Object Name, NumberOfCores, NumberOfLogicalProcessors
```

**RAM**

```powershell
Get-CimInstance Win32_PhysicalMemory |
  Select-Object Manufacturer, Capacity, Speed, PartNumber
```

**Physical drives**

```powershell
Get-PhysicalDisk |
  Select-Object FriendlyName, MediaType, HealthStatus, Size
```

**Unexpected shutdown logs**

```powershell
Get-WinEvent -FilterHashtable @{
  LogName = 'System'
  Id = 41, 6008
} -MaxEvents 15 |
  Select-Object TimeCreated, Id, Message
```

> **Event ID 41 (Kernel-Power)** indicates an unexpected shutdown/restart, but **does not prove the PSU failed**.

## 10. Hands-On Lab Checklist

- [ ] Identify motherboard, CPU, RAM, storage, GPU, and PSU in an unplugged desktop.
- [x] Identify ATX 24-pin, EPS 4+4-pin, PCIe 6+2-pin, and SATA power connectors.
- [ ] Open BIOS/UEFI and identify firmware version and boot settings.
- [ ] Perform a safe RAM diagnostic test.
- [ ] List installed drives and inspect supported health information.
- [ ] Review Windows Reliability Monitor and Event Viewer.
- [ ] Troubleshoot a mock no-boot situation using a systematic checklist.
- [ ] Write a service ticket with symptoms, tests, fix, and verification.

## 11. Interview Practice Questions

1. What happens when you press the power button?
2. What is the difference between RAM and storage?
3. What does the motherboard do?
4. What is POST?
5. What is the difference between BIOS and UEFI?
6. Why does a PC need a PSU?
7. Which connectors provide motherboard and CPU power?
8. What does 80 PLUS mean?
9. How do you troubleshoot a completely dead PC?
10. Why might a PC restart under load?
11. How could you distinguish a RAM fault from a PSU fault?
12. What does Windows Event ID 41 tell you?
13. How do SATA SSDs and NVMe SSDs differ?
14. What are the safe steps for PSU replacement?
