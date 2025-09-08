# Transaction and Concurrency Control 

## ACID Properties

### **What are ACID Properties?**
ACID stands for **Atomicity, Consistency, Isolation, and Durability** - four fundamental properties that ensure reliable database transaction processing.[1][2][3][4]

### **Atomicity**
Transactions are "all-or-nothing" - either all operations succeed or none are applied.[2][3][4][1]
- **Commit**: All changes permanently applied
- **Rollback**: All changes discarded if any operation fails

**Example**: Bank transfer of $100 from Account A to B
```sql
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE account_id = 'A';
UPDATE accounts SET balance = balance + 100 WHERE account_id = 'B';
COMMIT; -- Only if both updates succeed
```

### **Consistency**
Database remains in valid state before and after transaction; all integrity constraints are preserved.[3][4][1][2]

**Example**: Total money in banking system remains constant after transfers.

### **Isolation**
Concurrent transactions don't interfere with each other; changes invisible until committed.[1][2][3]

### **Durability**
Committed transactions persist permanently, even after system failures.[2][3][1]

### **Interview Questions - ACID**
**Q: What happens if atomicity is violated in a banking transaction?**
**A: Money could be debited from one account but not credited to another, causing inconsistency and potential financial loss.**

**Q: How does durability prevent data loss?**
**A: By ensuring committed transactions are written to non-volatile storage and can survive system crashes through logs and backups.**

***

## Schedules (Serial vs Parallel)

### **Serial Schedule**
Transactions execute one after another without any interleaving.[5][6][7][8]

**Characteristics**:[6][7][5]
- **Consistency**: Always correct results
- **No concurrency problems**: No conflicts between transactions
- **Low throughput**: High waiting time, poor performance
- **n! possible serial schedules** for n transactions

**Example**: T1 → T2 → T3 (complete T1, then T2, then T3)

### **Parallel (Non-Serial) Schedule**
Multiple transactions execute concurrently with interleaved operations.[9][7][5][6]

**Characteristics**:[5][6][9]
- **High throughput**: Better resource utilization
- **Potential concurrency problems**: May cause inconsistency
- **Many more possible schedules** than n!

### **Interview Questions - Schedules**
**Q: Why don't we always use serial schedules for correctness?**
**A: Serial schedules have very poor performance due to high waiting times; parallel schedules improve throughput and resource utilization significantly.**

**Q: What problems can arise with parallel schedules?**
**A: Lost updates, dirty reads, inconsistent analysis, and phantom reads due to concurrent access to shared data.**

***

## Isolation Levels

### **Four Standard Isolation Levels**[10][11][12][13][14]

### **1. Read Uncommitted** (Lowest)
- Allows **dirty reads** - can read uncommitted changes from other transactions
- No read locks held[11][12][13]
- Fastest but least safe

### **2. Read Committed**
- Prevents dirty reads - only reads committed data[12][13][10][11]
- Read locks released immediately after SELECT
- Allows **non-repeatable reads** (same query may return different results)

### **3. Repeatable Read**
- Prevents dirty reads and non-repeatable reads[14][10][11][12]
- Read locks held until transaction ends
- May still have **phantom reads** (new rows appearing)
- **Ideal for read-only transactions**[14]

### **4. Serializable** (Highest)
- Highest isolation level - prevents all anomalies[10][11][12]
- Transactions appear to execute serially
- Maximum data consistency but lowest performance

### **Read Phenomena**[11][12]
- **Dirty Read**: Reading uncommitted data
- **Non-repeatable Read**: Same query returns different results within transaction
- **Phantom Read**: New rows appear in subsequent reads

### **Interview Questions - Isolation Levels**
**Q: When would you choose Repeatable Read over Read Committed?**
**A: For read-only transactions requiring consistent data throughout, like financial reports where values shouldn't change during calculation.**

**Q: What's the trade-off between isolation levels?**
**A: Higher isolation levels provide better data consistency but reduce concurrency and performance due to increased locking.**

***

## Serializability and Concurrency Control

### **Serializability**
A schedule is serializable if its result is equivalent to some serial execution of the same transactions.[15][16][17][9]

### **Types of Serializability**[16][18][15]

