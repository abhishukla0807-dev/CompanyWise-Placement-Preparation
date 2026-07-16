# Process

#### The Fundamental Unit of Execution in an Operating System

> A process is a program in execution. It is the basic unit the OS manages, schedules, and controls during system operation.

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 1 | [What is a Process](#1-what-is-a-process) |
| 2 | [Program vs Process](#2-program-vs-process) |
| 3 | [✦ Process in Memory](#3--process-in-memory) |
| 4 | [✦ Process Components](#4--process-components) |
| 5 | [✦ Process States](#5--process-states) |
| 6 | [✦ Process Control Block](#6--process-control-block) |
| 7 | [✦ Process Scheduling](#7--process-scheduling) |
| 8 | [Types of Processes](#8-types-of-processes) |
| 9 | [Interview Questions](#9-interview-questions) |
| 10 | [Resources](#10-resources) |

---

## 1. What is a Process

> A process is an active instance of a program currently being executed by the CPU.

- A program becomes a process the moment it is loaded into memory and starts executing
- The OS creates, manages, schedules, and terminates processes
- Multiple processes can run concurrently on a single CPU via time-sharing
- Each process operates in its own isolated memory space — it cannot access another process's memory directly
- The OS tracks every process using a data structure called the **Process Control Block**

---

## 2. Program vs Process

> A program is a passive entity stored on disk. A process is an active entity executing in memory.

| Feature | Program | Process |
|---------|---------|---------|
| Nature | Passive | Active |
| Location | Stored on disk | Loaded in RAM |
| Existence | Permanent until deleted | Temporary, exists during execution |
| Resources | Needs none | Needs CPU, memory, I/O |
| Instances | One copy on disk | Multiple processes can run from one program |
| Example | `chrome.exe` on disk | Chrome window open and running |

- One program can spawn multiple processes simultaneously
- Example: Opening three Chrome windows creates three separate processes from the same program

---

## 3. ✦ Process in Memory

> Every process is given its own dedicated memory layout divided into four segments.

```
High Address
┌─────────────────┐
│      Stack      │  ← Function calls, local variables, return addresses
├─────────────────┤
│       ↓         │  Stack grows downward
│                 │
│       ↑         │  Heap grows upward
├─────────────────┤
│      Heap       │  ← Dynamic memory allocation (malloc, new)
├─────────────────┤
│      Data       │  ← Global and static variables
├─────────────────┤
│      Text       │  ← Compiled program code (read-only)
└─────────────────┘
Low Address
```

![Process Memory Layout](../diagrams/process_memory_layout.png)
> *Diagram: Visual of the four memory segments with Stack and Heap growing toward each other*

- **Text segment** — compiled machine code of the program, read-only
- **Data segment** — initialized and uninitialized global and static variables
- **Heap** — dynamically allocated memory at runtime, grows upward
- **Stack** — function call frames, local variables, return addresses, grows downward
- Stack and Heap grow toward each other — a stack overflow occurs when they collide

---

## 4. ✦ Process Components

> A process consists of more than just its code — it carries full execution context.

- **Program Code** — the instructions being executed
- **Program Counter** — holds address of the next instruction to execute
- **CPU Registers** — current values of all processor registers
- **Stack** — stores function calls and local variables
- **Heap** — dynamically allocated memory during runtime
- **Open File Table** — list of files currently opened by the process
- **Process ID** — unique identifier assigned by the OS
- **Priority** — scheduling priority used by the CPU scheduler
- **I/O Status** — list of I/O devices allocated to or requested by the process

---

## 5. ✦ Process States

> A process moves through defined states during its lifetime — from creation to termination.

```
New → Ready → Running → Terminated
                ↕
             Waiting
```

| State | Description |
|-------|-------------|
| **New** | Process is being created |
| **Ready** | Process is loaded in memory and waiting for CPU |
| **Running** | Process is actively executing on CPU |
| **Waiting** | Process is waiting for I/O or an event to complete |
| **Terminated** | Process has finished execution |

- Only one process can be in the **Running** state per CPU core at any time
- A process moves from Running to Waiting when it requests I/O
- A process moves from Waiting to Ready when I/O completes
- A process moves from Running to Ready when its time slice expires

---

## 6. ✦ Process Control Block

> The PCB is the OS data structure that stores all information about a process.

- Created by the OS when a new process is created
- Stored in kernel memory — inaccessible to the process itself
- Contains everything the OS needs to manage, schedule, and restore a process

**PCB contains:**
- Process ID and parent process ID
- Process state
- Program counter
- CPU register values
- Memory management information
- List of open files
- I/O status and device allocations
- Scheduling priority and CPU time used

- During a **context switch**, the OS saves the current process's state into its PCB and loads the next process's PCB

---

## 7. ✦ Process Scheduling

> The OS uses scheduling to decide which process runs on the CPU at any given time.

- **Long-term scheduler** — decides which processes are admitted into the ready queue from the job pool
- **Short-term scheduler** — decides which ready process gets the CPU next, runs very frequently
- **Medium-term scheduler** — handles swapping — moves processes between RAM and disk

**Scheduling queues:**
- **Job Queue** — all processes in the system
- **Ready Queue** — processes in memory waiting for CPU
- **Wait Queue** — processes waiting for I/O or an event

---

## 8. Types of Processes

> Processes are classified based on their resource usage and behavior.

**CPU-Bound Process**
- Spends most of its time performing computations
- Rarely waits for I/O
- Example: video encoding, scientific simulations, matrix multiplication

**I/O-Bound Process**
- Spends most of its time waiting for I/O operations to complete
- Rarely uses CPU for long stretches
- Example: file copy, database queries, web servers

**Independent Process**
- Does not share data with any other process
- Execution is not affected by other processes
- Example: running a calculator app

**Cooperating Process**
- Shares data or communicates with other processes
- Requires synchronization to avoid race conditions
- Example: producer-consumer pipelines, multi-process web servers

---

## 9. Interview Questions

**Q1. What is a process?**
- An active instance of a program in execution
- Includes program code, current activity, stack, heap, and OS resources like open files and I/O devices

**Q2. What is the difference between a program and a process?**
- A program is a passive set of instructions stored on disk
- A process is an active entity in memory with allocated CPU, RAM, and I/O resources
- One program can give rise to multiple processes simultaneously

**Q3. What are the segments of process memory?**
- Text — compiled program code, read-only
- Data — global and static variables
- Heap — dynamically allocated memory, grows upward
- Stack — function calls and local variables, grows downward

**Q4. What is a PCB?**
- Process Control Block — OS data structure holding all information about a process
- Contains process ID, state, program counter, register values, memory info, open files, and scheduling data
- Saved and restored during every context switch

**Q5. What is the difference between CPU-bound and I/O-bound processes?**
- CPU-bound processes spend most time computing — example is video encoding
- I/O-bound processes spend most time waiting for I/O — example is file copy or database read

**Q6. Can two processes run the same program?**
- Yes — multiple processes can be created from a single program
- Each gets its own separate memory space, PCB, and resources
- Example: opening multiple instances of a text editor

**Q7. What happens when a process terminates?**
- OS reclaims all resources allocated to the process — CPU, memory, open files, I/O devices
- PCB is deleted after the parent process reads the exit status
- Child processes without a parent become orphan processes and are adopted by Init

---

## 10. Resources

- 📖 [GeeksforGeeks — Process in OS](https://www.geeksforgeeks.org/introduction-of-process-management/)
- 📖 [InterviewBit — OS Process Questions](https://www.interviewbit.com/operating-system-interview-questions/)
- 📖 [PrepInsta — OS Process](https://prepinsta.com/operating-system/)
- 📖 [Baeldung — OS Process Concepts](https://www.baeldung.com/cs/os-intro)

---

*Made for CS Students | Internship & Job Prep Series*