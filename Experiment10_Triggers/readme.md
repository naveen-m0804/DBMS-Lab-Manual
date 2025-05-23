# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

**Program:**
```sql
CREATE TABLE employees (
    emp_id     NUMBER PRIMARY KEY,
    emp_name   VARCHAR2(100),
    designation VARCHAR2(100),
    salary     NUMBER,
    dept_no    NUMBER
);
CREATE TABLE employee_log (
    log_id       NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    emp_id       NUMBER,
    emp_name     VARCHAR2(100),
    designation  VARCHAR2(100),
    salary       NUMBER,
    dept_no      NUMBER,
    log_date     DATE
);
CREATE OR REPLACE TRIGGER trg_log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (
        emp_id, emp_name, designation, salary, dept_no, log_date
    ) VALUES (
        :NEW.emp_id, :NEW.emp_name, :NEW.designation,
        :NEW.salary, :NEW.dept_no, SYSDATE
    );
END;
/
INSERT INTO employees (emp_id, emp_name, designation, salary, dept_no)
VALUES (3, 'Carol', 'Analyst', 50000, 30);

INSERT INTO employees (emp_id, emp_name, designation, salary, dept_no)
VALUES (4, 'David', 'Tester', 40000, 20);

COMMIT;
SELECT emp_id, emp_name FROM employees;

DELETE FROM employees WHERE emp_id IN (1, 2);
COMMIT;

INSERT INTO employees (emp_id, emp_name, designation, salary, dept_no)
VALUES (1, 'Alice', 'Manager', 85000, 10);
```
**Output:**

![image](https://github.com/user-attachments/assets/1b03dbc5-b112-4638-98a6-9307745e54aa)

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
**Program:**
```sql
CREATE TABLE sensitive_data (
    record_id   NUMBER PRIMARY KEY,
    info        VARCHAR2(100)
);

-- Insert sample data
INSERT INTO sensitive_data (record_id, info) VALUES (1, 'Top Secret Document A');
INSERT INTO sensitive_data (record_id, info) VALUES (2, 'Confidential File B');
COMMIT;

-- Create a trigger to prevent deletion
CREATE OR REPLACE TRIGGER prevent_sensitive_data_deletion
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/
```

**Output:**

  ![image](https://github.com/user-attachments/assets/4db817a0-4611-42bb-b92f-3ad301df59db)

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
**Program:**

```sql
CREATE TABLE products (
    product_id     NUMBER PRIMARY KEY,
    product_name   VARCHAR2(100),
    price          NUMBER,
    last_modified  DATE
);

INSERT INTO products (product_id, product_name, price) VALUES (1, 'Laptop', 75000);
INSERT INTO products (product_id, product_name, price) VALUES (2, 'Mobile Phone', 30000);
COMMIT;
CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSDATE;
END;
/

```
**Output:**
  ![image](https://github.com/user-attachments/assets/14d4efc6-b018-49ae-b0ff-f6b0fd27ff4d)

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

**Program:**
```sql
INSERT INTO audit_log (table_name, update_count)
VALUES ('CUSTOMER_ORDERS', 0);
CREATE OR REPLACE TRIGGER trg_count_updates_customer_orders
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'CUSTOMER_ORDERS';
END;
/
-- Update a row in customer_orders
UPDATE customer_orders
SET total_amount = total_amount + 10
WHERE order_id = 1;

-- Check the update count
SELECT * FROM audit_log;
```  

  
  
**Output:**

![image](https://github.com/user-attachments/assets/86838b33-9a48-41c0-9290-317c08c95fb8)

---


## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

```sql
CREATE TABLE employees (
    emp_id     NUMBER PRIMARY KEY,
    emp_name   VARCHAR2(100),
    salary     NUMBER
);
CREATE OR REPLACE TRIGGER trg_check_min_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/
INSERT INTO employees (emp_id, emp_name, salary)
VALUES (1, 'John Doe', 2500);

INSERT INTO employees (emp_id, emp_name, salary)
VALUES (2, 'Jane Smith', 4000);

```
**Output:**

![image](https://github.com/user-attachments/assets/2a106a98-456b-4915-bde7-f94d7de0f750)


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
