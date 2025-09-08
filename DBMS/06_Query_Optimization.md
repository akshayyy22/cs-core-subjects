# Query Optimization

## Techniques for Optimizing SQL Queries

### **Core Optimization Principles**
Query optimization focuses on minimizing execution time, resource usage, and server load through strategic query design and structure modifications.[1][2][3][4]

### **Key Optimization Techniques**[2][3][4][1]

### **1. Indexing Strategy**
**Add Missing Indexes**: Most common cause of slow performance
```sql
-- Check missing indexes
SELECT * FROM sys.dm_db_missing_index_details;

-- Create strategic indexes
CREATE NONCLUSTERED INDEX IX_Customers_LastName 
ON Customers (LastName);
```

**Remove Unused Indexes**: Clean up to improve write performance
- Monitor index usage with system views
- Drop indexes with low usage statistics

### **2. SELECT Statement Optimization**[3][1][2]
**Use SELECT fields instead of SELECT ***: Reduces I/O and network load
```sql
-- Bad
SELECT * FROM employees;

-- Good  
SELECT employee_id, name, department FROM employees;
```

**Avoid SELECT DISTINCT**: Use EXISTS or proper JOINs instead
```sql
-- Instead of
SELECT DISTINCT customer_id FROM orders;

-- Use
SELECT customer_id FROM customers c 
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.customer_id = c.customer_id);
```

### **3. JOIN Optimization**[1][2]
**Use INNER JOIN syntax explicitly**: More efficient than WHERE clause joins
```sql
-- Better performance
SELECT c.name, o.order_date 
FROM customers c INNER JOIN orders o ON c.id = o.customer_id;

-- Less efficient
SELECT c.name, o.order_date 
FROM customers c, orders o WHERE c.id = o.customer_id;
```

**Minimize JOIN complexity**: Avoid too many JOINs in single query
- Consider breaking complex queries into smaller parts
- Use temporary tables for intermediate results

### **4. WHERE Clause Optimization**[3][1]
**Avoid multiple OR conditions**: Use UNION instead
```sql
-- Slow
SELECT * FROM products WHERE category = 'electronics' OR category = 'books';

-- Faster
SELECT * FROM products WHERE category = 'electronics'
UNION ALL
SELECT * FROM products WHERE category = 'books';
```

**Place wildcards at end only**: Enables index usage
```sql
-- Can use index
SELECT * FROM customers WHERE name LIKE 'John%';

-- Cannot use index effectively  
SELECT * FROM customers WHERE name LIKE '%John%';
```

### **Interview Questions - Query Optimization**
**Q: What are the top 3 query optimization techniques?**
**A: Proper indexing on frequently queried columns, avoiding SELECT *, and using appropriate JOIN types instead of subqueries where possible.**

**Q: How do you identify slow queries?**
**A: Use execution plans, query profilers, and system DMVs to analyze I/O costs, CPU usage, and identify table scans vs index seeks.**

***

## Indexing and Its Types

### **What is Indexing?**
Indexing creates data structures that improve the speed of data retrieval operations by providing efficient access paths to table data.[5][6][7]

### **Types of Indexes**[6][7][5]

### **1. Clustered Index**[7][5][6]
**Definition**: Determines physical order of data in table; only one per table
```sql
-- Automatically created for primary key
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,  -- Clustered index
    name VARCHAR(50),
    department_id INT
);
```

**Characteristics**:[6]
- Data pages stored in order of index key
- Leaf nodes contain actual data rows
- Ideal for range queries and sorting
- Faster for sequential access

### **2. Non-Clustered Index**[5][7][6]
**Definition**: Separate structure with pointers to data rows; multiple allowed per table
```sql
-- Create non-clustered index
CREATE NONCLUSTERED INDEX IX_Employee_Name 
ON employees (name);
```

**Characteristics**:[6]
- Index structure separate from table data
- Leaf nodes contain key values + row locators
- Better for specific lookups
- Requires additional storage space

