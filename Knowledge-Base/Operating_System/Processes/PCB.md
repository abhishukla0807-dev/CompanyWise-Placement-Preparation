# Process Control Block

#### The Data Structure That Gives Every Process Its Identity in the OS

> A Process Control Block is a kernel data structure that stores all information the OS needs to manage, schedule, and restore a process.

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 1 | [What is a PCB](#1-what-is-a-pcb) |
| 2 | [✦ PCB Structure](#2--pcb-structure) |
| 3 | [✦ Fields of PCB](#3--fields-of-pcb) |
| 4 | [✦ PCB and Context Switching](#4--pcb-and-context-switching) |
| 5 | [✦ PCB and Process Scheduling](#5--pcb-and-process-scheduling) |
| 6 | [Role of PCB in Resource Management](#6-role-of-pcb-in-resource-management) |
| 7 | [Process Table](#7-process-table) |
| 8 | [Interview Questions](#8-interview-questions) |
| 9 | [Resources](#9-resources) |

---

## 1. What is a PCB

> A PCB is a unique data structure created by the OS for every process at the moment of its creation.

- Acts as the identity card of a process — the OS uses it to distinguish one process from another
- Stored in kernel memory — the process itself cannot access or modify its own PCB
- Created when a process is born and deleted after the process terminates and the parent reads its exit status
- Without PCB, the OS would have no way to track, schedule, or restore any process

![PCB in OS](https://scaler.com/topics/images/pcb-in-os.webp)
> *Image credit: [Scaler Topics — Process Control Block in OS](https://www.scaler.com/topics/operating-system/process-control-block-in-os/)*

---

## 2. ✦ PCB Structure

> The PCB is organized as a collection of fields, each storing a specific category of process information.

![Structure of Process Control Block](https://scaler.com/topics/images/structure-of-process-control-block.webp)
> *Image credit: [Scaler Topics — Process Control Block in OS](https://www.scaler.com/topics/operating-system/process-control-block-in-os/)*

```
┌──────────────────────────┐
│       Process ID         │
├──────────────────────────┤
│       Process State      │
├──────────────────────────┤
│      Process Priority    │
├──────────────────────────┤
│      Program Counter     │
├──────────────────────────┤
│       CPU Registers      │
├──────────────────────────┤
│   Memory Management Info │
├──────────────────────────┤
│    Accounting Information│
├──────────────────────────┤
│     List of Open Files   │
├──────────────────────────┤
│    I/O Status Information│
├──────────────────────────┤
│        PCB Pointer       │
└──────────────────────────┘
```

- PCBs are stored as a **linked list** in memory — each PCB has a pointer to the next PCB in the ready state
- The OS maintains a **process table** that holds references to all active PCBs

---

## 3. ✦ Fields of PCB

> Each field in the PCB serves a specific and critical purpose in process management.

**Process ID**
- Unique numeric identifier assigned by the OS at process creation
- Used to distinguish this process from all others in the system
- Process IDs are reused once a process terminates and its slot is freed
- The OS limits the maximum number of concurrent processes — IDs range from 0 to N-1

**Process State**
- Stores the current state of the process: New, Ready, Running, Waiting, or Terminated
- Updated by the OS every time a state transition occurs

**Process Priority**
- A numeric value representing scheduling priority
- Lower value means higher priority in most systems
- Assigned at creation time based on process type, age, or user specification
- Used by the CPU scheduler to decide which process runs next

**Program Counter**
- Holds the address of the next instruction to be executed by this process
- Saved into PCB during a context switch so execution can resume from the exact same point

**CPU Registers**
- Stores the current values of all CPU registers used by the process
- Includes accumulator, index registers, stack pointer, and general-purpose registers
- Saved and restored during every context switch

**Memory Management Information**
- Contains base and limit registers, page table pointers, or segment table details
- Defines the memory boundaries for this process
- Prevents the process from accessing memory outside its allocated space

**Accounting Information**
- Tracks resource usage throughout the process's lifetime
- Includes total CPU time consumed, real time elapsed, time limits, and job numbers
- Used for billing in shared systems and for performance analysis

**List of Open Files**
- Contains details of all files currently opened by the process
- Ensures the OS can close all open file handles when the process terminates
- Prevents file descriptor leaks

**I/O Status Information**
- Lists all I/O devices currently allocated to the process
- Tracks pending I/O requests and which devices the process is waiting on

**PCB Pointer**
- Stores the address of the next PCB in the linked list
- Helps the OS maintain hierarchical control between parent and child processes

---

## 4. ✦ PCB and Context Switching

> Every context switch relies entirely on the PCB to save and restore process state.

**Steps during a context switch:**

```
Process A running on CPU
       │
       │ Interrupt / Time Slice Expired
       ▼
Save Process A state into PCB-A
  - Program Counter
  - CPU Registers
  - Memory pointers
       │
       ▼
Load Process B state from PCB-B
  - Restore Program Counter
  - Restore CPU Registers
  - Restore Memory pointers
       │
       ▼
Process B resumes execution on CPU
```

- Without PCB, the OS would have no record of where Process A was in its execution
- Context switch overhead is the time spent saving and loading PCB fields — this is pure OS overhead with no useful work done
- Faster memory access for PCBs directly improves context switch performance

---

## 5. ✦ PCB and Process Scheduling

> The CPU scheduler consults the PCB of every process before making scheduling decisions.

- Scheduler reads **process priority** from PCB to decide which process runs next
- Scheduler reads **process state** to filter only Ready processes
- Scheduler reads **CPU burst time** and **accounting info** for algorithms like SJF and MLFQ
- After selecting a process, the dispatcher loads its state from its PCB onto the CPU

**Scheduling queues use PCB pointers:**
- Ready Queue — linked list of PCBs of all Ready processes
- Wait Queue — linked list of PCBs of all Waiting processes
- Moving a process between queues means updating PCB pointer links

---

## 6. Role of PCB in Resource Management

> PCB serves as the single source of truth for everything a process owns or is waiting for.

- **Resource Allocation** — tracks which memory segments, files, and I/O devices are assigned to the process
- **Resource Release** — on termination, OS reads the PCB to identify and free all held resources
- **Deadlock Detection** — OS scans PCBs to build the Resource Allocation Graph and detect circular waits
- **Memory Protection** — memory limits stored in PCB prevent the process from accessing addresses outside its space
- **Process Isolation** — each process has its own PCB with its own memory map — no two processes share a PCB

---

## 7. Process Table

> The process table is the OS-maintained index of all active PCBs in the system.

- A system-wide data structure stored in kernel memory
- Contains one entry per active process — each entry is a reference to that process's PCB
- OS consults the process table during context switches, scheduling, and resource allocation
- When a process terminates, its entry is removed from the process table and its PCB memory is freed

```
Process Table
┌────┬─────────────────────┐
│ ID │ Pointer to PCB      │
├────┼─────────────────────┤
│  0 │ → PCB of Process 0  │
│  1 │ → PCB of Process 1  │
│  2 │ → PCB of Process 2  │
│  … │ …                   │
└────┴─────────────────────┘
```

---

## 8. Interview Questions

**Q1. What is a Process Control Block?**
- A kernel data structure that stores all information about a process
- Created when a process is born, deleted when it terminates
- Contains process ID, state, priority, program counter, CPU registers, memory info, open files, and I/O status

**Q2. What information does a PCB contain?**
- Process ID, process state, process priority, program counter, CPU register values, memory management info, accounting information, list of open files, I/O status, and PCB pointer

**Q3. How does PCB help in context switching?**
- When a running process is preempted, its entire execution state is saved into its PCB
- When it is scheduled again, the OS restores its state from the PCB
- This allows the process to resume execution from the exact instruction where it was interrupted

**Q4. Where are PCBs stored?**
- In kernel memory — inaccessible to user processes
- Organized as a linked list where each PCB has a pointer to the next
- The OS maintains a process table with references to all active PCBs

**Q5. What happens to the PCB when a process terminates?**
- Process state in PCB is updated to Terminated
- All resources listed in the PCB are freed — memory, files, I/O devices
- PCB is deleted after the parent process reads the exit status
- The process table entry for this process is removed

**Q6. What is the difference between a process table and a PCB?**
- PCB is the data structure for one individual process containing all its details
- Process table is the system-wide index maintained by the OS that holds references to all active PCBs
- Process table is the directory; PCBs are the individual records

**Q7. How does PCB help in deadlock detection?**
- PCB stores which resources a process currently holds and which it is waiting for
- OS scans all PCBs to build a Resource Allocation Graph
- A cycle in this graph indicates a deadlock among the involved processes

---

## 9. Resources

- 📖 [Scaler Topics — Process Control Block in OS](https://www.scaler.com/topics/operating-system/process-control-block-in-os/)
- 📖 [GeeksforGeeks — Process Control Block](https://www.geeksforgeeks.org/process-table-and-process-control-block-pcb/)
- 📖 [InterviewBit — OS Interview Questions](https://www.interviewbit.com/operating-system-interview-questions/)
- 📖 [PrepInsta — PCB in OS](https://prepinsta.com/operating-system/)

---

*Made for CS Students | Internship & Job Prep Series*