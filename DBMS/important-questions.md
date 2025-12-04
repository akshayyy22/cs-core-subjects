# DBMS Question Bank


# 1. What is DBMS?
A **DBMS (Database Management System)** is software that stores, manages, retrieves, and updates data efficiently.

### ✔ Advantages of DBMS
- Reduces **data redundancy**
- Ensures **data security**
- Maintains **data consistency**
- Provides **backup & recovery**
- Supports **multi-user access**
- Ensures **data integrity**

---

# 2. What is a Database?
A **database** is an organized collection of related data that can be easily accessed, managed, and updated.

---

# 3. What is a Database System?
A **database system** includes:
- The **database**
- The **DBMS software**
- **Hardware**
- **Users**
- **Application programs**

It is the **complete environment** for managing and processing data.

---

# 4. What is RDBMS? (Properties)
A **Relational Database Management System** stores data in **tables** (rows & columns) and maintains **relationships** using keys.

### ✔ Properties of RDBMS
- Data stored in **tables**
- Supports **primary key** & **foreign key**
- Ensures **referential integrity**
- Supports **ACID properties**
- Allows **SQL operations**
- Follows **normalization** rules

---

# 5. Types of Database Languages
- **DDL** – Data Definition Language  
  (CREATE, DROP, ALTER)
- **DML** – Data Manipulation Language  
  (INSERT, UPDATE, DELETE)
- **DCL** – Data Control Language  
  (GRANT, REVOKE)
- **TCL** – Transaction Control Language  
  (COMMIT, ROLLBACK, SAVEPOINT)
- **DQL** – Data Query Language  
  (SELECT)

---

# 6. ACID Properties (Very Important)

### **A – Atomicity**
Transaction is **all or nothing**.

### **C – Consistency**
Database must remain **valid and correct** after transaction.

### **I – Isolation**
Each transaction works **independently** without interference.

### **D – Durability**
Committed data is **permanent** even after a crash.

---

# 7. Vertical vs Horizontal Scaling

| Feature | Vertical Scaling | Horizontal Scaling |
|--------|------------------|--------------------|
| Also called | Scale Up | Scale Out |
| How it works | Increase power of single server (CPU/RAM) | Add more servers to the system |
| Example | 8GB → 32GB RAM | Add multiple servers |
| Cost | More expensive | Cost-effective |
| Limit | Hardware limit | Almost unlimited |
| Used in | Traditional DBs | Distributed systems, NoSQL |

---


## 8. What is Sharding?

Sharding is a method of splitting a large database into smaller,  
more manageable parts called **shards**. Each shard contains a  
portion of the data and is stored on a separate server.

### Why use Sharding?
- Improves performance  
- Reduces load on a single server  
- Increases scalability  
- Makes large systems faster  

### Simple Example:
Instead of storing all users in one big database, split them:

- **Shard 1:** Users A–F  
- **Shard 2:** Users G–L  
- **Shard 3:** Users M–R  
- **Shard 4:** Users S–Z  

Each shard is handled separately, improving efficiency.




