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

SELECT country_id, COUNT(*)
FROM locations
GROUP BY country_id

SELECT country_id, COUNT(*)
FROM locations
GROUP BY country_id
HAVING COUNT(*) > 1;

-- find out no of employees for only those departments where
-- salary is more than 12000 and include those department 
-- which satisfies for more than 2 employees
SELECT department_id, COUNT(employee_id)
  FROM employees
 WHERE salary > 12000
 GROUP BY department_id
HAVING COUNT(employee_id) > 2

-- show no(count) of employees for each manager id
-- now show only those manager id and count of employees which ahs count of employees 
-- more then 2

SELECT manager_id, COUNT(employee_id)
FROM employees
WHERE manager_id IS NOT null
GROUP BY manager_id
HAVING COUNT(employee_id) > 2
ORDER BY COUNT(employee_id) desc;

-- List the countries located in Europe?
SELECT country_name 
FROM countries
WHERE region_id = ( SELECT region_id 
                      FROM regions 
                     WHERE region_name = 'Europe');

-- list all employee name for department_name IT.
-- use employee and department table 
SELECT * 
  FROM employees 
 WHERE department_id = ( SELECT department_id 
                           FROM departments 
                          WHERE department_name = 'IT');  

SELECT * 
  FROM employees
 WHERE job_id = ( SELECT job_id
                    FROM jobs
                   WHERE job_title = 'Accountant');
                   
SELECT job_title
  FROM jobs
 WHERE job_id in ( SELECT job_id 
                    FROM employees                   
                   WHERE salary > 11000 );       

-- Who manages the Purchasing department?
SELECT * FROM employees WHERE employee_id = ( SELECT manager_id FROM departments WHERE department_name = 'Purchasing');

-- Who are the employees that work for the Shipping department and earn more than $2500?
SELECT * 
  FROM employees
 WHERE salary > 2500
   AND department_id = ( SELECT department_id FROM departments WHERE department_name = 'Shipping');
 
-- Return the names of the departments that operates in the location with address 2014 Jabberwocky Rd

SELECT department_name 
  FROM departments 
 WHERE location_id = (SELECT location_id FROM locations WHERE street_address = '2014 Jabberwocky Rd');

-- How many employees are managed by Adam Fripp
SELECT COUNT(*) FROM employees WHERE manager_id = (SELECT employee_id FROM employees WHERE first_name = 'Adam');

-- What is the name of the employee(s) who has the highest salary
SELECT first_name+' '+last_name FROM employees WHERE salary = (SELECT MAX(salary) FROM employees);

-- What are the names of the employees who work in the location with the address ‘2004 Charade Rd’

SELECT first_name +' '+last_name 
  FROM employees 
 WHERE department_id IN (SELECT department_id 
                           FROM departments 
								  WHERE location_id = (SELECT location_id 
								                         FROM locations 
																WHERE street_address = '2004 Charade Rd'));                                             

```