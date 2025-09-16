## OSI Model Overview

**Definition:**  
The **OSI Model** (Open Systems Interconnection Model) is a seven-layer framework that standardizes how different computer systems communicate over a network, promoting interoperability and modular design.

**Purpose:**  
It breaks network communication into seven distinct layers, each handling a specific networking function, and is widely referenced in technical interviews.

**Example:**  
When sending an email, data travels from the Application layer down to Physical, then up each layer at the destination.

**FAANG Interview Question:**  
Q: What is the OSI Model? Why is it used?  
A: OSI Model is a layered framework for network communication, facilitating interoperability, abstraction, and troubleshooting by separating concerns into seven distinct layers. 

***

## Layers of OSI Model

| Layer Number | Name               | Key Functions                                     | Example Device/Protocol      |
|--------------|--------------------|---------------------------------------------------|------------------------------|
| 7            | Application        | User interface and network services               | HTTP, FTP, SMTP              |
| 6            | Presentation       | Data formatting, encryption, compression          | SSL, JPEG                    |
| 5            | Session            | Session establishment, management, termination    | NetBIOS, RPC                 |
| 4            | Transport          | Reliable delivery, flow control, segmentation     | TCP, UDP                     |
| 3            | Network            | Routing, logical addressing                       | IP, Routers                  |
| 2            | Data Link          | Framing, MAC addressing, error detection/correction| Switches, Ethernet, PPP     |
| 1            | Physical           | Transmission of raw bits over physical medium     | Cables, Hubs                 |

### Brief Layer Descriptions

- **Application Layer**  
  Interfaces with end-user applications, enabling network services like email, web browsing.

- **Presentation Layer**  
  Translates and formats data (character encoding, encryption/decryption), ensuring compatibility.

- **Session Layer**  
  Manages sessions between applications, handles establishment, maintenance, and termination.

- **Transport Layer**  
  Ensures reliable data transfer with error checking and flow control (TCP for reliability, UDP for speed).

- **Network Layer**  
  Handles packet routing and addresses (IP addressing), finds best path for data.

- **Data Link Layer**  
  Provides local data transfer, MAC addressing, error detection (Ethernet, PPP).

- **Physical Layer**  
  Converts bits to electrical or optical signals, manages cables/connectors.

***

## Common FAANG-Level Interview Questions and Model Answers

1. **What are the layers of the OSI Model?**  
   The OSI Model has seven layers starting from Physical, Data Link, Network, Transport, Session, Presentation, to Application, each with distinct networking roles.

2. **Explain the difference between TCP and UDP in the Transport Layer.**  
   TCP ensures reliable, ordered delivery; UDP is fast and connectionless, suitable for streaming and gaming.

3. **Which layers deal with error correction, and how?**  
   Data Link layer provides error detection/correction for local delivery; Transport layer handles end-to-end error recovery.

4. **How does a router fit into the OSI Model?**  
   Routers operate at the Network layer, routing packets based on logical IP addresses.

5. **Is data encryption handled by OSI Model? Where?**  
   Yes, encryption occurs at the Presentation layer for data security before transmission.

***

## Tricky Edge Cases Tested in Interviews

- **Session Layer Issues:**  
  If a protocol doesn’t support session management, the application must manage session state—interviewers may ask how you'd design this.
  
- **Fragmentation:**  
  Network layer fragmentation and reassembly can cause lost data if sequence info is missing or if MTU sizes mismatch between networks.

- **Physical Layer Faults:**  
  Signal attenuation and synchronization issues arise with long cable runs or different cable types (Ethernet vs. optical).

- **Protocol Layer Violations:**  
  If a device wrongly mixes OSI roles (e.g., switches acting as routers), it introduces hard-to-diagnose bugs.

- **Handling Duplicate or Out-of-Order Delivery:**  
  Transport layer needs robust logic to detect and resolve duplicate/out-of-order packets (TCP sequence numbers often tested).

- **Data Link Layer – MAC Address Conflicts:**  
  If two devices share the same MAC address, the switch can misroute traffic leading to unreachable hosts.

***

# Reference Links

## OSI Model (Interview & Guides)
- [1. OSI Model Interview Questions – Pynetlabs](https://www.pynetlabs.com/osi-model-interview-questions-and-answers/)
- [2. OSI Model Guide – GeeksforGeeks](https://www.geeksforgeeks.org/computer-networks/open-systems-interconnection-model-osi/)
- [3. OSI Model Comprehensive Guide – InfosecTrain](https://www.infosectrain.com/blog/osi-model-a-comprehensive-guide-for-exam-and-interview/)
- [4. OSI Model Explained – InterviewBit](https://www.interviewbit.com/blog/osi-model/)
- [5. OSI Model Q&A – Imedita](https://www.imedita.com/blog/osi-model-interview-questions-answers/)
- [6. Most Asked OSI Questions – TimesPro](https://timespro.com/blog/most-asked-osi-interview-questions-and-answers)
- [7. OSI Interview Questions – Indeed](https://in.indeed.com/career-advice/interviewing/osi-model-interview-questions)
- [11. OSI Model Q&A – Uninets](https://www.uninets.com/blog/osi-model-interview-questions-answers)

---

## Edge Cases in Coding Interviews
- [8. Thinking in Edge Cases – Algocademy](https://algocademy.com/blog/thinking-in-edge-cases-how-to-bulletproof-your-coding-solutions-in-interviews/)
- [9. Edge Cases in Coding Interviews – LinkedIn (Sandeep Jain)](https://www.linkedin.com/pulse/what-should-you-know-edge-cases-excel-coding-interviews-sandeep-jain-anldc)
- [10. Examples of Edge Cases (Frontend) – Reddit](https://www.reddit.com/r/Frontend/comments/o81f6a/what_are_some_example_of_edge_cases_in_a_front/)
- [14. Finding Edge Cases in DSA Problems – Jointaro](https://www.jointaro.com/question/JbK5LlJsKk9SW7sKc5Cc/how-do-you-find-edge-cases-in-dsa-problems-for-faang/)

---

## System Design
- [12. Common System Design Interview Questions – Leland](https://www.joinleland.com/library/a/20-common-system-design-interview-questions-with-sample-answers)
- [13. System Design Interview Prep (Video)](https://www.youtube.com/watch?v=v5mw-jK25Fg)
- [15. System Design Interview Guide – GeeksforGeeks](https://www.geeksforgeeks.org/system-design/system-design-interviews-faang/)


