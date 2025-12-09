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


## 9. Keys in DBMS

### Keys are attributes that help uniquely identify records in a table.

### Types of Keys

- Primary Key → Uniquely identifies a record; cannot be NULL.

- Candidate Key → Attributes that can potentially be a primary key.

- Super Key → Any attribute(s) that uniquely identify a record (includes candidate keys).

- Composite Key → Key made from more than one attribute.

- Foreign Key → Establishes a link between two tables; references primary key of another table.

- Alternate Key → Candidate keys not chosen as primary key.

- Unique Key → Similar to primary key but allows one NULL value.



### 10. Types of Relationships in DBMS

## Defines how rows in different tables relate to each other.

### Relationship Types

- One-to-One (1:1)

  One record in A ↔ One record in B

  Example: Person ↔ Passport

- One-to-Many (1:N)

  One record in A → Many in B

  Example: Customer → Orders

- Many-to-One (N:1)

  Many records in A → One in B

  Example: Students → Department

- Many-to-Many (M:N)

  Many in A ↔ Many in B

  Requires a junction table

  Example: Students ↔ Courses

----

### Data Abstraction in DBMS

  DBMS hides unnecessary complexity.

## Three Levels

  1. Physical Level (Lowest)

      How data is stored internally (files, blocks, indexes).

  2. Logical/Conceptual Level (Middle)

      Database structure → tables, relationships, constraints.

  3. View/External Level (Highest)

      What end-users see → custom views, filtered data.

### 11. Indexing in DBMS

    Indexes help in faster searching, like a book index.

    Types of Indexes

    1. Primary Index

    2. Secondary Index

    3. Clustered Index (sorts the table itself)

    4. Non-Clustered Index (separate structure)

    5. B-Tree Index

    6. Hash Index


### 12. DDL (Data Definition Language)

    Used to define or modify database structure.

  Commands

    - CREATE → Create tables/databases

    - ALTER → Modify structure

    - DROP → Delete table/database

    - TRUNCATE → Remove all rows (cannot be rolled back)

    - RENAME → Rename table


### 13. DML (Data Manipulation Language)

    - Used to manage data inside tables.

    Commands

    - SELECT → Retrieve data

    - INSERT → Add data

    - UPDATE → Modify data

    - DELETE → Remove data

### 14. Normalization

  - Process of organizing data to reduce redundancy and improve consistency.

  Simple Definition:

  Store clean, non-repetitive data to avoid update issues.

  Types (Forms)

  - 1NF:

    No repeating groups

    Atomic values

  - 2NF:

    In 1NF

    No partial dependency (on part of composite key)

  - 3NF:

    In 2NF

    No transitive dependency (non-key → non-key)

  - BCNF:

    Stronger 3NF

    Every determinant = candidate key

  -  4NF / 5NF:

    Deal with multivalued and join dependencies (rare)

  ### 15. Denormalization

    - Opposite of normalization.

    Simple Explanation:

    Add redundancy intentionally to improve performance.

    Example:

    Instead of calculating total orders each time, store total in the customer's table.




# 16. Conflict Serializability (DBMS)

**Goal:** Ensure transactions running together don’t break correctness.

A schedule is **conflict serializable** if you can **rearrange non-conflicting operations** to get a **serial schedule**.

### Conflicting Operations

Two operations conflict if:

1. They are from **different transactions**
2. They access the **same data item**
3. At least one is a **write**

Conflicts:

* `R(x)` vs `W(x)`
* `W(x)` vs `R(x)`
* `W(x)` vs `W(x)`

Not a conflict:

* `R(x)` vs `R(x)`

### Precedence Graph Method

* Nodes → transactions
* Edge Ti → Tj if Ti’s action conflicts with Tj and appears before it

✔ **No cycle → conflict serializable**
✘ **Cycle → not serializable**

---

# 17. Concurrency Control Protocols (CCP)

Rules DBMS uses to control how transactions run together.

### 1. Lock-Based Protocols

* Use **shared lock** (read) and **exclusive lock** (write)
* Can cause deadlocks

### 2. Two-Phase Locking (2PL)

* **Growing phase:** acquire locks
* **Shrinking phase:** release locks
* Once you start releasing, you **cannot acquire new locks**

### 3. Timestamp Ordering Protocol

* Each transaction gets a **timestamp**
* Older timestamp → higher priority
* Ensures serializability without locks

### 4. Optimistic Concurrency Control

* No locks
* Transactions run freely
* Conflicts checked at **commit time**

---

