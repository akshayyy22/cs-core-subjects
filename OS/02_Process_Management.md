
## Process Scheduling Algorithms (Preemptive & Non-Preemptive)

- **Preemptive:** OS can interrupt and switch out a running process (e.g., Round Robin, SRTF); responsive but more overhead.
- **Non-Preemptive:** Once running, process holds CPU until it finishes/blocks (e.g., FCFS, SJF); simpler, but less flexible.[1][2]

### Interview Q&A
- Q: Difference between preemptive and non-preemptive scheduling?
  - A: Preemptive allows interruption of processes; non-preemptive runs to completion without interruption.[2]
- Q: Example of preemptive scheduling?
  - A: Round Robin.[1][2]

### Tricky Edge Cases
- Low-priority processes can starve if high-priority ones keep arriving.[2]

***

## Scheduling Algorithms: FCFS, SJF, SRTF, HRNN, RR, PBS, MLQ, MLFQ

- **FCFS:** Simple, non-preemptive; processes served in arrival order—high wait time possible.[3][4]
- **SJF:** Picks shortest job next; optimal average waiting time but tough to predict burst time.[5][4]
- **SRTF:** Preemptive SJF; switches if a shorter new job arrives.[6][7]
- **HRNN:** Highest Response Ratio Next; balances waiting and service time for fairness.[6]
- **RR:** Preemptive, circular queue with time quantum—excellent for timesharing systems.[8][6]
- **PBS:** Priority-based, can be preemptive (interrupt lower-priority) or non-preemptive.[9][6]
- **MLQ/MLFQ:** Multilevel (Feedback) Queues partition jobs by type/priority or history; jobs migrate among queues for fairness/adaptiveness.[10][6]

### Interview Q&A
- Q: When does SJF give the best performance?
  - A: When job lengths are known and predictable; gives minimum average waiting time.[5]
- Q: How does RR prevent starvation?
  - A: By regularly cycling through all processes—ensuring each process is served.[8]

### Tricky Edge Cases
- SJF/SRTF can cause starvation for long/low-priority jobs—aged jobs risk never running.[11][12]

***

## Starving and Aging

- **Starvation:** A process waits indefinitely (often in priority scheduling) because it’s always bypassed for higher-priority ones.[13][12]
- **Aging:** Increases waiting process’s priority over time, so starving jobs eventually run.[12][11]

### Interview Q&A
- Q: How does aging prevent starvation?
  - A: Gradually increases a waiting process’s priority, so it is eventually scheduled.[11][12]

### Tricky Edge Case
- Without aging, important background tasks may never execute.[12]

***

## Producer-Consumer Problem

- Classic synchronization issue: Producers add, consumers remove items from a finite buffer—must avoid buffer under/overflows.[14][15]
- Requires mutual exclusion to prevent race conditions.

### Interview Q&A
- Q: What tools solve the producer-consumer problem?
  - A: Semaphores or mutexes ensure safe buffer access.[15][14]

### Tricky Edge Cases
- Overfilling or emptying the buffer (violating resource bounds) causes deadlock or data corruption.[15]

***

## Critical Section Problem

- Deals with safely sharing resources among concurrent processes.
- Requires: Mutual exclusion, progress, and bounded waiting.[16][17]

### Interview Q&A
- Q: Key properties of critical section solutions?
  - A: Mutual exclusion, progress, bounded waiting.[17][16]

### Tricky Edge Case
- Poorly designed entry section leads to deadlocks or starvation.

***

## Process Synchronization and Its Tools

- Means coordinating execution to avoid race conditions and ensure data consistency.
- Tools: Semaphores, mutexes, condition variables, monitors.[18][19]

### Interview Q&A
- Q: Difference between mutex and semaphore?
  - A: Mutex is binary (lock/unlock); semaphore is counting, tracks resource count.[20][21]

### Tricky Edge Cases
- Using weak/naive semaphores can still allow starvation or priority inversion.[20]

***

## Semaphores and Its Types

- **Counting Semaphore:** Integer value—tracks resource count.
- **Binary Semaphore (Mutex):** 0 or 1—ensures exclusive access.[21][20]
- **Strong Semaphore:** Fair FIFO wakeup of waiters; **Weak Semaphore:** Arbitrary order (risk starvation).[20]

### Interview Q&A
- Q: Where are binary semaphores used?
  - A: To protect critical sections—guarantee only one process enters at a time.[20]

### Tricky Edge Case
- Poor handling can deadlock the entire system (if signal never occurs).

***

## Deadlock and Methods for Preventing Deadlock

