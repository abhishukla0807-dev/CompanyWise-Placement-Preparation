# 01 — Introduction to Operating Systems

#### Foundation Concepts Every CS Student Must Know Before Diving Deeper

> This chapter covers the core building blocks of OS — what it is, why it exists, how it is structured, and how it boots. These topics appear in almost every placement test and technical interview.

---

## 📌 Table of Contents

| # | File | Description |
|---|------|-------------|
| 1 | [What is an Operating System](./What_is_Operating_System.md) | Definition, role, components, OS vs Kernel |
| 2 | [Goals of OS](./Goals_of_OS.md) | Convenience, Efficiency, Ability to Evolve |
| 3 | [Functions of OS](./Functions_of_OS.md) | Process, Memory, File, I/O, Security, Networking |
| 4 | [Types of OS](./Types_of_OS.md) | Batch, Time-Sharing, Real-Time, Distributed, Mobile |
| 5 | [OS Structure](./OS_Structure.md) | Monolithic, Layered, Microkernel, Modular, Hybrid |
| 6 | [Booting Process](./Booting_Process.md) | BIOS, POST, MBR, Bootloader, Kernel Init, systemd |

---

## 📖 Chapter Overview

This chapter answers three fundamental questions:

**What is an OS?**
- Software layer between hardware and user applications
- Manages CPU, memory, storage, and I/O devices
- Provides system calls so programs do not interact with hardware directly

**Why does an OS exist?**
- Without an OS every program must manage hardware on its own
- OS enables resource sharing, process isolation, and hardware abstraction
- Designed around three goals: convenience, efficiency, and ability to evolve

**How is an OS built and started?**
- Internal structure determines performance and reliability tradeoffs
- Five structural models: Monolithic, Layered, Microkernel, Modular, Hybrid
- Boot sequence: Power ON → BIOS/UEFI → POST → Bootloader → Kernel → Init → Login

---

## ✦ Interview Relevance

| Company Type | Commonly Asked Topics |
|-------------|----------------------|
| TCS, Infosys, Wipro | What is OS, Functions of OS, Types of OS |
| Accenture, Cognizant | OS vs Kernel, Booting Process, Types of OS |
| Amazon, Microsoft, Flipkart | OS Structure, Kernel types, Microkernel vs Monolithic |
| Google, Uber, Paytm | Booting internals, systemd vs Init, Kernel mode vs User mode |

---

## ✦ Key Concepts at a Glance

**OS Definition**
- Intermediary between hardware and user programs
- Kernel is the core resident component; OS includes kernel plus shell plus utilities

**Goals**
- Convenience — ease of use for end user
- Efficiency — optimal hardware utilization
- Ability to Evolve — support new hardware and features without breaking existing ones

**Functions**
- Process Management, Memory Management, File System, I/O Management, Security, Networking

**Types**
- Batch — sequential, no interaction
- Time-Sharing — multiple users, time slices
- Real-Time — strict timing guarantees
- Distributed — multiple machines as one system
- Mobile — touch, battery-optimized, sandboxed

**Structure**
- Monolithic — everything in kernel space, fastest but fragile
- Microkernel — minimal kernel, services in user space, most reliable
- Hybrid — balance of both, used in Windows and macOS

**Booting**
- BIOS/UEFI initializes hardware
- POST checks hardware health
- Bootloader loads kernel into RAM
- Init/systemd starts all services

---




*Made for CS Students | Internship & Job Prep Series*