# 18. Entity, Entity Type, Entity Set, Weak Entity Set

### Entity

A real-world object you can identify uniquely.
Example: *Student*, *Car*, *Employee*

### Entity Type

A class/category of similar entities.
Example: `Student(ID, Name, Age)`

### Entity Set

Collection of entities of the same type.
Example: All students in a college.

### Weak Entity Set

Cannot be uniquely identified by its own attributes.
Depends on a **strong** entity.

Characteristics:

* Has **partial key**
* Shows **total participation**
* Identified using strong entity’s key

Example: `OrderItem` depends on `Order`.

---

# 19. SQL Commands & Types

SQL commands are instructions to interact with the database.

### 1. DDL – Data Definition Language

Defines table structure.

* `CREATE`
* `DROP`
* `ALTER`
* `TRUNCATE`

### 2. DML – Data Manipulation Language

Changes table data.

* `INSERT`
* `UPDATE`
* `DELETE`
* `SELECT` (sometimes DQL)

### 3. DQL – Data Query Language

* `SELECT`

### 4. DCL – Data Control Language

* `GRANT`
* `REVOKE`

### 5. TCL – Transaction Control Language

* `COMMIT`
* `ROLLBACK`
* `SAVEPOINT`

---

# 20. Nested Queries (Subqueries)

A **query inside another query**.

Example:

```sql
SELECT name 
FROM Students 
WHERE marks > (SELECT AVG(marks) FROM Students);
```

Used for:

* Filtering
* Comparisons with aggregates
* `IN`, `EXISTS`, etc.

---

# 21. JOIN in SQL

JOIN combines rows from multiple tables using a **common column**.

## Types of JOIN

### 1. INNER JOIN

Returns rows that **match in both tables**.

### 2. LEFT JOIN (Left Outer)

* All rows from **left** table
* Matching rows from right
* No match → NULL

### 3. RIGHT JOIN (Right Outer)

* All rows from **right** table
* Matching rows from left

### 4. FULL OUTER JOIN

* All rows from both tables
* No match → NULL on one side

### 5. CROSS JOIN

* Cartesian product (A × B)

### 6. SELF JOIN

A table joined **with itself**.

Example:

```sql
SELECT e.name, m.name
FROM Employee e
JOIN Employee m ON e.manager_id = m.id;
```

# 22. Inner Join vs Outer Join

## INNER JOIN
- Returns **only matching rows** between two tables.
- Non-matching rows are **not shown**.
- **Example:** Show students who *have* marks.

## OUTER JOIN
Returns matching rows **plus** non-matching rows.

### Types:
- **LEFT OUTER JOIN** → all rows from left table + matching right rows  
- **RIGHT OUTER JOIN** → all rows from right table + matching left rows  
- **FULL OUTER JOIN** → all rows from both tables, even if not matching

---

# 23. 2-Tier vs 3-Tier Architecture

## 2-Tier Architecture
- Only **Client ↔ Database**
- Client talks directly to DB.
- Example: Desktop app directly connected to MySQL.

**Simple:** 2 layers → **Client + Database**

## 3-Tier Architecture
- **Client ↔ Application Server ↔ Database**
- Client never talks directly to DB.
- Example: Web app → Browser → Backend → DB.

**Simple:** 3 layers → **UI + Logic + DB**

---

# 24. TRUNCATE vs DELETE

## DELETE
- Deletes **specific rows** using WHERE.
- **Slow** (row-by-row).
- **Can be rolled back**.
- **Triggers fire**.
- Does not reset auto-increment.

## TRUNCATE
- Removes **all rows** instantly.
- **Very fast**.
- **Cannot be rolled back** in many DBs.
- **Triggers do NOT fire**.
- **Resets auto-increment**.

---

# 25. Intension vs Extension (Database)

## Intension
- The **schema/structure** of the table.
- Column names + data types.
- Stable definition.

**Think:** What the table *looks like*.

## Extension
- The **actual data/rows** stored in the table at a given time.

**Think:** What the table *contains*.

---

# 26. Locks (Shared vs Exclusive)

## What is a Lock?
A lock controls read/write access to a row/table to avoid conflicts.

---

## Shared Lock (S-Lock)
- Allows **read-only** access.
- Multiple transactions can read together.
- No one can write.

**Think:** “You can read, I can read… but nobody edits.”

---

## Exclusive Lock (X-Lock)
- Allows **writing** (insert/update/delete).
- Only one transaction can hold it.
- Others cannot read or write.

**Think:** “I’m editing this, nobody touch it!”

