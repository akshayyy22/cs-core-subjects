# Introduction to OS
---

## OS and Main Functions

- An **Operating System** is system software that manages hardware, runs application programs, and provides common services such as process management, memory management, file management, security, and I/O handling.[1][2]
- Example: Windows, Linux, macOS manage user logins, handle files, and enable multitasking by allocating CPU time.

### FAANG Interview Q&A
- Q: What is the primary role of an OS?
  - A: Acts as an intermediary between user and hardware, managing resources efficiently.[2][1]
- Q: Name three main functions of an OS.
  - A: Process management, memory management, and file management.[1]

### Edge Cases
- Deadlocks can occur if resources aren’t carefully managed.
- Improper memory management may lead to fragmentation or security vulnerabilities.[2]

***

## Process, Program, and Thread

- A **program** is a set of instructions; a **process** is a program in execution (runs independently); a **thread** is the smallest unit of execution within a process (shares resources with other threads in the same process).[3][4][5][6]
- Example: A web browser (process) opening multiple tabs (threads).

### FAANG Interview Q&A
- Q: Process vs. Thread?
  - A: Process runs independently with separate memory; threads share memory within a process and are lightweight.[6][3]
- Q: Why use threads?
  - A: For efficient multitasking, like background loading in apps.[3][6]

### Edge Cases
- Data corruption possible due to unsynchronized thread access.
- Shared memory in threads can cause race conditions.[5][3]

***

## Types of Operating Systems

- **Batch OS**: Processes batches of tasks without user interaction; e.g., payroll systems.[7][2]
- **Multiprogramming OS**: Multiple jobs share CPU to maximize utilization.[2]
- **Multitasking/Time-Sharing OS**: Tasks switch rapidly to provide responsiveness (e.g., UNIX).[8][2]
- **Multi-User OS**: Multiple users access simultaneously (e.g., mainframes).[2]
- **Distributed OS**: Multiple computers work together (e.g., cluster systems).[2]
- **Network OS**: Manages network resources (e.g., Windows Server).[2]
- **Real-Time OS**: Executes tasks within strict timing constraints (e.g., automotive systems).[7][2]

### FAANG Interview Q&A
- Q: Difference between multitasking and multiprogramming?
  - A: Multitasking focuses on tasks for a single user with rapid switching; multiprogramming maximizes CPU for multiple jobs.[2]
- Q: What is a real-time OS used for?
  - A: Systems requiring strict response times, like robotics or embedded devices.[7][2]

### Edge Cases
- Batch OS: Debugging is hard; one failure can block all jobs.[7]
- Real-time OS: Missing deadlines can cause system failure.[7]

***

## Batch OS

- Uses offline input and processes jobs in the order received; minimal user intervention (common in old banking systems).[9][7]
- Pros: High throughput, handles repetitive tasks efficiently.
- Cons: Hard to debug, can cause job backlog on failure.

### FAANG Interview Q&A
- Q: When would you use a batch OS?
  - A: For repetitive tasks like payroll or billing that don’t need user interaction.[7]

### Edge Case
- Input errors can halt all jobs until addressed.

***

## Multiprogramming and Multitasking OS

- **Multiprogramming**: Multiple programs in memory; OS switches between them for efficiency.
- **Multitasking**: Multiple tasks for single/multiple users; quick switching gives illusion tasks run in parallel.[8][2]

### FAANG Interview Q&A
- Q: Why is CPU utilization higher in multiprogramming OS?
  - A: CPU switches to another job on I/O wait, reducing idle time.[2]
- Q: Risk of multitasking OS?
  - A: Data corruption if user programs are not isolated.[7]

***

## Kernel and User Modes

- **Kernel mode**: OS runs with full hardware access, unrestricted operations.
- **User mode**: Applications run with limited access, increasing security and stability.[10]

### FAANG Interview Q&A
- Q: Why are two modes needed?
  - A: To protect the system by isolating user programs from sensitive instructions.[10]
