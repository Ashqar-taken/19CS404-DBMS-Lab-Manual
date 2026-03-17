# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

**Program:**
```
CREATE TABLE Employee (
  Emp_id INTEGER,
  Emp_name VARCHAR(40),
  Salary NUMBER);
  
CREATE TABLE Employee_log (
  Log_id NUMBER GENERATED AS IDENTITY,
  Emp_id INTEGER,
  Emp_name VARCHAR(40),
  Salary NUMBER,
  Log_date DATE);

CREATE OR REPLACE TRIGGER trg_employee_log
AFTER INSERT ON Employee
FOR EACH ROW
BEGIN 
  INSERT INTO Employee_log(Emp_id, Emp_name, Salary, Log_date) VALUES ( :New.Emp_id, :New.Emp_name, :New.Salary, SYSDATE);
END;
/

INSERT INTO Employee VALUES (1, 'John', 50000);
INSERT INTO Employee VALUES (10, 'Alice', 60000);

SELECT * FROM Employee_log
```

**Output:**

<img width="1919" height="994" alt="output" src="https://github.com/user-attachments/assets/47a46bba-065a-4432-8d08-fbc046e73f86" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

**Program:**
```
CREATE TABLE Sensitive_Table (
  Id INTEGER,
  Data VARCHAR(40)
  );


CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON Sensitive_Table
FOR EACH ROW
BEGIN 
  RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion is not allowed on this Table');
END;
/

INSERT INTO Sensitive_Table VALUES (1, 'John');
INSERT INTO Sensitive_Table VALUES (2, 'Alice');
INSERT INTO Sensitive_Table VALUES (3, 'Ben');

DELETE FROM Sensitive_Table WHERE Id=1;
```

**Output:**

<img width="1919" height="935" alt="q2" src="https://github.com/user-attachments/assets/223f7997-687e-48ae-a29d-150a75c9b1b5" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

**Program:**
```
CREATE TABLE Product (
  Id INTEGER,
  Name VARCHAR(40),
  Price Number,
  Last_modified TIMESTAMP
  );


CREATE OR REPLACE TRIGGER trg_last_modified
BEFORE UPDATE ON Product
FOR EACH ROW
BEGIN 
  :New.Last_modified := SYSTIMESTAMP;
END;
/

INSERT INTO Product VALUES (1, 'Ball', 18, NULL);
INSERT INTO Product VALUES (2, 'Rice', 250, NULL);

UPDATE Product SET price=300 WHERE Id=2;

SELECT * FROM Product;
```

**Output:**

<img width="1919" height="926" alt="output" src="https://github.com/user-attachments/assets/d0d1eced-f0b9-4461-91d8-888ee7e04972" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
