

## What is Network?

**Definition:**  
A network is a group of two or more interconnected devices (computers, printers, servers) that share resources and communicate with each other.

**Example:**  
The internet is the largest global network that connects billions of devices worldwide.

**FAANG Interview Question:**  
Q: What is a computer network?  
A: A computer network is a collection of multiple interconnected devices that communicate and share resources using communication protocols.[1][2][3]

**Edge Case:**  
- Two computers connected directly via a crossover cable need proper configuration (e.g., IP addresses) to communicate.

***

## Types of Network (LAN, WAN, MAN)

| Network Type       | Description                                              | Range               | Example                              |
|--------------------|----------------------------------------------------------|---------------------|------------------------------------|
| LAN (Local Area Network)  | Connects devices within a limited area (home, office)       | Up to few kilometers | Office network, home Wi-Fi          |
| MAN (Metropolitan Area Network) | Covers a city or campus; larger than LAN, smaller than WAN       | 5-50 km             | ISP city network, university campus|
| WAN (Wide Area Network) | Connects devices across large geographical areas, often via public networks | Thousands of km     | The Internet, corporate networks   |

**FAANG Interview Question:**  
Q: Differentiate LAN, MAN, and WAN.  
A: LAN covers small local areas, MAN covers an entire city or campus, and WAN spans large geographical distances using public or leased telecommunication lines.[3][4]

**Edge Case:**  
- MAN is costly and more difficult to maintain due to its larger scale than LANs, and performance can degrade with congestion.

***

## Hub, Switch, and Router

| Device   | Layer       | Function                                           | Data Transmission                  | Example Use                         |
|----------|-------------|---------------------------------------------------|----------------------------------|-----------------------------------|
| Hub      | Physical (Layer 1)  | Broadcasts data to all ports                      | Sends packets to all ports       | Small/simple networks              |
| Switch   | Data Link (Layer 2) | Sends data only to intended device (MAC address) | Forwards selectively, reduces collisions | Larger LANs                      |
| Router   | Network (Layer 3)   | Routes packets between different networks         | Uses IP addresses to forward data | Connects LAN to WAN/Internet      |

**FAANG Interview Question:**  
Q: Compare hub, switch, and router.  
A: Hub broadcasts to all ports, switch sends data to specific MAC addresses, router routes data based on IP addresses between different networks.[5][6]

**Edge Cases:**  
- Hub causes network collisions due to broadcasting.  
- Switch segment collision domains but still has broadcast domains unless VLANs are configured.  
- Router can filter traffic and manage multiple network topologies.

***

## Network Topology and Its Types

**Definition:**  
Network topology is the arrangement or layout of nodes and links in a network physically or logically.

**Common Types:**

- **Bus:** All devices share a single communication line. Simple but single point failure affects the whole network.  
- **Star:** Devices connect to a central hub/switch. Failure of the center affects all nodes.  
- **Ring:** Each node connects to exactly two others forming a loop. Data flows in one or both directions.  
- **Mesh:** Every node connects to one or more nodes; full mesh connects all nodes. Provides high redundancy.  
- **Tree:** Hierarchical topology combining characteristics of star and bus.  
- **Point-to-Point:** Direct connection between two nodes.

**FAANG Interview Question:**  
Q: What is network topology? Name types.  
A: It is the layout structure of the network. Types include bus, star, ring, mesh, tree, and point-to-point.[7][8]

**Edge Cases:**  
- Bus topology suffers from collision and troubleshooting issues.  
- Mesh topology provides fault tolerance but is expensive to implement.

***

## Nodes and Links

- **Node:** Any device or point in a network that can send, receive, or forward information (e.g., computers, printers, routers).  
- **Link:** The communication pathway between two nodes; can be wired (cables) or wireless.

**FAANG Interview Question:**  
Q: What are nodes and links in networking?  
A: Nodes are devices connected in a network, and links are the physical or logical connections between these nodes facilitating data transfer.[9][10]

**Edge Cases:**  
- Nodes can be passive (like repeaters) or active (like switches).  
- Links may vary in bandwidth and latency affecting network performance.

