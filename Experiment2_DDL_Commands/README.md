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
```
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER
For example:

Test	Result
pragma table_info('Orders');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     OrderID     INTEGER     0                       0
1     OrderDate   TEXT        0                       0
2     CustomerID  INTEGER     0                       0

```

```sql
create table Orders 
( OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER)
```

**Output:**

<img width="1294" height="858" alt="q1" src="https://github.com/user-attachments/assets/0a40c9bc-1af6-4b77-8033-41e216f7a39c" />


**Question 2**
---
```
In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 

For example:

Test	Result
SELECT * FROM Employee;
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
```

```sql
insert into Employee (EmployeeID, Name, Position) Values (5, "George Clark", "Consultant");
insert into Employee (EmployeeID, Name, Position, Department, Salary) Values (7, "Noah Davis", "Manager", "HR", 60000);
insert into Employee (EmployeeID, Name, Position, Department) Values (8, "Ava Miller", "Consultant", "IT");
```

**Output:**

<img width="1297" height="770" alt="q2" src="https://github.com/user-attachments/assets/7947e165-110e-4a10-b282-3fa58f8a3494" />


**Question 3**
---
```
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      MobileNumber     NUMBER           0                  0
6      Address          VARCHAR(100)     0                  0

```

```
ALter Table Student_details add MobileNumber NUMBER;
ALTER Table Student_details add Address VARCHAR(100);
```

**Output:**

<img width="1299" height="853" alt="q3" src="https://github.com/user-attachments/assets/877de1f4-d733-4092-8057-9e35cd96c7df" />


**Question 4**
---
```
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint failed
```

```sql
create table Shipments 
(ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
FOREiGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1286" height="738" alt="q4" src="https://github.com/user-attachments/assets/0f009d85-1640-43b9-a1c3-d7ae7a48af6b" />

**Question 5**
---
```
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1
```

```sql
create table Invoices 
(InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL Check (Amount > 0),
DueDate DATE check (DueDate > InvoiceDate),
OrderID INTEGER,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1300" height="775" alt="image" src="https://github.com/user-attachments/assets/9d6452e2-bb5c-4412-a99a-0a8c40e0b1b6" />


**Question 6**
---
```
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID

```

```sql
Create Table Invoices 
(InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE Check (DueDate > InvoiceDate),
Amount REAL Check (Amount > 0)
);
```

**Output:**

<img width="1295" height="754" alt="q6" src="https://github.com/user-attachments/assets/be15db87-4b8e-48dd-bae3-8535eafe8b99" />

**Question 7**
---
```
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	Result
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000

```

```sql
create table jobs (
    job_id INT,
    job_title VARCHAR(255) DEFAULT '',
    min_salary INT DEFAULT 8000,
    max_salary INT DEFAULT NULL
    );
```

**Output:**

<img width="1299" height="824" alt="q7" src="https://github.com/user-attachments/assets/2f22ca66-75f2-47e9-ba22-87aecfdd1cf5" />


**Question 8**
---
```
Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

For example:

Test	Result
SELECT * FROM Books;
ISBN            Title                    Author      Publisher   Year
--------------  -----------------------  ----------  ----------  ----------
978-1234567890  Data Science Essentials  Jane Doe    TechBooks   2024

```

```sql
insert into Books (ISBN, Title, Author, Publisher, Year) Values ("978-1234567890","Data Science Essentials", "Jane Doe", "TechBooks", 2024)

```

**Output:**

<img width="1292" height="742" alt="q8" src="https://github.com/user-attachments/assets/f46b5788-7a31-4a11-a54e-176d0087c2e1" />

**Question 9**
---
```
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
```

```sql
alter table Companies RENAME COLUMN name to first_name;
alter table Companies add mobilenumber number;
alter table Companies add DOB Date
```

**Output:**

<img width="1294" height="868" alt="q9" src="https://github.com/user-attachments/assets/c042b1d6-dd15-4802-97fd-044191ee9171" />


**Question 10**
---
```
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

Test	Result
select * from Customers;
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com

```

```sql
insert into Customers (CustomerID, Name, Address, Email) SELECT CustomerID, Name, Address, Email FROM Old_customers

```

**Output:**

<img width="1294" height="784" alt="q10" src="https://github.com/user-attachments/assets/6d06e1c9-b6e1-41aa-a0ce-f9e1232e448a" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
