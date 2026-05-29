# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

<img width="581" height="686" alt="image" src="https://github.com/user-attachments/assets/c2ec5d61-43a5-49d5-bcbd-1742a67a7af0" />

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**

<img width="965" height="543" alt="image" src="https://github.com/user-attachments/assets/261c4476-4387-4bb4-8ca2-8b9d10e47a45" />


**Question 2**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="800" height="555" alt="image" src="https://github.com/user-attachments/assets/3452f001-1213-47ae-a6a9-366c1a2a88e6" />


```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**

<img width="571" height="382" alt="image" src="https://github.com/user-attachments/assets/6bcc46d0-52ae-439b-8fdc-cd8394f3cef9" />


**Question 3**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)
<img width="739" height="177" alt="image" src="https://github.com/user-attachments/assets/40d29ea7-9e33-46b3-9a16-957cfeb848d6" />

```sql
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);

```

**Output:**

<img width="669" height="370" alt="image" src="https://github.com/user-attachments/assets/fb5c6a63-4ed2-4099-bf46-116c4e044881" />


**Question 4**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

<img width="460" height="524" alt="image" src="https://github.com/user-attachments/assets/4ed9f0d8-ac5f-4662-b778-115f83314c31" />

```sql
SELECT *
FROM customer
WHERE customer_id = (
    SELECT salesman_id - 2001
    FROM salesman
    WHERE name = 'Mc Lyon'
);

```

**Output:**
<img width="991" height="303" alt="image" src="https://github.com/user-attachments/assets/bcad064a-8911-4ddf-acf4-8a0fbac0b1e9" />

**Question 5**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

<img width="354" height="548" alt="image" src="https://github.com/user-attachments/assets/50cb240c-e43c-4e87-9ab2-632a74563c83" />


```sql
SELECT ord_no, purch_amt, ord_date, salesman_id
FROM orders
WHERE salesman_id = (
    SELECT salesman_id
    FROM salesman
    WHERE commission = (SELECT MAX(commission) FROM salesman)
);


```

**Output:**

<img width="792" height="422" alt="image" src="https://github.com/user-attachments/assets/a678ef60-f78b-412d-9970-d04f54fd060a" />


**Question 6**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID
<img width="518" height="386" alt="image" src="https://github.com/user-attachments/assets/cc9bc178-2e36-4403-9831-7ef8c9b6ad19" />

```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);

```

**Output:**

<img width="1096" height="434" alt="image" src="https://github.com/user-attachments/assets/5241ac5a-212d-48e1-a0fd-0bd540520be1" />


**Question 7**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

<img width="452" height="382" alt="image" src="https://github.com/user-attachments/assets/3f5d622c-b5f4-4392-87ac-5ed33ceeb99f" />


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM orders
    WHERE ord_date = '2012-10-10'
);


```

**Output:**

<img width="974" height="428" alt="image" src="https://github.com/user-attachments/assets/bd6fbc8f-5b5f-4328-bd38-a558f2fb425f" />


**Question 8**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

<img width="505" height="456" alt="image" src="https://github.com/user-attachments/assets/4922f0f9-b8ba-4448-850f-4d9fa3f62f03" />


```sql
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**

<img width="1099" height="457" alt="image" src="https://github.com/user-attachments/assets/cd0bf7c1-f37e-4d4c-97f3-23845b876289" />


**Question 9**
---From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

<img width="449" height="557" alt="image" src="https://github.com/user-attachments/assets/dbfb8175-2a4c-4f82-9016-46eaf1e299ab" />


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE salesman_id IN (
    SELECT salesman_id
    FROM salesman
    WHERE city = 'New York'
);

```

**Output:**

<img width="983" height="410" alt="image" src="https://github.com/user-attachments/assets/024531f6-c6d5-4284-91d9-91a0b417cb26" />


**Question 10**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

<img width="450" height="505" alt="image" src="https://github.com/user-attachments/assets/8aaeeea9-6324-41a3-b761-5e250c28c174" />

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE salesman_id IN (
    SELECT salesman_id
    FROM salesman
    WHERE city = 'London'
);

```

**Output:**

<img width="978" height="371" alt="image" src="https://github.com/user-attachments/assets/ba2bb856-2b00-4fce-bf82-aed3893a67d2" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