***

# Frequently Asked Interview Questions and Model Answers

1. **What is the difference between a hub and a switch?**  
   Hub broadcasts data to all devices causing collisions, while switch sends data only to the intended recipient using MAC addresses, improving efficiency and security.[6][5]

2. **Explain how a router differs from a switch.**  
   A router connects different networks and uses IP addresses to route packets, whereas a switch connects devices within the same network and uses MAC addresses.[1][6]

3. **Why is mesh topology considered fault-tolerant?**  
   Because each node is connected to multiple others, failure of one link does not disrupt communication between nodes.[7]

4. **Can two computers communicate without IP addresses if connected directly?**  
   No, IP addresses or at least link-layer addresses are needed for proper communication at network or data link layers.[11]

5. **What are common media types for network links?**  
   Twisted pair cables, fiber optics, coaxial cables, and wireless links like Wi-Fi and Bluetooth.[10]

***

# References

## General Networking Interview Questions
1. [InterviewBit - Networking Interview Questions](https://www.interviewbit.com/networking-interview-questions/)
2. [PyNetLabs - Networking Interview Questions and Answers](https://www.pynetlabs.com/networking-interview-questions-and-answers/)
3. [Edureka - Networking Interview Questions](https://www.edureka.co/blog/interview-questions/networking-interview-questions/)
4. [Scribd - Computer Network Interview Questions (PDF)](https://www.scribd.com/document/595131478/Computer-Network-Interview-Question)
5. [ComputerNetworkingNotes - Top 100 Networking Interview Questions](https://www.computernetworkingnotes.com/career-resources/top-100-networking-interview-questions-with-answers.html)
6. [Shiksha - Networking Interview Questions & Answers](https://www.shiksha.com/online-courses/articles/networking-interview-questions-answers/)
7. [WeCreateProblems - Networking Interview Questions](https://www.wecreateproblems.com/interview-questions/computer-networking-interview-questions)
8. [LetsCode - Computer Network Interview](https://www.lets-code.co.in/interview/computernetworkinterview/)
9. [HelloIntern - LAN/WAN Management Interview Questions](https://hellointern.in/blog/lanwan-management-interview-questions-and-answers-57443)

---

## Basics of Computer Networking
1. [GeeksforGeeks - Basics of Computer Networking](https://www.geeksforgeeks.org/computer-networks/basics-computer-networking/)
2. [TakeUForward - Most Asked Computer Networks Interview Questions](https://takeuforward.org/computer-network/most-asked-computer-networks-interview-questions)

---

## Network Types & Topologies
1. [GeeksforGeeks - Types of Area Networks (LAN, MAN, WAN)](https://www.geeksforgeeks.org/computer-networks/types-of-area-networks-lan-man-and-wan/)
2. [GeeksforGeeks - Types of Network Topology](https://www.geeksforgeeks.org/computer-networks/types-of-network-topology/)
3. [WebAsha - CCNA Interview Questions on Network Topologies](https://www.webasha.com/blog/ccna-interview-questions-on-network-topologies)
4. [NetworkWalks - Network Topologies Interview Questions](https://networkwalks.com/network-topologies-interview-questions/)

---

## Hub, Switch & Router
1. [FiberMall - Hub, Switch, and Router Explained](https://www.fibermall.com/blog/hub-switch-and-router.htm)
2. [GeeksforGeeks - Difference Between Hub, Switch, and Router](https://www.geeksforgeeks.org/computer-networks/difference-between-hub-switch-and-router/)
3. [PyNetLabs - Hub vs Switch vs Router](https://www.pynetlabs.com/hub-vs-switch-vs-router/)

---

## IP Addressing
1. [GeeksforGeeks - Top 50 IP Addressing Interview Questions](https://www.geeksforgeeks.org/blogs/top-50-ip-addressing-interview-questions-and-answers/)

---

## Video Resources
1. [YouTube - Computer Networks Interview Questions](https://www.youtube.com/watch?v=qUBHLZEtS0M)

---
