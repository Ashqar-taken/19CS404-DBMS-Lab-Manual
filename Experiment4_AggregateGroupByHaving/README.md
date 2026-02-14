# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
```
How many medical records does each doctor have?
Sample table:MedicalRecords Table
Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3

```


```sql
SELECT DISTINCT DoctorID, COUNT(RecordID) AS TotalRecords FROM MedicalRecords GROUP BY DoctorID
```

**Output:**

<img width="1266" height="869" alt="q1" src="https://github.com/user-attachments/assets/2ef1002c-445b-44f3-b3dc-a10215d600ca" />


**Question 2**
---
```
How many patients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?
Sample table: Patients Table
For example:
Result
AgeGroup    TotalPatients
----------  -------------
20-30       1
31-40       5
41-50       3
Above 50    1
```

```sql
SELECT CASE WHEN age < 20 THEN 'Under 20' WHEN age BETWEEN 20 AND 30 THEN '20-30' WHEN age BETWEEN 31 AND 40 THEN '31-40' WHEN age BETWEEN 41 AND 50 THEN '41-50' ELSE 'Above 50' END AS AgeGroup, COUNT(*) AS TotalPatients FROM( SELECT (strftime('%Y', 'now') - strftime('%Y', DateOfBirth) - (strftime('%m-%d','now') < strftime('%m-%d',DateOfBirth))) AS age FROM Patients) GROUP BY AgeGroup ORDER BY AgeGroup;
```

**Output:**

<img width="1214" height="909" alt="q2" src="https://github.com/user-attachments/assets/c6d57e19-54e3-46c8-ad28-3527fb9f18a3" />


**Question 3**
---
```
What is the total number of appointments scheduled by each doctor?
Sample table:Appointments Table
For example:
Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1
```
```sql
SELECT DISTINCT DoctorID, COUNT(AppointmentID) AS TotalAppointments FROM Appointments GROUP BY DoctorID
```

**Output:**

<img width="1206" height="874" alt="q3" src="https://github.com/user-attachments/assets/a07ec7f1-5c17-470a-8256-8c4e6455abec" />


**Question 4**
---
```
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.
Note: Inventory attribute contains amount of fruits
Table: fruits
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 
For example:
Result
total
----------
225

```

```sql
SELECT SUM(inventory) AS total FROM fruits GROUP BY unit HAVING unit='LB'
```

**Output:**

<img width="1231" height="912" alt="q4" src="https://github.com/user-attachments/assets/f19ae43b-11c1-4a81-8f47-7ed9e4f7958d" />


**Question 5**
---
```
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
avg_income
----------
5000000.0

```

```sql
SELECT AVG(income) AS avg_income FROM employee WHERE name LIKE 'A%'
```

**Output:**

<img width="1264" height="854" alt="q5" src="https://github.com/user-attachments/assets/ff0c69e7-e6f5-495d-b51d-98c50773eac6" />


**Question 6**
---
```
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.
Sample table: customer
For example:
Result
COUNT
----------
1
```

```sql
SELECT COUNT(*) AS COUNT FROM customer WHERE city='Noida'
```

**Output:**

<img width="1259" height="832" alt="q6" src="https://github.com/user-attachments/assets/2d02c033-cb79-418d-b0a9-28a0f46db3dc" />


**Question 7**
---
```
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

For example:
Result
COUNT
----------
4
```

```sql
SELECT COUNT(DISTINCT age) AS COUNT FROM employee
```

**Output:**

<img width="1262" height="902" alt="q7" src="https://github.com/user-attachments/assets/de756131-34b9-4ee2-bfcd-3a1229a713d0" />


**Question 8**
---
```
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.
Sample table: employee
For example:
Result
age         MIN(income)
----------  -----------
32          200000
```

```sql
SELECT age, MIN(income) FROM employee GROUP BY age HAVING MIN(income)<400000
```

**Output:**

<img width="1265" height="878" alt="q8" src="https://github.com/user-attachments/assets/3c21032f-0ac7-4713-b0d9-18bfe11e47f3" />


**Question 9**
---
```
Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

name        type
----------  ----------
RecordID    INTEGER
PatientID   INTEGER
DoctorID    INTEGER
Date        DATE
Diagnosis   TEXT
Treatment   TEXT
Medication  TEXT
For example:

Result
PatientID   TotalRecords
----------  ------------
1           4
```

```sql
SELECT PatientID, COUNT(RecordID) AS TotalRecords FROM MedicalRecords GROUP BY PatientID HAVING COUNT(RecordID)>3
```

**Output:**

<img width="1243" height="836" alt="q9" src="https://github.com/user-attachments/assets/cf80c54f-3682-4f9f-807c-c68f6805696a" />


**Question 10**
---
```
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.
Table: customer1
For example:
Result
age_group   MIN(salary)
----------  -----------
25          1500
```

```sql
SELECT (age / 5)*5 AS age_group, MIN(salary) FROM customer1 GROUP BY (age/5)*5 HAVING MIN(salary)<2000
```

**Output:**

<img width="1263" height="897" alt="q10" src="https://github.com/user-attachments/assets/706cb66b-a35b-4866-837a-4e0ff9d57f68" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
