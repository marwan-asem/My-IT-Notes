
## 1. What Is a Motherboard?

A **motherboard** is the main circuit board in a computer. It connects the CPU, RAM, storage, power supply, and expansion devices so they can communicate.

**Think of a computer as a city:**

- **CPU:** The brain that processes instructions.
- **RAM:** A temporary workspace.
- **SSD/HDD:** Long-term storage.
- **PSU:** Supplies electrical power.
- **Motherboard:** Connects the components, like roads connecting buildings.

**Key idea:** The motherboard connects hardware, distributes power to components, provides expansion ports, and supports system firmware.

## 2. Main Motherboard Components

| Component | What it does | What to remember |
|---|---|---|
| CPU socket | Holds the processor | CPU and socket must be compatible |
| DIMM slots | Hold desktop RAM | Match DDR generation and motherboard support |
| Chipset / PCH | Manages many I/O connections | Capabilities vary by platform |
| PCIe slots | Support expansion cards | Commonly used for GPUs and network cards |
| SATA ports | Connect SATA data devices | SATA drives also need PSU power |
| M.2 slots | Accept compatible SSDs and other modules | M.2 is a form factor; not every slot supports every protocol |
| 24-pin ATX connector | Main motherboard power | Often PSU cable is 20+4 pin |
| 4/8-pin CPU power (EPS) | Powers CPU voltage regulation | Not interchangeable with GPU PCIe power |
| VRM | Regulates voltage to CPU and other parts | Often near CPU socket |
| BIOS/UEFI firmware | Initializes hardware and starts boot | Settings accessible during startup |
| CMOS/RTC battery | Maintains real-time clock when disconnected from power | A weak battery may reset date/time |
| Fan headers | Connect cooling fans | Often CPU_FAN and SYS_FAN |
| Front-panel header | Connects case power/reset buttons and LEDs | Pin layout varies; check manual |
| Internal USB headers | Connect case front USB ports | Types vary by board |
| Rear I/O | External USB, audio, network, display, etc. | Available connectors vary by board |

**Memory trick:** CPU → socket; RAM → DIMM; GPU → PCIe; storage → SATA/M.2; PSU → ATX/EPS.

## 3. Motherboard Form Factors

| Form factor | Common dimensions | Typical use |
|---|---|---|
| ATX | 305 × 244 mm | Full-size desktops; more expansion room |
| microATX | Up to 244 × 244 mm | Office and budget desktops |
| Mini-ITX | 170 × 170 mm | Small-form-factor PCs |

**Exam tip:** Case size and mounting support matter. Many ATX cases also support microATX and Mini-ITX, but always verify the case specifications.

## 4. Power Connectors

### 24-pin ATX power
- Main power connection between PSU and motherboard.
- Some PSU cables split as **20+4**.

### 4/8-pin EPS CPU power
- Supplies CPU voltage-regulation circuitry.
- Sometimes labeled **CPU_PWR** or **ATX12V**.
- **Never interchange EPS/CPU cables with PCIe/GPU cables.**

### Important safety warning
- Modular PSU cables are **not universally interchangeable** between PSU models—even if connectors look the same.
- Disconnect AC power before installing or disconnecting internal parts.
- Never open a PSU housing: capacitors can retain dangerous electrical charge.

## 5. Storage Interfaces

### SATA
- A connection used for SATA SSDs, HDDs, and some optical drives.
- A typical SATA drive needs **two separate connections**:
  1. SATA **data** cable to motherboard.
  2. SATA **power** cable from PSU.

### M.2
- A compact physical form factor often used for SSDs.
- Some slots support **PCIe/NVMe**, some support **SATA**, and some support both.
- Check **M.2 keying, length (e.g., 2280), protocol, and motherboard manual**.
- NVMe SSDs communicate using the NVMe protocol, typically over PCIe.

**Remember:** *M.2 describes the physical form factor; NVMe describes a storage protocol.*

## 6. PCI Express (PCIe)

PCIe is a high-speed interface for expansion cards.

| Lanes | Common uses |
|---|---|
| x1 | Wi-Fi cards, sound cards, some USB cards |
| x4 | Storage and network adapters |
| x8 | Network adapters and specialized cards |
| x16 | Graphics cards and other high-bandwidth cards |

- **Physical slot size** does not always equal **electrical lane count**.
- PCIe versions offer different data rates.
- Older PCs may have legacy **PCI** slots.

