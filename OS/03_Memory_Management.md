# Memory Management




### Memory Management Techniques (First Fit, Best Fit, Worst Fit)

- **First Fit:** Allocates the first free memory block large enough for the process—fast but can cause external fragmentation (unused small blocks left scattered).[1][2]
- **Best Fit:** Allocates the smallest suitable block; minimizes wasted space but can create many tiny unusable fragments.[2][3]
- **Worst Fit:** Allocates the largest block; slows fragmentation but tends to break big blocks, making future allocations harder.[3][2]

### Interview Q&A
- Q: What is the key disadvantage of Best Fit?
  - A: Causes many small holes (external fragmentation) that cannot be reused easily.[2]
- Q: When does Worst Fit work poorly?
  - A: When large requests arrive after all big blocks have been broken up by smaller allocations.[2]

### Tricky Edge Case
- "50-percent rule": About half of allocated memory is lost to fragmentation with First Fit.[4]

***

## Virtual Memory

- Separates logical (user) memory from physical memory—lets programs use more memory than physically available using disk as extension.[5][6]
- Implements through paging or segmentation; allows multitasking, process isolation, and easier memory allocation.[7][5]
- Downside: Too much swapping between disk and RAM causes **thrashing**—system spends more time moving data than doing actual work.[5][7]

### Interview Q&A
- Q: What is virtual memory?
  - A: Technique allowing use of disk as additional memory, supporting large or many programs.[7][5]
- Q: What causes thrashing?
  - A: Excessive page swaps between disk and RAM due to low physical memory.[5][7]

### Tricky Edge Case
- Set swap space too low, and the system might crash under load.[5]

***

## Contiguous Allocation, Paging, Segmentation

- **Contiguous Allocation:** Each process gets a single, continuous memory block—simple but causes fragmentation.[8][9]
- **Paging:** Divides memory into fixed-size **frames**, process into **pages**; avoids external fragmentation. Logical address split into page number and offset.[10][11]
- **Segmentation:** Divides programs into variable-sized segments by logical units (code, data, stack); fits programmer’s view, but can cause external fragmentation.[4][10]

### Interview Q&A
- Q: How does paging differ from segmentation?
  - A: Paging uses fixed sizes; segmentation uses variable, logical units.[10][4]
- Q: What is external fragmentation?
  - A: Unusable free memory due to scattered small gaps—not enough contiguous space for new allocations.[8][4]

### Tricky Edge Case
- Segmentation faults occur if trying to access beyond segment boundary.[4]

***

## Dynamic Binding

- The process of linking procedure calls to their definitions at runtime (not compile time)—enables location flexibility and dynamic loading of routines.
- Widely used in virtual memory management, shared libraries, and dynamic linking.

### Interview Q&A
- Q: Why is dynamic binding important for memory management?
  - A: Allows flexible and efficient use of memory by loading modules only when needed.

### Tricky Edge Case
- Poor dynamic binding can cause unresolved references or runtime exceptions.

***

## Page Fault

- Occurs when a program accesses a page not present in RAM; OS must load the page from disk.[12]
- Results in significant delay (disk reads are slow); can be minor (page in memory but not mapped) or major (not in memory at all).[13][12]

### Interview Q&A
- Q: What steps occur in a page fault?
  - A: Trap to OS → check access → swap in page → update page table → resume process.[13]
- Q: What are the effects of frequent page faults?
  - A: Increased latency, CPU wait, possible thrashing.[13]

### Tricky Edge Case
- Accessing invalid or protected addresses results in process termination, not page load.[13]

***

## Page Replacement Algorithms (LRU, Optimal, FIFO)

- **FIFO:** Replaces oldest loaded page; easy but can lead to more faults (Belady’s Anomaly).[14][15]
- **LRU (Least Recently Used):** Replaces page not used for longest time—closely tracks actual usage but needs additional tracking structures.[16][14]
- **Optimal:** Replaces page that won’t be used for the longest future time—ideal but only possible if future references are known (used as a benchmark).[15][14]

### Interview Q&A
- Q: Why use LRU over FIFO?
  - A: LRU better matches real access patterns and usually reduces page faults.[14][16]
- Q: When do these algorithms matter?
  - A: When physical memory is full and pages need to be swapped in/out.[16]

