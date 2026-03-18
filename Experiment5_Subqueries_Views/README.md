# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500

```

**Program:**

```sql
SELECT * FROM CUSTOMERS WHERE ADDRESS="Delhi"
```

**Output:**

<img width="1312" height="814" alt="q1" src="https://github.com/user-attachments/assets/d575c04d-bc59-4e49-83e9-f43103cf02c3" />


**Question 2**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi          1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500
```

**Program:**

```sql
SELECT * FROM CUSTOMERS WHERE SALARY = 1500
```

**Output:**

<img width="1266" height="808" alt="q2" src="https://github.com/user-attachments/assets/80645b24-ce46-46fe-94cc-cc0ba56f172d" />


**Question 3**
---
```
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name   city
-----  ---------------
Neha   Bangalore
Rohit  Bangalore
Manoj  Bangalore
Vivek  Chandigarh

```
**Program:**

```sql
SELECT name, city FROM customer WHERE city IN (SELECT city FROM customer WHERE ID IN (3,7)); 
```

**Output:**

<img width="1265" height="906" alt="q3" src="https://github.com/user-attachments/assets/4e3b39b0-98db-45a8-ba10-3caec21a2d68" />


**Question 4**
---
```
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
grade       COUNT(*)
----------  ----------
300         2

```

**Program:**

```sql
SELECT grade, COUNT(*) FROM customer WHERE grade > (SELECT AVG(grade) FROM customer WHERE city='New York') GROUP BY grade
```

**Output:**

<img width="1315" height="847" alt="q4" src="https://github.com/user-attachments/assets/92c302b7-68dd-477e-bbdd-316d93bba160" />


**Question 5**
---
```
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70011       75.29       2012-08-17  3003         5007

```
**Program:**

```sql
SELECT * FROM orders WHERE salesman_id IN (SELECT salesman_id FROM salesman WHERE name="Paul Adam")
```

**Output:**

<img width="1300" height="883" alt="q5" src="https://github.com/user-attachments/assets/8bc50084-7285-4cd9-8a0e-b0a731d6ea83" />

**Question 6**
---
```
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
commission
----------
0.14

```

**Program:**

```sql
SELECT commission FROM salesman WHERE salesman_id IN (SELECT salesman_id FROM customer WHERE city="Paris")
```

**Output:**

<img width="1304" height="836" alt="q6" src="https://github.com/user-attachments/assets/9705cf2d-71ba-4912-bfaa-5aa1e5bb38ad" />


**Question 7**
---
```
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
3                Charlie          Math             95
5                Emma             Science          92
7                John             Social           85

```

**Program:**

```sql
SELECT * FROM GRADES GROUP BY subject HAVING(MAX(grade)) ORDER BY student_id
```

**Output:**

<img width="1272" height="902" alt="q7" src="https://github.com/user-attachments/assets/038e09ba-ecd1-4e74-8bbe-375611b2744b" />


**Question 8**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000

```

**Program:**

```sql
SELECT * FROM CUSTOMERS WHERE salary < 2500
```

**Output:**

<img width="1291" height="909" alt="q8" src="https://github.com/user-attachments/assets/9fd5d09f-7e6b-490f-a549-9d2e8eff8d2e" />


**Question 9**
---
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
7           Muffy       24          Indore      10000
```
**Program:**

```sql
SELECT * FROM CUSTOMERS WHERE SALARY > 4500
```

**Output:**

<img width="1264" height="899" alt="q9" src="https://github.com/user-attachments/assets/288dbd3f-2be9-47a3-b210-0f93e45f27da" />


**Question 10**
---
```
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

For example:
Result
student_name     grade
---------------  ---------------
Bob              85
Frank            85
John             85
```
**Program:**

```sql
SELECT student_name, grade FROM GRADES GROUP BY subject HAVING(MIN(grade)) ORDER BY student_id
```

**Output:**

<img width="1292" height="887" alt="q10" src="https://github.com/user-attachments/assets/8179951a-b78b-40b3-8754-71cff67754bb" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
