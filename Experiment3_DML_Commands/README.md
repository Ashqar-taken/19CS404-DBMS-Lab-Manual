# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
```
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT * FROM EMPLOYEES WHERE DEPARTMENT_ID=80 AND COMMISSION_PCT=.25;
EMPLOYEE_ID  FIRST_NAME  LAST_NAME   EMAIL       PHONE_NUMBER        HIRE_DATE   JOB_ID      SALARY      COMMISSION_PCT  MANAGER_ID  DEPARTMENT_ID
-----------  ----------  ----------  ----------  ------------------  ----------  ----------  ----------  --------------  ----------  -------------
151          John        Bernstein   DBERNSTE    011.44.1344.345268  8/7/87      SA_REP      9500        0.25            145         80
152          John        Hall        PHALL       011.44.1344.478968  8/8/87      SA_REP      9000        0.25            145         80
161          John        Sewall      SSEWALL     011.44.1345.529268  8/17/87     SA_REP      7000        0.25            146         80
162          John        Vishney     CVISHNEY    011.44.1346.129268  8/18/87     SA_REP      10500       0.25            147         80
168          John        Ozer        LOZER       011.44.1343.929268  8/24/87     SA_REP      11500       0.25            148         80
175          John        Hutton      AHUTTON     011.44.1644.
```


```sql
UPDATE EMPLOYEES
SET first_name = 'John'
WHERE department_id=80 AND commission_pct<0.35;

```

**Output:**

<img width="1292" height="936" alt="q1" src="https://github.com/user-attachments/assets/ac83f9cc-c409-4725-a8f2-babea6c65992" />



**Question 2**
---
```
Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lv     INT        
quantity       INT        
supplier_id    INT           
For example:

Test	Result
select changes();
changes()
----------
4

```

```sql
UPDATE Products
SET sell_price = sell_price * 1.15
WHERE quantity<50 AND supplier_id=10
```

**Output:**

<img width="1292" height="933" alt="q2" src="https://github.com/user-attachments/assets/d774a660-8eab-4b3c-bab4-c4f92536c22d" />


**Question 3**
---
```
Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

Test	Result
--pragma table_info('products');
select changes();
changes()
----------
2
```

```sql
UPDATE Products
SET reorder_lvl = reorder_lvl * 0.7
WHERE cost_price > 50 AND quantity < 100
```

**Output:**

<img width="1301" height="929" alt="q3" src="https://github.com/user-attachments/assets/f8153b34-5079-4a74-ae58-eae29a49fcdb" />


**Question 4**
---
```
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
4
```

```sql
DELETE FROM Customer WHERE CUST_COUNTRY='UK' AND WORKING_AREA="London" AND GRADE<3
```

**Output:**

<img width="1296" height="924" alt="q4" src="https://github.com/user-attachments/assets/6069af0e-7573-4643-8852-9d3d37de401d" />

**Question 5**
---
```
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin       Jones
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
```

```sql
DELETE FROM Doctors WHERE specialization IS NULL
```

**Output:**

<img width="1303" height="767" alt="q5" src="https://github.com/user-attachments/assets/de2f529a-43ac-45ff-995c-60cbd53c056c" />



**Question 6**
---
```
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
1

```
```sql
DELETE FROM Customer WHERE GRADE=2 AND CUST_NAME LIKE 'm%' AND PAYMENT_AMT<3000
```

**Output:**

<img width="1296" height="877" alt="q6" src="https://github.com/user-attachments/assets/5c55bf26-6c9a-4b2f-863f-52ce080b428b" />


**Question 7**
---
```
Write a query to find all the employees whose salary is between 50000 to 100000 from employeeposition table.

EmpID
EmpPosition
DateOfJoining
Salary
1
Manager
01/05/2024
500000
2
Executive
02/05/2024
75000

For example:

Result
EmpID       EmpPosition  DateOfJoining  Salary
----------  -----------  -------------  ----------
2           Executive    2024-05-02     75000
3           Manager      2024-05-01     90000
2           Lead         2024-05-02     85000

```

```sql
SELECT * FROM employeeposition WHERE Salary>50000 AND Salary<100000
```

**Output:**

<img width="1278" height="767" alt="q7" src="https://github.com/user-attachments/assets/cb06ff91-056c-44c0-873c-d7c07635cbdc" />


**Question 8**
---
```
Write a SQL query to Select all patients who were admitted during the year 2023.

Table: Patients

name                  type
--------------------  ----------
patient_id            INT
first_name            VARCHAR(50)
last_name             VARCHAR(50)
date_of_birth         DATE
admission_date        DATE
discharge_date        DATE
doctor_id             INT
For example:

Result
patient_id  first_name  admission_date
----------  ----------  --------------
4           Abhishek    2023-02-10
5           Alice       2023-08-02

```

```sql
SELECT patient_id, first_name, admission_date FROM Patients WHERE admission_date LIKE "2023%"
```

**Output:**

<img width="1296" height="815" alt="q8" src="https://github.com/user-attachments/assets/5e5e80df-8c7c-40aa-b30b-ec572fc23a60" />


**Question 9**
---
```
Write a SQL query to assess the performance of value2 as 'Poor', 'Average', or 'Excellent' based on whether it is less than 30, between 30 and 70, or greater than 70 in the Calculations table

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          value2      performance
----------  ----------  -----------
1           10.0        Poor
2           35.0        Average
3           90.0        Excellent

```

```sql
SELECT id,value2, CASE WHEN value2<30 THEN 'Poor' WHEN value2 BETWEEN 30 AND 70 THEN 'Average' ELSE 'Excellent' END AS performance FROM Calculations
```

**Output:**

<img width="1290" height="902" alt="q9" src="https://github.com/user-attachments/assets/6f3b39b9-adcb-4f49-8d52-1309fc87fde9" />


**Question 10**
---
```
Write a SQL query to retrieve all orders where the purchase amount is between 500 and 4000 but exclude orders with purchase amounts of 948.50 and 1983.43. The query should return the columns: ord_no, purch_amt, ord_date, customer_id, and salesman_id.

Table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70003       2480.4      2012-10-10  3009         5003
70013       3045.6      2012-04-25  3002         5001

```

```sql
SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id FROM orders WHERE purch_amt BETWEEN 500 and 4000 AND purch_amt NOT IN (948.50, 1983.43)
```

**Output:**

<img width="1293" height="857" alt="q10" src="https://github.com/user-attachments/assets/1ade32bd-f1bd-4343-99c6-73bf7c150596" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
