# Experiment 7 : PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80
### Program :
```
DECLARE
   num1 NUMBER := 50; -- You can change the value to test
   num2 NUMBER := 80; -- You can change the value to test
BEGIN
   IF num1 > num2 THEN
      DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
   ELSE
      DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
   END IF;
END;

```
### Output :
![image](https://github.com/user-attachments/assets/01f8dc82-b38c-4949-87e9-9733fb7376ef)

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55
### Code :
```DECLARE
   n NUMBER := 10; -- You can change this value to any N
   sum NUMBER := 0;
   i NUMBER := 1;
BEGIN
   WHILE i <= n LOOP
      sum := sum + i;
      i := i + 1;
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;

```
### Output :
![image](https://github.com/user-attachments/assets/ab06f52c-f71f-4bcc-bff5-40cd5097d1c6)

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8
### Program :
```DECLARE
   n NUMBER := 7;  
   a NUMBER := 0;  
   b NUMBER := 1;  
   c NUMBER;       
   i NUMBER := 3;  
BEGIN
   DBMS_OUTPUT.PUT('Fibonacci sequence: ' || a || ', ' || b);
   WHILE i <= n LOOP
      c := a + b;
      DBMS_OUTPUT.PUT(', ' || c);
      a := b;
      b := c;
      i := i + 1;
   END LOOP;
   DBMS_OUTPUT.NEW_LINE; 
END;
```
### Output :
![image](https://github.com/user-attachments/assets/6acafdc0-117c-406d-9b10-f478921f70b3)

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351
### program : 
```
DECLARE
   n NUMBER := 1535;  
   rev NUMBER := 0;
BEGIN
   WHILE n > 0 LOOP
      rev := rev * 10 + MOD(n, 10); 
      n := TRUNC(n / 10);          
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
```
### Output : 
![image](https://github.com/user-attachments/assets/2d3ed7ed-8d1f-4eaa-ba46-cdb983f5b6b7)


---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15
### Program : 
```
DECLARE
   a NUMBER := 10;
   b NUMBER := 9;
   c NUMBER := 15;
BEGIN
   IF (a >= b) AND (a >= c) THEN
      DBMS_OUTPUT.PUT_LINE('Largest of three numbers is: ' || a);
   ELSIF (b >= a) AND (b >= c) THEN
      DBMS_OUTPUT.PUT_LINE('Largest of three numbers is: ' || b);
   ELSE
      DBMS_OUTPUT.PUT_LINE('Largest of three numbers is: ' || c);
   END IF;
END;
```
### Output :

![image](https://github.com/user-attachments/assets/ee556598-da1e-4fea-9072-0cc22cf3b1e1)

## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
