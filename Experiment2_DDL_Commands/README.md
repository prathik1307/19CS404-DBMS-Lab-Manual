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
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700

```
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT CHECK(LENGTH(icom_id) = 4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE SET NULL
        ON DELETE SET NULL
);

```

**Output:**
![Output1]
<img width="1535" height="547" alt="Screenshot 2025-09-29 133840" src="https://github.com/user-attachments/assets/39672f1b-7c4b-45ce-a90a-6f99cb563bd3" />


**Question 2**
---
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values.    
For example:

Test	Result
SELECT EmployeeID, Name, Position 
FROM Employee;
EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst


```
INSERT INTO Employee (EmployeeID, Name, Position)
VALUES (4, 'Emily White', 'Analyst');

```

**Output:**

![Output2]
<img width="1473" height="465" alt="Screenshot 2025-09-29 134129" src="https://github.com/user-attachments/assets/e6d08f6d-31a4-49e8-9148-87b8b3b23e29" />


**Question 3**
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
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-0

```
CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK (Amount > 0),
    DueDate DATE,
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    CHECK (DueDate > InvoiceDate)
);

```

**Output:**

![Output3]
<img width="1516" height="479" alt="Screenshot 2025-09-29 134314" src="https://github.com/user-attachments/assets/56bb3106-b861-49e6-ab7f-b1a96434d769" />


**Question 4**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0
```
ALTER TABLE customer
ADD discount DECIMAL(5,2);

```

**Output:**

![Output4]
<img width="1672" height="599" alt="Screenshot 2025-09-29 134437" src="https://github.com/user-attachments/assets/90c7713f-7383-4611-a514-4338623bf8f2" />

**Question 5**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	Result
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;
AttendanceID  EmployeeID  AttendanceDate  Status
------------  ----------  --------------  ----------
1             1           2024-08-01      Present


```
CREATE TABLE Attendance (
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present', 'Absent', 'Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);

```

**Output:**

![Output5]
<img width="1682" height="456" alt="Screenshot 2025-09-29 134738" src="https://github.com/user-attachments/assets/4f39e782-617d-4963-88c0-e5ac40b2539d" />


**Question 6**
---
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER
For example:

Test	Result
pragma table_info('Products');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     ProductID   INTEGER     0                       0
1     ProductNam  TEXT        0                       0
2     Price       REAL        0                       0
3     Stock       INTEGER     0                       0


```
CREATE TABLE Products (
    ProductID INTEGER,
    ProductName TEXT,
    Price REAL,
    Stock INTEGER
);

```

**Output:**

![Output6]
<img width="1645" height="514" alt="Screenshot 2025-09-29 134913" src="https://github.com/user-attachments/assets/91bfbf02-695b-4972-aa0c-b909cd727cd2" />


**Question 7**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 

For example:

Test	Result
SELECT * FROM Products;
ProductID   Name             Category    Price       Stock
----------  ---------------  ----------  ----------  ----------
106         Fitness Tracker  Wearables
107         Laptop           Electronic  999.99      50
108         Wireless Earbud  Accessorie              100
```
INSERT INTO Products (ProductID, Name, Category)
VALUES (106, 'Fitness Tracker', 'Wearables');


INSERT INTO Products (ProductID, Name, Category, Price, Stock)
VALUES (107, 'Laptop', 'Electronics', 999.99, 50);


INSERT INTO Products (ProductID, Name, Category, Stock)
VALUES (108, 'Wireless Earbuds', 'Accessories', 100);

```

**Output:**

![Output7]
<img width="1652" height="501" alt="Screenshot 2025-09-29 135018" src="https://github.com/user-attachments/assets/18153a41-8d47-41ba-b15e-085e8d08a8aa" />

**Question 8**
---
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
6           DOB         Date        0                       0

```
ALTER TABLE Companies
RENAME COLUMN name TO first_name;


ALTER TABLE Companies
ADD mobilenumber number;


ALTER TABLE Companies
ADD DOB Date;


```

**Output:**

![Output8]
<img width="1618" height="613" alt="Screenshot 2025-09-29 135128" src="https://github.com/user-attachments/assets/6808e1dd-9be6-466f-b8f3-8003b6df1816" />

**Question 9**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5


```
INSERT INTO Products (ProductID, ProductName, Price, Stock)
SELECT ProductID, ProductName, Price, Stock
FROM Discontinued_products;

```

**Output:**

![Output9]
<img width="1627" height="493" alt="Screenshot 2025-09-29 135230" src="https://github.com/user-attachments/assets/99b13e78-b4a9-4618-8d8b-daced97156de" />

**Question 10**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
ProductID   ProductName  Price       StockQuantity
----------  -----------  ----------  -------------
1           Laptop       999.99      10


```
CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT UNIQUE NOT NULL,
    Price REAL CHECK (Price > 0),
    StockQuantity INTEGER CHECK (StockQuantity >= 0)
);

```

**Output:**

![Output10]
<img width="1638" height="472" alt="Screenshot 2025-09-29 135330" src="https://github.com/user-attachments/assets/322c8e96-10de-498a-9497-38f19d2e4aa9" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
