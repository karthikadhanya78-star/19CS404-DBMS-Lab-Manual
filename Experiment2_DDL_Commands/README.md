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
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5

```sql

CREATE TABLE item (
    item_id   TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate      INTEGER NOT NULL,
    icom_id   TEXT(4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
);

```

**Output:**

<img width="1417" height="417" alt="image" src="https://github.com/user-attachments/assets/9641a875-2315-4e92-9712-57eefd70f2da" />


**Question 2**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	Result
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;

```sql

CREATE TABLE jobs (
    job_id     INTEGER,
    job_title  VARCHAR(50) DEFAULT '',
    min_salary INTEGER DEFAULT 8000,
    max_salary INTEGER DEFAULT NULL
);

```

**Output:**

<img width="1870" height="402" alt="image" src="https://github.com/user-attachments/assets/d16ad3ec-124b-4462-adb0-b47ac682c047" />


**Question 3**
---
Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           first_name  varchar(50  0                       0
3           last_name   varchar(50  0                       0

```sql

ALTER TABLE employee
ADD COLUMN first_name varchar(50);

ALTER TABLE employee
ADD COLUMN last_name varchar(50);

```

**Output:**

<img width="1592" height="348" alt="image" src="https://github.com/user-attachments/assets/47e95488-fa06-4d04-904a-9456469ce968" />


**Question 4**
---
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
 

For example:

Test	Result
SELECT * FROM Customers;
CustomerID  Name          Address     City        ZipCode
----------  ------------  ----------  ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Mano  Gotham      10007
308         Peter Parker  Queens                  11375

```sql

INSERT INTO Customers (CustomerID, Name, Address)
VALUES (306, 'Diana Prince', 'Themyscira');

INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES (307, 'Bruce Wayne', 'Wayne Manor', 'Gotham', '10007');

INSERT INTO Customers (CustomerID, Name, Address, ZipCode)
VALUES (308, 'Peter Parker', 'Queens', '11375');

```

**Output:**

<img width="1297" height="355" alt="image" src="https://github.com/user-attachments/assets/c3b83fbf-dd6e-4ffb-8a37-50310ee958d4" />


**Question 5**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.Invoice

```sql
CREATE TABLE Invoices (
    InvoiceID   INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    DueDate     DATE,
    Amount      REAL,
    CHECK (DueDate > InvoiceDate),
    CHECK (Amount > 0)
);
```

**Output:**

<img width="1338" height="365" alt="image" src="https://github.com/user-attachments/assets/544cf79d-5088-4f3f-a8e7-f23575b0f7e7" />


**Question 6**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

For example:

Test	Result
SELECT * FROM Products WHERE ProductID = 101;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
101         Laptop      Electronics  1500        50

```sql
INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES (101, 'Laptop', 'Electronics', 1500, 50);
```

**Output:**

<img width="1513" height="295" alt="image" src="https://github.com/user-attachments/assets/a07de045-c1f8-4832-b9dc-b7a36463fbf1" />


**Question 7**
---
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           mobilenumb  number      0                       0
```sql
ALTER TABLE Student_details
ADD COLUMN mobilenumber number;
```

**Output:**

<img width="1625" height="396" alt="image" src="https://github.com/user-attachments/assets/7e4fee8d-94aa-4d18-a5fa-64940ac47918" />


**Question 8**
---
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

```sql
INSERT INTO Customers (CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email
FROM Old_customers;
```

**Output:**

<img width="1465" height="347" alt="image" src="https://github.com/user-attachments/assets/80ba9883-90f2-4eb0-9662-f1c383a19fc2" />


**Question 9**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT
For example:

Test	Result
pragma table_info('Departments');
cid    name             type        notnull     dflt_value  pk
-----  ---------------  ----------  ----------  ----------  ----------
0      DepartmentID     INTEGER     0                       0
1      DepartmentName   TEXT        0                       0


```sql
CREATE TABLE Departments (
    DepartmentID   INTEGER,
    DepartmentName TEXT
);
```

**Output:**
<img width="1623" height="428" alt="image" src="https://github.com/user-attachments/assets/9e48bdf5-2195-433d-a89e-3c2276a690f4" />


**Question 10**
---
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

```sql

CREATE TABLE Invoices (
    InvoiceID   INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount      REAL CHECK (Amount > 0),
    DueDate     DATE,
    OrderID     INTEGER,
    CHECK (DueDate > InvoiceDate),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

```

**Output:**

<img width="1882" height="352" alt="image" src="https://github.com/user-attachments/assets/8022eadf-f194-4a05-be25-8a60a3514872" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
