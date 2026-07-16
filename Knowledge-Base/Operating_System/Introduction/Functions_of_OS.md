# ⚙️ Functions of an Operating System

> *Made for CS Students | Internship & Job Prep Series*

---

## 📋 Table of Contents

| # | Topic |
|---|-------|
| 1 | [Overview](#1-overview) |
| 2 | [Process Management](#2-process-management) |
| 3 | [Memory Management](#3-memory-management) |
| 4 | [File System Management](#4-file-system-management) |
| 5 | [I/O Device Management](#5-io-device-management) |
| 6 | [Security and Protection](#6-security-and-protection) |
| 7 | [Networking](#7-networking) |
| 8 | [Interview Questions](#8-interview-questions) |
| 9 | [Resources](#9-resources) |

---

## 1. Overview

📌 An OS performs **six core functions** to manage hardware and provide services to user programs.

- **P** — Process Management
- **M** — Memory Management
- **F** — File System Management
- **I** — I/O Device Management
- **S** — Security and Protection
- **N** — Networking

![OS Functions Block Diagram](../diagrams/os_functions_overview.png)
> *Diagram: Central OS block with six function modules radiating outward*

---

## 2. Process Management

📌 A process is a program in execution. The OS manages every aspect of a process's lifecycle.

- Creates and terminates processes when programs are launched or finished
- Allocates CPU time to processes using scheduling algorithms like FCFS, Round Robin, and SJF
- Performs **context switching** — saves the state of a running process and restores another
- Handles **Inter-Process Communication** via pipes, message queues, shared memory, and sockets
- Coordinates processes sharing resources to prevent **race conditions** using mutexes and semaphores
- Detects and resolves **deadlocks** where processes are stuck waiting on each other indefinitely

---

## 3. Memory Management

📌 The OS tracks every byte of RAM — what is in use, what is free, and who owns what.

- Allocates memory to a process when it starts and deallocates it when the process ends
- Implements **virtual memory** to create the illusion of more RAM than physically available
- Uses **paging and segmentation** to map virtual addresses to physical memory locations
- Enforces **memory protection** — one process cannot access another process's address space
- Manages **swapping** — moves inactive process data to disk to free RAM for active processes

---

## 4. File System Management

📌 The OS provides a structured way to store, retrieve, and organize data on storage devices.

- Handles file operations: create, open, read, write, close, delete, rename
- Organizes files in a **hierarchical directory structure** and resolves path names
- Maps logical files to physical disk blocks using contiguous, linked, or indexed allocation
- Enforces **file permissions** — read, write, execute access per user and group
- Supports multiple file system formats: NTFS, ext4, APFS, FAT32

---

## 5. I/O Device Management

📌 The OS abstracts all hardware devices and provides a uniform interface for programs to use them.

- Uses **device drivers** as translators between generic OS I/O calls and device-specific behavior
- Handles **interrupts** — hardware signals the OS when I/O is complete; OS pauses current task to respond
- Uses **buffering** to temporarily hold data during transfer and smooth out speed differences between device and process
- Implements **spooling** to queue I/O jobs for devices that cannot handle simultaneous requests
- Uses **DMA** to allow devices to transfer data directly to RAM without constant CPU involvement

| Technique | Purpose |
|-----------|---------|
| **Buffering** | Smooths speed mismatch between fast CPU and slow devices |
| **Spooling** | Queues jobs for shared devices like printers |
| **DMA** | Offloads bulk data transfer from CPU to DMA controller |
| **Interrupts** | Notifies CPU when a device finishes its operation |

---

## 6. Security and Protection

📌 The OS enforces policies to protect data, processes, and hardware from unauthorized access and misuse.

- **Authentication** — Verifies user identity via passwords, PINs, biometrics, or tokens before granting access
- **Authorization** — Controls what resources an authenticated user can access
- **User mode vs Kernel mode** — User programs run in restricted mode; only the kernel runs in privileged mode with full hardware access
- **Memory protection** — Prevents processes from accessing each other's memory space
- **Audit logs** — Records login attempts, resource access, and system events for forensic analysis

> **Protection** = internal control between users and processes within the system
> **Security** = defense against external threats like malware and unauthorized network access

---

## 7. Networking

📌 The OS manages the full network stack and provides programs with simple interfaces to communicate over a network.

- Implements the TCP/IP protocol stack inside the kernel
- Provides the **socket API** so applications can send and receive data without knowing protocol internals
- Manages **network device drivers** for NICs and wireless adapters
- Handles packet routing, network buffer management, and connection state tracking

---

## 8. Interview Questions

**Q1. What are the main functions of an OS?**
- Process management, memory management, file system management, I/O device management, security and protection, and networking

**Q2. How does the OS manage multiple processes at once?**
- Via CPU scheduling algorithms that time-share the processor among ready processes
- Context switching saves and restores process state during each switch
- Synchronization tools like semaphores and mutexes prevent conflicts on shared data

**Q3. What is the difference between security and protection in OS?**
- Protection is internal — controlling access between processes and users within the system
- Security is external — defending against outside threats like malware, unauthorized logins, and network attacks

**Q4. What is a device driver?**
- A software module that allows the OS to communicate with a specific hardware device
- Translates generic OS I/O calls into device-specific commands
- Runs in kernel mode and has direct hardware access

**Q5. What is DMA and why is it used?**
- Direct Memory Access allows devices to transfer data directly to RAM without CPU involvement
- Frees the CPU to do other work during bulk data transfers like disk reads or network packet reception
- Significantly improves I/O performance on modern systems

**Q6. What is context switching?**
- The process of saving the state of a currently running process and loading the state of the next scheduled process
- State includes CPU registers, program counter, stack pointer, and memory mappings
- Enables time-sharing but introduces overhead — too many switches reduce CPU efficiency

---

## 9. Resources

- 📖 [GeeksforGeeks — Functions of Operating System](https://www.geeksforgeeks.org/functions-of-operating-system/)
- 📖 [PrepInsta — OS Functions](https://prepinsta.com/operating-system/)
- 📖 [Baeldung — OS Introduction](https://www.baeldung.com/cs/os-intro)
- 📖 [InterviewBit — OS Interview Questions](https://www.interviewbit.com/operating-system-interview-questions/)

---

*Made for CS Students | Internship & Job Prep Series*