- **Deadlock:** Multiple processes block each other by each holding and waiting for resources.
- **Prevention:** Remove at least one of 4 necessary conditions (mutual exclusion, hold-and-wait, no preemption, circular wait).[22][23][24]
- **Avoidance:** Dynamically ensure system stays in a "safe state" (e.g., Banker's Algorithm).[23][22]
- **Detection/Recovery:** Allow deadlock, periodically detect and recover.[25][22]

### Interview Q&A
- Q: Four necessary conditions for deadlock?
  - A: Mutual exclusion, hold and wait, no preemption, circular wait.[24]
- Q: What is deadlock avoidance?
  - A: Dynamically checks resource requests to ensure they don't lead to deadlock (e.g., Banker's Algorithm).[22][23]

### Tricky Edge Cases
- Aggressive prevention can reduce resource utilization/throughput.

***

## Banker's Algorithm

- Ensures safe resource allocation by simulating each grant to check for possible deadlock.
- Uses `Available`, `Max`, `Allocation`, `Need` matrices.[26][27][28]
- Only grants requests that leave the system in a safe state.

### Interview Q&A
- Q: What does a "safe state" mean?
  - A: At least one process execution sequence exists where all can complete without deadlock.[28]
- Q: Why is it called Banker's Algorithm?
  - A: Like a bank lending without exceeding reserves, always keeps the system "solvent" (safe).[26]

### Tricky Edge Case
- Requires advance knowledge of max resource needs; overestimation reduces concurrency, underestimation risks deadlock.[27][26]

***

# References

