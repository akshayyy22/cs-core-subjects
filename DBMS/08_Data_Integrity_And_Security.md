# Data Integrity and Security - FAANG Interview Guide

## Role-Based Access Control (RBAC)

Role-Based Access Control (RBAC) assigns permissions to roles rather than individual users, simplifying management and enforcing the principle of least privilege[web:??].  

**Core Concepts**  
- **Role**: Named job function (e.g., “Admin,” “Developer,” “Analyst”).  
- **Permission**: Approval to perform operations (e.g., SELECT, INSERT on specific tables).  
- **User–Role Assignment**: Users inherit permissions by being assigned one or more roles.  
- **Role Hierarchies**: Roles can inherit permissions from other roles (e.g., “Senior Analyst” inherits “Analyst” permissions).  

**Example**  
```sql
CREATE ROLE analyst;
GRANT SELECT ON sales TO analyst;
CREATE ROLE senior_analyst;
GRANT analyst TO senior_analyst;  -- role hierarchy
CREATE USER alice;
GRANT senior_analyst TO alice;    -- user-role assignment
```

**Interview Question**  
Q: How does RBAC differ from MAC and DAC?  
A: RBAC grants permissions to roles not users directly, MAC uses system-enforced labels, and DAC allows users to grant their own permissions.  

**Edge Case**  
In complex hierarchies, cyclical role grants can inadvertently escalate privileges—must enforce acyclic role assignments.  

***

## Encryption

Encryption transforms data into unreadable ciphertext to prevent unauthorized access.  

**Types of Encryption**  
- **At-Rest Encryption**: Encrypts stored data (e.g., Transparent Data Encryption in SQL Server).  
- **In-Transit Encryption**: Secures data over networks (e.g., TLS/SSL).  
- **Column-Level Encryption**: Encrypts specific sensitive columns (e.g., credit card numbers).  

**Example**  
```sql
-- Column-level encryption in SQL Server
CREATE TABLE customers (
    id INT PRIMARY KEY,
    name NVARCHAR(100),
    credit_card VARBINARY(MAX) ENCRYPTED WITH (KEY = cc_key)
);
```

**Interview Question**  
Q: When would you choose column-level over at-rest encryption?  
A: Column-level secures specific sensitive fields with minimal performance overhead; at-rest encrypts whole database for broad protection.  

**Edge Case**  
Key management failures—losing encryption keys renders data irrecoverable; secure key rotation and backup are critical.  

***

## Data Masking Techniques

Data masking obfuscates sensitive data for non-production use cases (e.g., development, testing) while preserving data format and realism[web:??].  

**Masking Methods**  
- **Static Masking**: Creates anonymized copy of production data for test environments.  
- **Dynamic Masking**: Masks data in real-time for specific users or roles without altering source.  
- **Tokenization**: Replaces sensitive values with non-sensitive tokens mapped externally.  

**Example**  
```sql
-- Dynamic data masking in SQL Server
CREATE TABLE employees (
    id INT,
    name NVARCHAR(100) MASKED WITH (FUNCTION = 'partial(1,"XXXX",0)'),
    ssn CHAR(11) MASKED WITH (FUNCTION = 'default()')
);
GRANT UNMASK TO hr_role;  -- only HR can see unmasked data
```

**Interview Question**  
Q: What’s the difference between masking and encryption?  
A: Encryption secures data confidentiality at storage/transit; masking hides data for authorized viewing contexts without cryptography.  

**Edge Case**  
PK and FK constraints on masked columns can break referential integrity if masking changes values; use reversible masking or surrogate keys to maintain integrity.  

***
