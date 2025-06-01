# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

**Question 1**
--

Write a SQL query to label rows in the Calculations table as 'Even' if value1 is even, otherwise 'Odd'.
```
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0

```

```sql
 SELECT id, value1,
    CASE 
        WHEN CAST(value1 AS INTEGER) % 2 = 0 THEN 'Even' 
        ELSE 'Odd' 
    END AS parity
FROM Calculations;
```

**Output:**

![image](https://github.com/user-attachments/assets/94ee9638-806f-42b4-8862-9e9f4639db1e)


**Question 2**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.
```
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```

```sql
DELETE FROM customer
WHERE GRADE % 2 = 1;

```

**Output:**

![image](https://github.com/user-attachments/assets/790e3195-8bfe-4bec-b28b-cbb0a2b0cd74)


**Question 3**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id
![image](https://github.com/user-attachments/assets/37264381-d019-43af-a015-487c7f269399)


```sql
UPDATE products SET reorder_lvl = 20 
WHERE quantity < 10 AND category = 'Snacks';
```

**Output:**
![image](https://github.com/user-attachments/assets/7e67d60a-431e-4bad-a38e-1a98813a45ac)


**Question 4**
---
write a SQL query to find customers who are either from the city 'New York' or who do not have a grade greater than 100. Return customer_id, cust_name, city, grade, and salesman_id.
```
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```
```sql
SELECT customer_id, cust_name, city, grade, salesman_id FROM customer
WHERE city = 'New York'
   OR NOT grade > 100;
```

**Output:**

![image](https://github.com/user-attachments/assets/8a3f20bf-71e7-439f-b8e3-03bad5be1b98)


**Question 5**
---
Write a SQL query to calculate the number of days between the hiredate and a specified date ('2024-12-31') for each employee using the JULIANDAY function from the emp table.
```
emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT   

```
```sql
SELECT ename, hiredate, JULIANDAY('2024-12-31') - JULIANDAY(hiredate) AS days_worked
FROM emp;
```

**Output:**

![image](https://github.com/user-attachments/assets/bf334db8-7546-4887-b418-4d231fc23f58)


**Question 6**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.   
![image](https://github.com/user-attachments/assets/714abfac-2d5f-4f46-a8d5-23b625c5e0e7)

```sql
UPDATE purchases
SET 
    per_unit_price = 25,
    total_price = quantity * 25
WHERE 
    purchase_date = '2022-08-15'
    AND product_id = 12;
```

**Output:**

![image](https://github.com/user-attachments/assets/59730d42-394b-46d9-9007-b5f625aa8762)

**Question 7**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_country' must be 'India',

2. 'cus_city' must not be 'Chennai',
```
Sample table: Customer
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```

```sql
DELETE FROM customer
WHERE cust_country = 'India'
  AND cust_city != 'Chennai';
```

**Output:**

![image](https://github.com/user-attachments/assets/9ce8986c-b12a-4a6f-a64c-2a1f9f12d520)


**Question 8**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -
```
1. 'cust_city' should begin with the letter 'L',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```
```sql
DELETE FROM customer
WHERE cust_city LIKE 'L%';
```

**Output:**

![image](https://github.com/user-attachments/assets/0976c1eb-e6b4-41df-b880-602a2439429c)

**Question 9**
---
Write a SQL query to locate the details of customers with grade values above 100. Return customer_id, cust_name, city, grade, and salesman_id.
```
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
```
```sql
select * from customer
where grade>100;
```

**Output:**

![image](https://github.com/user-attachments/assets/4d3464f0-f6cc-476d-9432-518f16d72586)


**Question 10**
---
 Write a query to get information of Employees from EmployeeInfo1 table where the Employee is not assigned to any department.

![image](https://github.com/user-attachments/assets/f0dfbbd9-0244-4ae5-85aa-b9be7d710397)

```sql
SELECT EmpID, EmpFname, EmpLname, Department, Project, Address, DOB, Gender
FROM EmployeeInfo1
WHERE Department IS NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/08de48e0-d220-4459-a99c-fbe034a69526)