### **3. Bitmap Index**[5]
**Definition**: Uses bits to represent value presence; efficient for low-cardinality columns
- Ideal for data warehousing
- Excellent for AND/OR operations
- Not suitable for OLTP systems
- Compact storage for categorical data

### **4. Composite Index**[6]
**Definition**: Index on multiple columns
```sql
CREATE INDEX IX_Employee_Dept_Salary 
ON employees (department_id, salary);
```

### **Index Selection Guidelines**[7][5][6]
- **Primary keys**: Automatic clustered index
- **Foreign keys**: Non-clustered indexes
- **WHERE clause columns**: High priority for indexing
- **JOIN columns**: Essential for performance
- **ORDER BY columns**: Improve sorting performance

### **Interview Questions - Indexing**
**Q: When would you choose clustered vs non-clustered index?**
**A: Use clustered for primary keys and range queries; use non-clustered for search conditions on non-primary columns and when multiple indexes are needed.**

**Q: What are the drawbacks of having too many indexes?**
**A: Increased storage overhead, slower INSERT/UPDATE/DELETE operations, and higher maintenance costs during data modifications.**

***

## B-Trees and B+ Trees

### **B-Tree Structure**[8][9][10]
**Definition**: Self-balancing tree data structure that maintains sorted data for efficient insertion, deletion, and search operations.

**Key Properties**:[10][8]
- All leaf nodes at same level
- Internal nodes store keys and child pointers
- Keys stored in sorted order
- Maximum of M-1 keys per node (M = order)
- Minimum of ⌈M/2⌉-1 keys per node (except root)

### **B+ Tree Structure**[9][8][10]
**Enhanced version of B-tree optimized for database systems**

**Key Differences from B-Tree**:[8][9][10]

### **1. Data Storage**
- **B-Tree**: Keys and values in all nodes
- **B+ Tree**: Only keys in internal nodes, all data in leaf nodes

### **2. Leaf Node Organization**[9][8]
- **B+ Tree**: Leaf nodes linked as doubly-linked list
- Enables efficient sequential and range queries
- All values at same level for consistent access time

### **3. Internal Node Capacity**[9]
- **B+ Tree**: More keys per internal node (no values stored)
- Results in shallower trees
- Better cache performance

### **B+ Tree in MySQL**[9]
**InnoDB Storage Engine**:
- All table data stored in B+ tree structure
- Primary key used as tree key
- 16KB default node size
- Automatic page loading from disk

### **Advantages of B+ Trees for Databases**[10][8][9]

### **1. Range Query Efficiency**
```sql
-- Efficient range scans using linked leaf nodes
SELECT * FROM orders WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31';
```

### **2. Sequential Access**
- Leaf node linking enables fast sequential scans
- ORDER BY queries benefit significantly
- Excellent for analytical workloads

### **3. Disk I/O Optimization**
- High fan-out reduces tree height
- Fewer disk accesses for searches
- Better cache utilization

### **4. Consistent Performance**
- All data at leaf level ensures uniform access time
- Predictable query performance

### **Interview Questions - B Trees**
**Q: Why do databases prefer B+ trees over B-trees?**
**A: B+ trees store all data in leaf nodes enabling efficient range queries, have higher fan-out for shallower trees, and support sequential access through linked leaves.**

**Q: How does B+ tree structure improve range query performance?**
**A: Leaf nodes are linked in sequential order, allowing range scans to traverse leaves efficiently without returning to internal nodes.**

***

## Tricky Edge Cases & FAANG Interview Insights

### **Index Selection Edge Cases**

### **1. Composite Index Column Order**[4][6]
```sql
-- Index on (department_id, salary)
CREATE INDEX IX_Dept_Salary ON employees (department_id, salary);

-- This query uses index efficiently
SELECT * FROM employees WHERE department_id = 5 AND salary > 50000;

-- This query only uses first column of index
SELECT * FROM employees WHERE salary > 50000;
```

**Key Point**: Left-most prefix rule - composite indexes only help queries that use leading columns.

