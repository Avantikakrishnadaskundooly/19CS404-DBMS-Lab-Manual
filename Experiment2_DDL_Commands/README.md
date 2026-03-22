# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Bonuses with the following constraints:
1. BonusID as INTEGER should be the primary key.
2. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
3. BonusAmount as REAL should be greater than 0.
4. BonusDate as DATE.
5. Reason as TEXT should not be NULL.

```sql
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK(Bonusamount>0),
    BonusDate DATE,
    Reason TEXT NOT NULL
);
```

**Output:**
<img width="1780" height="183" alt="image" src="https://github.com/user-attachments/assets/cdcbf803-9ca6-4930-aa85-1b8268ed7381" />



**Question 2**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

```sql
INSERT Into Products(ProductID,Name,Category,Price,Stock)
VALUES(104,'Tablet','Electronics',100,50);
```

**Output:**
<img width="1699" height="233" alt="image" src="https://github.com/user-attachments/assets/69f5d0f0-bc90-48c5-a163-7e66d54643b8" />



**Question 3**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

```sql
ALTER TABLE Student_details
ADD column MobileNumber NUMBER;
ALTER TABLE Student_details
ADD column Address VARCHAR(100);
```

**Output:**
<img width="1567" height="330" alt="image" src="https://github.com/user-attachments/assets/74122950-b5b3-4367-81b9-ab23e7c50046" />



**Question 4**
---
Create a table named ProjectAssignments with the following constraints:
1. AssignmentID as INTEGER should be the primary key.
2. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
3. ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
4. AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments (
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    foreign key (EmployeeID) references
Employees(EmployeeID),
    foreign key (ProjectID) references
Projects(ProjectID)
);
```

**Output:**
<img width="1763" height="225" alt="image" src="https://github.com/user-attachments/assets/0196a914-abe7-4f20-bb94-07671f79dedb" />



**Question 5**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
INSERT INTO Customers (CustomerID, Name, Address, Email) 
SELECT CustomerID, Name, Address, Email 
FROM Old_customers;
```

**Output:**
<img width="1287" height="224" alt="image" src="https://github.com/user-attachments/assets/6a102705-583b-4528-8bdd-261bb5cd45b4" />



**Question 6**
---
Create a table named Invoices with the following constraints:
1. InvoiceID as INTEGER should be the primary key.
2. InvoiceDate as DATE.
3. Amount as REAL should be greater than 0.
4. DueDate as DATE should be greater than the InvoiceDate.
5. OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK (Amount >0),
    DueDate DATE CHECK (DueDate > InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**
<img width="1609" height="189" alt="image" src="https://github.com/user-attachments/assets/e4266615-e783-44d2-8db4-645e05b8b657" />



**Question 7**
---
Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

```sql
ALTER TABLE employee
ADD column designation varchar(50);
```

**Output:**
<img width="1541" height="249" alt="image" src="https://github.com/user-attachments/assets/cce3d563-e4da-4391-adaf-2f5c23d0db72" />



**Question 8**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
CREATE TABLE jobs (
    job_id INTEGER,
    job_title TEXT DEFAULT NULL,
    min_salary INTEGER DEFAULT 8000,
    max_salary INTEGER DEFAULT NULL
);
```

**Output:**
<img width="1626" height="249" alt="image" src="https://github.com/user-attachments/assets/a5d2c71c-d850-487c-86fd-c2eba577d763" />



**Question 9**
---
Create a table named Customers with the following columns:
1. CustomerID as INTEGER
2. Name as TEXT
3. Email as TEXT
4. JoinDate as DATETIME

```sql
create table Customers(
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME
);
```

**Output:**
<img width="1654" height="306" alt="image" src="https://github.com/user-attachments/assets/96bd058f-3a35-4dff-b844-aeb7268d13bc" />



**Question 10**
---
Insert the following products into the Products table:

```sql
INSERT INTO Products (Name, Category, Price, Stock) VALUES ('Smartphone', 'Electronics',800,150);
INSERT INTO Products (Name, Category, Price, Stock) VALUES ('Headphones', 'Accessories',200,300);
```

**Output:**
<img width="1153" height="269" alt="image" src="https://github.com/user-attachments/assets/331300b1-e646-497f-be62-4c071d27513a" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
