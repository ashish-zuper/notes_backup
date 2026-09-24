
---

#### `employees`

| id  | name  | department_id | salary | join_date  |
| --- | ----- | ------------- | ------ | ---------- |
| 1   | Alice | 1             | 60000  | 2022-01-10 |
| 2   | Bob   | 2             | 45000  | 2021-03-15 |
| 3   | Carol | 1             | 70000  | 2020-07-20 |
| 4   | Dave  | 3             | 50000  | 2023-02-01 |
| 5   | Eve   | 2             | 55000  | 2022-11-05 |

---

#### `departments`

| id  | name        |     |
| --- | ----------- | --- |
| 1   | Engineering |     |
| 2   | Sales       |     |
| 3   | HR          |     |

---

## Section 1: Basic SQL

### 1. Fetch all columns from `employees`

```sql
SELECT * FROM employees;
```

---

### 2. Display name and salary of all employees

```sql
SELECT name, salary
FROM employees;
```

---

### 3. Employees with salary > 50,000

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

### 4. Employees who joined after 1st Jan 2022

```sql
SELECT *
FROM employees
WHERE join_date > '2022-01-01';
```

---

## Section 2: Filtering & Sorting

### 5. Employees from Sales department

```sql
SELECT *
FROM employees
WHERE department_id = 2;
```

---

### 6. Employees ordered by salary (highest first)

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

### 7. Employees whose name starts with ‘A’

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

---

## Section 3: Aggregations

### 8. Total number of employees

```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```

---

### 9. Average salary of all employees

```sql
SELECT AVG(salary) AS avg_salary
FROM employees;
```

---

### 10. Highest salary in the company

```sql
SELECT MAX(salary) AS max_salary
FROM employees;
```

---

## Section 4: GROUP BY & HAVING

### 11. Number of employees in each department

```sql
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

---

### 12. Average salary per department

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

---

### 13. Departments having more than 1 employee

```sql
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 1;
```

---

## Section 5: JOINs

### 14. Employee Name | Department Name | Salary

```sql
SELECT e.name AS employee_name,
       d.name AS department_name,
       e.salary
FROM employees e
JOIN departments d
ON e.department_id = d.id;
```

---

### 15. Employees working in Engineering

```sql
SELECT e.*
FROM employees e
JOIN departments d
ON e.department_id = d.id
WHERE d.name = 'Engineering';
```

---

### 16. Employees working in HR

```sql
SELECT e.*
FROM employees e
JOIN departments d
ON e.department_id = d.id
WHERE d.name = 'HR';
```

---

## Section 6: Subqueries

### 17. Employees earning more than average salary

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

### 18. Employee(s) with maximum salary

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

---

## Section 7: Practical Thinking

### 19. Second highest salary

**Method 1 (Most common)**

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

**Method 2 (Using DISTINCT – safer)**

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

---

### 20. Employees who joined in the last 1 year

**MySQL / PostgreSQL**

```sql
SELECT *
FROM employees
WHERE join_date >= CURRENT_DATE - INTERVAL '1 year';
```

---

## Bonus Section

### 21. Departments with no employees

```sql
SELECT d.*
FROM departments d
LEFT JOIN employees e
ON d.id = e.department_id
WHERE e.id IS NULL;
```

---

### 22. Increase salary by 10% for Sales department

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 2;
```

---