### **2. Function Usage Breaking Index**[4][3]
```sql
-- Cannot use index on created_date
SELECT * FROM orders WHERE YEAR(created_date) = 2024;

-- Can use index
SELECT * FROM orders WHERE created_date >= '2024-01-01' 
    AND created_date < '2025-01-01';
```

### **3. Data Type Mismatches**[3]
```sql
-- Index on employee_id (INT) won't be used efficiently
SELECT * FROM employees WHERE employee_id = '123';  -- String literal

-- Proper usage
SELECT * FROM employees WHERE employee_id = 123;    -- Integer literal
```

### **Query Optimization Edge Cases**

### **4. Subquery vs JOIN Performance**[2][1]
```sql
-- Often slower - correlated subquery
SELECT name FROM employees e1 
WHERE salary > (SELECT AVG(salary) FROM employees e2 
                WHERE e2.department_id = e1.department_id);

-- Often faster - window function
SELECT name FROM (
    SELECT name, salary, AVG(salary) OVER (PARTITION BY department_id) as avg_dept_salary
    FROM employees
) t WHERE salary > avg_dept_salary;
```

### **5. NULL Handling in Indexes**[1]
- Most databases don't index NULL values in single-column indexes
- Can cause unexpected performance issues
- Consider filtered indexes for columns with many NULLs

### **FAANG Interview Patterns**

### **System Design Questions**
- "Design indexing strategy for a social media platform with billions of users"
- "How would you optimize queries for real-time analytics?"
- "Explain trade-offs between normalization and query performance"

### **Performance Analysis**
- Given execution plans, identify bottlenecks
- Explain when to denormalize for performance
- Discuss partitioning strategies for large tables

### **Real-World Scenarios**
- **Hot Spotting**: Avoiding sequential primary keys in distributed systems
- **Index Maintenance**: Managing index fragmentation in high-write environments
- **Memory Constraints**: Choosing between covering indexes and table scans

### **Advanced Optimization Techniques**[2][1]

### **6. Covering Indexes**
```sql
-- Covering index includes all needed columns
CREATE INDEX IX_Employee_Covering 
ON employees (department_id) INCLUDE (name, salary);

-- Query satisfied entirely by index
SELECT name, salary FROM employees WHERE department_id = 5;
```

### **7. Filtered Indexes**
```sql
-- Index only active employees
CREATE INDEX IX_Active_Employees 
ON employees (name) WHERE status = 'ACTIVE';
```

### **8. Index Intersection**
Database optimizer can combine multiple single-column indexes instead of requiring composite indexes.


## References

1. [How to Optimize SQL Query – Devart Blog](https://blog.devart.com/how-to-optimize-sql-query.html)  
2. [Query Optimization in SQL: Techniques, Tools & Best Practices – Acceldata](https://www.acceldata.io/blog/query-optimization-in-sql-essential-techniques-tools-and-best-practices)  
3. [SQL Performance Tuning – GeeksforGeeks](https://www.geeksforgeeks.org/sql-performance-tuning/)  
4. [Best Practices for SQL Query Optimizations – GeeksforGeeks](https://www.geeksforgeeks.org/sql/best-practices-for-sql-query-optimizations/)  
5. [Data Indexing Strategies – CrownRMS](https://www.crownrms.com/in/insights/data-indexing-strategies/)  
6. [Clustered and Non-Clustered Indexing – GeeksforGeeks](https://www.geeksforgeeks.org/sql/clustered-and-non-clustered-indexing/)  
7. [Indexing in Databases (Set 1) – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/indexing-in-databases-set-1/)  
8. [Introduction of B-Tree in DBMS – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/introduction-of-b-tree/)  
9. [B-Trees and Database Indexes – PlanetScale](https://planetscale.com/blog/btrees-and-database-indexes)  
10. [Difference Between B-Tree and B+ Tree – GeeksforGeeks](https://www.geeksforgeeks.org/dsa/difference-between-b-tree-and-b-tree/)  
