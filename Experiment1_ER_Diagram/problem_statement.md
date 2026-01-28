# ER Diagram Workshop – Submission Template
```
Name: Ashqar Ahamed S.T
Reg.No: 212224240018
```

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="1536" height="1024" alt="Scenario1(2)" src="https://github.com/user-attachments/assets/fe816369-7df4-42bd-9015-2e9a159aef70" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|  Member      |member_id, Name, Membership_type, Start Date            |   Tracks members   |
|   Trainer |          Trainer_Id, Name, Specialization          |   Records Details of Trainers    |
| Program  |      Program_ID (PK), Program_Name, Type              | Yoga, Zumba, Weight Training      |
| Session    |      Session_ID (PK), Member_ID (FK), Trainer_ID (FK), Date, Time	  |  For presonal training sessions    |
| Attendance  |   Attendance_ID (PK), Session_ID (FK), Status (Present/Absent)	      | Records session attendance  |
|  Payment     | Payment_ID (PK), Member_ID (FK), Amount, Peyment_method, Payment_date      | Records all the payments  |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|    Member - Program      |      M:N      |       Partial        |    Many members can join many programs   |
|      Trainer - Program        |     1:M       |  Total             | A trianer can facilitate many programs      |
|    Member - Payment |    1:M       |        Total       |  A member can make multiple Payments     |

### Assumptions
- A Member can attend multiple Programs
- A trainer may take multiple or one programs
- Payment may vary depending on the Membership Type

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="711" height="817" alt="Scenario2" src="https://github.com/user-attachments/assets/a2b196cd-a683-4324-a9fa-6b579b57e2e0" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|Members |     Member_ID (PK), Name, Address, Email, Phone_No |  Library Members     |
|Book | BookID (PK), Title, Author, Category, ISBN, PubYear | Books in collection      |
| Loan       |  LoanID (PK), LoanDate, DueDate, ReturnDate, FineAmount, MemberID (FK), BookID (FK)                  |    Tracks Book's Borrowing   |
|   Event     |   EventID (PK), Name, Description, EventDate, StartTime, EndTime, RoomID (FK)                 |   Library Events    |
|  Speaker      |     SpeakerID (PK), Name, Bio, ContactInfo               |  Event speakers/authors     |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|Member–Book |  M:N |  Mandatory for Loan, Optional for Member/Book             | Members borrow books      |
|   Member–Event           | 	M:N           |  Mandatory for Registration, Optional for Member/Event             | Members register for events      |
|   Event–Speaker           |   	M:N         |    Mandatory for EventSpeaker, Optional for Event/Speaker           |  Events may have multiple speakers     |
| Room–Booking | 1:N | Mandatory for Booking, Optional for Room | Rooms booked for study by members |

### Assumptions
- Overdue fines are stored per Loan record.
- BookCopy not modeled
- Rooms serve both events and study bookings.
---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="1255" height="758" alt="Scenario3" src="https://github.com/user-attachments/assets/3f4c47cb-adc8-4a9c-ade7-bdd6ac0e827d" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Chef       |  Chef_id (PK), Chef_name, Chef_salary                  |  Each chef is uniquely identified by Chef_id. Prepares meals.     |
| Meal       | meal_name (PK), meal_price                   | 	A meal is prepared by chefs, ordered by customers, and consists OF ingredients.      |
| Ingredients       | 	ing_name (PK), description                   | 	Each ingredient has a unique name and is linked to meals.      |
| Customers       |   cust_phone (PK), cust_name, cust_address                 |  	Customers place orders for meals.     |
|  Supplier     |     	S_id (PK), S_name, S_city               |  	Suppliers attend to customers.     |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|   Chef - Meal           |   1:N         |  	CHEF (total), MEAL (partial)             |   One chef can prepare many meals, but a meal is prepared by one chef.    |
|      Customers - Meal        |      M:N      |   Both Partial            |   A customer can order many meals    |
|     Meal - Ingridients         |    M:N          |    Both Parital           | Each meal consists of multiple ingredients, and each ingredient can be part of many meals.      |

### Assumptions
- Each chef can prepare multiple meals, but a meal is prepared by only one chef
-  A customer can place multiple orders, and each order may include one or more meals
- Each meal consists of one or more ingredients, and an ingredient may be used in multiple meals.

---

### Result
Hence, ER diagram for three scenarios are created successfully. 
<!--
## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
-->
