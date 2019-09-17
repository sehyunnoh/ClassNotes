# Orders
```sql
SELECT *
FROM employees
ORDER BY first_name, last_name;
```

# Distinct Parameter
```sql
SELECT DISTINCT country_id
FROM locations;
```

# Aggregate Functions
```sql
SELECT COUNT(commission_pct)
FROM employees;

SELECT COUNT(*)
FROM employees
WHERE commission_pct IS NOT NULL;

SELECT MAX(salary)
FROM employees;

SELECT MAX(CAST(salary AS INT))
FROM employees;

SELECT AVG(salary)
FROM employees
WHERE department_id = 10;

SELECT job_id, SUM(salary) AS 'combined salary'
FROM employees
GROUP BY job_id;

SELECT department_id, COUNT(*)
FROM employees
WHERE salary > 12000
GROUP BY department_id;

```