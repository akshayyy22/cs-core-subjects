## What is RDBMS?

**Definition:**  
Relational Database Management System (**RDBMS**) is a database system based on E.F. Codd’s relational model, storing data in tables (relations) structured by rows and columns.[2][1]

**Example:**  
MySQL, PostgreSQL, Oracle, and SQL Server are all RDBMS platforms.

**Interview Question:**  
- What are the key features of RDBMS?
  - **Model Answer:** Atomic values, unique rows, unique column names, primary/foreign keys, and data consistency across tables via integrity constraints.

**Edge Case:**  
Why might RDBMS struggle with huge distributed data?  
- RDBMS may have bottlenecks with sharding, distributed queries, or direct hierarchical/modeling needs.

***

## Essential Components of a Table

**1. Columns (Attributes):** Define types of data fields (e.g., Name, Age).[3]
**2. Rows (Tuples/Records):** Each row represents a unique entity instance (e.g., a student record).[3]
**3. Column Names:** Must be unique for unambiguous reference.[3]
**4. Data Items:** Actual values at the intersection of row and column.[3]
**5. Data Types:** Specify kind of data held (e.g., `INT`, `VARCHAR`, `DATE`).[3]
**6. Primary Key:** Unique identifier for each row, cannot be null.[3]
**7. Foreign Key:** Enforces relational integrity with other tables.[3]

**Example:**  
A `Students` table with columns: `StudentID` (Primary Key), `Name`, `Age`, `Course`, etc.

**Interview Question:**  
- What is the difference between primary and foreign keys?
  - **Model Answer:** The primary key uniquely identifies rows in its table; the foreign key references a primary key in another table, enforcing referential integrity.

**Edge Case:**  
Handling NULLs or non-unique values in primary keys can lead to data corruption.

***

## Intension and Extension

**Intension:** The schema/structure of a relation (table blueprint: columns, types, constraints).[4][10]
**Extension:** The actual data (set of tuples) stored at a given time; changes over time.[10][4]

**Example:**  
- Intension: Definition `Employee(RegNo, Name, Age, Company)`
- Extension: Current employee records in the table.

**Interview Question:**  
- What is the difference between intension and extension?
  - **Model Answer:** Intension is the schema (permanent), extension is the real-time data (variable).

**Edge Case:**  
Changing intension (schema updates) without considering existing extension can cause data loss.

***

## Keys

**Types of Keys:**
- **Super Key:** Any attribute set uniquely identifying a row.
- **Candidate Key:** Minimal super key; no subset of it can uniquely identify.
- **Primary Key:** Chosen candidate key; unique and non-null.[5][11][12]
- **Alternate Key:** Candidate keys not chosen as primary.
- **Foreign Key:** Field in one table matching primary key in another, enforcing relationships.
- **Composite Key:** Multiple fields uniquely identifying a row.
- **Unique Key:** Ensures distinct values in a column but may allow NULLs.

**Example:**  
- EmployeeID as primary key; Email as alternate key.

**Interview Question:**  
- Can a table have multiple candidate keys? How many primary keys?
  - **Model Answer:** Yes, there can be many candidate keys but only one can be chosen as primary key.

**Edge Case:**  
Circular foreign key references can create insertion or deletion dependencies.

***

## Normalisation and Its Types (1NF, 2NF, 3NF)

**1NF:** Eliminate repeating groups; each cell must hold atomic values.[6]
**2NF:** Must be in 1NF and have no partial dependencies (every non-key fully depends on the whole primary key).[6]
**3NF:** In 2NF and removes transitive dependencies (non-key attributes depend only on candidate keys, nothing else).[6]

**Example:**  
- [1NF] Splitting address fields so each cell holds just one value.
- [2NF] Moving department name to a separate table if it depends only on part of a composite key.
- [3NF] Removing derived/indirect dependencies, e.g., storing department location separately.

**Interview Question:**  
- Why is normalization important in RDBMS design?
  - **Model Answer:** It reduces redundancy, avoids anomalies, and improves data integrity by structuring tables logically.

**Edge Case:**  
Over-normalization can harm query speed and complicate simple queries.

***

## Functional Dependency

**Definition:**  
A relationship where an attribute's value is determined by another attribute or group of attributes.[7]

**Example:**  
In `Student(RollNo, Name, City)`, `RollNo → Name, City`.

