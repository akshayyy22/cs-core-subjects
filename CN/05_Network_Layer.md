

## Routing Algorithms

**Definition:**  
Routing algorithms determine the optimal path for data packets between source and destination across networks.[1][2]

**Types:**
- **Distance Vector:** Routers exchange info with neighbors (RIP). Prone to slow convergence and loops.
- **Link State:** Each router builds a complete map of the network (OSPF, IS-IS). Faster, scalable, prevents loops.
- **Hybrid:** Combines both (EIGRP).

**Model Answer:**  
Distance vector routing uses hop count updates from neighbors, while link-state routers share complete network info for shortest path calculation.[2]

**Edge Case:**  
Distance vector suffers from count-to-infinity problem, leading to incorrect routing for extended periods.[3]

***

## Congestion Control Algorithms

**Definition:**  
Congestion control keeps network traffic below capacity, using proactive and reactive mechanisms.[4]

**Types:**
- **Open-loop:** Prevents congestion (admission control, traffic shaping).
- **Closed-loop:** Detects and reacts (feedback via ICMP, flow control).

**Examples:**  
Leaky Bucket, Token Bucket algorithms for regulating data flow.

**Model Answer:**  
Congestion control ensures optimal network utilization via techniques like leaky bucket, admission control, and feedback systems.[4]

**Edge Case:**  
Rapid traffic bursts or misbehaving nodes can overwhelm algorithms, causing congestion collapse.

***

## IP Addressing and Subnetting

**Definition:**  
IP addresses uniquely identify devices; subnetting divides large networks for efficient routing and management.[5][6]

**Subnet Mask:**  
Differentiates network and host parts (e.g., 255.255.255.0).

**Examples:**  
IP: 192.168.1.10; subnet: 255.255.255.0 isolates 254 hosts per subnet.

**Model Answer:**  
Subnetting splits networks to improve efficiency, security, and manageability. Subnet mask indicates the network section of an IP address.[7]

**Edge Case:**  
Complex subnets may waste addresses: each needs unique network and broadcast addresses.[7]

***

## IPv4 and IPv6 Protocols

| Feature       | IPv4                                    | IPv6                                     |
|---------------|-----------------------------------------|------------------------------------------|
| Address size  | 32-bit, dotted decimal (e.g., 192.0.2.1)| 128-bit, hexadecimal (e.g., 2001:db8::1) |
| Address count | ~4.3 billion                            | ~340 undecillion                         |
| Header        | Complex, many fields                    | Simplified, supports extension headers   |
| Security      | Optionally supports IPsec               | IPsec mandatory                          |

**Model Answer:**  
IPv6 solves IPv4 exhaustion, offers larger address space, built-in security (IPsec), and simpler headers.[8][9]

**Edge Case:**  
IPv6 routers don’t fragment packets; hosts must discover path MTU to avoid dropped packets, unlike IPv4.[9][8]

***

## ICMP (Internet Control Message Protocol)

**Definition:**  
ICMP reports errors, provides diagnostics (ping, traceroute), and sends control messages.[10][11]

**Model Answer:**  
ICMP is used by routers and hosts to report errors and status, facilitating troubleshooting and network control.[11]

**Edge Case:**  
ICMP errors aren’t sent for broadcast/multicast or certain reserved addresses, protecting network stability.[10]

***

## Fragmentation

**Definition:**  
Breaking data into smaller pieces for networks with lower Maximum Transmission Unit (MTU).[12]

**Process:**  
Data and repeated headers are fragmented at source or routers, each fits MTU limits.

**Model Answer:**  
Fragmentation allows a packet to traverse networks with differing MTU by splitting data and replicating headers.[12]

**Edge Case:**  
Further fragmentation at routers can lead to reassembly complexity or data loss if fragments are lost.[12]

***

## Tunneling

**Definition:**  
Encapsulating packets within another protocol for secure or incompatible network traversal.[13]

**Examples:**  
VPNs use tunneling to send private network data across public Internet.

