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

---

## 2. What is a socket, kernel, and monolithic kernel?  

**Socket:**  
A socket is like a door for data when two computers talk over a network.  

**Kernel:**  
The kernel is the core of an OS that manages hardware, memory, CPU, and communication between apps and hardware.  

**Monolithic Kernel:**  
All OS services run in the kernel space. It’s fast but complex.  
*Example:* Unix, Linux.

---

## 3. Difference between process, program, and thread  

**Process:**  
An instance of a running program.  

**Program:**  
A set of instructions to perform a task.  

**Thread:**  
A smaller unit inside a process that runs tasks in parallel.

---

## 4. Define virtual memory, thrashing, threads  

**Virtual Memory:**  
Extra memory on disk that acts like RAM so programs can be bigger than physical memory.  

**Thrashing:**  
When the computer keeps swapping pages instead of running programs → very slow.  

**Thread:**  
A single sequence of execution inside a process.

---

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

---

## 6. What is a deadlock? Necessary conditions  

**Deadlock:**  
When two or more processes wait for each other forever, none can continue.  

**Example:** Process A needs a resource held by B, and B needs a resource held by A → both stuck.  

**Necessary Conditions for Deadlock:**  
1. Mutual Exclusion  
2. Hold and Wait  
3. No Preemption  
4. Circular Wait