### **Conflict Serializability**
Schedule can be transformed into serial schedule by swapping **non-conflicting operations**.[17][15][16]

**Conflicting Operations**:
- Belong to different transactions
- Operate on same data item  
- At least one is a write operation

**Testing Method**: Use **precedence graph** - if no cycles, then conflict serializable.[16]

### **View Serializability**
Schedule produces same result as serial schedule based on:
- Initial reads
- Final writes  
- Intermediate reads[18][15][16]

**Key Relationship**: Conflict Serializable ⊆ View Serializable[16]

### **Interview Questions - Serializability**
**Q: What's the difference between conflict and view serializability?**
**A: Conflict serializability is stricter, focusing on operation ordering; view serializability only cares about final results, allowing some schedules conflict serializability rejects.**

**Q: How do you test for conflict serializability?**
**A: Create a precedence graph from conflicting operations; if acyclic, the schedule is conflict serializable.**

***

## Locking Protocols

### **Types of Locks**[19][20][21]

### **Shared Lock (S-Lock)**
- Multiple transactions can read simultaneously
- No modifications allowed
- Compatible with other shared locks[21][19]

### **Exclusive Lock (X-Lock)**  
- Only one transaction can hold at a time
- Allows both read and write operations
- Not compatible with any other locks[19][21]

**Lock Compatibility Matrix**:[21]
|Lock Type|Shared|Exclusive|
|---------|------|---------|
|Shared   |✓     |✗        |
|Exclusive|✗     |✗        |

### **Two-Phase Locking (2PL) Protocol**[20][19][21]

**Two Phases**:
1. **Growing Phase**: Acquire locks, cannot release any
2. **Shrinking Phase**: Release locks, cannot acquire any

**Lock Point**: Moment when transaction has acquired all needed locks[19]

### **2PL Variants**[20]

**Strict 2PL**: Release exclusive locks only after commit
**Rigorous 2PL**: Release no locks until commit  
**Conservative 2PL**: Acquire all locks before transaction starts (deadlock-free)

### **Interview Questions - Locking**
**Q: Why is 2PL necessary for serializability?**
**A: 2PL ensures conflict-serializable schedules by preventing transactions from interfering with each other's lock acquisitions and releases.**

**Q: What causes deadlocks in locking protocols?**
**A: Circular wait conditions where transactions hold locks that other transactions need, and vice versa.**

***

## Database Recovery Management

### **Log-Based Recovery**[22][23]
System maintains transaction log recording all database modifications for recovery purposes.[22]

### **Write-Ahead Logging (WAL)**[22]
**Critical Rule**: Log records must be written to stable storage **before** corresponding database changes.[22]

### **Recovery Components**[24][23][22]

### **Checkpoints**[25][23][24][22]
Periodic points where:
- All modified data written to disk
- Checkpoint record added to log
- Limits log scanning during recovery[25][24][22]

### **Recovery Process**[23][22]

**Three Phases**:
1. **Analysis**: Identify active transactions at crash time
2. **Redo Phase**: Reapply all committed transaction changes
3. **Undo Phase**: Reverse incomplete transaction effects

### **Recovery Rules**[24][23]
- **Redo List**: Transactions with COMMIT records
- **Undo List**: Transactions with START but no COMMIT/ABORT

### **Interview Questions - Recovery**
**Q: Why is Write-Ahead Logging essential?**
**A: It ensures we have a record of all changes before they're applied, enabling complete recovery even if the system crashes during writes.**

**Q: How do checkpoints improve recovery performance?**
**A: They limit the log scan to recent transactions only, reducing recovery time by avoiding examination of entire log history.**

***

## Tricky Edge Cases & FAANG Interview Insights

### **Deadlock Scenarios**
- **Classic Example**: T1 holds X-lock on A, wants X-lock on B; T2 holds X-lock on B, wants X-lock on A
- **Detection**: Wait-for graphs or timeout mechanisms
- **Prevention**: Conservative 2PL, timestamp ordering

### **Phantom Read Edge Case**[12]
```sql
-- Transaction 1
SELECT COUNT(*) FROM employees WHERE salary > 50000; -- Returns 10

-- Transaction 2 (concurrent)
INSERT INTO employees VALUES ('John', 60000);
COMMIT;

-- Transaction 1 (continued)
SELECT COUNT(*) FROM employees WHERE salary > 50000; -- Returns 11
```

