# Introduction to DBMS
---

## Data, Database, and File System
- Data: Raw facts or figures without context (e.g., "John", "30").
- Database: Organized collection of structured data, usually electronic.
- File System: Stores data in files/directories. Limitations include redundancy, inconsistency, isolation issues, and poor security/integrity.

Example:  
A student’s details stored in separate text files by departments vs. centrally in one database table.

Interview Questions:
- What is the difference between a file system and a database?  
  A file system manages data as independent files, leading to redundancy. A database organizes data in a structured manner, reducing redundancy and improving consistency.  
- What are some problems with the file system approach?  
  Key issues include data redundancy, inconsistency, poor security, difficult data isolation, and integrity problems.

---

## Types of Databases
- Hierarchical Database: Data organized as a tree (parent-child). Example: IBM IMS.  
- Network Database: Web-like structure with many-to-many relationships. Example: IDS.  
- Object-Oriented Database: Data stored as objects with attributes and methods. Example: Berkeley DB.  
- Relational Database: Data stored in tables with rows and columns; relationships via keys. Examples: MySQL, PostgreSQL.  
- Cloud Database: Service-based or hosted databases. Examples: AWS RDS, Google Cloud SQL.  
- Centralized Database: Stored at a single location for consistency.  
- Personal Database: Used by a single user. Example: SQLite.

Example:  
Customer records stored in relational tables vs. multimedia objects stored in an object-oriented database.

Interview Questions:
- Explain the differences between hierarchical and relational databases.  
  Hierarchical databases have a tree structure, while relational databases organize data in tables with relationships through keys.

---

## What is DBMS and Its Applications
- DBMS: Software that stores, retrieves, manipulates, and secures databases.
- Applications:  
  - Banking: Transactions  
  - Airlines: Reservations  
  - Universities: Student information  
  - E-commerce: Inventory, customer data

Example:  
Amazon uses DBMS to manage user information, orders, inventory, and reviews.

Interview Questions:
- What is a DBMS and why is it important?  
  A DBMS is software for storing, securing, and organizing data efficiently. It underpins mission-critical business, web, and mobile applications.

---

## Need, Advantages, and Disadvantages of DBMS
- Need: Centralized management, security, reduced redundancy, and integrity enforcement.
- Advantages: Improved sharing and security, minimized redundancy, easier access and integration, higher productivity.
- Disadvantages: Complexity, cost, and possible performance overhead for simple use cases.

Tricky Edge Case:  
Multi-user transactions in banking. Without DBMS, a "lost update" problem may occur when multiple withdrawals are processed at the same time.

Interview Questions:
- Name some key advantages of DBMS over file systems.  
  DBMS offers reduced redundancy, improved security, easier integration, and better decision-making.  
- What is a common disadvantage of DBMS?  
  Greater complexity and higher cost for basic scenarios.

---

## Data Abstraction
- Physical Level: How data is stored.  
- Logical Level: What data is stored.  
- View Level: How users see the data.

Interview Questions:
- Name the three levels of data abstraction in DBMS.  
  Physical, logical, and view levels.

---

## DBMS Architecture
- Defines structure for data management.  
- Key Components:  
  - Query Processor  
  - Storage Manager  
  - Transaction Manager  

Interview Questions:
- What does the architecture of a DBMS contain?  
  Major components are query processor, storage manager, and transaction manager.

---

## 3-Tier Architecture
- Layers:  
  - Presentation: User interface  
  - Application: Business logic  
  - Database: Data storage

Example:  
A web application where the browser is the presentation layer, the server is the application layer, and the database is the data layer.

Interview Questions:
- Describe the three-tier architecture of DBMS.  
  It consists of client (presentation), application (logic), and database (storage) layers.

---

## Frequently Asked Interview Edge Cases
- Lost Update Problem: Multiple processes updating the same data. DBMS prevents this using transactions.  
- Phantom Reads: Data changes during a transaction's execution. Isolation levels handle this.  
- Non-repeatable Reads: Data read twice with different results due to updates. Solved via consistency controls.  
- Authorization Challenge: Enforcing access controls on sensitive fields.

---

## Model Short Answers
- How does DBMS solve data inconsistency?  
  It maintains a centralized version of data and uses integrity constraints and transactions to avoid inconsistency.  
- What is a primary key? What happens if it is not unique?  
  A primary key uniquely identifies records in a table. If not unique, integrity breaks and errors occur.  
- How can you prevent lost update problems in DBMS?  
  Use transaction management with ACID properties to ensure atomic and consistent updates.

---

## References
1. [TakeUForward – DBMS Core Questions](https://takeuforward.org/interviews/must-do-questions-for-dbms-cn-os-interviews-sde-core-sheet/)  
2. [GeeksforGeeks – Types of Databases](https://www.geeksforgeeks.org/dbms/types-of-databases/)  
3. [TakeUForward – Advantages & Disadvantages](https://takeuforward.org/dbms/adv-disadv-dbms)  
4. [YouTube – File Systems Explained](https://www.youtube.com/watch?v=U5Gg9R-Dc0Q)  
5. [Splunk – DBMS Overview](https://www.splunk.com/en_us/blog/learn/dbms-database-management-systems.html)  
6. [TakeUForward – Data & File System](https://takeuforward.org/dbms/data-database-and-file-system)  
7. [TakeUForward – DBMS Applications](https://takeuforward.org/dbms/dbms-and-its-applications)  
8. [TakeUForward – File System](https://takeuforward.org/operating-system/file-system)  
9. [TakeUForward – Types of File System](https://takeuforward.org/operating-system/types-of-file-system)  
10. [TakeUForward – RDBMS](https://takeuforward.org/dbms/rdbms)  
11. [TakeUForward – Data Models](https://takeuforward.org/dbms/data-models)  
