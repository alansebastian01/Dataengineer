A good way to learn MariaDB is to create an **Employee** table and practice queries from basic to advanced. Here's a complete example.

## Step 1: Create Database

```sql
CREATE DATABASE company_db;
USE company_db;
```

---

# Step 2: Create Employee Table

```sql
CREATE TABLE employee (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    gender CHAR(1),
    age INT,
    department VARCHAR(50),
    designation VARCHAR(50),
    salary DECIMAL(10,2),
    hire_date DATE,
    city VARCHAR(50),
    manager_id INT
);
```

---

# Step 3: Insert Sample Data

```sql
INSERT INTO employee
(first_name, last_name, gender, age, department, designation, salary, hire_date, city, manager_id)
VALUES
('John','Smith','M',30,'IT','Software Engineer',65000,'2021-01-15', 'New York',101),
('Emma','Johnson','F',28,'HR','HR Executive',50000,'2022-03-10','Chicago',102),
('Michael','Brown','M',35,'Finance','Accountant',70000,'2019-07-21','Dallas',103),
('Sophia','Williams','F',32,'IT','Senior Developer',90000,'2018-06-11','New York',101),
('David','Jones','M',40,'Sales','Sales Manager',85000,'2017-09-25','Los Angeles',104),
('Olivia','Garcia','F',26,'Marketing','Marketing Executive',55000,'2023-02-18','Miami',105),
('James','Miller','M',45,'Finance','Finance Manager',95000,'2015-11-30','Dallas',103),
('Isabella','Davis','F',29,'IT','Software Engineer',68000,'2021-05-19','Seattle',101),
('William','Rodriguez','M',38,'HR','HR Manager',88000,'2016-04-15','Chicago',102),
('Mia','Martinez','F',31,'Sales','Sales Executive',60000,'2020-08-22','Los Angeles',104);
```

---

# Basic Queries

### 1. Display all employees

```sql
SELECT * FROM employee;
```

### 2. Display selected columns

```sql
SELECT first_name, department, salary
FROM employee;
```

### 3. Distinct departments

```sql
SELECT DISTINCT department
FROM employee;
```

### 4. Employees from IT

```sql
SELECT *
FROM employee
WHERE department='IT';
```

### 5. Salary greater than 70000

```sql
SELECT *
FROM employee
WHERE salary > 70000;
```

### 6. Employees from New York

```sql
SELECT *
FROM employee
WHERE city='New York';
```

### 7. Employees aged between 25 and 35

```sql
SELECT *
FROM employee
WHERE age BETWEEN 25 AND 35;
```

### 8. Employees in IT or HR

```sql
SELECT *
FROM employee
WHERE department IN ('IT','HR');
```

### 9. Employees not in Sales

```sql
SELECT *
FROM employee
WHERE department <> 'Sales';
```

### 10. Employees hired after 2020

```sql
SELECT *
FROM employee
WHERE hire_date > '2020-01-01';
```

---

# Sorting

### Salary ascending

```sql
SELECT *
FROM employee
ORDER BY salary;
```

### Salary descending

```sql
SELECT *
FROM employee
ORDER BY salary DESC;
```

### Department then Salary

```sql
SELECT *
FROM employee
ORDER BY department, salary DESC;
```

---

# Aggregate Functions

### Count employees

```sql
SELECT COUNT(*) FROM employee;
```

### Maximum salary

```sql
SELECT MAX(salary) FROM employee;
```

### Minimum salary

```sql
SELECT MIN(salary) FROM employee;
```

### Average salary

```sql
SELECT AVG(salary) FROM employee;
```

### Total salary

```sql
SELECT SUM(salary) FROM employee;
```

---

# GROUP BY

### Employees per department

```sql
SELECT department, COUNT(*)
FROM employee
GROUP BY department;
```

### Average salary by department

```sql
SELECT department, AVG(salary)
FROM employee
GROUP BY department;
```

### Highest salary in each department

```sql
SELECT department, MAX(salary)
FROM employee
GROUP BY department;
```

### Departments with more than 2 employees

```sql
SELECT department, COUNT(*)
FROM employee
GROUP BY department
HAVING COUNT(*) > 2;
```

---

# String Functions

### Full Name

```sql
SELECT CONCAT(first_name,' ',last_name) AS full_name
FROM employee;
```

### Uppercase names

```sql
SELECT UPPER(first_name)
FROM employee;
```

### Lowercase department

```sql
SELECT LOWER(department)
FROM employee;
```

### Length of names

```sql
SELECT first_name, LENGTH(first_name)
FROM employee;
```

---

# Date Functions

### Current Date

```sql
SELECT CURDATE();
```

### Years of Experience

```sql
SELECT
first_name,
TIMESTAMPDIFF(YEAR, hire_date, CURDATE()) AS experience
FROM employee;
```

---

# LIKE Operator

### Names starting with J

```sql
SELECT *
FROM employee
WHERE first_name LIKE 'J%';
```

### Names ending with a

```sql
SELECT *
FROM employee
WHERE first_name LIKE '%a';
```

### Contains "son"

```sql
SELECT *
FROM employee
WHERE last_name LIKE '%son%';
```

---

# LIMIT

Top 5 highest salaries

```sql
SELECT *
FROM employee
ORDER BY salary DESC
LIMIT 5;
```

---

# CASE Statement

```sql
SELECT
first_name,
salary,
CASE
    WHEN salary >= 90000 THEN 'High'
    WHEN salary >= 70000 THEN 'Medium'
    ELSE 'Low'
END AS Salary_Level
FROM employee;
```

---

# Subqueries

Employees earning above average salary

```sql
SELECT *
FROM employee
WHERE salary >
(
SELECT AVG(salary)
FROM employee
);
```

Highest paid employee

```sql
SELECT *
FROM employee
WHERE salary =
(
SELECT MAX(salary)
FROM employee
);
```

---

# Self Join

Employee with Manager ID

```sql
SELECT
e.first_name,
e.manager_id
FROM employee e;
```

If you create a separate `manager` table, you can join employees to their managers.

---

# UPDATE

```sql
UPDATE employee
SET salary = salary + 5000
WHERE department='IT';
```

---

# DELETE

```sql
DELETE FROM employee
WHERE age > 60;
```

---

# ALTER TABLE

Add Email column

```sql
ALTER TABLE employee
ADD email VARCHAR(100);
```

---

# DROP COLUMN

```sql
ALTER TABLE employee
DROP COLUMN email;
```

---

# Practice Interview Questions

1. List all employees.
2. Find employees earning more than 60,000.
3. Show employees in the IT department.
4. Find employees hired after 2021.
5. Count employees in each department.
6. Find the highest-paid employee.
7. Find the second-highest salary.
8. Display employees sorted by salary descending.
9. Find employees whose names start with "M".
10. Calculate the average salary by department.
11. Find employees earning above the department average.
12. List the top 3 highest-paid employees.
13. Find duplicate cities.
14. Find employees with the same salary.
15. Increase the salary of all HR employees by 10%.
16. Delete employees who joined before 2016.
17. Find employees with more than 5 years of experience.
18. Show department-wise total salary.
19. Find the youngest employee.
20. Find the oldest employee.

These queries cover most SQL concepts used in MariaDB, including `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`, aggregate functions, string/date functions, subqueries, `CASE`, `LIMIT`, and DML (`INSERT`, `UPDATE`, `DELETE`). They provide a solid foundation for interviews and day-to-day database work.
