# SQL Concepts 

## SQL Commands and Types

### **DDL (Data Definition Language)**
Commands that modify database structure:

**CREATE**: Creates database objects
```sql
CREATE TABLE employees (id INT, name VARCHAR(50));
```

**ALTER**: Modifies existing structure
```sql
ALTER TABLE employees ADD email VARCHAR(100);
```

**DROP**: Permanently removes objects
```sql
DROP TABLE employees;
```

**TRUNCATE**: Removes all rows but preserves structure
```sql
TRUNCATE TABLE employees;
```

### **DML (Data Manipulation Language)**
Commands that modify data:[2][1]

**INSERT**: Adds new records
```sql
INSERT INTO employees (id, name) VALUES (1, 'John');
```

**UPDATE**: Modifies existing data
```sql
UPDATE employees SET name = 'Jane' WHERE id = 1;
```

**DELETE**: Removes records
```sql
DELETE FROM employees WHERE id = 1;
```

**SELECT**: Retrieves data
```sql
SELECT name FROM employees WHERE id = 1;
```

### **Interview Questions - SQL Commands**
**Q: What's the difference between DELETE, DROP, and TRUNCATE?**
**A: DELETE removes rows (can be rolled back), DROP removes entire table structure, TRUNCATE removes all rows faster than DELETE (cannot be rolled back).**

**Q: Can you rollback DDL commands?**
**A: Generally no, DDL commands like CREATE, DROP are auto-committed and cannot be rolled back in most databases.**

***

## Operators and Aggregation Functions

### **Aggregate Functions**[4][5][6]
Functions that operate on multiple rows and return single values:

**COUNT()**: Counts rows
```sql
SELECT COUNT(*) FROM employees; -- Counts all rows including NULLs
SELECT COUNT(email) FROM employees; -- Counts non-NULL emails
```

**SUM()**: Totals numeric values
```sql
SELECT SUM(salary) FROM employees;
```

**AVG()**: Calculates average
```sql
SELECT AVG(salary) FROM employees;
```

**MIN()/MAX()**: Finds minimum/maximum values
```sql
SELECT MIN(salary), MAX(salary) FROM employees;
```

### **Important Notes**
- All aggregate functions ignore NULL values except COUNT(*)[4]
- Can be used with GROUP BY for grouped calculations[6][4]

### **Interview Questions - Aggregation**
**Q: What's the difference between COUNT(*) and COUNT(column)?**
**A: COUNT(*) counts all rows including NULLs, COUNT(column) counts only non-NULL values in that specific column.**

**Q: How do aggregate functions handle NULL values?**
**A: They ignore NULL values except COUNT(*), which counts all rows regardless of NULL values.**

***

## SQL Clauses

### **WHERE Clause**
Filters rows before grouping:[7][8]
```sql
SELECT * FROM employees WHERE salary > 50000;
```

### **GROUP BY Clause**
Groups rows with same values:[9][8][7]
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

### **HAVING Clause**
Filters groups after GROUP BY:[8][7][9]
```sql
SELECT department, COUNT(*) FROM employees 
GROUP BY department HAVING COUNT(*) > 5;
```

### **ORDER BY Clause**
Sorts result set:[10][9]
```sql
SELECT name, salary FROM employees ORDER BY salary DESC;
```

### **LIMIT Clause**
Restricts number of rows returned:
```sql
SELECT * FROM employees LIMIT 10;
```

### **Execution Order**[8]
1. FROM - Retrieve data
2. JOIN - Perform joins  
3. WHERE - Filter rows
4. GROUP BY - Form groups
5. HAVING - Filter groups
6. SELECT - Select columns
7. ORDER BY - Sort results
8. LIMIT - Limit rows

### **Interview Questions - Clauses**
**Q: What's the difference between WHERE and HAVING?**
**A: WHERE filters individual rows before grouping; HAVING filters groups after GROUP BY and can use aggregate functions.**