- Q: What can happen if a process gains kernel mode?
  - A: It can override security, risking system compromise.[10]

***

## Process and Its States

- Process states: New, Ready, Running, Waiting, Terminated.
- State transitions handled by OS for scheduling and resource management.[2]

### FAANG Interview Q&A
- Q: When does a process enter the waiting state?
  - A: When waiting for I/O or resource.[2]
- Q: Role of PCB (Process Control Block)?
  - A: Stores process state, program counter, memory info, etc.[2]

***

## Normal Function Call vs System Calls in OS

- **Function call**: Executes code within application, no OS privilege required.
- **System call**: Interface for applications to request OS services (e.g., file I/O, process creation).[10]

### FAANG Interview Q&A
- Q: Why are system calls needed?
  - A: To safely request OS-level resources from user programs.[10]
- Q: Give an example of a system call.
  - A: `fork()` in UNIX creates a new process.[10]

### Edge Cases
- System calls can be slow due to user-to-kernel mode switch.
- Malformed system call arguments can crash the process.

***

## Frequently Asked Edge Cases

- Handling deadlocks and race conditions
- Context switching costs in process/thread design
- Securing system calls from malicious programs
- Synchronization in shared-memory multithreading

***

## References

1. [OS and Main Functions – TakeUForward](https://takeuforward.org/operating-system/os-and-main-functions)  
2. [Last Minute Notes – Operating Systems (GFG)](https://www.geeksforgeeks.org/operating-systems/last-minute-notes-operating-systems/)  
3. [Difference Between Process and Thread (GFG)](https://www.geeksforgeeks.org/operating-systems/difference-between-process-and-thread/)  
4. [Processes and Threads – Microsoft Docs](https://learn.microsoft.com/en-us/windows/win32/procthread/processes-and-threads)  
5. [Difference Between Process, Program, and Thread – TakeUForward](https://takeuforward.org/operating-system/difference-between-process-program-and-thread-different-types/)  
6. [Virtual Memory, Thrashing, and Threads – TakeUForward](https://takeuforward.org/operating-system/define-virtual-memory-thrashing-and-threads/)  
7. [Types of Operating Systems – Indeed](https://www.indeed.com/career-advice/career-development/types-of-operating-systems)  
8. [Types of Operating Systems – GFG](https://www.geeksforgeeks.org/operating-systems/types-of-operating-systems/)  
9. [Types of OS – StudyTonight](https://www.studytonight.com/operating-system/types-of-os)  
10. [Operating System – Wikipedia](https://en.wikipedia.org/wiki/Operating_system)  
11. [Purpose and Types of OS – TakeUForward](https://takeuforward.org/operating-system/what-is-main-purpose-of-operating-system-discuss-different-types/)  
12. [Different Types of OS and Real-Time OS – TakeUForward](https://takeuforward.org/operating-system/different-types-of-operating-systems-and-real-time-os/)  
13. [Functions of Operating System – Hero Vired](https://herovired.com/learning-hub/blogs/functions-of-operating-system/)  
14. [Types of Operating Systems – Scaler](https://www.scaler.com/topics/operating-system/types-of-operating-system/)  
15. [Processes and Threads in Android – Developer Docs](https://developer.android.com/guide/components/processes-and-threads)  
16. [Most Asked OS Interview Questions – TakeUForward](https://takeuforward.org/operating-system/most-asked-operating-system-interview-questions)  
17. [BCA II Sem – Operating Systems Notes (PDF)](https://sim.edu.in/wp-content/uploads/2018/11/BCA-II-SEM-OPERATING-SYSTEMS.pdf)  
18. [Types of Operating Systems – Hero Vired](https://herovired.com/learning-hub/blogs/types-of-operating-systems/)  
19. [Operating Systems Notes PDF – AITS TPT](https://aits-tpt.edu.in/wp-content/uploads/2022/06/Operating_System-min.pdf)  
20. [Processes and Threads – Workat.Tech](https://workat.tech/core-cs/tutorial/processes-and-threads-os-6iboki1s2y3t)  
