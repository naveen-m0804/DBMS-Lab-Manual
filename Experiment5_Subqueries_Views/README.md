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
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE
```
name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int
```
### Code:
```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM ORDERS o
JOIN SALESMAN s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**

![image](https://github.com/user-attachments/assets/630468aa-e225-47c7-9ab7-4b3e32c0e464)


**Question 2**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES

![image](https://github.com/user-attachments/assets/75bd1081-513f-47a8-a57f-59f6cddac0ed)

### Code:
```sql
SELECT g.student_name, g.grade
FROM GRADES g
WHERE g.grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**

![image](https://github.com/user-attachments/assets/aec676cd-4eb7-46ff-884e-77d4edefe5e2)


**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS
```
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```
### Code:
```sql
SELECT * FROM CUSTOMERS
WHERE salary > 4500;
```

**Output:**

![image](https://github.com/user-attachments/assets/a8e7a81b-cc08-415b-9122-124b5b3d4c5d)


**Question 4**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES


![image](https://github.com/user-attachments/assets/717f856f-60ad-4296-b67c-3d7863b7166b)

### Code:
```sql
SELECT g.student_id, g.student_name, g.subject, g.grade
FROM GRADES g
WHERE g.grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**

![image](https://github.com/user-attachments/assets/750605f2-fee3-4847-a506-7f8626c54b57)

**Question 5**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table
```
name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER
```
### Code:
```sql
SELECT id, name, age, city, income
FROM employee
WHERE age < (
    SELECT AVG(age)
    FROM employee
    WHERE income > 1000000
);
```

**Output:**

![image](https://github.com/user-attachments/assets/e8ef7737-fc02-44ab-8318-8bd15201b890)


**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS
```
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```
### Code:
```sql
SELECT *
FROM customers
WHERE salary < 2500;
```

**Output:**

![image](https://github.com/user-attachments/assets/6266fc44-07f5-447e-83bb-058b27ca3158)


**Question 7**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi
```
Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000
```
### Code:
```sql
SELECT * FROM customers
WHERE address = 'Delhi';
```

**Output:**

![image](https://github.com/user-attachments/assets/8e17c578-339a-4085-a278-647b661e8b86)


**Question 8**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Medications Table

![image](https://github.com/user-attachments/assets/34a4cdc3-e032-46c9-a82a-7b4685e8051b)

### Code:
```sql
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
  SELECT MAX(dosage)
  FROM Medications);
```

**Output:**

![image](https://github.com/user-attachments/assets/eafb533c-b6fc-4a34-9d87-54888a74b2d7)


**Question 9**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer
```
name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```
### Code:
```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/646cd1a7-1d05-4417-9b87-8e40bf24b0f3)


**Question 10**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES
![image](https://github.com/user-attachments/assets/87e1d353-0854-4774-ae77-b581cd9e87cf)

### Code:
```sql
SELECT student_id, student_name, subject, grade
FROM grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM grades
    WHERE subject = g.subject
);
```

**Output:**

![image](https://github.com/user-attachments/assets/7166b982-7e3f-4888-a35f-6d7ef46af2b8)



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
