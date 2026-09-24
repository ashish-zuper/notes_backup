

# 🧩 SQL Problem Statement: Enterprise Resource Utilization & Hiring Analysis

## Context

A company uses an internal **Resource Management & Hiring System** to track employees, project allocations, and hiring activities.  
Management wants **actionable insights** to improve **resource utilization** and **reduce bench time**.

You are given access to the following database tables.

---

## Database Schema

### 1. `employees`

|Column|Type|
|---|---|
|id|INT (PK)|
|name|VARCHAR|
|department|VARCHAR|
|role|VARCHAR|
|skills|TEXT|
|joining_date|DATE|
|is_active|BOOLEAN|

---

### 2. `projects`

|Column|Type|
|---|---|
|id|INT (PK)|
|name|VARCHAR|
|start_date|DATE|
|end_date|DATE|
|priority|INT|

---

### 3. `allocations`

|Column|Type|
|---|---|
|id|INT (PK)|
|employee_id|INT (FK → employees.id)|
|project_id|INT (FK → projects.id)|
|allocation_percentage|INT|
|start_date|DATE|
|end_date|DATE|

---

### 4. `candidates`

|Column|Type|
|---|---|
|id|INT (PK)|
|name|VARCHAR|
|role_applied|VARCHAR|
|application_date|DATE|
|status|VARCHAR|
|_(Applied, Screened, Interviewed, Offered, Hired, Rejected)_||

---

## Tasks

---

### **Task 1: Identify Bench Employees**

Find all **active employees** who are **not allocated to any project today** or whose total allocation is **less than 50%**.

**Output Columns**

- employee_id
    
- name
    
- total_allocation_percentage
    

---

### **Task 2: High-Utilization Projects**

List projects where **average allocation per employee exceeds 80%**.

**Output Columns**

- project_id
    
- project_name
    
- avg_allocation
    

---

### **Task 3: Resource Over-Allocation**

Find employees who are **over-allocated** (total allocation > 100%) at any point in time.

**Output Columns**

- employee_id
    
- name
    
- total_allocation_percentage
    

---

### **Task 4: Hiring Funnel Conversion**

For each `role_applied`, calculate the **conversion rate from Applied → Hired**.

**Output Columns**

- role_applied
    
- applied_count
    
- hired_count
    
- conversion_rate_percentage
    

---

### **Task 5: Time-to-Hire Analysis**

Calculate the **average number of days** taken to move a candidate from **Applied → Hired**.

---

### **Task 6 (Advanced): Utilization Trend**

For each department, calculate **monthly average utilization** over the last 6 months.

**Expected Approach**

- Time-range joins
    
- Grouping by month
    
- Handling partial allocations
    

---

## ⭐ Bonus (Optional – SDE-3 Signal)

### **Task 7: Optimization**

You are told Task 1 runs slowly in production.

1. Which indexes would you create?
    
2. How would you validate improvement?
    
3. What query patterns would you avoid?
    

---

## 🔎 Evaluation Criteria

|Area|What Interviewers Look For|
|---|---|
|Correctness|Accurate joins & filters|
|Performance|Index-aware queries|
|Readability|Clean, maintainable SQL|
|Edge Cases|NULLs, overlapping dates|
|Depth|Window functions, CTEs|

---

## 🧠 Expected Concepts Tested

- Aggregations & GROUP BY
    
- LEFT JOIN vs INNER JOIN
    
- Date range overlaps
    
- Window functions
    
- Query optimization
    
- Business reasoning with data
    

---



> ⚠️ Assumptions

- `CURRENT_DATE` represents “today”
    
- `end_date` can be `NULL` (meaning ongoing)
    
- Allocation dates are **inclusive**
    

---

# ✅ SQL Problem – Reference Answers

---

## **Task 1: Identify Bench Employees**

**Active employees with total allocation < 50% today**

```sql
WITH current_allocations AS (
    SELECT
        a.employee_id,
        SUM(a.allocation_percentage) AS total_allocation
    FROM allocations a
    WHERE CURRENT_DATE BETWEEN a.start_date AND COALESCE(a.end_date, CURRENT_DATE)
    GROUP BY a.employee_id
)
SELECT
    e.id AS employee_id,
    e.name,
    COALESCE(ca.total_allocation, 0) AS total_allocation_percentage
FROM employees e
LEFT JOIN current_allocations ca
    ON e.id = ca.employee_id
WHERE e.is_active = TRUE
  AND COALESCE(ca.total_allocation, 0) < 50;
```

**Key Concepts**

- LEFT JOIN to include unallocated employees
    
- `COALESCE` to handle NULL allocations
    
- Date range filtering
    

---

## **Task 2: High-Utilization Projects**

**Projects where average allocation per employee > 80%**

```sql
SELECT
    p.id AS project_id,
    p.name AS project_name,
    AVG(a.allocation_percentage) AS avg_allocation
FROM projects p
JOIN allocations a
    ON p.id = a.project_id
GROUP BY p.id, p.name
HAVING AVG(a.allocation_percentage) > 80;
```