### **Lost Update Problem**
Two transactions reading same value and updating based on read value:
```sql
-- Both T1 and T2 read balance = 1000
-- T1: UPDATE account SET balance = 1000 + 100
-- T2: UPDATE account SET balance = 1000 + 200
-- Final result: 1200 (should be 1300)
```

### **Cascading Rollback**
When one transaction's rollback forces other dependent transactions to rollback, creating performance issues.

### **FAANG Interview Patterns**
- **Design questions**: "How would you handle high-concurrency banking transactions?"
- **Trade-off questions**: "When would you sacrifice ACID properties for performance?"
- **Failure scenarios**: "What happens if the system crashes during a checkpoint?"
- **Optimization**: "How do you minimize deadlocks in a high-traffic system?"

### **Performance Optimization Tips**
- Use appropriate isolation levels (don't always use SERIALIZABLE)
- Implement deadlock detection and timeout mechanisms
- Consider optimistic concurrency for read-heavy workloads
- Use connection pooling and batch operations
- Monitor lock contention and adjust timeout values

## References

1. [ACID Properties – Yugabyte](https://www.yugabyte.com/key-concepts/acid-properties/)  
2. [ACID Definition – TechTarget](https://www.techtarget.com/searchdatamanagement/definition/ACID)  
3. [ACID Properties in DBMS – Simplilearn](https://www.simplilearn.com/acid-properties-in-dbms-article)  
4. [ACID Properties in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/acid-properties-in-dbms/)  
5. [Serial Schedules, Concurrent Schedules, and Conflict Operations – Ashutosh Tripathi](https://ashutoshtripathi.com/2017/11/28/serial-schedules-concurrent-schedules-and-conflict-operations/)  
6. [Schedules in DBMS – CSTaleem](https://cstaleem.com/schedule-in-dbms)  
7. [Schedules in DBMS – Scaler](https://www.scaler.com/topics/dbms/schedule-in-dbms/)  
8. [Schedules in DBMS (YouTube)](https://www.youtube.com/watch?v=NpWvx4glyGY)  
9. [Types of Schedules in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/types-of-schedules-in-dbms/)  
10. [Difference Between Read Committed and Repeatable Read (SQL Server) – StackOverflow](https://stackoverflow.com/questions/4034976/difference-between-read-commited-and-repeatable-read-in-sql-server)  
11. [Transaction Isolation Levels in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/transaction-isolation-levels-dbms/)  
12. [Decoding Isolation Levels in MySQL – Decentro](https://decentro.tech/blog/decoding-isolation-levels-in-mysql/)  
13. [Isolation (Database Systems) – Wikipedia](https://en.wikipedia.org/wiki/Isolation_(database_systems))  
14. [SQL Isolation Levels Explained – Cockroach Labs](https://www.cockroachlabs.com/blog/sql-isolation-levels-explained/)  
15. [Serializability in DBMS – UpGrad](https://www.upgrad.com/blog/serializability-in-dbms/)  
16. [Difference Between Conflict and View Serializability – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/difference-between-conflict-and-view-serializability/)  
17. [Serializability in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/serializability-in-dbms/)  
18. [Serializability in DBMS – PrepBytes Blog](https://blog.prepbytes.com/serializability-in-dbms/)  
19. [Two-Phase Locking Protocol – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/two-phase-locking-protocol/)  
20. [Two-Phase Locking Protocol – Scaler](https://www.scaler.com/topics/two-phase-locking-protocol/)  
21. [Two-Phase Locking – Wikipedia](https://en.wikipedia.org/wiki/Two-phase_locking)  
22. [Step-by-Step Log-Based Recovery in DBMS – Cyfuture Cloud](https://cyfuture.cloud/kb/database/step-by-step-log-based-recovery-in-dbms)  
23. [Log-Based Recovery in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/log-based-recovery-in-dbms/)  
24. [Checkpoints in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/checkpoints-in-dbms/)  
25. [Database Checkpoints in SQL Server – Microsoft Docs](https://learn.microsoft.com/en-us/sql/relational-databases/logs/database-checkpoints-sql-server?view=sql-server-ver17)  
