### SQL Constraints Overview

Constraints in SQL define rules for data stored in a database, ensuring accuracy and integrity. These constraints control what values are allowed in specific columns.

| Constraint      | Description                                      |
|-----------------|--------------------------------------------------|
| **NOT NULL**    | Prevents NULL values in a column                 |
| **UNIQUE**      | Ensures unique values in a column                |
| **PRIMARY KEY** | Uniquely identifies each row (combines NOT NULL and UNIQUE) |
| **FOREIGN KEY** | References a record in another table             |
| **CHECK**       | Validates data based on a specified condition    |
| **DEFAULT**     | Sets a default value if none is provided         |
| **CREATE INDEX**| Speeds up data retrieval for indexed columns     |

---

### Details and Examples of SQL Constraints

#### 1. NOT NULL Constraint
Ensures that a column cannot contain NULL values.
```sql
CREATE TABLE Colleges (
  college_id INT NOT NULL,
  college_code VARCHAR(20) NOT NULL,
  college_name VARCHAR(50)
);
```
In this example, `college_id` and `college_code` columns cannot have NULL values.

---

#### 2. UNIQUE Constraint
Enforces unique values in a column, preventing duplicates.
```sql
CREATE TABLE Colleges (
  college_id INT NOT NULL UNIQUE,
  college_code VARCHAR(20) UNIQUE,
  college_name VARCHAR(50)
);
```
Here, both `college_id` and `college_code` must have unique values.

---

#### 3. PRIMARY KEY Constraint
Combines NOT NULL and UNIQUE constraints to uniquely identify rows. Typically used as the main identifier for each row.
```sql
CREATE TABLE Colleges (
  college_id INT PRIMARY KEY,
  college_code VARCHAR(20) NOT NULL,
  college_name VARCHAR(50)
);
```
The `college_id` column is used to uniquely identify each row in the `Colleges` table.

---

#### 4. FOREIGN KEY Constraint
Links a column in one table to the primary key of another table, ensuring referential integrity.
```sql
CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  customer_id INT REFERENCES Customers(id)
);
```
In this example, `customer_id` in `Orders` references `id` in the `Customers` table, ensuring that each `customer_id` corresponds to an existing customer.

---

#### 5. CHECK Constraint
Validates that column values meet a specific condition.
```sql
CREATE TABLE Orders (
  order_id INT PRIMARY KEY,
  amount INT CHECK (amount >= 100)
);
```
The `CHECK` constraint ensures that `amount` in `Orders` is always greater than or equal to 100.

---

#### 6. DEFAULT Constraint
Sets a default value for a column when no specific value is provided.
```sql
CREATE TABLE College (
  college_id INT PRIMARY KEY,
  college_code VARCHAR(20),
  college_country VARCHAR(20) DEFAULT 'US'
);
```
Here, if no value is specified for `college_country`, it defaults to "US".

---

#### 7. CREATE INDEX Constraint
Creates an index to speed up data retrieval on a specific column.
```sql
CREATE TABLE Colleges (
  college_id INT PRIMARY KEY,
  college_code VARCHAR(20) NOT NULL,
  college_name VARCHAR(50)
);

-- Creating an index
CREATE INDEX college_index
ON Colleges(college_code);
```
The `CREATE INDEX` command creates an index on `college_code` in the `Colleges` table, which helps speed up data searches on that column.

---

