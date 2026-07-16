# Process States

#### Lifecycle of a Process from Creation to Termination

> A process passes through a series of defined states during its lifetime. The OS transitions a process between states based on scheduling decisions and I/O events.

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 1 | [What are Process States](#1-what-are-process-states) |
| 2 | [✦ The Five States](#2--the-five-states) |
| 3 | [✦ State Transition Diagram](#3--state-transition-diagram) |
| 4 | [✦ State Transitions Explained](#4--state-transitions-explained) |
| 5 | [Seven State Model](#5-seven-state-model) |
| 6 | [Comparison Table](#6-comparison-table) |
| 7 | [Interview Questions](#7-interview-questions) |
| 8 | [Resources](#8-resources) |

---

## 1. What are Process States

> Process states represent the current condition of a process as it moves through its lifecycle.

- The OS tracks the state of every process in its PCB
- State changes are triggered by scheduling decisions, I/O requests, and I/O completions
- Only one process can be in the **Running** state per CPU core at any given time
- Understanding state transitions is essential for CPU scheduling and deadlock analysis

---

## 2. ✦ The Five States

> The standard process lifecycle model defines five distinct states.

| State | Description |
|-------|-------------|
| **New** | Process is being created by the OS |
| **Ready** | Process is in memory, waiting to be assigned to the CPU |
| **Running** | Process is actively executing instructions on the CPU |
| **Waiting** | Process is waiting for an I/O event or resource to become available |
| **Terminated** | Process has completed execution or has been killed |

- **New** and **Terminated** are transient states — a process spends very little time in them
- **Ready** and **Waiting** are queue states — multiple processes can be in these states simultaneously
- **Running** is exclusive — only one process per CPU core at any time

---

## 3. ✦ State Transition Diagram

> The diagram below shows all valid transitions between process states.

```
                    ┌─────────────┐
                    │     New     │
                    └──────┬──────┘
                           │ Admitted
                           ▼
                    ┌─────────────┐
            ┌──────►│    Ready    │◄──────────────┐
            │       └──────┬──────┘               │
            │              │ Dispatch             │
            │ Time         ▼                      │ I/O Complete
            │ Expired┌─────────────┐  I/O Request ┌─────────────┐
            └────────│   Running   │─────────────►│   Waiting   │
                     └──────┬──────┘              └─────────────┘
                            │ Exit
                            ▼
                     ┌─────────────┐
                     │  Terminated │
                     └─────────────┘
```

![Process State Diagram](../diagrams/process_state_diagram.png)
> *Diagram: Clean circular flow of all five process states with labeled transition arrows*

---

## 4. ✦ State Transitions Explained

> Each arrow in the diagram represents a specific event that triggers a state change.

**New → Ready**
- Triggered when the OS admits the process into the ready queue
- Process is loaded into memory and all initial resources are allocated
- Long-term scheduler makes this decision

**Ready → Running**
- Triggered when the short-term scheduler (dispatcher) selects this process for CPU execution
- Called **dispatch**
- The CPU registers are loaded with the process's saved state from its PCB

**Running → Ready**
- Triggered when the process's CPU time slice expires
- OS preempts the process and moves it back to the ready queue
- Process state is saved into its PCB before the switch

**Running → Waiting**
- Triggered when the process requests an I/O operation or waits for an event
- Process voluntarily gives up the CPU while waiting
- Example: reading from disk, waiting for network response, waiting for user input

**Waiting → Ready**
- Triggered when the I/O operation completes or the awaited event occurs
- Process does not go directly back to Running — it must wait in the Ready queue again
- I/O completion is signaled to the OS via an interrupt

**Running → Terminated**
- Triggered when the process finishes execution or is killed by the OS or user
- OS reclaims all resources held by the process
- PCB is removed after the parent reads the exit status

---

## 5. Seven State Model

> The seven state model extends the five state model by adding Suspended states to handle swapping.

```
                    ┌─────────────┐
                    │     New     │
                    └──────┬──────┘
                           │ Admitted
                           ▼
                    ┌─────────────┐     Suspend     ┌──────────────────┐
            ┌──────►│    Ready    │────────────────►│  Ready Suspended │
            │       └──────┬──────┘                 └────────┬─────────┘
            │              │ Dispatch                        │ Activate
            │ Time         ▼                                 ▼
            │ Expired┌─────────────┐  I/O Request  ┌─────────────┐
            └────────│   Running   │──────────────►│   Waiting   │
                     └──────┬──────┘               └──────┬──────┘
                            │ Exit                        │ Suspend
                            ▼                             ▼
                     ┌─────────────┐            ┌──────────────────┐
                     │  Terminated │            │ Blocked Suspended │
                     └─────────────┘            └──────────────────┘
```

**Ready Suspended**
- Process is swapped out of RAM to disk but is ready to run once swapped back in
- Medium-term scheduler handles this transition

**Blocked Suspended**
- Process is swapped out of RAM and is also waiting for an I/O event
- Must wait for both I/O completion and swap-back into memory before it can run

---

## 6. Comparison Table

| Transition | From | To | Trigger |
|-----------|------|----|---------|
| Admitted | New | Ready | OS allocates resources and loads process |
| Dispatch | Ready | Running | Scheduler selects process for CPU |
| Time Expired | Running | Ready | CPU time slice exhausted |
| I/O Request | Running | Waiting | Process requests I/O or waits for event |
| I/O Complete | Waiting | Ready | I/O finishes, signaled by interrupt |
| Exit | Running | Terminated | Process completes or is killed |

---

## 7. Interview Questions

**Q1. What are the states of a process?**
- New, Ready, Running, Waiting, and Terminated
- New — process being created
- Ready — waiting for CPU
- Running — executing on CPU
- Waiting — waiting for I/O or event
- Terminated — execution complete

**Q2. Can a process go directly from Waiting to Running?**
- No — a process always goes from Waiting to Ready first
- The scheduler then selects it from the Ready queue to move it to Running
- Direct Waiting to Running transition does not exist in the standard model

**Q3. How many processes can be in the Running state at once?**
- One per CPU core
- On a quad-core processor, a maximum of four processes can be Running simultaneously
- All other processes are in Ready or Waiting state

**Q4. What is the difference between Ready and Waiting state?**
- Ready — process has everything it needs and is only waiting for CPU time
- Waiting — process is blocked and cannot proceed until an external event like I/O completion occurs

**Q5. What triggers a Running to Ready transition?**
- Time slice expiration — the OS preempts the process when its allocated CPU time runs out
- Higher priority process arrives in the Ready queue in a preemptive scheduling system

**Q6. What is the seven state model?**
- Extends the five state model with two suspended states — Ready Suspended and Blocked Suspended
- Handles the case where the medium-term scheduler swaps processes out of RAM to disk
- A process in Ready Suspended is eligible to run but not currently in memory

**Q7. What happens to a process's state during a context switch?**
- The Running process is moved to Ready state
- Its full state — program counter, registers, memory pointers — is saved into its PCB
- The next scheduled process has its state restored from its PCB and moves to Running

---

## 8. Resources

- 📖 [GeeksforGeeks — Process States](https://www.geeksforgeeks.org/states-of-a-process-in-operating-systems/)
- 📖 [InterviewBit — OS Process Questions](https://www.interviewbit.com/operating-system-interview-questions/)
- 📖 [PrepInsta — Process States](https://prepinsta.com/operating-system/)
- 📖 [Baeldung — Process Lifecycle](https://www.baeldung.com/cs/os-intro)

---

*Made for CS Students | Internship & Job Prep Series*