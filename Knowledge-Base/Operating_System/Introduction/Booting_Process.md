# Booting Process

#### Step-by-Step Journey from Power ON to a Fully Loaded Operating System

> Booting loads the OS from storage into RAM so the computer becomes ready for use.

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 1 | [What is Booting](#1-what-is-booting) |
| 2 | [Boot Sequence Overview](#2-boot-sequence-overview) |
| 3 | [✦ BIOS / UEFI](#3--bios--uefi) |
| 4 | [✦ POST](#4--post) |
| 5 | [✦ Boot Sector and MBR](#5--boot-sector-and-mbr) |
| 6 | [✦ Bootloader](#6--bootloader) |
| 7 | [✦ Kernel Load](#7--kernel-load) |
| 8 | [✦ Init Process](#8--init-process) |
| 9 | [BIOS vs UEFI](#9-bios-vs-uefi) |
| 10 | [Types of Booting](#10-types-of-booting) |
| 11 | [Interview Questions](#11-interview-questions) |
| 12 | [Resources](#12-resources) |

---

## 1. What is Booting

> Booting is the process of starting a computer by loading the OS into RAM from a storage device.

- Begins the moment power is supplied to the system
- Ends when the OS is fully loaded and the login screen or desktop appears
- The term comes from "bootstrapping" — the system pulls itself up from nothing
- A small firmware program starts the chain that eventually loads the full OS

---

## 2. Boot Sequence Overview

```
Step 1: Power ON
        │
        ▼
Step 2: BIOS / UEFI
        • Initializes hardware components
        • Searches for a bootable device
        │
        ▼
Step 3: POST (Power-On Self-Test)
        • Verifies CPU, RAM, keyboard, storage, etc.
        │
        ▼
Step 4: MBR / GPT
        • Locates boot information on the storage device
        │
        ▼
Step 5: Bootloader (GRUB / Windows Boot Manager)
        • Loads the operating system kernel
        │
        ▼
Step 6: Kernel Initialization
        • Kernel is loaded into RAM
        • Initializes memory, drivers, and core subsystems
        │
        ▼
Step 7: Init Process (systemd / init)
        • Starts as Process ID (PID 1)
        • Launches essential system services
        │
        ▼
Step 8: System Services
        • Networking
        • Logging
        • Background services
        │
        ▼
Step 9: Login Screen / Desktop Ready
        • System is ready for user interaction
```

![Booting Sequence Diagram](../diagrams/booting_sequence.png)
> *Diagram: Linear flowchart of the full boot sequence from Power ON to Login screen*

---

## 3. ✦ BIOS / UEFI

> BIOS and UEFI are firmware programs stored on the motherboard that run before the OS loads.

- Firmware is the first code that executes when the computer powers on
- Stored in a ROM or flash chip on the motherboard — not on the hard drive
- Responsible for initializing all hardware components before handing control to the bootloader
- **BIOS** is the older standard; **UEFI** is the modern replacement with significantly more capabilities
- UEFI supports drives larger than 2 TB, Secure Boot, and a graphical setup interface

---

## 4. ✦ POST

> POST verifies all hardware is functioning before the boot process continues.

- Stands for **Power-On Self Test**
- Executed immediately by BIOS/UEFI after power is supplied
- Tests CPU, RAM, keyboard, storage devices, and GPU
- If POST succeeds, the system proceeds to locate the bootloader
- If POST fails, the system halts and emits beep codes or displays an error
- Different beep patterns indicate different hardware failures — for example, no RAM produces continuous beeping

---

## 5. ✦ Boot Sector and MBR

> The boot sector is the first region of a disk read by BIOS/UEFI to locate the bootloader.

- **MBR** stands for Master Boot Record — first 512 bytes of a bootable disk
- MBR contains a small bootstrap code and the partition table
- BIOS reads the MBR and transfers control to the bootstrap code inside it
- **GPT** is the modern replacement for MBR used with UEFI systems
- GPT supports more than 4 primary partitions and disks larger than 2 TB
- The bootloader code in MBR/GPT then loads the full bootloader from disk

---

## 6. ✦ Bootloader

> The bootloader locates the OS kernel on disk and loads it into RAM.

- A small program stored in the boot sector or EFI System Partition
- Executes in two stages on legacy BIOS systems: Stage 1 in MBR loads Stage 2 with full capabilities
- Presents a boot menu when multiple OS are installed
- Passes control to the kernel once it is loaded into memory

| Bootloader | OS | Storage Location |
|------------|----|-----------------|
| **GRUB 2** | Linux | MBR or EFI partition |
| **Bootmgr** | Windows Vista and later | Active partition |
| **NTLDR** | Windows XP | Root of C drive |
| **rEFInd** | macOS / Linux dual boot | EFI partition |

---

## 7. ✦ Kernel Load

> The bootloader transfers control to the kernel, which then initializes the entire OS environment.

- Bootloader loads the compressed kernel image into RAM
    - Linux kernel image: `vmlinuz`
    - Windows kernel image: `ntoskrnl.exe`
- Kernel decompresses itself in memory
- Sets up CPU registers, interrupt handlers, and memory management structures
- Detects hardware using ACPI tables and loads essential device drivers
- Mounts the root filesystem to make disk contents accessible
- Switches from real mode to protected mode on x86 systems during this phase

---

## 8. ✦ Init Process

> The kernel launches Init as the first user-space process — it becomes the parent of all other processes.

- Init always has **Process ID 1**
- Every process on the system is a child or descendant of Init
- Init is responsible for starting all background services and bringing the system to a usable state

| Init System | Description |
|-------------|-------------|
| **SysVinit** | Traditional Init; starts services sequentially using runlevel scripts |
| **systemd** | Modern replacement; starts services in parallel — significantly faster boot |
| **Upstart** | Event-driven Init developed by Ubuntu; now largely replaced by systemd |

- After Init starts all services, it launches the display manager or login shell
- System is now fully booted and ready for user interaction

---

## 9. BIOS vs UEFI

| Feature | BIOS | UEFI |
|---------|------|------|
| Full Form | Basic Input/Output System | Unified Extensible Firmware Interface |
| Interface | Text only, keyboard only | Graphical, mouse and keyboard |
| Partition Table | MBR | GPT |
| Max Disk Size | 2 TB | 9.4 ZB |
| Boot Speed | Slower | Faster due to parallel initialization |
| Secure Boot | Not supported | Supported |
| Storage Location | ROM chip | Flash memory |
| Max Partitions | 4 primary | 128 primary |

---

## 10. Types of Booting

> Two types of booting exist based on whether the system is starting fresh or restarting.

**Cold Boot**
- System starts from a completely powered-off state
- Full POST is performed
- All hardware is initialized from scratch
- Example: Pressing the power button on a shutdown computer

**Warm Boot**
- System restarts without full power-off
- POST may be skipped or shortened
- Faster than cold boot since hardware is already initialized
- Example: Clicking Restart in Windows or running `reboot` in Linux

---

## 11. Interview Questions

**Q1. What is the booting process?**
- Power ON → BIOS/UEFI → POST → Boot Sector → Bootloader → Kernel load into RAM → Init/systemd → OS ready

**Q2. What is BIOS?**
- Firmware stored on the motherboard ROM that initializes hardware and loads the bootloader
- First code executed on power-on before any OS code runs

**Q3. What is the difference between BIOS and UEFI?**
- UEFI supports GPT disks beyond 2 TB, provides a graphical interface, enables Secure Boot, and initializes hardware faster via parallel loading
- BIOS is limited to MBR, 2 TB disks, text interface, and sequential hardware initialization

**Q4. What is a Bootloader?**
- A small program that finds the OS kernel on disk and loads it into RAM
- Stored in MBR on BIOS systems or in the EFI partition on UEFI systems
- Common examples are GRUB on Linux and Bootmgr on Windows

**Q5. What is PID 1?**
- The Init process or systemd on modern Linux systems
- First user-space process spawned by the kernel after it finishes loading
- Parent of all other processes on the system

**Q6. What is Secure Boot?**
- A UEFI feature that verifies the bootloader is cryptographically signed by a trusted authority
- Prevents malicious software from replacing the bootloader during the boot sequence
- Can be disabled in UEFI settings, which is required for installing some Linux distributions

**Q7. What is the difference between Cold Boot and Warm Boot?**
- Cold Boot starts from a fully powered-off state with complete POST and hardware initialization
- Warm Boot is a restart where hardware is already powered and POST may be skipped, making it faster

---

## 12. Resources

- 📖 [GeeksforGeeks — Booting Process](https://www.geeksforgeeks.org/what-happens-when-we-turn-on-computer/)
- 📖 [PrepInsta — OS Boot Process](https://prepinsta.com/operating-system/)
- 📖 [Baeldung — Linux Boot Process](https://www.baeldung.com/linux/boot-process)
- 📖 [InterviewBit — OS Interview Questions](https://www.interviewbit.com/operating-system-interview-questions/)

---

*Made for CS Students | Internship & Job Prep Series*