## 🔹 Process Scheduling
1. [Preemptive vs Non-Preemptive Scheduling – TakeUForward](https://takeuforward.org/operating-system/process-scheduling-preemptive-and-non-preemptive)  
2. [Preemptive and Non-Preemptive Scheduling – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/preemptive-and-non-preemptive-scheduling/)  
3. [FCFS Scheduling – TakeUForward](https://takeuforward.org/operating-system/fcfs-scheduling-explained/)  
4. [Scheduling Algorithms – Tutorialspoint](https://www.tutorialspoint.com/operating_system/os_process_scheduling_algorithms.htm)  
5. [SJF Scheduling – TakeUForward](https://takeuforward.org/operating-system/sjf-scheduling-explained/)  
6. [CPU Scheduling Algorithms Overview – TakeUForward](https://takeuforward.org/operating-system/scheduling-algorithms)  
7. [SRTF Scheduling – TakeUForward](https://takeuforward.org/operating-system/srtf-scheduling-explained/)  
8. [Round Robin Scheduling – TakeUForward](https://takeuforward.org/operating-system/round-robin-scheduling-explained/)  
9. [Priority Scheduling – TakeUForward](https://takeuforward.org/operating-system/priority-scheduling/)  
10. [Multilevel Queue Scheduling – DrBTaneja](https://drbtaneja.com/multilevel-queue-mlq-scheduling/)  
29. [Types of Scheduling – Baeldung](https://www.baeldung.com/cs/scheduling-types)  
30. [CPU Scheduling Algorithms – NotesJam](https://notesjam.com/cpu-scheduling-algorithms/)  
31. [Multilevel Feedback Queue (MLFQ) Scheduling – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/multilevel-feedback-queue-scheduling-mlfq-cpu-scheduling/)  
33. [Scheduling Algorithm PDF – NotesJam](https://www.vbspu.ac.in/e-content/Scheduling-Algorithm.pdf)  

---

## 🔹 Starvation & Aging
11. [Starvation & Aging – AfterAcademy](https://afteracademy.com/blog/what-is-starvation-and-aging)  
12. [Starvation & Aging – TakeUForward](https://takeuforward.org/operating-system/starving-aging)  
13. [Starvation & Aging – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/starvation-and-aging-in-operating-systems/)  
32. [Starvation & Aging – Scaler](https://www.scaler.com/topics/operating-system/starvation-and-aging-in-os/)  
34. [Starvation & Aging – NotesJam](https://notesjam.com/starvation-and-aging-os/)  
35. [Starvation & Aging (Video)](https://www.youtube.com/watch?v=zFnrUVqtiOY)  

---

## 🔹 Process Synchronization
14. [Producer-Consumer Problem – TakeUForward](https://takeuforward.org/operating-system/producer-consumer-problem/)  
15. [Producer-Consumer – TakeUForward](https://takeuforward.org/operating-system/producer-consumer)  
16. [Critical Section – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/critical-section-in-synchronization/)  
17. [Critical Section Problem – Dev.to](https://dev.to/harshm03/critical-section-problem-process-synchronization-310d)  
18. [Process Synchronization & Tools – TakeUForward](https://takeuforward.org/operating-system/process-synchronisation-and-its-tools)  
19. [Process Synchronization – Scaler](https://www.scaler.com/topics/operating-system/process-synchronization-in-os/)  
36. [Producer-Consumer Problem – Dev.to](https://dev.to/harshm03/producer-consumer-problem-process-synchronisation-5glh)  
37. [Producer-Consumer Problem in Java – FreeCodeCamp](https://www.freecodecamp.org/news/java-multithreading-producer-consumer-problem/)  
38. [Producer-Consumer Problem – Scaler](https://www.scaler.com/topics/operating-system/producer-consumer-problem-in-os/)  
39. [Producer-Consumer Problem – Oracle Docs](https://docs.oracle.com/cd/E19253-01/816-5137/6mba5vq4p/index.html)  
40. [Semaphores in Java – TechVidvan](https://techvidvan.com/tutorials/semaphore-in-java/)  
41. [Producer–Consumer Problem – Wikipedia](https://en.wikipedia.org/wiki/Producer%E2%80%93consumer_problem)  
42. [Producer-Consumer Problem (Video)](https://www.youtube.com/watch?v=QxXez-kiLf0)  
43. [Producer-Consumer with Queues – HeyCoach](https://heycoach.in/blog/solving-the-producer-consumer-problem-with-queues/)  
45. [Producer-Consumer in Java – Baeldung](https://www.baeldung.com/java-producer-consumer-problem)  
48. [Critical Section Notes – Scribd](https://www.scribd.com/document/835345904/Process-Synchronization-and-Critical-Section-Problem)  
52. [Process Synchronization (Slideshare)](https://www.slideshare.net/slideshow/process-synchronization-in-operating-systems/53791801)  
53. [Process Synchronization (Video)](https://www.youtube.com/watch?v=pPM9Ajqmy_4)  

---

## 🔹 Semaphores
20. [Semaphores & Types – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/semaphores-and-its-types/)  
21. [Semaphore in OS – Scaler](https://www.scaler.com/topics/operating-system/semaphore-in-os/)  

---

## 🔹 Deadlocks
22. [Deadlock in Concurrent Systems – TakeUForward](https://takeuforward.org/operating-system/deadlock-in-concurrent-systems)  
23. [Deadlock Prevention – Scaler](https://www.scaler.com/topics/operating-system/deadlock-prevention-in-operating-system/)  
24. [Deadlock Prevention & Avoidance – INFLIBNET](https://ebooks.inflibnet.ac.in/csp3/chapter/deadlocks-prevention-avoidance/)  
25. [Deadlock Detection & Recovery – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/deadlock-detection-recovery/)  
26. [Banker’s Algorithm – Hackerearth](https://www.hackerearth.com/blog/dijkstras-bankers-algorithm-detailed-explaination)  
27. [Banker’s Algorithm Notes – Studocu](https://www.studocu.com/in/document/kannur-university/computer-science/banker-algorithm-notes-c4/49595425)  
28. [Banker’s Algorithm – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/bankers-algorithm-in-operating-system-2/)  
49. [Deadlock Prevention – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/deadlock-prevention/)  
50. [Deadlock Avoidance – HeroVired](https://herovired.com/learning-hub/blogs/deadlock-avoidance-in-os/)  
51. [Deadlock Avoidance – StudyTonight](https://www.studytonight.com/operating-system/deadlock-avoidance-in-operating-system)  
54. [Banker’s Algorithm – StudyTonight](https://www.studytonight.com/operating-system/bankers-algorithm)  
56. [Deadlock Avoidance (Slideshare)](https://www.slideshare.net/slideshow/deadlock-avoidance-os/250953500)  
57. [Banker’s Algorithm – Scaler](https://www.scaler.com/topics/bankers-algorithm-in-os/)  
58. [Deadlocks PPT – TXState](https://userweb.cs.txstate.edu/~xc10/ad-os/Deadlocks.ppt)  

---

## 🔹 Interview Prep
44. [Must-Do OS/DBMS/CN Questions – TakeUForward](https://takeuforward.org/interviews/must-do-questions-for-dbms-cn-os-interviews-sde-core-sheet/)  
46. [Most Asked OS Interview Questions – TakeUForward](https://takeuforward.org/operating-system/most-asked-operating-system-interview-questions)  
47. [OS Interview Questions (Video)](https://www.youtube.com/watch?v=XDIOC2EY5JE)  
55. [Operating System Full Course – TakeUForward](https://takeuforward.org/plus/course-details/operating-system)  
