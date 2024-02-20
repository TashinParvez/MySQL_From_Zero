# Class Performance 01 (Spring 24 DBMS Lab Sec E CP 1 File)

1. Insert this [(Link)](https://github.com/TashinParvez/MySQL_From_Zero/blob/Tashin/Files/hr_schema.sql) database on your system.
2. Perform the operations below

   > 1. Find out the employee names who is not assigned to any manager.
   > 2. Find out the 3rd maximum paid salary.
   > 3. Find out the name of the employees who is in IT department. [Having IT in the begining of job id and is not having any vowel after that.
   > 4. Find out the location details where the is so state province available and country id is not starting with "I".
   > 5. Find out the location id where the street address is not ending with odd digit. 

## Solution

### Q1
```sql
SELECT first_name, last_name
FROM employees
WHERE manager_id is NULL
```


### Q2
```sql
SELECT DISTINCT salary
FROM employees
WHERE salary
ORDER BY salary DESC
LIMIT 2, 1
```


### Q3
```sql
SELECT first_name , last_name
FROM employees
WHERE  NOT( job_id LIKE 'it%a%'   OR 
            job_id LIKE 'it%e%'   OR 
            job_id LIKE 'it%i%'   OR 
            job_id LIKE 'it%o%'   OR 
            job_id LIKE 'it%u%'
           );
```



### Q4
```sql
SELECT  location_id, street_address
FROM locations
WHERE state_province IS NOT NULL    AND  
      NOT(country_id LIKE "I%")
```



### Q5
```sql
SELECT  location_id 
FROM locations
WHERE  NOT(  street_address LIKE "%1"    OR   
             street_address LIKE "%3"    OR   
             street_address LIKE "%5"    OR   
             street_address LIKE "%7"    OR  
             street_address LIKE "%9"     
          );
```

