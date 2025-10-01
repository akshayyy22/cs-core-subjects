



## Domain Name System (DNS)

**Definition:**  
DNS translates human-friendly domain names (e.g., www.example.com) into IP addresses (e.g., 192.0.2.1) facilitating resource locating on the internet.[1][2]

**How it works:**  
Uses a hierarchical system with root servers, top-level domain servers, and authoritative DNS servers.

**Examples:**  
A resolver queries DNS servers to resolve a domain to an IP.

**Model Answer:**  
DNS converts domain names to IP addresses using a distributed, hierarchical database. It employs caching and recursive/iterative queries for efficient resolution.[3]

**Edge Case:**  
DNS poisoning can redirect traffic maliciously; DNSSEC helps secure resolutions.

***

## World Wide Web (WWW)

**Definition:**  
A system of interlinked hypertext documents accessed via the internet using browsers.[4]

**Components:**  
Web servers, browsers, URLs, hyperlinks, and protocols like HTTP.

**Example:**  
Accessing a web page triggers HTTP requests to servers hosting web content.

**Model Answer:**  
WWW uses HTTP to retrieve and display linked web pages via browsers, enabling multimedia and interactive content.[4]

**Edge Case:**  
URL hijacking or broken links can cause 404 errors affecting user experience.

***

## HTTP (Hypertext Transfer Protocol)

**Definition:**  
An application layer protocol for distributed, collaborative hypermedia information systems.[5][6]

**Features:**  
Connectionless, stateless protocol using request-response model (methods like GET, POST).

**Example:**  
Client sends GET request; server returns HTML page.

**Model Answer:**  
HTTP facilitates communication between clients and servers via stateless request-response transactions, supporting methods like GET, POST, PUT.[6]

**Edge Case:**  
Statelessness requires cookies or sessions to maintain state—security implications arise with improper management.

***

## FTP (File Transfer Protocol)

**Definition:**  
A standard network protocol for transferring files between a client and server.[7][8]

**Modes:**  
Active and Passive FTP differ in connection establishment — firewall challenges are common.

**Example:**  
Uploading or downloading files for website management.

**Model Answer:**  
FTP transfers files reliably using separate control and data connections, with active and passive modes to accommodate firewalls.[7]

**Edge Case:**  
FTP transmits data in plain text, causing security risks unless secured by FTPS or SFTP.

***

## SMTP (Simple Mail Transfer Protocol)

**Definition:**  
SMTP is used for sending email messages between servers.[9]

**Commands:**  
HELO/EHLO, MAIL FROM, RCPT TO, DATA, QUIT.

**Example:**  
Sending an email from client to server or between mail servers.

**Model Answer:**  
SMTP handles email sending by managing message formatting, addressing, and relay using simple text commands over TCP.[9]

**Edge Case:**  
SMTP is vulnerable to spam and spoofing; extensions like SMTP-AUTH and STARTTLS add security.

***

## DHCP (Dynamic Host Configuration Protocol)

**Definition:**  
DHCP dynamically assigns IP addresses and configuration to hosts on a network.[10][11]

**Process (DORA):**  
Discover, Offer, Request, Acknowledge.

**Example:**  
When a device connects to Wi-Fi, DHCP assigns an IP automatically.

**Model Answer:**  
DHCP automates IP address assignment and configuration using DORA to efficiently manage network resources.[10]

**Edge Case:**  
IP conflicts occur if lease management fails; DHCP relay agents help extend DHCP across subnets.

***

# Frequently Asked Interview Questions & Model Answers

1. **How does DNS improve user experience?**  
   It resolves memorable domain names to IP addresses quickly, reducing the need to remember numeric addresses.[2]

2. **Difference between HTTP and HTTPS?**  
   HTTPS encrypts HTTP traffic using TLS/SSL, providing confidentiality and integrity.[5][6]

3. **What are active and passive FTP modes?**  
   Active FTP requires the server to connect back to the client; passive FTP lets the client initiate both connections, easing firewall traversal.[7]

4. **How does SMTP handle multiple recipients?**  
   SMTP allows multiple RCPT TO commands for a single message, enabling simultaneous delivery to several addresses.[9]

5. **Explain DHCP lease and renewal.**  
   DHCP assigns IP leases with a validity period; clients request renewal before expiry to retain the address.[10]

***



[1](https://www.theknowledgeacademy.com/blog/dns-interview-questions/)
[2](https://www.finalroundai.com/blog/dns-interview-questions)
[3](https://in.indeed.com/career-advice/interviewing/dns-interview-questions)
[4](https://www.geeksforgeeks.org/computer-networks/world-wide-web-www/)
[5](https://in.indeed.com/career-advice/interviewing/http-interview-questions)
[6](https://www.remoterocketship.com/advice/10-http-interview-questions-and-answers-in-2023)
[7](https://climbtheladder.com/file-transfer-protocol-ftp-interview-questions/)
[8](https://www.tecmint.com/ftp-interview-questions-and-answers/)
[9](https://climbtheladder.com/smtp-interview-questions/)
[10](https://www.pynetlabs.com/dhcp-interview-questions-and-answers/)
[11](https://iq.iteanz.com/dhcp-interview-questions-and-answers)
[12](https://www.linuxforfreshers.com/p/interview-part-5.html)
[13](https://www.interviewbit.com/networking-interview-questions/)
[14](https://www.finalroundai.com/blog/http-interview-questions)
[15](https://www.vervecopilot.com/interview-questions/top-30-most-common-dns-interview-questions-you-should-prepare-for)
[16](https://interview4all.com/frequently-asked-ftp-interview-questions/)
[17](https://interview4all.com/latest-smtp-interview-questions/)
[18](https://www.webasha.com/blog/ccna-interview-questions-on-dhcp)
[19](https://www.vskills.in/interview-questions/dns-interview-questions)
[20](https://www.scribd.com/document/465113721/Top-25-Http-interview-questions-and-Answers)