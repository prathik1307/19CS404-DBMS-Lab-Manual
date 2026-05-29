# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**

Write an SQL query that retrieves all columns from the 'customer' table (using the alias 'c'), performs a LEFT JOIN with the 'orders' table on the 'customer_id' column, and includes only those orders with an order date after '2012-08-17'


```sql
SELECT c.customer_id, c.cust_name, c.city, c.grade, c.salesman_id
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';
```

**Output:**

<img width="1183" height="680" alt="image" src="https://github.com/user-attachments/assets/8da62941-77c0-4d04-ad07-c6fd9a04a053" />


**Question 2**
---
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

```sql
SELECT p.date_of_birth, a.appointment_id, a.patient_id, a.doctor_id, a.appointment_date
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**

<img width="1280" height="354" alt="image" src="https://github.com/user-attachments/assets/e7c70d75-74d4-4581-96cd-f075aa2053ff" />


**Question 3**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

```sql
SELECT o.ord_no, o.ord_date, o.purch_amt, c.cust_name AS "Customer Name", 
       c.grade, s.name AS "Salesman", s.commission
FROM orders o
INNER JOIN customer c ON o.customer_id = c.customer_id
INNER JOIN salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1224" height="782" alt="image" src="https://github.com/user-attachments/assets/3ed00245-dc8a-49fb-96a9-8fb0a97e97f4" />


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'.

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id
WHERE (t.test_name = 'Blood Test' OR t.test_name = 'Blood Pressure')
  AND t.result NOT LIKE '%Normal%';

```

**Output:**

<img width="1318" height="289" alt="image" src="https://github.com/user-attachments/assets/cc563c28-21dc-4658-9a02-faba40fcc0f2" />


**Question 5**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.


```sql
SELECT o.ord_no, o.purch_amt, c.cust_name, c.city
FROM orders o
INNER JOIN customer c ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

<img width="829" height="329" alt="image" src="https://github.com/user-attachments/assets/fead4958-cbcd-43d1-8058-cad8a6ac5ac9" />


**Question 6**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-01-01' and '2024-01-31'.

```sql
SELECT p.*
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="1312" height="287" alt="image" src="https://github.com/user-attachments/assets/fd221d1b-3a1d-4c37-bbda-cd61937e76b8" />


**Question 7**
---
From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

```sql
SELECT c.cust_name AS "Customer Name", c.city, s.name AS "Salesman", s.commission
FROM customer c
INNER JOIN salesman s ON c.salesman_id = s.salesman_id;

```

**Output:**

<img width="1115" height="813" alt="image" src="https://github.com/user-attachments/assets/5921329e-666b-40c0-bf1c-69ecfc54d550" />


**Question 8**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.

```sql
SELECT s.name
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE c.city = 'London';

```

**Output:**

<img width="352" height="455" alt="image" src="https://github.com/user-attachments/assets/d0e25c17-92f2-4dc4-b3b4-514bbf57d58a" />


**Question 9**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, 
       c.cust_name, c.city AS customer_city, c.grade, 
       s.name AS salesman_name, s.city AS salesman_city, s.commission
FROM orders o
INNER JOIN customer c ON o.customer_id = c.customer_id
INNER JOIN salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1197" height="588" alt="image" src="https://github.com/user-attachments/assets/3288976f-6cdb-40bd-add3-d20b992b122b" />


**Question 10**
---
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount"
FROM customer c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
ORDER BY o.ord_date ASC;
```

**Output:**

<img width="1179" height="872" alt="image" src="https://github.com/user-attachments/assets/491a7e04-c9d2-4f0d-b988-6c12fd6a2e18" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

