

## RAID and Its Types

- **RAID (Redundant Array of Independent Disks):** Combines multiple disks into one logical unit to improve performance, reliability, or both by using striping, mirroring, and parity.[1][2][3]
- **Common RAID Levels**:
  - **RAID 0 (Striping):** Splits data across disks for speed, no redundancy; one disk fails, all data lost.[2][3]
  - **RAID 1 (Mirroring):** Copies data to two+ disks for fault tolerance; higher disk usage, no speed gain on writes.[3][2]
  - **RAID 5 (Striping + Parity):** Distributes data and parity for fault tolerance with efficient storage; can tolerate one disk failure.[2][3]
  - **RAID 6 (Double Parity):** Like RAID 5 but can survive two disk failures; slightly slower writes.[3][2]
  - **RAID 10 (1+0, or Mirrored Stripes):** Stripes across mirrored pairs; best mix of speed and fault-tolerance but at high cost (needs at least 4 disks).[2][3]
  - **Nested and Non-Standard Levels:** Combinations (e.g., RAID 50, 60, 03/53) and vendor-specific implementations exist for special use cases.[4]

**Example:** RAID 5 is widely used in company file servers for a balance of space and risk protection.

### Interview Q&A
- Q: What happens if a disk fails in RAID 0?
  - A: All data is lost; RAID 0 has no redundancy.[3][2]
- Q: Why use RAID 10 over RAID 5?
  - A: RAID 10 offers better write performance and fault tolerance at the cost of usable capacity.[2][3]

### Tricky Edge Case
- RAID is not a substitute for backup; accidental deletes or ransomware still destroy data regardless of RAID.[4]

***

## Security Threats and Vulnerabilities

- **Security Threat:** Any circumstance/event with the potential to harm system integrity, availability, or confidentiality (e.g., malware, unauthorized access, DoS attacks).[5][6][7]
- **Vulnerability:** Weakness or flaw in OS code/configuration that can be exploited by threats (e.g., buffer overflows, unpatched software, improper access controls).[8][6][5]
- **Types of Threats**:
  - Malware (viruses, ransomware, spyware)
  - Phishing & social engineering
  - Denial of Service (DoS/DDoS)
  - Insider threats
  - Eavesdropping and man-in-the-middle attacks.[9][8]
- **Types of Vulnerabilities**:
  - Buffer overflows, injection flaws, privilege escalation, zero-days, misconfigurations.[5][8]
- **Consequences:** Data breach, system compromise, financial loss, loss of reputation.[6][8]

**Example:** WannaCry ransomware spread due to an unpatched MS Windows vulnerability, locking files for ransom worldwide.[8]

### Interview Q&A
- Q: What's a buffer overflow vulnerability?
  - A: When a process writes past buffer boundaries, possibly leading to arbitrary code execution.[5][8]
- Q: How does RAID help with data protection?
  - A: Provides fault tolerance against hardware failure, but does not guard against malware or accidental deletions.[3][2]

### Tricky Edge Cases
- Zero-day exploits are especially dangerous: attackers can compromise systems before patches exist.[8]
- Even secure setups can be undone by weak passwords or user error (phishing/insiders).[8]


### Resources

## 💽 RAID (Redundant Arrays of Independent Disks)
1. [What is RAID & Different Types (TakeUForward)](https://takeuforward.org/operating-system/what-is-raid-different-types-of-raid/)  
2. [RAID and Its Types (TakeUForward)](https://takeuforward.org/operating-system/raid-and-its-types)  
3. [What is RAID? – RenewTech](https://www.renewtech.com/blog/what-is-raid.html)  
4. [How RAID Works – Storware Blog](https://storware.eu/blog/what-is-raid-and-how-does-it-work/)  
5. [RAID in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/raid-redundant-arrays-of-independent-disks/)  
6. [RAID Definition – TechTarget](https://www.techtarget.com/searchstorage/definition/RAID)  
7. [What is RAID? – OnLogic Blog](https://www.onlogic.com/blog/what-is-raid/)  
8. [RAID Solutions – Western Digital](https://www.westerndigital.com/en-in/solutions/raid)  
9. [Guide to RAID – Dell Support](https://www.dell.com/support/kbdoc/en-in/000128638/guide-to-raid-redundant-array-of-independent-disks)  
10. [RAID Levels (0,1,5,6,10) – Trenton Systems](https://www.trentonsystems.com/en-au/blog/raid-levels-0-1-5-6-10-raid-types)  

---

## 🔒 OS Security Threats & Vulnerabilities
1. [OS Vulnerabilities – SternumIoT Blog](https://sternumiot.com/iot-blog/operating-system-vulnerabilities-understanding-and-mitigating-the-risk/)  
2. [Security Threats & Vulnerabilities (TakeUForward)](https://takeuforward.org/operating-system/security-threats-vulnerabilities)  
3. [Types of Security Threats – i2Tutorials](https://www.i2tutorials.com/os-introduction/os-types-of-security-threats/)  
4. [OS Vulnerability & Risk Management – Scalefusion Blog](https://blog.scalefusion.com/os-vulnerability-and-risk-management/)  
5. [Vulnerability in Security – Simplilearn](https://www.simplilearn.com/vulnerability-in-security-article)  
6. [Network Security Protocols (TakeUForward)](https://takeuforward.org/computer-network/network-security-protocols)  
7. [Vulnerabilities, Exploits & Threats – Rapid7](https://www.rapid7.com/fundamentals/vulnerabilities-exploits-threats/)  
8. [OS Vulnerabilities – ITU Online](https://www.ituonline.com/blogs/operating-system-vulnerabilities/)  
9. [System Security – GeeksforGeeks](https://www.geeksforgeeks.org/operating-systems/system-security/)  

---

## 🎥 Video Resources
1. [RAID & Security Concepts – YouTube](https://www.youtube.com/watch?v=YunvZspOuVs)  