**Q: Can you use aggregate functions in WHERE clause?**
**A: No, aggregate functions cannot be used in WHERE clause because WHERE executes before GROUP BY.**

***

## Joins in SQL

### **INNER JOIN**
Returns only matching records from both tables:[11][12]
```sql
SELECT e.name, d.department_name 
FROM employees e INNER JOIN departments d 
ON e.dept_id = d.id;
```

### **LEFT JOIN (LEFT OUTER JOIN)**
Returns all records from left table and matching from right:[12][11]
```sql
SELECT e.name, d.department_name 
FROM employees e LEFT JOIN departments d 
ON e.dept_id = d.id;
```

### **RIGHT JOIN (RIGHT OUTER JOIN)**
Returns all records from right table and matching from left:[11][12]
```sql
SELECT e.name, d.department_name 
FROM employees e RIGHT JOIN departments d 
ON e.dept_id = d.id;
```

### **FULL OUTER JOIN**
Returns all records when there's a match in either table:[12]
```sql
SELECT e.name, d.department_name 
FROM employees e FULL OUTER JOIN departments d 
ON e.dept_id = d.id;
```

### **Interview Questions - Joins**
**Q: When would you use LEFT JOIN vs INNER JOIN?**
**A: Use INNER JOIN when you need only matching records from both tables; use LEFT JOIN when you need all records from the left table regardless of matches.**

**Q: How do you handle many-to-many relationships?**
**A: Create a junction/bridge table containing foreign keys from both tables, then join through this intermediate table.**

***

## Unions in SQL

### **UNION vs UNION ALL**[13][14][15]

**UNION**: Removes duplicates, slower performance
```sql
SELECT name FROM employees
UNION
SELECT name FROM contractors;
```

**UNION ALL**: Keeps all rows including duplicates, faster
```sql
SELECT name FROM employees
UNION ALL
SELECT name FROM contractors;
```

### **Requirements for UNION**[14][15]
- Same number of columns
- Compatible data types
- Same column order

### **Interview Questions - Unions**
**Q: When would you choose UNION ALL over UNION?**
**A: Use UNION ALL when duplicates are acceptable or when you know there are no duplicates, as it's faster since it skips the deduplication step.**

***

## Views in SQL

### **What are Views?**
Virtual tables based on SQL queries that provide data abstraction and security:[16][17][18]

```sql
CREATE VIEW active_employees AS
SELECT id, name, department 
FROM employees 
WHERE status = 'active';
```

### **Benefits of Views**[17][16]
- **Simplify complex queries**: Hide complexity from users
- **Security**: Restrict access to sensitive columns
- **Data abstraction**: Present data in user-friendly format
- **Consistency**: Ensure same logic across applications

### **View Operations**[17]
```sql
-- Update view
CREATE OR REPLACE VIEW active_employees AS
SELECT id, name, department, salary 
FROM employees 
WHERE status = 'active';

-- Drop view
DROP VIEW active_employees;
```

### **Interview Questions - Views**
**Q: What are the advantages of using views?**
**A: Views provide data security, query simplification, abstraction from underlying structure, and ensure consistent business logic across applications.**

**Q: Can all views be updated?**
**A: No, views based on joins, aggregates, or complex expressions are typically read-only and cannot be directly updated.**

***

## SQL Subqueries

### **Types of Subqueries**[19][20][21]

**Non-Correlated Subquery**: Executes once
```sql
SELECT name FROM employees 
WHERE dept_id IN (SELECT id FROM departments WHERE location = 'NY');
```

**Correlated Subquery**: Executes for each outer row[20][19]
```sql
SELECT name FROM employees e1
WHERE salary > (SELECT AVG(salary) FROM employees e2 
                WHERE e2.dept_id = e1.dept_id);
```

### **EXISTS vs IN**[21][19][20]
**EXISTS**: Tests for existence, better for correlated subqueries
```sql
SELECT name FROM employees e
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.emp_id = e.id);
```