**Interview Question:**  
- What role do functional dependencies play in normalization?
  - **Model Answer:** They determine how attributes relate and guide decomposition of tables for normalization.

**Edge Case:**  
Unresolved partial or transitive dependencies can prevent a schema from reaching 2NF/3NF.

***

## Denormalisation

**Definition:**  
The process of deliberately introducing redundancy for performance optimization in read-heavy use cases.[8][9]

**Techniques:**  
- Materialized views[8]
- Partitioning large tables[8]
- Adding redundant columns to avoid joins[8]
- Clustering related data for faster access[8]

**Example:**  
Duplicating customer names in transactions to avoid joins for reporting.

**Interview Question:**  
- What are the risks of denormalization?
  - **Model Answer:** Can cause data redundancy, inconsistency, and increase update anomalies; but improves query performance where justified.

**Edge Case:**  
Too much denormalization can cause major data maintenance headaches and write slowdowns.

***

## Tricky Edge Cases Companies Test

- **Multi-column Primary Keys:** When composite keys have partial dependencies, ensure full normalization.
- **Circular Foreign Keys:** Order of inserts and deletes must be managed to satisfy all constraints.
- **Handling Massive Joins:** Normalization helps, but sometimes denormalization is needed for real-time analytics; trade-off between integrity and performance.
- **Consistent Schema Updates:** Changes in intension must always consider existing extension to prevent data loss.[4]

## References

### RDBMS & Basics
1. [What is RDBMS – TakeUForward](https://takeuforward.org/dbms/rdbms)  
2. [Must-Do DBMS, CN, OS Questions for Interviews (Core Sheet) – TakeUForward](https://takeuforward.org/interviews/must-do-questions-for-dbms-cn-os-interviews-sde-core-sheet/)  
3. [Components of Table in Database – GeeksforGeeks](https://www.geeksforgeeks.org/sql/components-of-table-in-database/)  
14. [Data Models in DBMS – TakeUForward](https://takeuforward.org/dbms/data-models)  

### Keys in DBMS
5. [Keys in DBMS – TakeUForward](https://takeuforward.org/dbms/keys)  
11. [Types of Keys in Relational Model – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/types-of-keys-in-relational-model-candidate-super-primary-alternate-and-foreign/)  
12. [Keys in DBMS – Scaler](https://www.scaler.com/topics/dbms/keys-in-dbms/)  
18. [Types of Keys in DBMS – Byju’s](https://byjus.com/gate/types-of-keys-in-dbms/)  

### Database Normalization & Dependencies
6. [Database Normalization (1NF, 2NF, 3NF) – FreeCodeCamp](https://www.freecodecamp.org/news/database-normalization-1nf-2nf-3nf-table-examples/)  
7. [Partial, Full, and Transitive Dependencies – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/partial-full-and-transitive-dependencies/)  
8. [Denormalization in Databases – InvGate Blog](https://blog.invgate.com/denormalization-in-databases)  
9. [Denormalization – Wikipedia](https://en.wikipedia.org/wiki/Denormalization)  
10. [Normalization & Denormalization (YouTube)](https://www.youtube.com/watch?v=VFdvu6dkGVE)  

### ER Model & Relational Mapping
4. [Difference Between Intension and Extension – TakeUForward](https://takeuforward.org/dbms/difference-between-intension-and-extension-in-a-database/)  
13. [Convert ER Model to Relational Model – TakeUForward](https://takeuforward.org/dbms/convert-er-model-to-relational-model)  
15. [Introduction of ER Model – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/introduction-of-er-model/)  
16. [ER Model (DU PDF Notes)](https://www.du.ac.in/du/uploads/departments/Operational%20Research/24042020_E-R%20Model.pdf)  
17. [Types of Attributes in ER Model – GeeksforGeeks](https://www.geeksforgeeks.org/dbms/types-of-attributes-in-er-model/)  

### Interview Prep
20. [Most Asked DBMS Interview Questions – TakeUForward](https://takeuforward.org/dbms/most-asked-dbms-interview-questions)  
19. [DBMS Keys & Concepts (YouTube)](https://www.youtube.com/watch?v=eexceRsWt3g)  
21. [DBMS Concepts for Interviews (YouTube)](https://www.youtube.com/watch?v=UlgEHaEjg3o)  
