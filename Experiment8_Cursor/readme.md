# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display the employee details or an error message.

**Program:**
```
CREATE TABLE Employee (emp_id INTEGER PRIMARY KEY, emp_name VARCHAR(40), designation VARCHAR(40));

INSERT INTO Employee VALUES (1, 'Ashqar', 'Kill');
INSERT INTO Employee VALUES (2, 'kumar', 'sales');
INSERT INTO Employee VALUES (3, 'Kali', 'manufacture');
DECLARE
  CURSOR emp_cur IS SELECT emp_name, designation FROM Employee;
  
  v_name Employee.emp_name%TYPE;
  v_designation Employee.designation%TYPE;
  
  v_count NUMBER := 0;
BEGIN 
  OPEN emp_cur;
  
  LOOP
    FETCH emp_cur INTO v_name, v_designation;
    EXIT WHEN emp_cur%NOTFOUND;
    v_count := v_count + 1;
    
    DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ' | designation: ' || v_designation);
  
  END LOOP;
  
  CLOSE emp_cur;
  
  IF v_count = 0 THEN 
    RAISE NO_DATA_FOUND;
  END IF; 
  
  EXCEPTION 
    WHEN NO_DATA_FOUND THEN 
      DBMS_OUTPUT.PUT_LINE('No Employee records found.');
      
    WHEN OTHERS THEN 
      DBMS_OUTPUT.PUT_LINE('ERROR OCCURED: ' || SQLERRM);
  
END;
/
```

**Output:**

<img width="1919" height="989" alt="output" src="https://github.com/user-attachments/assets/71e9e210-cf6a-465b-8ef0-30f59dd362a4" />

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

**Program:**
```
CREATE TABLE Employee (emp_id INTEGER PRIMARY KEY, emp_name VARCHAR(40), designation VARCHAR(40), salary INTEGER);

INSERT INTO Employee VALUES (1, 'Ashqar', 'Kill', '13000');
INSERT INTO Employee VALUES (2, 'kumar', 'sales', '20000');
INSERT INTO Employee VALUES (3, 'Kali', 'manufacture', '32000');
INSERT INTO Employee VALUES (4, 'Bob', 'Receptionist', '15000');
INSERT INTO Employee VALUES (5, 'Karen', 'sales', '20000');

DECLARE
  CURSOR emp_cur(p_min NUMBER, p_max NUMBER) IS SELECT emp_name, designation, salary FROM Employee WHERE salary BETWEEN p_min AND p_max;
  
  v_name Employee.emp_name%TYPE;
  v_designation Employee.designation%TYPE;
  v_salary Employee.salary%TYPE;
  
  v_count NUMBER := 0;
BEGIN 
  OPEN emp_cur(15000,30000);
  
  LOOP
    FETCH emp_cur INTO v_name, v_designation, v_salary;
    EXIT WHEN emp_cur%NOTFOUND;
    v_count := v_count + 1;
    
    DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ' | designation: ' || v_designation || ' | salary: ' || v_salary);
  
  END LOOP;
  
  CLOSE emp_cur;
  
  IF v_count = 0 THEN 
    RAISE NO_DATA_FOUND;
  END IF; 
  
  EXCEPTION 
    WHEN NO_DATA_FOUND THEN 
      DBMS_OUTPUT.PUT_LINE('No Employee found in given salary range');
      
    WHEN OTHERS THEN 
      DBMS_OUTPUT.PUT_LINE('ERROR OCCURED: ' || SQLERRM);
  
END;
/
```

**Output:**

<img width="1916" height="927" alt="output" src="https://github.com/user-attachments/assets/61fecb4c-c316-43b6-8c43-0e848ce700d4" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

**Program:**
```
CREATE TABLE Employee (emp_Id INTEGER PRIMARY KEY, emp_Name VARCHAR(40), designation VARCHAR(40));

INSERT INTO Employee VALUES (1, 'Ashqar', 'Kill');
INSERT INTO Employee VALUES (2, 'kumar', 'sales');
INSERT INTO Employee VALUES (3, 'kali', 'manufacture');

DECLARE
  CURSOR emp_cur IS SELECT emp_name, designation FROM Employee;
  
  v_name Employee.emp_name%TYPE;
  v_designation Employee.designation%TYPE;
  
  v_count INTEGER := 0;
BEGIN 
  OPEN emp_cur;
    LOOP
      FETCH emp_cur INTO v_name, v_designation;
      EXIT WHEN emp_cur%NOTFOUND;
       v_count := v_count + 1;
      DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ' | designation: ' || v_designation);
     
    END LOOP;
  CLOSE Emp_cur;
  
  IF v_count = 0 then
    RAISE NO_DATA_FOUND;
  END IF;
  
  EXCEPTION 
    WHEN NO_DATA_FOUND then
      DBMS_OUTPUT.PUT_LINE('No Employee Records Found');
    WHEN OTHERS then
      DBMS_OUTPUT.PUT_LINE('Error occured: ' || SQLERRM);
      
END;
/
```

**Output:**

<img width="1919" height="989" alt="output" src="https://github.com/user-attachments/assets/3dfe2851-7615-45bb-8e56-844aba44a7d0" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Output:**  
The program should display employee records or the appropriate error message if no data is found.

**Program:**
```
CREATE TABLE Employee (Emp_Id INTEGER PRIMARY KEY, Emp_Name VARCHAR(40), Emp_dept VARCHAR(40));

INSERT INTO Employee VALUES (1, 'harrigton', 'IT');
INSERT INTO Employee VALUES (2, 'Stefan', 'ML');
INSERT INTO Employee VALUES (3, 'Ellise', 'Sales');

DECLARE
  CURSOR emp_cur IS SELECT * FROM Employee;
  
  Emp_row Employee%ROWTYPE;
  
  v_count INTEGER := 0;
BEGIN 
  OPEN emp_cur;
    LOOP
      FETCH emp_cur INTO v_name, v_designation;
      EXIT WHEN emp_cur%NOTFOUND;
       v_count := v_count + 1;
      DBMS_OUTPUT.PUT_LINE('ID : ' || Emp_row.Emp_Id || 'Name: ' || Emp_row.Emp_Name || ' | Department: ' || Emp_row.Emp_dept);
     
    END LOOP;
  CLOSE Emp_cur;
  
  IF v_count = 0 then
    RAISE NO_DATA_FOUND;
  END IF;
  
  EXCEPTION 
    WHEN NO_DATA_FOUND then
      DBMS_OUTPUT.PUT_LINE('No Employee Records Found');
    WHEN OTHERS then
      DBMS_OUTPUT.PUT_LINE('Error occured: ' || SQLERRM);
      
END;
/
```

**Ouptut:**


<img width="1918" height="988" alt="output" src="https://github.com/user-attachments/assets/83420e1c-5f73-4fc3-a837-f1c36cf36002" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