### Tricky Edge Case
- LRU requires extra memory to track usage; may be costly.

***

## Belady's Anomaly

- Phenomenon where increasing memory frames can perversely increase the number of page faults (seen in FIFO, not in stack-based algorithms like LRU).[17][18][19]
- Demonstrates that not all algorithms benefit from more resources.

### Interview Q&A
- Q: Which algorithm shows Belady's Anomaly?
  - A: FIFO—not LRU or Optimal.[18][19]
- Q: What is the practical implication?
  - A: More memory isn’t always better for all page replacement policies.[17]

### Tricky Edge Case
- Unexpected increases in faults after hardware upgrade can be traced to algorithm choice, not system failure.[18]

***

## Thrashing

- Occurs when the system is overcommitted, with so many page faults that processing stalls.[7]
- Symptoms include high CPU wait times and very low throughput.[7]

### Interview Q&A
- Q: How to prevent thrashing?
  - A: Reduce multiprogramming degree or increase physical memory.[7]
- Q: What is a working set?
  - A: Set of pages a process needs over a time interval; managing it helps prevent thrashing.

### Tricky Edge Case
- Heavy background tasks can cause interactive applications to thrash and become unresponsive.[7]

***

## Disk Scheduling and Disk Scheduling Algorithms

- Refers to choosing the order in which disk I/O requests are served to optimize throughput and minimize seek/delay times.
- **Algorithms:** FCFS (first-come), SSTF (shortest seek), SCAN, C-SCAN, LOOK, C-LOOK.

### Interview Q&A
- Q: Why is SCAN better than FCFS?
  - A: SCAN (elevator algorithm) reduces average seek time by moving head in one direction, servicing all pending requests before reversing.

### Tricky Edge Case
- SSTF can starve requests far from the current head location.

***

## Cache

- Fast, small memory layer between CPU and main memory to speed up access to frequently-used data.
- Managed using policies/tracking (LRU, FIFO, etc.).

### Interview Q&A
- Q: Why use a cache?
  - A: Achieve speedup by leveraging temporal and spatial locality—reduce access time to data.

### Tricky Edge Case
- Poor cache policy or mismatch can lead to cache misses and performance drop.

***

## Direct and Associative Mapping

- **Direct Mapping:** Each block mapped to exactly one cache line—simple and fast but can cause frequent conflicts.
- **Associative Mapping:** Any block can go into any cache line—flexible, allows more efficient use but slower look-up.
- **Set-Associative Mapping:** Compromise; blocks mapped to a set of lines.

### Interview Q&A
- Q: Difference between direct and associative mapping?
  - A: Direct is simple but prone to conflict; associative is flexible but complex; set-associative balances both.

### Tricky Edge Case
- Direct mapping: frequent replacements if multiple hot blocks map to the same line.

***


# References

## 1. Memory Management Basics

