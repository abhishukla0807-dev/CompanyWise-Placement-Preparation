# Context Switch

#### The Mechanism That Enables Multitasking on a Single CPU

> A context switch is the process of saving the state of a running process and loading the state of the next scheduled process so the CPU can switch between them seamlessly.

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 1 | [What is a Context Switch](#1-what-is-a-context-switch) |
| 2 | [✦ What Gets Saved and Restored](#2--what-gets-saved-and-restored) |
| 3 | [✦ Step-by-Step Process](#3--step-by-step-process) |
| 4 | [✦ Context Switch Triggers](#4--context-switch-triggers) |
| 5 | [✦ Context Switch Overhead](#5--context-switch-overhead) |
| 6 | [Context Switch vs Mode Switch](#6-context-switch-vs-mode-switch) |
| 7 | [Context Switch in Threads](#7-context-switch-in-threads) |
| 8 | [Interview Questions](#8-interview-questions) |
| 9 | [Resources](#9-resources) |

---

## 1. What is a Context Switch

> A context switch transfers CPU control from one process to another by saving and restoring execution state.

- Enables time-sharing — multiple processes share a single CPU by taking turns
- Performed entirely by the OS kernel — no user program involvement
- The saved state of a process is called its **context**
- Context is stored in the process's **PCB** and restored when the process runs again
- A context switch involves pure overhead — no useful work is done during the switch itself

---

## 2. ✦ What Gets Saved and Restored

> The complete execution context of a process must be preserved so it can resume exactly where it left off.

| Component | Description |
|-----------|-------------|
| **Program Counter** | Address of the next instruction to execute |
| **CPU Registers** | Accumulator, index, stack pointer, general-purpose registers |
| **Process State** | Current state — Running, Ready, or Waiting |
| **Memory Management Info** | Page table base register, segment pointers |
| **Stack Pointer** | Top of the current execution stack |
| **Open File Descriptors** | List of files currently open |
| **Scheduling Info** | Priority, remaining time slice, CPU time used |

- All of the above is stored in the PCB of the outgoing process
- The incoming process has its context loaded from its own PCB onto the CPU

---

## 3. ✦ Step-by-Step Process

> A context switch follows a strict sequence to ensure no execution state is lost.

```
┌─────────────────────────────────────────┐
│          Process A — Running            │
└──────────────────┬──────────────────────┘
                   │
                   │  Interrupt / Time Slice Expired
                   ▼
┌─────────────────────────────────────────┐
│   OS takes control (Kernel Mode)        │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│  Save Process A context into PCB-A      │
│  - Program Counter                      │
│  - CPU Registers                        │
│  - Stack Pointer                        │
│  - Memory pointers                      │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│  Scheduler selects Process B            │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│  Load Process B context from PCB-B      │
│  - Restore Program Counter              │
│  - Restore CPU Registers                │
│  - Restore Stack Pointer                │
│  - Restore Memory pointers              │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│          Process B — Running            │
└─────────────────────────────────────────┘
```

- Process A moves from Running to Ready or Waiting depending on the trigger
- Process B moves from Ready to Running
- The entire switch happens in kernel mode — user programs are unaware of the switch

---

## 4. ✦ Context Switch Triggers

> A context switch is initiated by one of four events.

**Time Slice Expiration**
- The running process exhausts its allocated CPU time quantum
- Timer interrupt fires — OS preempts the process and switches to the next in the ready queue
- Most common trigger in time-sharing systems

**I/O Request**
- The running process requests an I/O operation such as reading from disk or waiting for network data
- Process is moved to Waiting state and CPU is given to another ready process
- I/O completion later triggers an interrupt that moves the process back to Ready

**Higher Priority Process Arrives**
- A higher-priority process enters the Ready queue
- In preemptive scheduling, the OS immediately preempts the current process and runs the higher-priority one

**System Call or Interrupt**
- Process makes a system call that cannot be satisfied immediately
- Hardware interrupt requires OS attention
- OS handles the interrupt and may switch to a different process afterward

---

## 5. ✦ Context Switch Overhead

> Every context switch consumes CPU time without doing any productive work.

- Time spent saving PCB-A and loading PCB-B is pure overhead
- During this time the CPU executes no user instructions — throughput is lost
- Typical context switch time ranges from 1 to 100 microseconds depending on hardware
- High context switch frequency reduces overall system throughput

**Factors that increase overhead:**
- Large number of CPU registers to save and restore
- Complex memory management structures such as large page tables
- Cache invalidation — incoming process has different memory, causing cache misses
- TLB flush — Translation Lookaside Buffer must be cleared for the new process's address space

**How OS minimizes overhead:**
- Hardware support for fast register save and restore
- Thread-level context switches are cheaper than process-level switches since threads share the same address space
- Some architectures support hardware context switching directly

---

## 6. Context Switch vs Mode Switch

> These two are frequently confused but are fundamentally different operations.

| Feature | Context Switch | Mode Switch |
|---------|---------------|-------------|
| Definition | Switches CPU from one process to another | Switches CPU between user mode and kernel mode |
| PCB involved | Yes — saves and restores full process state | No — process remains the same |
| Process change | Yes | No |
| Cost | High — full state save and restore | Low — only privilege level changes |
| Trigger | Scheduler, interrupt, I/O request | System call, interrupt, exception |
| Example | Process A gives way to Process B | Process A calls `read()` — OS handles it, returns to Process A |

- A context switch always involves a mode switch first
- A mode switch does not always involve a context switch

---

## 7. Context Switch in Threads

> Thread context switches are significantly cheaper than process context switches.

**Process Context Switch**
- Different virtual address spaces — TLB must be flushed
- Page tables are different — memory management info must be fully replaced
- More expensive due to cache and TLB invalidation

**Thread Context Switch**
- Threads within the same process share the same address space
- No TLB flush required — memory mappings remain the same
- Only CPU registers and stack pointer need to be saved and restored
- Much faster than process-level context switching

```
Process Context Switch Cost  >>  Thread Context Switch Cost
```

- This is one of the primary reasons threads are preferred over processes for concurrent tasks

---

## 8. Interview Questions

**Q1. What is a context switch?**
- The process of saving the execution state of the currently running process into its PCB and loading the saved state of the next scheduled process from its PCB
- Enables multiple processes to share a single CPU through time-sharing

**Q2. What information is saved during a context switch?**
- Program counter, CPU registers, stack pointer, memory management info, process state, open file descriptors, and scheduling data
- All stored in the outgoing process's PCB

**Q3. Is a context switch useful work?**
- No — it is pure overhead
- During a context switch the CPU executes no user instructions
- Minimizing context switch time directly improves system throughput

**Q4. What triggers a context switch?**
- Time slice expiration, I/O request by the running process, arrival of a higher-priority process, or a system call or hardware interrupt that cannot be satisfied immediately

**Q5. What is the difference between a context switch and a mode switch?**
- A mode switch changes the CPU privilege level between user mode and kernel mode without changing the running process
- A context switch changes the running process entirely and always involves a mode switch as part of it

**Q6. Why is a thread context switch cheaper than a process context switch?**
- Threads within the same process share the same address space
- No TLB flush or page table replacement is needed
- Only registers and the stack pointer need to be saved and restored

**Q7. What role does the PCB play in a context switch?**
- PCB is the storage location for the entire execution context of a process
- On switch-out: current process state is written into its PCB
- On switch-in: next process state is read from its PCB and loaded onto the CPU
- Without PCB, context switching would be impossible

---

## 9. Resources

- 📖 [GeeksforGeeks — Context Switching in OS](https://www.geeksforgeeks.org/context-switch-in-operating-system/)
- 📖 [InterviewBit — OS Interview Questions](https://www.interviewbit.com/operating-system-interview-questions/)
- 📖 [PrepInsta — OS Context Switch](https://prepinsta.com/operating-system/)
- 📖 [Baeldung — Context Switching](https://www.baeldung.com/cs/os-context-switching)

---

*Made for CS Students | Internship & Job Prep Series*