## 7. CPU and RAM Compatibility

Before upgrading, check:

1. **CPU socket** — e.g., AM5 or a particular Intel socket.
2. **CPU model compatibility** — matching socket alone is not enough.
3. **BIOS/UEFI version** — some CPUs require a firmware update.
4. **RAM generation** — DDR4 and DDR5 are not interchangeable.
5. **RAM capacity and supported speeds** — use board/CPU documentation.
6. **Case form factor** and physical clearance.
7. **Power connections** and PSU suitability.

**Example:** DDR4 RAM will not fit a DDR5 DIMM slot. A CPU with a matching socket may still be unsupported by a specific board or firmware version.

## 8. BIOS, UEFI, CMOS, POST

| Term | Simple meaning |
|---|---|
| BIOS | Traditional firmware that initializes hardware |
| UEFI | Modern firmware interface with enhanced boot and security features |
| POST | Power-On Self-Test; checks essential hardware during startup |
| CMOS | Legacy term often associated with firmware settings storage |
| RTC battery | Keeps the system clock running when external power is absent |
| Secure Boot | UEFI feature that helps ensure trusted boot components load |
| TPM | Security hardware/functionality used for cryptographic operations |

### What happens when you press the power button?

1. The power button signals the motherboard to start the system.
2. The PSU enables its main outputs; motherboard/CPU power stabilizes.
3. The CPU starts executing firmware code.
4. BIOS/UEFI initializes hardware and performs POST.
5. Firmware selects a configured boot entry/device.
6. The bootloader starts the operating system.

**Note:** The exact sequence varies by platform.

## 9. Rear I/O and Internal Headers

Common rear ports to recognize:

- **USB-A / USB-C:** Peripherals, storage, and more.
- **RJ-45 Ethernet:** Wired networking.
- **3.5 mm audio:** Speakers, microphones, headsets.
- **HDMI / DisplayPort:** Display output *if supported by the motherboard and CPU/platform*.
- **PS/2:** Older keyboard/mouse connector on some PCs.

Common internal headers:

- **F_PANEL:** Power button, reset button, power LED, drive activity LED.
- **CPU_FAN / SYS_FAN:** Cooling fan connections.
- **USB headers:** Front-panel USB connections.
- **Front audio header:** Case audio ports.

**Tip:** Always use the exact motherboard manual for front-panel pin positions and polarity.

## 10. Troubleshooting: Symptoms and Checks

| Symptom | Possible causes | First checks |
|---|---|---|
| Completely dead PC | Wall power, PSU, switch, cables, motherboard | Outlet, power cable, PSU switch, 24-pin/EPS, front-panel switch |
| Powers on, no display | Monitor/input, RAM, GPU, CPU, firmware | Monitor, video cable, diagnostic LEDs, RAM/GPU seating |
| Random restarts | Heat, power instability, RAM | Temperatures, cooling, PSU, event logs |
| SSD not detected | Cable, slot compatibility, BIOS setting, failed SSD | BIOS/UEFI detection, SATA data/power, M.2 support |
| Date/time repeatedly resets | Weak RTC battery | Clock settings and battery |
| USB ports do not work | Device, port, internal cable, driver | Test different device/port; inspect Device Manager |
| No boot device found | Boot-order issue, missing drive, drive problem | Firmware boot list and storage detection |
| Fails POST after upgrade | Compatibility or installation issue | CPU/RAM support, BIOS version, power, seated modules |

### A simple troubleshooting method

1. **Identify the symptom.** What exactly happens?
2. **Check easy external causes first.** Power, display, cables, peripherals.
3. **Check diagnostics.** Beep codes, POST LEDs/codes, BIOS messages.
4. **Change one thing at a time.** Reseat RAM, use known-good parts if available.
5. **Verify the fix.** Restart and test normal usage.
6. **Document your findings.** Especially useful in IT Support tickets.

**Don't assume:** No display does not automatically mean a bad motherboard.

## 11. Windows Tools for Motherboard Information

**PowerShell — motherboard model:**

```powershell
Get-CimInstance Win32_BaseBoard | Select-Object Manufacturer, Product, Version
```

**Open System Information:**

```powershell
msinfo32
```

Look for **BaseBoard Manufacturer/Product**, **BIOS Version/Date**, and **BIOS Mode**.

**Open Device Manager:**

```powershell
devmgmt.msc
```

Useful for investigating controllers and connected hardware.






