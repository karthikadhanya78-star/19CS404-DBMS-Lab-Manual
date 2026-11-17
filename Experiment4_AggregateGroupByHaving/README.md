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
How many medical records does each doctor have?

Sample table:MedicalRecords Table
<img width="952" height="138" alt="image" src="https://github.com/user-attachments/assets/0846c733-dbaf-4fa1-9631-1f4fef2f5c73" />



For example:

Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3

```sql
SELECT DoctorID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY DoctorID
ORDER BY DoctorID;
```

**Output:**

<img width="472" height="632" alt="image" src="https://github.com/user-attachments/assets/9e4f26ec-fa10-406d-b1f1-68f8b0c9a5f3" />

**Question 2**
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3

```sql
SELECT PatientID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID
ORDER BY PatientID;
```

**Output:**

<img width="546" height="628" alt="image" src="https://github.com/user-attachments/assets/f8728948-300c-4495-a8d7-24dcc8e09f18" />


**Question 3**
---
What is the total number of appointments scheduled for each day?

Table: Appointments

name                 type
-------------------  ----------
AppointmentID        INTEGER
PatientID            INTEGER
DoctorID             INTEGER
AppointmentDateTime  DATETIME
Purpose              TEXT
Status               TEXT
 

For example:

Result
AppointmentDate  TotalAppointments
---------------  -----------------
2024-02-16       4
2024-02-18       1
2024-02-20       1
2024-02-21       1
2024-02-22       1
2024-02-23       2

```sql
SELECT DATE(AppointmentDateTime) AS AppointmentDate,
       COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY AppointmentDate;
```
**Output:**

<img width="650" height="646" alt="image" src="https://github.com/user-attachments/assets/ff05c16c-9d84-47e3-b35c-c38fcb6a2463" />


**Question 4**
---
Write a SQL query to find the youngest employee in the company?

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
Employee_Name  Age
-------------  ----------
Peter          32


```sql
SELECT name AS Employee_Name, age AS Age
FROM employee
ORDER BY age ASC
LIMIT 1;
```

**Output:**

<img width="476" height="390" alt="image" src="https://github.com/user-attachments/assets/6d81742b-780c-4c38-97f4-decb37eea9a6" />


**Question 5**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer

<img width="825" height="176" alt="image" src="https://github.com/user-attachments/assets/a2efd820-4554-4142-ba3b-6c18f353e05b" />


For example:

Result
COUNT
----------
1

```sql
SELECT COUNT(*) AS "COUNT"
FROM customer
WHERE city = 'Noida';
```

**Output:**

<img width="311" height="391" alt="image" src="https://github.com/user-attachments/assets/53ef2e12-bf3f-4645-9805-4c6f09a64dc2" />


**Question 6**
---
Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MAXIMUM
----------
5760.0


```sql
SELECT MAX(purch_amt) AS "MAXIMUM"
FROM orders;
```

**Output:**

<img width="346" height="386" alt="image" src="https://github.com/user-attachments/assets/4e2ebb11-c7eb-4409-809e-789429595bb9" />


**Question 7**
---
Write a SQL query to find the customer with longest name?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name          length
------------  ----------
Preeti Patel  12


```sql
SELECT name, LENGTH(name) AS length
FROM customer
ORDER BY LENGTH(name) DESC
LIMIT 1;
```

**Output:**

<img width="500" height="396" alt="image" src="https://github.com/user-attachments/assets/3fb3bbc5-7d10-4ad1-a99b-eb7f4b944b88" />


**Question 8**
---
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

```sql
SELECT PatientID, COUNT(RecordID) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(RecordID) > 3;
```

**Output:**

<img width="447" height="402" alt="image" src="https://github.com/user-attachments/assets/44d41b09-1239-42a7-b07a-17dc9ccb0051" />

**Question 9**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.

Sample table: customer1

<img width="831" height="137" alt="image" src="https://github.com/user-attachments/assets/ff84550e-5210-421c-adfa-a524ab02b35b" />

For example:

Result
age_group   SUM(salary)
----------  -----------
20          16500
25          16500

```sql
SELECT (age / 5) * 5 AS age_group, SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY (age / 5) * 5
HAVING SUM(salary) > 5000;
```

**Output:**

<img width="466" height="412" alt="image" src="https://github.com/user-attachments/assets/abf768da-563b-4945-83c7-dd52764b69ab" />


**Question 10**
---
Write the SQL query that achieves the selection of product names and the maximum price for each category from the "products" table, and includes only those products where the maximum price is greater than 15.

Sample table: products
<img width="767" height="167" alt="image" src="https://github.com/user-attachments/assets/9d1eb711-c156-4c41-b401-faaa4dda28f0" />

For example:

Result
category_id  product_name  Price
-----------  ------------  ----------
1            Orange        15.5
2            Monitor       25

```sql
SELECT category_id, product_name, Price
FROM products p
WHERE Price = (
    SELECT MAX(Price)
    FROM products
    WHERE category_id = p.category_id
)
AND Price > 15;
```

**Output:**

<img width="687" height="332" alt="image" src="https://github.com/user-attachments/assets/20a17c97-59a3-4db4-9406-39607d6bcbfb" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
