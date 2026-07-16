# Types of Operating System

#### Classification of Operating Systems Based on Their Design and Use Case

> An operating system can be classified into several types based on how it handles processes, users, timing, and hardware. Each type is designed for a specific environment and set of requirements.

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 1 | [Overview](#1-overview) |
| 2 | [Batch Operating System](#2-batch-operating-system) |
| 3 | [Time-Sharing Operating System](#3-time-sharing-operating-system) |
| 4 | [Real-Time Operating System](#4-real-time-operating-system) |
| 5 | [Distributed Operating System](#5-distributed-operating-system) |
| 6 | [Network Operating System](#6-network-operating-system) |
| 7 | [Mobile Operating System](#7-mobile-operating-system) |
| 8 | [Comparison Table](#8-comparison-table) |
| 9 | [Interview Questions](#9-interview-questions) |
| 10 | [Resources](#10-resources) |

---

## 1. Overview

📌 Operating systems are classified based on how they manage processes, users, and time constraints.

- Different environments demand different OS designs
- No single OS type fits all use cases
- Real-world OS often combine characteristics of multiple types

![Types of OS Overview](../diagrams/os_types_overview.png)


> *Diagram: Classification tree showing all OS types branching from a central Operating System node*

---
```text
Operating System
│
├── Batch Operating System
├── Multiprogramming Operating System
├── Multitasking Operating System
├── Multiprocessing Operating System
├── Time-Sharing Operating System
├── Real-Time Operating System (RTOS)
├── Distributed Operating System
├── Network Operating System
└── Mobile Operating System
```

## 2. Batch Operating System

📌 Jobs are collected, grouped into batches, and executed **sequentially without user interaction** during execution.

- User submits jobs in advance via punched cards or job scripts
- OS operator groups similar jobs together to minimize setup time between jobs
- CPU processes one job at a time with no user involvement once execution starts
- User receives output only after the entire batch finishes

**Advantages:**
- High CPU utilization — no idle time between similar jobs
- Efficient for large, repetitive workloads

**Disadvantages:**
- Long turnaround time — user waits for entire batch to complete
- No interactivity — errors cannot be corrected mid-execution
- CPU sits idle when a job performs I/O operations

**Real-world use:** Payroll processing, bank statement generation, early IBM mainframes

---

## 3. Time-Sharing Operating System

📌 Multiple users share the CPU simultaneously — each user gets a **small time slice** in rapid rotation.

- Also called **Multitasking OS**
- Each user's time slice is so small that all users feel they have dedicated access
- Response time is kept very short — typically under one second
- Enables interactive computing where users can type commands and get immediate responses

**Advantages:**
- Fast response time for all users
- Better resource utilization compared to batch OS
- Supports multiple simultaneous users on one machine

**Disadvantages:**
- Security risks from shared environment
- Overhead from frequent context switching between users
- Performance degrades as number of users increases

**Real-world use:** Unix, Linux, all modern desktop and server operating systems

---

## 4. Real-Time Operating System

📌 Guarantees a **response within a strict, fixed time deadline** — missing the deadline is treated as a system failure.

- Used where timing is as important as correctness
- Two subtypes based on consequence of missing a deadline:

| Subtype | Deadline Miss Consequence | Example Use Case |
|---------|--------------------------|------------------|
| **Hard RTOS** | System failure — catastrophic | Airbag control, pacemaker, aircraft autopilot |
| **Soft RTOS** | Performance degradation — acceptable | Video streaming, online gaming, ATM machines |

**Advantages:**
- Predictable and deterministic behavior
- Maximum resource utilization within time constraints

**Disadvantages:**
- Complex and expensive to design
- Limited multitasking capability
- Difficult to debug and test exhaustively

**Real-world use:** FreeRTOS, VxWorks, QNX — used in embedded systems, robotics, aerospace, medical devices

---

## 5. Distributed Operating System

📌 Multiple physically separate computers connected by a network are managed **as a single coherent system**.

- Users interact with one unified system — they are unaware of which machine executes their task
- Workload is automatically distributed across nodes for load balancing
- If one node fails, others continue — provides **fault tolerance**

**Advantages:**
- High fault tolerance and availability
- Scalable — add more machines to increase capacity
- Efficient resource sharing across geographically distributed nodes

**Disadvantages:**
- Complex to design and implement
- Network failure can affect the entire system
- Data consistency and synchronization across nodes is challenging

**Real-world use:** Google's internal systems, Apache Hadoop clusters, Amoeba OS, Plan 9

---

## 6. Network Operating System

📌 OS that runs on a **server** and allows sharing of resources such as files and printers across a network.

- Each machine retains its own local OS
- Network OS adds features on top for controlled resource sharing
- Users are **aware** they are accessing remote resources — no location transparency

**Key difference from Distributed OS:**

| Feature | Network OS | Distributed OS |
|---------|-----------|----------------|
| User awareness | Knows it is accessing remote machine | Unaware of which machine runs the task |
| Location transparency | No | Yes |
| Coupling | Loosely coupled | Tightly coupled |

**Real-world use:** Windows Server, Novell NetWare, Linux as a file or print server

---

## 7. Mobile Operating System

📌 Designed specifically for mobile devices — optimized for **touch input, battery efficiency, and cellular connectivity**.

- Handles limited hardware constraints — smaller RAM, slower CPU, no cooling system
- Each app runs in a **sandbox** — cannot access other apps' data without explicit permission
- Manages aggressive power saving to extend battery life
- Integrates sensors — GPS, accelerometer, camera, fingerprint — directly into OS services

**Advantages:**
- Optimized for low power consumption
- Strong app isolation and security model
- Seamless hardware-software integration

**Disadvantages:**
- Limited multitasking compared to desktop OS
- Restricted filesystem access for user and apps
- Updates tied to device manufacturers causing fragmentation

**Real-world use:** Android, iOS, HarmonyOS

---

## 8. Comparison Table

| Type | User Interaction | Key Feature | Timing | Example |
|------|-----------------|-------------|--------|---------|
| Batch | None during execution | Job grouping, sequential processing | No constraint | IBM 1401, early mainframes |
| Time-Sharing | Interactive, real-time | Time slicing, multitasking | Soft | Unix, Linux, Windows |
| Hard Real-Time | Minimal or automated | Strict deadline guarantee | Hard | VxWorks, FreeRTOS |
| Soft Real-Time | Interactive | Best-effort deadline | Soft | Multimedia systems |
| Distributed | Transparent location | Multiple machines, one system | Varies | Hadoop, Google systems |
| Network | Aware of remote access | Shared resources over network | No constraint | Windows Server |
| Mobile | Touch, voice, sensors | Battery-optimized, sandboxed | Soft | Android, iOS |

---

## 9. Interview Questions

**Q1. What are the types of operating systems?**
- Batch, Time-Sharing, Real-Time, Distributed, Network, and Mobile OS
- Each is designed for a specific environment and set of requirements

**Q2. What is the difference between Batch OS and Time-Sharing OS?**
- Batch OS executes jobs sequentially with no user interaction during execution
- Time-Sharing OS allows multiple users to interact simultaneously via CPU time slicing

**Q3. What is the difference between Hard RTOS and Soft RTOS?**
- Hard RTOS — missing a deadline is a complete system failure, used in safety-critical systems like airbags and pacemakers
- Soft RTOS — missing a deadline causes degraded performance but not failure, used in streaming and gaming

**Q4. What is the difference between Distributed OS and Network OS?**
- Distributed OS provides full location transparency — users do not know which machine runs their task
- Network OS requires users to explicitly connect to and address remote machines by name

**Q5. Why are mobile OS different from desktop OS?**
- Mobile OS is built for touch input, battery constraints, cellular connectivity, and sensor integration
- App sandboxing is stricter, filesystem access is limited, and power management is deeply integrated into the OS design

**Q6. Give a real-world example of a Hard Real-Time OS.**
- The airbag deployment system in a car uses a Hard RTOS
- The system must detect a collision and trigger deployment within milliseconds
- Any delay beyond the deadline renders the airbag useless and is treated as a critical failure

---

## 10. Resources

- 📖 [GeeksforGeeks — Types of Operating Systems](https://www.geeksforgeeks.org/types-of-operating-systems/)
- 📖 [PrepInsta — Types of OS](https://prepinsta.com/operating-system/types-of-os/)
- 📖 [InterviewBit — OS Interview Questions](https://www.interviewbit.com/operating-system-interview-questions/)
- 📖 [Baeldung — OS Classification](https://www.baeldung.com/cs/os-intro)

---

*Made for CS Students | Internship & Job Prep Series*