**Key Concepts**

- `HAVING` vs `WHERE`
    
- Aggregate filtering
    

---

## **Task 3: Resource Over-Allocation**

**Employees with total allocation > 100%**

```sql
SELECT
    e.id AS employee_id,
    e.name,
    SUM(a.allocation_percentage) AS total_allocation_percentage
FROM employees e
JOIN allocations a
    ON e.id = a.employee_id
WHERE CURRENT_DATE BETWEEN a.start_date AND COALESCE(a.end_date, CURRENT_DATE)
GROUP BY e.id, e.name
HAVING SUM(a.allocation_percentage) > 100;
```

**Key Concepts**

- Business rule enforcement via aggregation
    
- Time-aware joins
    

---

## **Task 4: Hiring Funnel Conversion**

**Applied → Hired conversion rate per role**

```sql
SELECT
    role_applied,
    COUNT(*) FILTER (WHERE status = 'Applied') AS applied_count,
    COUNT(*) FILTER (WHERE status = 'Hired') AS hired_count,
    ROUND(
        COUNT(*) FILTER (WHERE status = 'Hired') * 100.0 /
        NULLIF(COUNT(*) FILTER (WHERE status = 'Applied'), 0),
        2
    ) AS conversion_rate_percentage
FROM candidates
GROUP BY role_applied;
```

### MySQL Alternative

```sql
SELECT
    role_applied,
    SUM(CASE WHEN status = 'Applied' THEN 1 ELSE 0 END) AS applied_count,
    SUM(CASE WHEN status = 'Hired' THEN 1 ELSE 0 END) AS hired_count,
    ROUND(
        SUM(CASE WHEN status = 'Hired' THEN 1 ELSE 0 END) * 100.0 /
        NULLIF(SUM(CASE WHEN status = 'Applied' THEN 1 ELSE 0 END), 0),
        2
    ) AS conversion_rate_percentage
FROM candidates
GROUP BY role_applied;
```

**Key Concepts**

- Conditional aggregation
    
- Divide-by-zero safety
    

---

## **Task 5: Time-to-Hire Analysis**

**Average days from Applied → Hired**

```sql
SELECT
    AVG(DATEDIFF(h.application_date, a.application_date)) AS avg_days_to_hire
FROM candidates a
JOIN candidates h
    ON a.name = h.name
   AND a.role_applied = h.role_applied
WHERE a.status = 'Applied'
  AND h.status = 'Hired';
```

### Better (Normalized) Version

If you had `candidate_status_history`:

```sql
SELECT
    AVG(DATEDIFF(h.changed_at, a.changed_at)) AS avg_days_to_hire
FROM candidate_status_history a
JOIN candidate_status_history h
    ON a.candidate_id = h.candidate_id
WHERE a.status = 'Applied'
  AND h.status = 'Hired';
```

**Key Concepts**

- Lifecycle modeling
    
- Why event tables are superior
    

---

## **Task 6 (Advanced): Monthly Utilization Trend (Last 6 Months)**

```sql
WITH monthly_allocations AS (
    SELECT
        e.department,
        DATE_TRUNC('month', a.start_date) AS month,
        AVG(a.allocation_percentage) AS avg_utilization
    FROM allocations a
    JOIN employees e
        ON a.employee_id = e.id
    WHERE a.start_date >= CURRENT_DATE - INTERVAL '6 months'
    GROUP BY e.department, DATE_TRUNC('month', a.start_date)
)
SELECT *
FROM monthly_allocations
ORDER BY department, month;
```

**Key Concepts**

- Time-series grouping
    
- Trend analysis
    
- CTE readability
    

---

## **Task 7 (Bonus): Query Optimization**

### ❓ Which indexes would you add?

```sql
CREATE INDEX idx_allocations_employee_date
ON allocations (employee_id, start_date, end_date);

CREATE INDEX idx_employees_active
ON employees (is_active);

CREATE INDEX idx_candidates_role_status
ON candidates (role_applied, status);
```

---

### ❓ How to validate improvement?

- `EXPLAIN ANALYZE`
    
- Compare:
    
    - Rows scanned
        
    - Execution time
        
- Monitor slow query logs
    

---

### ❓ What to avoid?

- Functions on indexed columns
    
- `SELECT *`
    
- Wildcard searches without indexes
    
- Large joins without filters
    

---

## 🎯 What This Tests at SDE-3 Level

|Skill|Signal|
|---|---|
|SQL Mastery|Complex joins & aggregation|
|Data Modeling|Time & lifecycle handling|
|Performance|Index-aware queries|
|Business Logic|Correct assumptions|
|Seniority|Explains trade-offs|

---

If you want, I can:

- Add **sample datasets**
    
- Create **grading rubrics**
    
- Turn this into a **90-minute interview exercise**
    
- Make a **FAANG-hard SQL variant**
    
- Add **common incorrect answers & red flags**
    

Just say the word 🚀