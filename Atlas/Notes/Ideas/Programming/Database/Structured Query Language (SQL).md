---
up:
  - "[[Database MOC]]"
related: 
created: 2024-05-20
---
## What is SQL?
SQL (Structured Query Language) is a programming language for managing data in [[Conceptual Data Models#3. Relational Model (**الأشهر**)|Relational Database]], where data is organized in tables with rows and columns. 
SQL commands allow users to **store, update, retrieve, and manage** data effectively.
### SQL Standards
ANSI and ISO adopted SQL standards in 1986, helping ensure consistency in SQL usage across different database systems.
## Why is SQL Important?
SQL is widely used across industries because:
- It integrates well with languages like Java.
- It's simple to learn, using common English syntax.
- SQL powers major databases like Oracle and MS SQL Server.
## Components of a SQL System

### SQL Table
**SQL Table**: The core data structure, organized in rows and columns, often linked by relational keys.

For example, the database engineer creates a SQL table for products in a store

| **Product ID** | **Product Name** | **Color ID** |
| -------------- | ---------------- | ------------ |
| 0001           | Mattress         | Color 1      |
| 0002           | Pillow           | Color 2      |

Then the database engineer links the product table to the color table with the _Color ID:_

| **Color ID** | **Color Name** |
| ------------ | -------------- |
| Color 1      | Blue           |
| Color 2      | Red            |
### SQL Statements
**SQL Statements**: Queries that retrieve, store, update, or delete data (e.g., `INSERT INTO`).
For example, the following SQL statement uses a SQL INSERT command to store _Mattress Brand A,_ priced _$499,_ into a table named _Mattress_table,_ with column names _brand_name_ and _cost:_
`INSERT INTO Mattress_table (brand_name, cost)`
### Stored Procedures
**Stored Procedures**: Reusable SQL statements stored within the database for improved performance.
## How SQL Works
1. **Parser**: Checks syntax, tokenizes commands, and verifies user permissions.
2. **Relational Engine**: Plans efficient data retrieval or modification using bytecode.
3. **Storage Engine**: Executes SQL commands by reading/writing data on physical storage.

## Types of SQL Commands
1. **Data Definition Language (DDL)**: Creates and modifies database structures (e.g., `CREATE TABLE`).
2. **Data Query Language (DQL)**: Retrieves data (e.g., `SELECT`).
3. **Data Manipulation Language (DML)**: Adds or changes records (e.g., `INSERT`, `UPDATE`).
4. **Data Control Language (DCL)**: Manages user permissions (e.g., `GRANT`).
5. **Transaction Control Language (TCL)**: Controls transaction behavior (e.g., `ROLLBACK`).

## More
### SQL Injection
A cyberattack method where attackers use SQL queries to exploit database vulnerabilities, often through input fields.

### SQL vs. MySQL
- **SQL**: A standard language for relational databases.
- **MySQL**: A specific open-source relational database management system using SQL, commonly used in web applications.
### SQL vs. NoSQL
- **SQL**: Best for structured data and transactional applications.
- **NoSQL**: Flexible for unstructured data, allowing scaling across multiple servers for heavy, responsive applications.
### SQL Server
Microsoft's SQL Server is a relational database system designed for varied workloads, offering multiple editions to meet different business needs.