**IN**: Tests membership, better for small result sets
```sql
SELECT name FROM employees 
WHERE dept_id IN (1, 2, 3);
```

### **Interview Questions - Subqueries**
**Q: What's the difference between correlated and non-correlated subqueries?**
**A: Non-correlated subqueries execute once independently; correlated subqueries execute once for each row in the outer query and reference outer query columns.**

**Q: When should you use EXISTS vs IN?**
**A: Use EXISTS for correlated subqueries and when checking existence; use IN for small, known value lists or when you need exact matches.**

***

## Tricky Edge Cases & FAANG Interview Insights

### **NULL Handling Edge Cases**[22][23][24]
- **GROUP BY**: All NULLs group together
- **ORDER BY**: NULLs typically sort first in ASC, last in DESC
- **Aggregates**: Most ignore NULLs except COUNT(*)
- **Comparisons**: NULL = NULL returns NULL, not TRUE

```sql
-- Handle NULLs properly
SELECT COALESCE(salary, 0) FROM employees; -- Replace NULL with 0
SELECT * FROM employees WHERE salary IS NOT NULL; -- Never use = NULL
```

### **Performance Optimization**[25][26]
- **Index NULL columns**: Some databases don't index NULLs
- **UNION vs UNION ALL**: Choose based on duplicate requirements
- **EXISTS vs IN**: EXISTS often faster for large datasets
- **Subquery vs JOIN**: JOINs typically faster than correlated subqueries

### **FAANG-Style Questions**[27][28][29][25]
Companies like Google, Amazon, Microsoft test:
- **Complex window functions** with ranking
- **Correlated subqueries** for row-by-row comparisons  
- **NULL handling** in edge scenarios
- **Performance optimization** trade-offs
- **Real business problems** with multiple table joins

### **Example FAANG Question Pattern**[25][27]
"Find users who have sent more emails than the average for their department, but exclude departments with fewer than 10 users."

**Edge Cases to Consider:**
- What if a department has exactly 10 users?
- How to handle NULLs in email counts?
- Should inactive users be included?
- Performance with millions of records?

### **Key Interview Tips**[30][29][25]
- **Always ask clarifying questions** about NULL handling
- **Consider performance implications** of your solutions
- **Think about edge cases** like empty result sets
- **Explain your reasoning** for choosing JOIN vs subquery
- **Test boundary conditions** in your mental walk-through



## References

