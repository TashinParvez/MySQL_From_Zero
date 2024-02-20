# Class Performance 02 (Spring 24 DBMS Lab Sec E CP 2 File)

1. Insert this [(Link)](https://github.com/TashinParvez/MySQL_From_Zero/blob/Tashin/Files/hr_schema.sql) database on your system.
2. Perform the operations below

   > 1.	Find out the country names which is having vowel as last character but not starting with a vowel and located in “Asia” region.
   > 2.	Find out the employee’s name who are having job history experience (can be found in job history table) of more than 2 years but not more than 5.
   > 3.	Find out the location id and departments name under that location where the state province is not available and location id is in between 1200 to 1400.
   > 4.	Count the number of employees along with their total paid amount considering salary as yearly salary who are having salary greater than 5000 and working under a manager.


## Solution

### Q1
```sql

SELECT countries.country_name

FROM countries INNER JOIN regions
ON countries.region_id = regions.region_id

WHERE (countries.country_name LIKE '%a' OR 
       countries.country_name LIKE '%e' OR
       countries.country_name LIKE '%i' OR
       countries.country_name LIKE '%o' OR
       countries.country_name LIKE '%u' 
      ) 
      and not(
       countries.country_name LIKE 'a%' OR 
       countries.country_name LIKE 'e%' OR
       countries.country_name LIKE 'i%' OR
       countries.country_name LIKE 'o%' OR
       countries.country_name LIKE 'u%' 
      ) 
      and regions.region_name = 'Asia'; 

```


### Q2
```sql

SELECT e.first_name

FROM employees as e INNER JOIN job_history as js
ON e.employee_id = js.employee_id

WHERE 2< (Year(js.end_date)-Year(js.start_date)) <= 5;

```


### Q3
```sql

SELECT l.location_id, dep.department_name

FROM locations as l JOIN departments as dep 

WHERE l.state_province is Null AND l.location_id BETWEEN 1200 AND 1400; 

```



### Q4
```sql

SELECT count(emp.employee_id), sum(emp.salary*12) as total_pay
FROM employees as emp 
WHERE emp.salary > 5000 AND emp.manager_id is NOT Null 
```




