# Operating System Question Bank

## 1. What is the main purpose of an operating system? Discuss different types.  
**Answer:**  
An OS manages computer hardware and software, handles memory, processes, files, devices, and security. It allows us to use the computer without knowing machine language.  

**Types of Operating Systems:**  
1. Batch OS  
2. Distributed OS  
3. Multitasking OS  
4. Network OS  
5. Real-Time OS  
6. Mobile OS  


## 2. What is a socket, kernel, and monolithic kernel?  

**Socket:**  
A socket is like a door for data when two computers talk over a network.  

**Kernel:**  
The kernel is the core of an OS that manages hardware, memory, CPU, and communication between apps and hardware.  

**Monolithic Kernel:**  
All OS services run in the kernel space. It’s fast but complex.  
*Example:* Unix, Linux.


## 3. Difference between process, program, and thread  

**Process:**  
An instance of a running program.  

**Program:**  
A set of instructions to perform a task.  

**Thread:**  
A smaller unit inside a process that runs tasks in parallel.


## 4. Define virtual memory, thrashing, threads  

**Virtual Memory:**  
Extra memory on disk that acts like RAM so programs can be bigger than physical memory.  

**Thrashing:**  
When the computer keeps swapping pages instead of running programs → very slow.  

**Thread:**  
A single sequence of execution inside a process.


## 5. What is RAID? Different types  

**RAID (Redundant Array of Independent Disks):**  
Using multiple disks together to:  
1. Increase speed (performance)  
2. Protect data (redundancy) in case one disk fails  

**Types of RAID:**  
- RAID 0 (Striping)  
- RAID 1 (Mirroring)  
- RAID 5 (Striping with Parity)  
- RAID 6 (Double Parity)  
- RAID 10 (Combination of 1 and 0)


## 6. What is a deadlock? Necessary conditions  

**Deadlock:**  
When two or more processes wait for each other forever, none can continue.  

**Example:** Process A needs a resource held by B, and B needs a resource held by A → both stuck.  

**Necessary Conditions for Deadlock:**  
1. Mutual Exclusion  
2. Hold and Wait  
3. No Preemption  
4. Circular Wait


## 6. Fragmentation

**Definition:**  
Fragmentation occurs when processes are loaded and removed from memory, leaving small unused spaces that are too small to hold new processes. This results in inefficient memory usage.

**Example: Think of it like a bookshelf: if you keep putting and removing books of different sizes, you’ll end up with gaps that are too small for new books.**

**Types of Fragmentation:**

1. **Internal Fragmentation:**  
   - Memory allocated is **larger than required** by the process.  
   - Wasted memory exists **inside the allocated block**.  
   - **Example:** Process needs 18 KB, system allocates 20 KB → 2 KB wasted.

2. **External Fragmentation:**  
   - Free memory is **scattered into small chunks**.  
   - Even if total free memory is enough, **no single chunk can fit the process**.  
   - **Example:** 3 free blocks of 5 KB each, but a process needs 12 KB → cannot fit.


## 7. Spooling

**Definition:**  
SPOOL = **Simultaneous Peripheral Operations OnLine**  
Spooling temporarily stores data for devices to process later, so the CPU doesn't wait for slow I/O operations.

**Key Points:**  
- CPU continues working without waiting for devices like printers.  
- Tasks are executed one by one from the queue.  

**Example:** Printing documents stored in a print queue, CPU continues other operations.


## 8. Semaphore

**Think of it as a traffic signal for processes.**

Controls how many processes can access a resource at the same time.

Counting semaphore: lets multiple processes in (like multiple cars allowed on a bridge).

Binary semaphore: only 0 or 1, acts like a lock (only one car can pass at a time).

**Mutex**

Short for Mutual Exclusion.

**Like a key to a locked room. Only one process can hold the key and enter at a time.**

Prevents two processes from using the same resource simultaneously.

Difference from Binary Semaphore:

Mutex is owned by the process that locks it; only that process can unlock.

Binary semaphore any process can signal to unlock.

## 10. Belady’s Anomaly

Usually, giving more memory should reduce page faults.

**But sometimes, more memory can actually increase page faults → that’s Belady’s Anomaly.**

Fix: Use smart algorithms like LRU or Optimal Replacement to avoid it.


## 11. Starvation (Starving)

When a low-priority process keeps waiting for CPU because high-priority processes always get the chance first.
It waits forever and does not get executed.

Simple example:
If a teacher always checks toppers’ papers first and keeps ignoring lower-rank students → lower ones starve.

**Aging (Solution to Starvation)**

Aging slowly increases the priority of a waiting process.
So even a low-priority process will eventually become high priority and get executed.

Example:
A student waiting long gets extra marks over time → teacher checks their paper soon.

## 12. Why does Thrashing occur?

Thrashing happens when the CPU spends more time swapping pages between RAM and disk than executing processes.

It occurs due to:

Too many processes in memory → high multiprogramming.

Too few frames/page allocation → continuous page faults.

Simple idea:
Like opening too many apps on a phone with low RAM – phone hangs and keeps loading screens.

## 13. Paging

A technique in which memory is divided into fixed-size blocks called pages.
Pages of a single program need not be stored together (non-contiguous).

Why we need paging?
It reduces memory wastage and allows a process to fit anywhere in RAM, not necessarily in one big block.

Simple example:
You can keep book pages in different shelves instead of one long shelf.

## 14. Demand Paging

Pages are loaded into RAM only when they are needed, not all at once.

Simple example:
You don't bring all books to the table.
You bring a book only when you need it.

**Segmentation**

Memory is divided into variable-sized segments, each storing related information (code, data, stack etc.).

Each segment has:

Base → starting address

Limit → size/length of the segment

Simple example:
A book has chapters of different sizes → each chapter is a segment.


## 15. Real Time Operating System (RTOS)

A **Real Time Operating System (RTOS)** is an operating system that must respond within a fixed and guaranteed time.  
It is used in time-critical systems like medical devices, robots, aircraft control etc.

## Types of RTOS

| Type | Explanation (Simple) | Examples |
|---|---|---|
| **Hard RTOS** | Deadline missed = system fails. No delay allowed. | Pacemakers, Airbag systems |
| **Firm RTOS** | Delay acceptable rarely. Missing deadline reduces quality. | Industrial automation |
| **Soft RTOS** | Small delays allowed, not harmful. | Multimedia, Gaming |


# 16. Difference Between Main Memory & Secondary Memory

| Main Memory (Primary) | Secondary Memory (Storage) |
|---|---|
| Very Fast | Slower than RAM |
| Temporary / Volatile | Permanent / Non-Volatile |
| Data lost after power off | Data remains after power off |
| Directly used by CPU | Used for long-term storage |
| Examples: RAM, Cache | Examples: HDD, SSD, Pendrive |

# Static Binding vs Dynamic Binding

| Static Binding | Dynamic Binding |
|---|---|
| Happens at **compile time** | Happens at **run time** |
| Faster execution | Slower execution |
| Less flexible | More flexible |
| Example: Function Overloading | Example: Function Overriding |

# 17. CPU Scheduling Algorithms – Simple Words

| Algorithm | Meaning |
|---|---|
| **FCFS (First Come First Serve)** | Process that arrives first gets CPU first. |
| **SJF (Shortest Job First)** | Process with smallest execution time runs first. |
| **SRTF (Shortest Remaining Time First)** | New shorter task can interrupt running process (preemptive SJF). |
| **LRTF (Longest Remaining Time First)** | Opposite of SRTF. Longest job given CPU first. |
| **Priority Scheduling** | CPU given to process with highest priority. |
| **Round Robin** | Each process gets fixed CPU time slice (fair rotation). |