**Model Answer:**  
Tunneling wraps packets inside compatible protocols, enabling secure or special-type data transfer over different networks.[14][13]

**Edge Case:**  
Incorrect encapsulation or protocol mismatch can break communication or introduce latency.

***

## Subnet

**Definition:**  
A smaller network segment within a larger IP network, created using subnet masks.[7]

**Purpose:**  
Enhances address management, security, and traffic isolation.

**Model Answer:**  
A subnet divides large IP ranges for efficient management, reducing broadcast domains and improving routing.[7]

**Edge Case:**  
Too many subnets may complicate management and waste addresses; each consumes network and broadcast addresses.[7]

***

## Gateway and Router

**Definition:**  
A **router** directs packets between different networks; a **gateway** connects networks using different protocols or architectures.[15][6]

**Model Answer:**  
Routers forward packets across networks; gateways connect networks with protocol translation as needed.[15]

**Edge Case:**  
Misconfigured routing tables in routers or gateways can cause network outages or security gaps.

***

## Count to Infinity Problem

**Definition:**  
A flaw in distance-vector routing; incorrect route updates propagate slowly, causing persistent routing errors.[2][3]

**Model Answer:**  
“Count to infinity” occurs when routers update routes in loops after a network failure—solved by techniques like split horizon or poisoned reverse.[3]

**Edge Case:**  
Large networks can amplify the problem, delaying convergence and causing packet loss for extended periods.

***

# Frequently Asked Interview Questions & Model Answers

1. **What’s the difference between static and dynamic routing?**  
   Static routing is manually configured and static; dynamic routing adapts to network changes automatically.[14]

2. **How does subnetting enhance network security?**  
   Subnetting isolates traffic, restricts broadcast domains, and simplifies management for distinct groups.[6][7]

3. **What does ICMP do?**  
   ICMP sends error and status messages such as destination unreachable, time exceeded, and echo (ping) replies.[11][10]

4. **Why can IPv6 process more addresses than IPv4?**  
   IPv6 uses 128-bit addresses, dramatically increasing address capacity and ending exhaustion issues.[8][9]

5. **How does network layer handle fragmentation?**  
   Splits large packets into fragments fitting MTU limits; each fragment has replicated headers for proper delivery and reassembly.[12]

***



[1](https://in.indeed.com/career-advice/interviewing/routing-interview-questions)
[2](https://www.nwkings.com/ccna-routing-and-switching-interview-questions)
[3](https://www.geeksforgeeks.org/computer-networks/classification-of-routing-algorithms/)
[4](https://www.slideshare.net/slideshow/congestion-control-68607381/68607381)
[5](https://nitizsharma.com/questions-and-answers-for-subnetting/)
[6](https://www.java-success.com/networking-basics-for-developers-interview-questions-answers/)
[7](https://in.indeed.com/career-advice/interviewing/subnetting-interview-questions)
[8](https://bunny.net/academy/network/what-is-the-difference-between-ipv4-and-ipv6/)
[9](https://www.linkedin.com/posts/alexxubyte_systemdesign-coding-interviewtips-activity-7193636995808514048-x0KU)
[10](https://snaprecruit.com/interview-questions/icmp-interview-questions.html)
[11](https://www.interviewplus.ai/network-and-system-administration/icmp-internet-control-message-protocol/questions)
[12](https://www.scaler.com/topics/fragmentation-in-networking/)
[13](https://www.geeksforgeeks.org/computer-networks/tunneling/)
[14](https://flexiple.com/networking/interview-questions)
[15](https://www.rfwireless-world.com/interview-qa/network-layer-interview-questions)
[16](https://www.imedita.com/blog/routing-interview-questions/)
[17](https://www.webasha.com/blog/ccna-routing-and-switching-interview-questions)
[18](https://www.interviewbit.com/networking-interview-questions/)
[19](https://www.youtube.com/watch?v=OglqIhtpw9o)
[20](https://www.youtube.com/watch?v=_xpVAPo5ROk)