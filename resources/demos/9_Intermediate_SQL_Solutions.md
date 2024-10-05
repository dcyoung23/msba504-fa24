---
title: Intermediate SQL Solutions
layout: default
parent: Demos
grand_parent: Resources
nav_order: 5
---

### Employee Small Database  

The following 10 questions were referenced in the [7_SQL_Autograder_Warmup](../demos/7_SQL_Autograder_Warmup.html) demo as well as the day 9_Intermediate_SQL_2 lecture.

**Question 1**

Write a query that returns the total number of employees for the company.

**Answer:**  

``` sql
SELECT
  COUNT(*) AS employee_cnt
FROM
  employee;
```

**Question 2**

Write a query that returns the minimum, maximum, and average salary for all employees in the company.
   
**Answer:**  

``` sql
SELECT
  MIN(salary) AS salary_min,
  MAX(salary) AS salary_max,
  AVG(salary) AS salary_avg
FROM
  employee;
```
**Question 3**

Write a query that returns the employee with the Programmer title that has the lowest salary.
   
**Answer:**  

``` sql
SELECT
  e.employee_id,
  e.first_name,
  e.last_name,
  e.salary,
  j.job_title
FROM
  employee e
  INNER JOIN job j ON e.job_id = j.job_id
WHERE
  j.job_title = 'Programmer'
ORDER BY
  e.salary
LIMIT
  1;
```
   
**Question 4**

Write a query that returns all employees that make less than 50% of their max salary for the job title and order the results by their salary in ascending order.
  
``` sql
SELECT
  e.employee_id,
  e.first_name,
  e.last_name,
  e.salary,
  j.job_title,
  j.max_salary AS job_max_salary
FROM
  employee e
  INNER JOIN job j ON e.job_id = j.job_id
WHERE
  e.salary < j.max_salary * .50
ORDER BY
  e.salary;
```
   
**Question 5**

Write a query that returns the minimum, maximum, and average salary in each department and order the results by average salary in descending order. Round the average salary to 2 decimal places.
   
``` sql
SELECT
  d.department_name,
  MIN(salary) AS dept_min_salary,
  MAX(salary) AS dept_max_salary,
  ROUND(AVG(salary),2) AS dept_avg_salary,
  COUNT(e.employee_id) AS employee_cnt
FROM
  employee e
  INNER JOIN department d ON e.department_id = d.department_id
GROUP BY
  d.department_name
ORDER BY
  dept_avg_salary DESC;
```
   
**Question 6**

Write a query that returns the minimum, maximum, and average salary in each department with at least 5 employees and order the results by average salary in descending order. Round the average salary to 2 decimal places.
   
``` sql
SELECT
  d.department_name,
  MIN(salary) AS dept_min_salary,
  MAX(salary) AS dept_max_salary,
  ROUND(AVG(salary),2) AS dept_avg_salary,
  COUNT(e.employee_id) AS employee_cnt
FROM
  employee e
  INNER JOIN department d ON e.department_id = d.department_id
GROUP BY
  d.department_name
HAVING
  employee_cnt >= 5
ORDER BY
  dept_avg_salary DESC;
```
   
**Question 7**

Write a query that returns the number of dependents per employee in the Sales and Executive departments. Employees that have no dependents should be zero and order the results by the number of dependents in descending order.
   
``` sql
SELECT
  e.employee_id,
  e.first_name,
  e.last_name,
  d.department_name,
  COUNT(d.dependent_id) AS dependent_cnt
FROM employee e
  INNER JOIN department d ON e.department_id = d.department_id
  LEFT JOIN dependent d ON e.employee_id = d.employee_id
WHERE d.department_name IN  ('Sales', 'Executive')
GROUP BY
  e.employee_id,
  e.first_name,
  e.last_name,
  d.department_name
ORDER BY
  dependent_cnt DESC;
```

**Question 8**

Write a query that returns the number of employees by region and country with locations not in the United States and Canada and order the results by the number of employees in descending order.

``` sql
SELECT
  r.region_name,
  c.country_name,
  COUNT(e.employee_id) AS employee_cnt
FROM region r
  INNER JOIN country c ON r.region_id = c.region_id
  INNER JOIN location l ON c.country_id = l.country_id
  LEFT JOIN department d ON l.location_id = d.location_id
  LEFT JOIN employee e ON d.department_id = e.department_id
WHERE r.region_name <> 'Americas'
GROUP BY
  r.region_name,
  c.country_name
ORDER BY
  employee_cnt DESC;
```

**Question 9**

Write a query that returns the % of employees that work in the USA.

``` sql
SELECT
  ROUND(SUM(CASE WHEN l.country_id = 'US' THEN 1 ELSE 0 END)
  /
  CAST(COUNT(*) AS REAL) * 100,2) AS usa_employee_percentage
FROM employee e
INNER JOIN main.department d on d.department_id = e.department_id
INNER JOIN main.location l on l.location_id = d.location_id;
```

**Question 10**

Write a query that returns all employees that have a manager that is not in the same department. Employees that do not have a manager should be included in the results.

``` sql
SELECT
  e.employee_id,
  e.first_name,
  e.last_name,
  d.department_name,
  m.first_name as manager_first_name,
  m.last_name as manager_last_name,
  d2.department_name as manager_department_name
FROM employee e
INNER JOIN main.department d on d.department_id = e.department_id
LEFT JOIN employee m on e.manager_id = m.employee_id
LEFT JOIN department d2 on m.department_id = d2.department_id
WHERE d.department_name <> COALESCE(d2.department_name,'?');
```

### Sales Database

The following query uses the `sales` database that has been referenced in the Intermediate SQL lectures. Click [here](https://drive.google.com/file/d/10b2sQPrQ4fCvAfaxE9Qlhf5fGc9rjnAy/view?usp=sharing) to download resource files to create the database in PostgreSQL and SQLite and insert the sample data into the tables.

**Question 1**

A customer is currently looking at the GT RTS-2 Mountain Bike (11) but the price point is out of their budget.
Write a query that returns all other bikes that have a retail price less than the GT RTS-2 Mountain Bike.

``` sql
SELECT
  p.product_num,
  p.product_name,
  p.retail_price
FROM product p
INNER JOIN public.product_category pc on pc.category_id = p.category_id
INNER JOIN product p2 ON p2.product_num = 11 AND p.retail_price < p2.retail_price
WHERE pc.description = 'Bikes';
```