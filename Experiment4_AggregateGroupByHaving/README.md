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
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits
```
name        type

----------  ----------

id          INTEGER

name        TEXT

unit        TEXT

inventory   INTEGER

price       REAL
```
```sql
SELECT MAX(price) - MIN(price) AS price_diff
FROM fruits;
```

**Output:**

![image](https://github.com/user-attachments/assets/7f8da42c-3ef2-45bf-a16b-764da79e9fb8)


**Question 2**
---
Write a SQL query to find  how many employees work in California?
```
Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```
```sql
SELECT COUNT(*) AS employees_in_california
FROM employee
WHERE city='California';
```

**Output:**

![image](https://github.com/user-attachments/assets/3a5232e4-f493-4781-b849-66020585af62)


**Question 3**
---
Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1
![image](https://github.com/user-attachments/assets/8b9bc3b7-7609-47f7-b734-48ff166000d4)


```sql
SELECT SUM(workhour) AS "Total working hours"
FROM employee1;
```

**Output:**

![image](https://github.com/user-attachments/assets/39a0976f-7924-4f5a-947c-f3b1d6bd244b)


**Question 4**
---
How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table
![image](https://github.com/user-attachments/assets/07171251-5604-404e-a7c6-50cfa4b5b974)


```sql
SELECT Specialty, Gender, COUNT(*) AS TotalDoctors
FROM Doctors
GROUP BY Specialty, Gender;
```

**Output:**

![image](https://github.com/user-attachments/assets/84c1fb2f-f469-40a1-8a90-35ee714190b8)


**Question 5**
---
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table
![image](https://github.com/user-attachments/assets/585377e8-d567-4247-a05b-570a8886b7a8)


```sql
SELECT Medication, AVG(Dosage) AS AvgDosage
FROM Prescriptions
GROUP BY Medication;
```

**Output:**

![image](https://github.com/user-attachments/assets/e61137a4-ddbb-453b-9c2a-dc554fc8a61f)


**Question 6**
---
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table
![image](https://github.com/user-attachments/assets/718c6c2c-5eeb-439d-a4de-7e12e0f96ebe)


```sql
SELECT Frequency, COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY Frequency;
```

**Output:**

![image](https://github.com/user-attachments/assets/593f876c-3a19-4da9-ac84-9976fda41d33)


**Question 7**
---
Write a SQL query to find the customer with longest name?

Table: customer
```
name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
```
```sql
select name,length(name) as length
from customer
order by length(name) desc limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/4aa34bb3-f132-4df6-825b-353bbf8b49c3)


**Question 8**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.
Sample table: employee

![image](https://github.com/user-attachments/assets/1be1bbb1-bbbc-4e3a-8f59-5290dabe8bf9)


```sql
Select age,min(income) as "MIN(income)"
from employee
group by age
having min(income)<400000;
```

**Output:**

![image](https://github.com/user-attachments/assets/369d2d76-9275-433e-b56b-8abf5ab5dd43)


**Question 9**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1
![image](https://github.com/user-attachments/assets/53ec6678-1206-4582-bee4-43f0a75c84d7)


```sql
select occupation, min(workhour) as "MIN(workhour)"
from employee1
group by occupation 
having min(workhour)>8;
```

**Output:**

![image](https://github.com/user-attachments/assets/f2138f40-b64d-4b13-93bb-ac3581031903)


**Question 10**
---
How many prescriptions were written for each medication?

Sample tablePrescriptions Table

![image](https://github.com/user-attachments/assets/b82a6394-a33f-4962-867d-116446d46e01)


```sql
SELECT medication AS Medication, COUNT(*) AS TotalPrescriptions
FROM prescriptions
GROUP BY medication;
```

**Output:**

![image](https://github.com/user-attachments/assets/eaaa5887-826d-4d79-b72d-261f897de349)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