### SQL Basics & DML
1. [SQL DML Operations: Insert, Update, Delete – DZone](https://dzone.com/articles/sql-data-manipulation-language-dml-operations-inse)  
2. [Basics of SQL Commands – ScholarHat](https://www.scholarhat.com/tutorial/sqlserver/basics-of-sql-commands)  
3. [Basic SQL Queries for Beginners – StormInternet](https://www.storminternet.co.uk/blog/basic-sql-queries-for-beginners-select-insert-update-delete/)  
31. [SQL Commands and Their Types – TakeUForward](https://takeuforward.org/dbms/sql-command-and-their%20types)  

### Aggregate Functions & Grouping
4. [SQL Aggregate Functions – W3Schools](https://www.w3schools.com/sql/sql_aggregate_functions.asp)  
5. [SQL Aggregate Functions – Hyperskill](https://hyperskill.org/university/sql/sql-aggregate-functions)  
6. [Aggregate Functions Glossary – Mimo](https://mimo.org/glossary/sql/aggregate-functions)  
7. [GROUP BY & HAVING Clause – Geekster](https://www.geekster.in/articles/group-by-having-clause-in-sql/)  
8. [GROUP BY Clauses Explained – FreeCodeCamp](https://www.freecodecamp.org/news/sql-group-by-clauses-explained/)  
9. [Using GROUP BY & ORDER BY – Navicat Blog](https://www.navicat.com/en/company/aboutus/blog/1708-using-group-by-and-order-by-in-the-same-query)  
10. [GROUP BY, HAVING, ORDER BY – Dummies](https://www.dummies.com/article/technology/programming-web-design/sql/how-to-use-group-by-having-and-order-by-sql-clauses-160800/)  
32. [How to Use GROUP BY and ORDER BY – DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-groupby-and-orderby-in-sql)  

### Joins & Set Operations
11. [Understanding SQL Joins – FreeCodeCamp](https://www.freecodecamp.org/news/understanding-sql-joins/)  
12. [SQL Joins (Inner, Left, Right, Full) – GeeksforGeeks](https://www.geeksforgeeks.org/sql/sql-join-set-1-inner-left-right-and-full-joins/)  
34. [Inner Join vs Outer Join – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/inner-join-vs-outer-join/)  
35. [SQL Joins – W3Schools](https://www.w3schools.com/sql/sql_join.asp)  
13. [UNION vs UNION ALL – GeeksforGeeks](https://www.geeksforgeeks.org/sql/union-vs-union-all-in-sql/)  
14. [Difference Between UNION and UNION ALL – Atlassian](https://www.atlassian.com/data/sql/what-is-the-difference-between-union-and-union-all)  
15. [SQL UNION vs UNION ALL Explained – StrataScratch](https://www.stratascratch.com/blog/sql-union-vs-union-all-differences-you-need-to-know/)  

### Views & Subqueries
16. [SQL CREATE VIEW – Hightouch](https://hightouch.com/sql-dictionary/sql-create-view)  
17. [SQL Views – W3Schools](https://www.w3schools.com/sql/sql_view.asp)  
18. [SQL Views – GeeksforGeeks](https://www.geeksforgeeks.org/sql/sql-views/)  
19. [SQL Server Correlated Subquery – GeeksforGeeks](https://www.geeksforgeeks.org/sql-server/sql-server-correlated-subquery/)  
20. [SQL Correlated Subqueries – GeeksforGeeks](https://www.geeksforgeeks.org/sql/sql-correlated-subqueries/)  
21. [Correlated Subqueries with Aliases – W3Resource](https://www.w3resource.com/sql/subqueries/correlated-subqueries-using-aliases.php)  
36. [Difference: Nested Subquery vs Correlated Subquery vs Join – CogentUniversity](https://www.cogentuniversity.com/post/difference-between-nested-subquery-correlated-subquery-and-join-operation)  

### NULL Handling
22. [Handling NULL Values in SQL – Milvus](https://milvus.io/ai-quick-reference/how-do-you-handle-null-values-in-sql)  
23. [MSSQL IS NULL & Interview Insights – VerveCopilot](https://www.vervecopilot.com/interview-questions/what-no-one-tells-you-about-mssql-is-null-and-interview-performance)  
24. [Master NULL Values in MS SQL Queries – Moldstud](https://moldstud.com/articles/p-master-null-values-in-ms-sql-queries-for-data-management)  
26. [Guide to IFNULL Function – SQLPad](https://sqlpad.io/tutorial/mastering-sql-a-guide-to-the-ifnull-function/)  

### SQL Functions
33. [SQL Functions for Beginners – Data36](https://data36.com/sql-functions-beginners-tutorial-ep3/)  

### SQL Interview Prep
25. [SQL Interview Questions Guide – StrataScratch](https://www.stratascratch.com/blog/sql-interview-questions-you-must-prepare-the-ultimate-guide/)  
27. [SQL Interview (YouTube) – FAANG Question](https://www.youtube.com/watch?v=xN2PRAd8IZQ)  
28. [Real SQL Interview Question from FAANG – Techtfq](https://techtfq.com/blog/real-sql-interview-question-asked-by-a-faang-company)  
29. [SQL Practice Problems – DataLemur](https://datalemur.com/questions)  
30. [Top 100 SQL Interview Questions – DataInterview](https://www.datainterview.com/blog/top-100-sql-interview-questions)  
