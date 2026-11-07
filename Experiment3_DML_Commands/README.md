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
Write a query to fetch details of all employees excluding the employees with first names, “Sanjay” and “Sonia” from the EmployeeInfo table.
EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F



For example:

Result
EmpID       EmpFname    EmpLname    Department  Project     Address     DOB         Gender
----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
2           Ananya      Mishra      Admin       P2          Delhi(DEL)  1968-05-02  F
3           Rohan       Diwan       Account     P3          Mumbai(BOM  1980-01-01  M
5           Ankit       Kapoor      Admin       P2          Delhi(DEL)  1994-07-03  M


```sql
SELECT *
FROM EmployeeInfo
WHERE EmpFname NOT IN ('Sanjay', 'Sonia');
```

**Output:**

<img width="1735" height="355" alt="Screenshot 2026-11-06 182053" src="https://github.com/user-attachments/assets/138b30f3-d329-4edb-86cd-9891e77b2a38" />


**Question 2**
---
Question text
Write a SQL query to Concatenate the first three characters of the employee's name with the last three characters of their job title.

Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT
For example:

Result
ename       job         ConcatenatedString
----------  ----------  ------------------
KING        PRESIDENT   KINENT
SCOTT       ANALYST     SCOYST
FORD        ANALYST     FORYST
JAMES       CLERK       JAMERK
MILLER      CLERK       MILERK

```sql
SELECT ename,
       job,
       SUBSTR(ename, 1, 3) || SUBSTR(job, -3) AS ConcatenatedString
FROM emp;

```

**Output:**

<img width="826" height="656" alt="image" src="https://github.com/user-attachments/assets/fe670ef3-4d6e-4bea-a3b5-4e889c82bdd8" />


**Question 3**
---
Write a query to list all products that have a discounted price between $100 and $250. Return product_id, original_price, discount_percentage, and discounted_price from products table.

 

For example:

Result
product_id  original_price  discount_percentage  discounted_price
----------  --------------  -------------------  ----------------
102         150.0           0.15                 127.5
103         200.0           0.2                  160.0
104         300.0           0.25                 225.0

```sql
SELECT product_id,
       original_price,
       discount_percentage,
       original_price * (1 - discount_percentage) AS discounted_price
FROM products
WHERE original_price * (1 - discount_percentage) BETWEEN 100 AND 250;
```

**Output:**

<img width="1237" height="333" alt="image" src="https://github.com/user-attachments/assets/2b4f69de-189c-4906-abca-b11d45f97814" />


**Question 4**
---
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

```sql
SELECT patient_id,
       first_name,
       admission_date
FROM Patients
WHERE admission_date BETWEEN '2023-01-01' AND '2023-12-31';
```

**Output:**

<img width="741" height="412" alt="image" src="https://github.com/user-attachments/assets/6d4cd1e4-22ad-40b6-9845-3cb78d048640" />


**Question 5**
---
Write a SQL query that displays order number, purchase amount, and the achieved and unachieved percentage (%) of target for those orders that exceed 50% of the target value of 6000.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
For example:

Result
ord_no      purch_amt   Achieved %  Unachieved %
----------  ----------  ----------  ------------
70008       5760.0      96.0        4.0
70013       3045.6      50.76       49.24

```sql
SELECT ord_no,
       purch_amt,
       ROUND((purch_amt / 6000) * 100, 2) AS "Achieved %",
       ROUND(100 - (purch_amt / 6000) * 100, 2) AS "Unachieved %"
FROM orders
WHERE purch_amt > 3000;
```

**Output:**

<img width="892" height="495" alt="image" src="https://github.com/user-attachments/assets/e4277675-c016-4078-bd15-ea8d04b600f2" />

**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is greater than or equal to 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
1
0

```sql
DELETE FROM customer
WHERE GRADE >= 2;
```

**Output:**

<img width="570" height="602" alt="image" src="https://github.com/user-attachments/assets/eacd9030-b6d7-413a-b1d1-cc162fa187f2" />


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

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
14

```sql
DELETE FROM customer
WHERE GRADE % 2 <> 0;
```

**Output:**

<img width="1897" height="482" alt="image" src="https://github.com/user-attachments/assets/f8bd1436-7028-4217-ade2-6de1437e10ac" />


**Question 8**
---
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.

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
SELECT EMPLOYEE_ID,FIRST_NAME,EMAIL FROM EMPLOYEES LIMIT 2;
EMPLOYEE_ID  FIRST_NAME  EMAIL
-----------  ----------  -----------
100          Steven      Unavailable
101          Neena       Unavailable


```sql
UPDATE Employees
SET email = 'Unavailable';
```

**Output:**

<img width="1245" height="497" alt="image" src="https://github.com/user-attachments/assets/6f5c7f0b-fc70-4378-9397-f8d87b5475b6" />


**Question 9**
---
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
For example:

Test	Result
SELECT*FROM Products WHERE supplier_id = 10;
product_id  product_name      category    cost_price  sell_price  reorder_lvl  quantity    supplier_id
----------  ----------------  ----------  ----------  ----------  -----------  ----------  -----------
6           Detergent Powder  Snacks      60          80          20           40          10
7           Surf Excel Deter  Snacks      85          100         10           40          10
8           Detergent Ariel   Items       85          100         10           40          10
product_id  product_name      category    cost_price  sell_price  reorder_lvl  quantity    supplier_id
----------  ----------------  ----------  ----------  ----------  -----------  ----------  -----------
6           Detergent Powder  Snacks      60          81          20           40          10
7           Surf Excel Deter  Snacks      85          114         10           40          10
8           Detergent Ariel   Items       85          114         10           40          10

```sql
UPDATE Products
SET sell_price = CAST(cost_price * 1.35 AS INT)
WHERE (sell_price - cost_price) / sell_price < 0.30;
```

**Output:**

<img width="1865" height="467" alt="image" src="https://github.com/user-attachments/assets/f453426e-1927-45c6-a3f2-5efc95608098" />

**Question 10**
---
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15

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
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE job_id = 'SA_REP' AND EMAIL='updated' LIMIT 5;
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
150          Peter       updated     10500       SA_REP
151          David       updated     10000       SA_REP
152          Peter       updated     9500        SA_REP
153          Christophe  updated     8500        SA_REP
154          Nanette     updated     8000        SA_REP

```sql
UPDATE Employees
SET salary = salary + 500,
    email = 'updated'
WHERE job_id = 'SA_REP'
  AND commission_pct > 0.15;
```

**Output:**
<img width="1790" height="531" alt="image" src="https://github.com/user-attachments/assets/5ac1bb1f-d1a6-47d1-819d-d9d1776cc1cf" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
