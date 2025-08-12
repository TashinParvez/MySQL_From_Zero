# MySQL Database Operations Guide

Authored by **Tashin Parvez** from **United International University**

This document provides a comprehensive guide to MySQL database operations, covering Data Definition Language (DDL) and Data Manipulation Language (DML) commands, along with examples and best practices.

---

## Table of Contents

1. [Data Definition Language (DDL)](#data-definition-language-ddl)
   - [Create Database](#create-database)
   - [Delete Database](#delete-database)
   - [Create Table](#create-table)
   - [Delete Table](#delete-table)
   - [Modify Table](#modify-table)
   - [Shortcuts to Run MySQL Code](#shortcuts-to-run-mysql-code)
   - [Comments in MySQL](#comments-in-mysql)

2. [Data Manipulation Language (DML)](#data-manipulation-language-dml)
   - [Insert Data](#insert-data)
   - [Update Data](#update-data)
   - [Delete Data](#delete-data)
   - [Select Data](#select-data)
     - [Read Full Database](#read-full-database)
     - [Read Specific Columns](#read-specific-columns)
     - [Column Aliasing](#column-aliasing)
     - [Row Filtering](#row-filtering)
     - [Sorting Data](#sorting-data)
     - [Distinct Rows](#distinct-rows)
     - [Limit and Offset](#limit-and-offset)
   - [String Operations](#string-operations)
   - [Numeric Functions](#numeric-functions)
   - [Date and Time Functions](#date-and-time-functions)
   - [NULL Handling with COALESCE](#null-handling-with-coalesce)
   - [Set Operations](#set-operations)
   - [Aggregate Functions](#aggregate-functions)
   - [Group By and Having](#group-by-and-having)
   - [Joins](#joins)
   - [Subqueries](#subqueries)

---

## Data Definition Language (DDL)

### Create Database

```sql
-- Way 1: Create a database (shows error if it already exists)
CREATE DATABASE database_name;

-- Way 2: Create a database only if it doesn't exist (no error)
CREATE DATABASE IF NOT EXISTS database_name;
```

### Delete Database

```sql
-- Way 1: Delete a database (shows error if it doesn't exist)
DROP DATABASE database_name;

-- Way 2: Delete a database only if it exists (no error, only warning)
DROP DATABASE IF EXISTS database_name;
```

### Create Table

```sql
CREATE TABLE table_name (
    col_name datatype [NOT NULL] [DEFAULT def_value] [AUTO_INCREMENT],
    col_name datatype [NOT NULL] [DEFAULT def_value] [AUTO_INCREMENT],
    ...
    CONSTRAINT constraint_name PRIMARY KEY(col_name, col_name_2),
    CONSTRAINT constraint_name UNIQUE(col_name_3, col_name_4),
    CONSTRAINT constraint_name FOREIGN KEY(col_name_5, col_name_6)
        REFERENCES ref_table_name(ref_table_col_name, ref_table_col_name_2)
);

-- Create table only if it doesn't exist
CREATE TABLE IF NOT EXISTS table_name (
    ...
);
```

**Note:**
- **Yellow Key**: Represents `PRIMARY KEY`.
- **Gray Key**: Represents `UNIQUE`.
- Avoid declaring `PRIMARY KEY` directly in the column definition; use `CONSTRAINT` instead.

### Delete Table

```sql
-- Way 1: Delete a table (shows error if it doesn't exist)
DROP TABLE table_name;

-- Way 2: Delete a table only if it exists (no error, only warning)
DROP TABLE IF EXISTS table_name;
```

### Modify Table

#### Add/Drop Column

```sql
-- Add a column
ALTER TABLE table_name ADD COLUMN col_name datatype [NOT NULL] [UNIQUE] [DEFAULT def_value] [PRIMARY KEY] [AUTO_INCREMENT];

-- Drop a column
ALTER TABLE table_name DROP COLUMN col_name;
```

#### Add/Drop Primary Key

```sql
-- Add a single primary key
ALTER TABLE table_name ADD PRIMARY KEY (attribute_1);

-- Add a composite primary key
ALTER TABLE table_name ADD PRIMARY KEY (attribute_1, attribute_2);

-- Drop primary key
ALTER TABLE table_name DROP PRIMARY KEY;
```

#### Add/Drop Unique Constraint

```sql
-- Add unique constraint
ALTER TABLE table_name ADD CONSTRAINT constraint_name UNIQUE (attribute_1, attribute_2);

-- Drop unique constraint
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```

#### Add/Drop Foreign Key

```sql
-- Drop foreign key
ALTER TABLE table_name DROP FOREIGN KEY constraint_name;

-- Add foreign key
ALTER TABLE table_name ADD CONSTRAINT constraint_name
    FOREIGN KEY (attribute_1, attribute_2)
    REFERENCES ref_table_name(ref_table_col_name, ref_table_col_name_2);
```

#### Add/Drop Default Constraint

```sql
-- Set default value
ALTER TABLE table_name ALTER COLUMN col_name SET DEFAULT def_value;

-- Drop default value
ALTER TABLE table_name ALTER COLUMN col_name DROP DEFAULT;
```

#### Modify Column Type

```sql
ALTER TABLE table_name MODIFY COLUMN col_name new_datatype;
```

#### Rename Table

```sql
ALTER TABLE table_name RENAME new_table_name;
```

### Shortcuts to Run MySQL Code

- **Ctrl + Enter**: Execute the selected MySQL code.

### Comments in MySQL

```sql
# Single-line comment

/* Multi-line
   comment */
```

---

## Data Manipulation Language (DML)

### Insert Data

```sql
-- Insert data into specific columns
INSERT INTO table_name (attribute_1, attribute_2, attribute_3)
VALUES (value_1, value_2, value_3);

-- Insert data into all columns (follow table structure order)
INSERT INTO table_name
VALUES (value_1, value_2, value_3);

-- Insert multiple rows
INSERT INTO table_name
VALUES (value_1, value_2, value_3),
       (value_1, value_2, value_3),
       (value_1, value_2, value_3);
```

**Note**: Always include values for `PRIMARY KEY` columns.

### Update Data

```sql
UPDATE table_name
SET col_1 = value_1, col_2 = value_2
WHERE condition;
```

**Note**: Without a `WHERE` clause, all rows will be updated.

**Example Conditions**:
- `CGPA < 3.35`
- `id IS NOT NULL`

### Delete Data

```sql
DELETE FROM table_name
WHERE condition;
```

**Note**: Without a `WHERE` clause, all rows will be deleted.

**Example Conditions**:
- `CGPA < 3.35`
- `id IS NOT NULL`

### Select Data

#### Read Full Database

```sql
SELECT *
FROM table_name;
```

- `*`: Selects all columns.
- Default: Selects all rows if no `WHERE` clause is specified.

**Tip**: Select only the necessary data to optimize performance.

#### Read Specific Columns

```sql
SELECT col_1, col_2
FROM table_name;
```

#### Column Aliasing

```sql
-- Perform calculations without aliasing
SELECT col_1 + 3, col_2 * 4
FROM table_name;

-- Perform calculations with aliasing
SELECT col_1 + col_4 AS new_col_name_1, col_2 / col_5 AS new_col_name_2
FROM table_name;
```

**Example**:

```sql
SELECT employee_id, salary / 1000 AS salary_in_thousands, salary + salary * commission_pct AS total_salary
FROM employees;
```

#### Row Filtering

```sql
SELECT col_1, col_2
FROM table_name
WHERE condition;
```

**MySQL Operators**:
- `AND`, `&&`: Logical AND
- `OR`, `||`: Logical OR
- `NOT`, `!`: Logical NOT
- `DESC`: Sort in descending order
- `ASC`: Sort in ascending order

**Example Conditions**:
- `CGPA < 3.35`
- `id IS NOT NULL`
- `col_1 > col_4`
- `(col_1 > col_4) AND (col_1 > col_2)`
- `dept = 50 OR salary > 1000`

#### Sorting Data

```sql
SELECT col_1, col_2
FROM table_name
WHERE condition
ORDER BY col_name [ASC|DESC], col_name [ASC|DESC];
```

**Example**:

```sql
SELECT first_name, email, salary, 2024 - YEAR(hire_date) AS experience
FROM employees
ORDER BY experience DESC;
```

#### Distinct Rows

```sql
-- Distinct values for a single column
SELECT DISTINCT col_1
FROM table_name;

-- Distinct combination of columns
SELECT DISTINCT col_1, col_2
FROM table_name;
```

#### Limit and Offset

```sql
-- Show top N rows
SELECT DISTINCT col_name
FROM table_name
WHERE condition
ORDER BY col_name DESC
LIMIT N;

-- Skip M rows and show N rows
SELECT DISTINCT col_name
FROM table_name
ORDER BY col_name DESC
LIMIT N OFFSET M;

-- Alternative syntax
SELECT DISTINCT col_name
FROM table_name
ORDER BY col_name DESC
LIMIT M, N; -- Skip M rows, show N rows
```

**Example**:

```sql
-- Show top 3 salaries
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 3;

-- Show salaries 6 to 10
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 5 OFFSET 5;
```

### String Operations

#### LIKE Operator

```sql
SELECT col_name
FROM table_name
WHERE col_name LIKE 'pattern';
```

- `%`: Matches zero or more characters.
- `_`: Matches exactly one character.

**Example**:

```sql
SELECT *
FROM employees
WHERE last_name LIKE '%g'; -- Last name ends with 'g'
```

#### String Functions

1. `LENGTH()`: Returns the length of a string.
2. `UPPER()`: Converts a string to uppercase.
3. `LOWER()`: Converts a string to lowercase.
4. `REVERSE()`: Reverses a string.
5. `CONCAT(string1, string2, ...)`: Concatenates strings.
6. `SUBSTRING(string, start_position, length)`: Extracts a substring.
7. `TRIM(string)`: Removes leading and trailing spaces.
8. `SUBSTR(str, pos)`: Extracts substring from position `pos`.
9. `SUBSTR(str, pos, len)`: Extracts `len` characters from position `pos`.
10. `LEFT(str, len)`: Extracts `len` characters from the left.
11. `RIGHT(str, len)`: Extracts `len` characters from the right.
12. `LPAD(str, len, padstr)`: Pads string from the left to length `len`.
13. `RPAD(str, len, padstr)`: Pads string from the right to length `len`.

**Example**:

```sql
SELECT employee_id, LOWER(CONCAT(SUBSTR(first_name, 1, 2), '_', RIGHT(last_name, 2))) AS code_name
FROM employees
ORDER BY salary ASC;
```

**Complex Example**:

```sql
SELECT employee_id, first_name,
       CASE
           WHEN salary >= 1000 THEN CONCAT(salary DIV 1000, ' Thousands ', (salary % 1000) DIV 100, ' Hundreds ', salary % 100, ' Taka')
           WHEN salary >= 100 THEN CONCAT((salary) DIV 100, ' Hundreds ', salary % 100, ' Taka')
           ELSE CONCAT(salary % 100, ' Taka')
       END AS amount,
       salary * 12 AS yearly_salary
FROM employees
ORDER BY salary ASC;
```

### Numeric Functions

1. `ABS()`: Returns the absolute value.
2. `FLOOR()`: Rounds down to the nearest integer.
3. `CEIL()`: Rounds up to the nearest integer.
4. `ROUND(x)`: Rounds to the nearest integer.
5. `ROUND(x, D)`: Rounds to `D` decimal places.
6. `TRUNCATE(x, D)`: Truncates to `D` decimal places.

**Examples**:

```sql
SELECT ROUND(1.34); -- Returns 1
SELECT ROUND(1.34, 1); -- Returns 1.3
SELECT TRUNCATE(1.45, 1); -- Returns 1.4
```

### Date and Time Functions

- `NOW()`: Returns current date and time.
- `CURDATE()`: Returns current date.
- `CURTIME()`: Returns current time.
- `DATE(datetime)`: Extracts date part.
- `TIME(datetime)`: Extracts time part.
- `HOUR(datetime)`: Extracts hour.
- `MINUTE(datetime)`: Extracts minute.
- `SECOND(datetime)`: Extracts second.
- `DAY(datetime)`: Extracts day.
- `MONTH(datetime)`: Extracts month.
- `YEAR(datetime)`: Extracts year.
- `DATEDIFF(datetime1, datetime2)`: Returns number of days between dates.
- `TIMEDIFF(datetime1, datetime2)`: Returns time difference.
- `DATE_ADD(datetime, INTERVAL n unit)`: Adds `n` units (SECOND, MINUTE, HOUR, DAY, MONTH, YEAR).
- `DATE_SUB(datetime, INTERVAL n unit)`: Subtracts `n` units.

**Example**:

```sql
SELECT DATE_ADD(hire_date, INTERVAL 1 DAY) AS next_day
FROM employees;
```

### NULL Handling with COALESCE

```sql
-- Returns the first non-NULL value
SELECT COALESCE(NULL, 10, 100, NULL); -- Returns 10

-- Example with calculation
SELECT customer_mail, COALESCE(salary + (salary * 12), 0) AS total_salary
FROM customer;
```

### Set Operations

#### UNION

```sql
SELECT first_name, manager_id
FROM employees
WHERE manager_id = 100
UNION
SELECT first_name, manager_id
FROM employees
WHERE manager_id = 114;
```

#### INTERSECT

```sql
SELECT first_name, manager_id, salary
FROM employees
WHERE manager_id = 100
INTERSECT
SELECT first_name, manager_id, salary
FROM employees
WHERE salary > 5000;
```

#### EXCEPT

```sql
SELECT first_name, manager_id, salary
FROM employees
WHERE manager_id = 100
EXCEPT
SELECT first_name, manager_id, salary
FROM employees
WHERE salary > 5000;
```

### Aggregate Functions

- `MAX(col)`: Maximum value in a column.
- `MIN(col)`: Minimum value in a column.
- `SUM(col)`: Sum of values in a column.
- `AVG(col)`: Average of values in a column.
- `COUNT(col)`: Count of non-NULL values in a column.
- `COUNT(*)`: Count of all rows, including NULLs.

**Example**:

```sql
SELECT MAX(col_1), MIN(col_1), COUNT(col_1), SUM(col_1), AVG(col_1)
FROM table_name;
```

### Group By and Having

```sql
SELECT col_1, COUNT(*)
FROM table_name
WHERE condition
GROUP BY col_1
HAVING COUNT(*) >= 5
ORDER BY COUNT(*) ASC;
```

**Examples**:

1. Group by first character of name:
```sql
SELECT LEFT(first_name, 1) AS first_char, COUNT(*)
FROM employees
WHERE job_id != 'IT_PROG'
GROUP BY LEFT(first_name, 1)
HAVING COUNT(*) >= 5
ORDER BY COUNT(*) ASC;
```

2. Group by phone number substring:
```sql
SELECT SUBSTR(phone_number, 5, 3) AS mid_3, COUNT(*)
FROM employees
GROUP BY SUBSTR(phone_number, 5, 3);
```

3. Group by year and month:
```sql
SELECT YEAR(hire_date) AS yr, MONTH(hire_date), COUNT(*)
FROM employees
GROUP BY yr, MONTH(hire_date)
ORDER BY hire_date;
```

4. Group by salary class:
```sql
SELECT department_id,
       CASE
           WHEN salary < 10000 THEN 'A'
           WHEN salary BETWEEN 10000 AND 20000 THEN 'B'
           ELSE 'C'
       END AS salary_class,
       AVG(salary)
FROM employees
GROUP BY department_id, salary_class
ORDER BY department_id;
```

### Joins

#### Inner Join / Cross Join

```sql
SELECT t1.col, t2.col
FROM table_1 AS t1
JOIN table_2 AS t2 ON t1.col = t2.col
JOIN table_3 AS t3 ON t2.col = t3.col;
```

#### Left Join

```sql
SELECT t1.col, t2.col
FROM table_1 AS t1
LEFT JOIN table_2 AS t2 ON t1.col = t2.col;
```

#### Right Join

```sql
SELECT t1.col, t2.col
FROM table_1 AS t1
RIGHT JOIN table_2 AS t2 ON t1.col = t2.col;
```

#### Self Join

```sql
SELECT emp.employee_id, emp.first_name, manag.manager_id, manag.first_name
FROM employees AS emp
JOIN employees AS manag ON emp.manager_id = manag.employee_id;
```

**Example**:

```sql
SELECT emp.first_name, jobs.job_title, dept.department_name, loc.city
FROM employees AS emp
JOIN jobs ON emp.job_id = jobs.job_id
JOIN departments AS dept ON emp.department_id = dept.department_id
JOIN locations AS loc ON dept.location_id = loc.location_id;
```

### Subqueries

#### Scalar Subquery

Returns a single value.

```sql
SELECT *
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM employees
    WHERE employee_id = 110
);
```

#### Column Subquery

Returns a single column with multiple rows.

```sql
SELECT *
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE department_id = 100
)
AND department_id = 100;
```

#### Row Subquery

Returns a single row with multiple columns.

```sql
SELECT *
FROM employees
WHERE (department_id, salary) = (
    SELECT department_id, salary
    FROM employees
    WHERE employee_id = 110
);
```

#### Derived Table

Returns a temporary table.

```sql
SELECT department_id, MIN(total_salary)
FROM (
    SELECT department_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY department_id
) AS dt;
```

#### Correlated Subquery

Inner query depends on the outer query.

```sql
SELECT *
FROM employees AS e
WHERE salary IN (
    SELECT MAX(salary)
    FROM employees AS d
    WHERE d.department_id = e.department_id
    GROUP BY department_id
);
```

**Example**:

```sql
SELECT year, department_id, MIN(total_emp) AS emp_hire
FROM (
    SELECT COUNT(employee_id) AS total_emp, YEAR(hire_date) AS year, department_id
    FROM employees
    GROUP BY YEAR(hire_date), department_id
) AS nt
GROUP BY nt.year
ORDER BY year;
```