* [Memory Management in OS – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/memory-management-in-operating-system/) \[2]
* [Contiguous Memory Allocation in OS – HeroVired](https://herovired.com/learning-hub/topics/contiguous-memory-allocation-in-os/) \[8]
* [Difference Between Contiguous and Noncontiguous Allocation – StudyTonight](https://www.studytonight.com/operating-system/difference-between-contiguous-and-noncontiguous-memory-allocation) \[9]
* [Contiguous Allocation, Paging, and Segmentation – TakeUForward](https://takeuforward.org/operating-system/contiguous-allocation-paging-segmentation) \[20]

---

## 2. Contiguous Memory Allocation (First Fit, Best Fit, Worst Fit)

* [First Fit Allocation – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/first-fit-allocation-in-operating-systems/) \[1]
* [First Fit in C – PrepInsta](https://prepinsta.com/operating-systems/page-replacement-algorithms/first-fit/first-fit-in-c/) \[24]
* [First Fit, Best Fit, Worst Fit – SlideShare](https://www.slideshare.net/slideshow/first-fit-best-fit-worst-fit/87591897) \[3]
* [Worst Fit / Best Fit / First Fit – Blogspot](http://avanthioslab.blogspot.com/2016/09/a-worst-fit-b-best-fit-c-first-fit.html) \[25]
* [Lecture Notes PDF – Jeppiaar Institute](https://www.jeppiaarinstitute.org/pdf/lectures/603.pdf) \[4]
* [Lecture Notes PDF – Karnataka GFGC](https://gfgc.karnataka.gov.in/gfgcmalur/public/uploads/media_to_upload1715967125.pdf) \[26]
* [YouTube – Memory Management](https://www.youtube.com/watch?v=hmPcMkvNkW8) \[27]

---

## 3. Virtual Memory

* [Virtual Memory – TechTarget](https://www.techtarget.com/searchstorage/definition/virtual-memory) \[5]
* [Virtual Memory in OS – Scaler](https://www.scaler.com/topics/operating-system/virtual-memory-in-os/) \[6]
* [Define Virtual Memory, Thrashing, Threads – TakeUForward](https://takeuforward.org/operating-system/define-virtual-memory-thrashing-and-threads/) \[7]
* [Virtual Memory – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/virtual-memory-in-operating-system/) \[28]
* [Virtual Memory – Indeed](https://www.indeed.com/career-advice/career-development/virtual-memory) \[23]
* [YouTube – Virtual Memory Explanation](https://www.youtube.com/watch?v=N3rG_1CEQkQ) \[21]
* [YouTube – Virtual Memory Tutorial](https://www.youtube.com/watch?v=0XzNPY2i4JY) \[22]
* [YouTube – Virtual Memory Deep Dive](https://www.youtube.com/watch?v=u5obgqo4rZ8) \[30]

---

## 4. Paging & Segmentation

* [Segmentation in OS – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/segmentation-in-operating-system/) \[10]
* [What is Paging & Why Do We Need It? – TakeUForward](https://takeuforward.org/operating-system/what-is-paging-and-why-do-we-need-it/) \[11]

---

## 5. Page Faults

* [Page Fault – TakeUForward](https://takeuforward.org/operating-system/page-fault) \[12]
* [Page Fault Handling – GeeksforGeeks](https://www.geeksforgeeks.org/page-fault-handling-in-operating-system/) \[13]
* [Page Fault – EduRev](https://edurev.in/t/187271/page-fault) \[29]
* [Page Fault Notes – Scribd](https://www.scribd.com/doc/316257833/Page-Fault) \[34]
* [Steps for Handling Page Fault – Scribd](https://www.scribd.com/document/489548086/Steps-for-handling-page-fault-Easy-Notes) \[36]

---

## 6. Page Replacement Algorithms

* [Page Replacement Algorithms – TakeUForward](https://takeuforward.org/operating-system/page-replacement-algorithm) \[14]
* [FIFO, LRU, Optimal Page Replacement – SlideShare](https://www.slideshare.net/slideshow/fifo-lru-optimal-page-replacement-algorithm/232594392) \[15]
* [Difference Between LRU & FIFO – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/difference-between-lru-and-fifo-page-replacement-algorithms-in-operating-system/) \[16]
* [Page Replacement Algorithms – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/page-replacement-algorithms-in-operating-systems/) \[35]
* [Page Replacement Algorithms – Scaler](https://www.scaler.com/topics/operating-system/page-replacement-algorithm/) \[37]

---

## 7. Belady’s Anomaly

* [Belady’s Anomaly Explained – TakeUForward](https://takeuforward.org/operating-system/beladys-anomaly-explained/) \[17]
* [Belady’s Anomaly – TakeUForward](https://takeuforward.org/operating-system/belady-anomaly) \[18]
* [Belady’s Anomaly – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/beladys-anomaly-in-page-replacement-algorithms/) \[19]
* [Belady’s Anomaly – Scaler](https://www.scaler.com/topics/beladys-anomaly/) \[31]
* [Belady’s Anomaly – Baeldung](https://www.baeldung.com/cs/security-belady-anomaly) \[33]
* [Belady’s Anomaly – UpGrad](https://www.upgrad.com/tutorials/software-engineering/software-key-tutorial/beladys-anomaly/) \[38]
* [YouTube – Belady’s Anomaly](https://www.youtube.com/watch?v=2YbZD3GHwlU) \[32]
* [CMU Research Paper – Belady’s Anomaly](http://reports-archive.adm.cs.cmu.edu/anon/2020/CMU-CS-20-124.pdf) \[39]

