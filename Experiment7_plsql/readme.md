# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

## Program:

```
DECLARE
  a int := 124;
  b int := 395;
BEGIN 
  if(a>b) THEN
    dbms_output.put_line('The Greater value is :'|| a); 
  else
    dbms_output.put_line('The Greater value is :'|| b);
  END if;
END;

```
## Output:

<img width="1919" height="495" alt="q1" src="https://github.com/user-attachments/assets/d66bfeae-101c-4218-841b-db0f10e3cea6" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

## Program:

```
DECLARE
  S int := 0;
  n int := 20;
  
BEGIN 
  WHILE n>=0 LOOP
    S := S + n;
    n := n - 1; 
  END LOOP;
  dbms_output.put_line('The sum of n natural numbers is : ' || S);
END;
```

## Output:

<img width="1909" height="468" alt="q2" src="https://github.com/user-attachments/assets/a183c803-43c3-453b-be99-445642cdb5d0" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

## Program:

```
DECLARE
  a int := 0;
  b int := 1;
  i int := 12;
  c int;
BEGIN 
  dbms_output.put_line(a);
  dbms_output.put_line(b);
  LOOP
  EXIT WHEN i=0;
    c := a + b;
    dbms_output.put_line(c);
    a := b;
    b := c;
    i := i - 1;
  END LOOP;
END;
```

## Output:

<img width="1919" height="602" alt="q2" src="https://github.com/user-attachments/assets/baa9657e-a84b-4bbc-befe-53c2de78b5cd" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

## Program:

```
DECLARE
  a int := 811;
  r int := 0;
  t int;
BEGIN 
  WHILE a > 0 LOOP
    t := MOD(a,10);
    r := r * 10 + t;
    a := FLOOR(a/10);
  END LOOP;
  dbms_output.put_line('The Reversed Number is: ' || r);
END;
```

## Output:

<img width="1919" height="373" alt="q4" src="https://github.com/user-attachments/assets/8e94b67b-f209-43e2-81f6-95686dde3368" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

## Program:

```
DECLARE
  a int := 811;
  b int := 203;
  c int := 1600;
BEGIN 
  IF (a>b AND a>c) then
    dbms_output.put_line('The Greatest value is : ' || a);
  ELSIF (b>c) then
    dbms_output.put_line('The Greates value is : ' || b);
  else
    dbms_output.put_line('The Greatest value is : ' || c);
  END IF;
END;
```

## Output:

<img width="1919" height="464" alt="q5" src="https://github.com/user-attachments/assets/57c4d0ac-cf68-428a-a161-3ce3f0a5ba30" />

---
## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

