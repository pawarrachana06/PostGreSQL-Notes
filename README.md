# PostGreSQL-Notes

An oraganised collection of data.


## Database vs DBMS

App --> DBMS -->Database .(DBMS+DATA eg postgres,oracle)


## what is RDBMS?

A type of database system that stores data in structured tables and uses sql for managing and querying data.

## Databse vs Schemas VS Table

📚 Analogy:
Database = Library 🏛️ → Holds multiple sections (schemas) with different types of books (tables).

Schema = Section in the library 📖 → Groups related bookshelves (tables) together.

Table = Bookshelf 📚 → Stores individual books (records/data) in an organized way

By default, PostgreSQL has a schema called "public", but you can create others for better organization.

## Commands

1. List database

``` sql

select datname from pg_database;
```


```sql

\l
```
2. Create Database

``` sql
create database databasename

```


3. Change database

``` sql

\ c databasename
```
4. Drop Database

``` sql

Drop database db_name
```

## CRUD operations

Table : A table is a collection of related data held in a a table format within a database

1.Create table


```sql

CREATE TABLE table_name (
id INT,  # name and type
name VARCHAR(100),
city VARCHAR(100),
);

```

2.Desc table

``` sql
\ d table_name
```


3.Insert data

``` sql
INSERT INTO table_name (id,name,city) values (1,"Rahul","Mumbai") , (..._,(...)

```

OR

``` sql
INSERT INTO table_name  values (1,"Rahul","Mumbai")

```

4. Reading the data

```
SELECT * from TABLE_NAME

```


5. Updating the values

``` sql

UPDATE TABLE_NAME
SET NEW_VALUE
WHERE  CONDITION

```


6. Delete data

``` sql
DELETE FROM TABLE_NAME
WHERE CONDITION

```

7. List tables

```
\dt
```
8. Describe table
```
\d table_name
```

9. Check the current value of serial variable
```
select currval('employees_emp_id_seq');
```
10. Set the value for variable

```
select setval('employees_emp_id_seq',1);
```



![image](https://github.com/user-attachments/assets/7b05b39e-55c5-4dd9-b016-455a565a6952)

The above table was given an auto increment contrain , it set the regclass variable

##  DATATYPES AND CONSTRAINTS

Datatypes: An attribute that specifies the type of data in a column of our database.


| Data Type  |  Values                  |
|------------|---------------------------------|
| **Numeric** | `INT`, `DOUBLE`, `FLOAT`, `DECIMAL` |
| **String**  | `VARCHAR`                      |
| **Date**    | `DATE`                          |
| **Boolean** | `BOOLEAN`                       |


Constraint

A constraint is postgreSQL is a rule applied to a column

| Constraint       | Description                                      | Example                                  | Rules                                      |
|-----------------|--------------------------------------------------|------------------------------------------|--------------------------------------------|
| **PRIMARY KEY**  | Ensures a unique, non-null identifier for a row | `employee_id SERIAL PRIMARY KEY`         | - Must be unique in the table <br> - Cannot be NULL |
| **NOT NULL**     | Prevents NULL values in a column               | `first_name VARCHAR(50) NOT NULL`        | - Column must always have a value |
| **DEFAULT**      | Assigns a default value if none is provided     | `status VARCHAR(10) DEFAULT 'Active'`    | - Used when inserting without specifying a value |
| **AUTO INCREMENT** | Automatically generates sequential values     | `id SERIAL PRIMARY KEY`                  | - Uses `SERIAL` in PostgreSQL <br> - Auto-increments with each new row |
| **UNIQUE**       | Ensures all values in a column are distinct     | `email VARCHAR(100) UNIQUE`              | - No two rows can have the same value in this column |


## Clauses

| Clause       | Description                                          | Example                                    | Rules                                      |
|-------------|------------------------------------------------------|--------------------------------------------|--------------------------------------------|
| **SELECT**  | Retrieves data from a table                          | `SELECT * FROM employees;`                | - Used to fetch data from a table |
| **FROM**    | Specifies the table from which to retrieve data      | `SELECT name FROM employees;`             | - Must be followed by a valid table name |
| **WHERE**   | Filters records based on conditions                  | `SELECT * FROM employees WHERE age > 30;` | - Used to apply conditions on rows |
| **ORDER BY**| Sorts the result set                                 | `SELECT * FROM employees ORDER BY name;`  | - Default is ascending (`ASC`), use `DESC` for descending |
| **GROUP BY**| Groups records with the same values                  | `SELECT dept_id, COUNT(*) FROM employees GROUP BY dept_id;` | - Used with aggregate functions like `COUNT`, `SUM` |
| **HAVING**  | Filters groups after grouping                        | `SELECT dept_id, COUNT(*) FROM employees GROUP BY dept_id HAVING COUNT(*) > 5;` | - Used only with `GROUP BY` |
| **JOIN**    | Combines rows from multiple tables                   | `SELECT e.name, d.department_name FROM employees e JOIN departments d ON e.dept_id = d.id;` | - Requires a common column between tables |
| **LEFT JOIN** | Returns all records from the left table and matching from the right | `SELECT e.name, d.department_name FROM employees e LEFT JOIN departments d ON e.dept_id = d.id;` | - Returns `NULL` for non-matching rows in the right table |
| **RIGHT JOIN** | Returns all records from the right table and matching from the left | `SELECT e.name, d.department_name FROM employees e RIGHT JOIN departments d ON e.dept_id = d.id;` | - Returns `NULL` for non-matching rows in the left table |
| **FULL JOIN** | Returns all records when there is a match in either table | `SELECT e.name, d.department_name FROM employees e FULL JOIN departments d ON e.dept_id = d.id;` | - Returns `NULL` where there’s no match |
| **LIMIT**   | Restricts the number of returned rows                | `SELECT * FROM employees LIMIT 5;`        | - Use `OFFSET` to skip rows (`LIMIT 5 OFFSET 2;`) |
| **DISTINCT**| Returns unique values                                | `SELECT DISTINCT department FROM employees;` | - Removes duplicate rows from result |
| **INSERT INTO** | Adds new rows to a table                         | `INSERT INTO employees (name, age) VALUES ('Tom', 36);` | - Specify column names and values |
| **UPDATE**  | Modifies existing records                            | `UPDATE employees SET salary = 60000 WHERE id = 1;` | - Be careful, without `WHERE` it updates all rows |
| **DELETE**  | Removes rows from a table                            | `DELETE FROM employees WHERE id = 5;`     | - Be careful, without `WHERE` it deletes all rows |
| **ALTER TABLE** | Modifies a table’s structure                     | `ALTER TABLE employees ADD COLUMN address VARCHAR(255);` | - Can add, modify, or drop columns |
| **DROP TABLE** | Deletes a table permanently                      | `DROP TABLE employees;`                   | - Deletes table structure and data |
| **TRUNCATE** | Removes all records but keeps the table structure   | `TRUNCATE TABLE employees;`               | - Faster than `DELETE`, cannot be rolled back |


## Relational operator

| Operator  | Description                                  | Example                                | Rules                                  |
|-----------|----------------------------------------------|----------------------------------------|----------------------------------------|
| **=**     | Checks if values are equal                  | `SELECT * FROM employees WHERE age = 30;` | - Returns rows where the condition is exactly met |
| **!=** or **<>** | Checks if values are not equal      | `SELECT * FROM employees WHERE age != 30;` | - Returns rows where values are different |
| **>**     | Checks if left value is greater than right | `SELECT * FROM employees WHERE salary > 50000;` | - Returns rows where left value is greater |
| **<**     | Checks if left value is less than right    | `SELECT * FROM employees WHERE age < 40;` | - Returns rows where left value is smaller |
| **>=**    | Checks if left value is greater or equal   | `SELECT * FROM employees WHERE salary >= 70000;` | - Returns rows where value is greater or equal |
| **<=**    | Checks if left value is less or equal      | `SELECT * FROM employees WHERE age <= 35;` | - Returns rows where value is smaller or equal |
| **BETWEEN** | Checks if value is within a range       | `SELECT * FROM employees WHERE salary BETWEEN 40000 AND 80000;` | - Includes both boundary values |
| **IN**    | Checks if value matches any in a list      | `SELECT * FROM employees WHERE department IN ('HR', 'IT', 'Finance');` | - Equivalent to multiple OR conditions |
| **NOT IN** | Excludes values from a list              | `SELECT * FROM employees WHERE department NOT IN ('HR', 'IT');` | - Returns rows that don’t match any in the list |
| **LIKE**  | Checks for pattern matching               | `SELECT * FROM employees WHERE name LIKE 'A%';` | - `%` represents any number of characters <br> - `_` represents a single character |
| **NOT LIKE** | Excludes pattern matches              | `SELECT * FROM employees WHERE name NOT LIKE 'J%';` | - Returns rows that don’t match the pattern |
| **IS NULL** | Checks if value is NULL                | `SELECT * FROM employees WHERE email IS NULL;` | - Returns rows where column has NULL values |
| **IS NOT NULL** | Checks if value is NOT NULL        | `SELECT * FROM employees WHERE email IS NOT NULL;` | - Returns rows where column has a value |


## Logical operator

| Operator  | Description                                        | Example                                              | Rules |
|-----------|----------------------------------------------------|------------------------------------------------------|-------|
| **AND**   | Returns rows where **both** conditions are true   | `SELECT * FROM employees WHERE age > 30 AND salary > 50000;` | - Both conditions must be true for the row to be included |
| **OR**    | Returns rows where **at least one** condition is true | `SELECT * FROM employees WHERE age > 30 OR salary > 50000;` | - At least one condition must be true |
| **NOT**   | Negates the condition (returns opposite result)   | `SELECT * FROM employees WHERE NOT department = 'HR';` | - Returns rows where the condition is false |



## Data Refining


### 1. WHERE  
**Filters records based on a condition (case-sensitive for `VARCHAR` unless using `ILIKE`).**  
```sql
SELECT * FROM employees WHERE name = 'leslie knope';
```
- **Case-sensitive:** Won’t return `Leslie Knope` unless the case matches exactly.  
- **Use `ILIKE` (PostgreSQL) for case-insensitive search:**  
  ```sql
  SELECT * FROM employees WHERE name ILIKE 'leslie knope';
  ```

### 2. DISTINCT  
**Removes duplicate values from the result set (case-sensitive for text values).**  
```sql
SELECT DISTINCT department FROM employees;
```
- **Case-sensitive:** Treats `HR` and `hr` as different values.  

### 3. ORDER BY  
**Sorts the result set in ascending (`ASC`, default) or descending (`DESC`) order (case-sensitive for text, sorts uppercase before lowercase).**  
```sql
SELECT * FROM employees ORDER BY name ASC;
```
- **Sorting behavior:** `Aaron` appears before `aaron` due to case sensitivity.  
- **To ignore case, use `LOWER(name)`:**  
  ```sql
  SELECT * FROM employees ORDER BY LOWER(name) ASC;
  ```

### 4. LIMIT  
**Restricts the number of rows returned (not case-sensitive).**  
```sql
SELECT * FROM employees LIMIT 5;
```
- **No case impact:** Always returns the first 5 rows without affecting case handling.  

### 5. LIKE  
**Searches for a pattern in a column (case-sensitive in PostgreSQL, use `ILIKE` for case-insensitive search).**  
```sql
SELECT * FROM employees WHERE name LIKE 'leslie%';
```
- **Case-sensitive:** Won’t match `Leslie Knope`.  
- **Use `ILIKE` for case-insensitive search:**  
  ```sql
  SELECT * FROM employees WHERE name ILIKE 'leslie%';
  ```
  - Matches both `Leslie` and `leslie`.
  - ![image](https://github.com/user-attachments/assets/226f1958-8c9f-4980-8bca-36a69647f611)


## Aggregate functions

1. Count : Number of rows (go for non empty primary key)

2. SUM : Returns the sum of specified column

3. Avg: Retruns the avg of the specified column

4. MAX: Retruns the max of the specified column

5. MIN: Retruns the min of the specified column

## Group by

Common column is must. Can work with aggregate functions
``` sql
SELECT dept, COUNT(fname)
FROM employees
GROUP BY dept
```
```
select dept,COUNT(*) from employees GROUP BY dept;
```

## String functions


### **1. CONCAT, CONCAT_WS: Join Two Columns**
```sql
SELECT CONCAT(fname, ' ', lname) FROM employees;
SELECT CONCAT_WS(' ', fname, lname) FROM employees;
```

### **2. SUBSTR: Extract a Substring**
```sql
SELECT SUBSTR('hello buddy', 1, 6);
```

### **3. LEFT, RIGHT: Extract a Specific Number of Characters**
```sql
SELECT LEFT(fname, 3) FROM employees;  -- First 3 letters
SELECT RIGHT(fname, 2) FROM employees; -- Last 2 letters
```

### **4. LENGTH: Get the Length of a String**
```sql
SELECT LENGTH(fname) FROM employees;
```

### **5. TRIM, LTRIM, RTRIM: Remove Spaces**
```sql
SELECT TRIM('   hello   ');   -- 'hello'
SELECT LTRIM('   hello');     -- 'hello'
SELECT RTRIM('hello   ');     -- 'hello'
```

### **6. REPLACE: Replace a Substring**
```sql
SELECT REPLACE('hello buddy', 'hello', 'hey');
```

### **7. POSITION: Find a Substring's Position**
```sql
SELECT POSITION('buddy' IN 'hello buddy');  -- Returns starting index
```

## Alter table


The `ALTER` statement in SQL is used to modify an existing database table structure.

### **1. Add a Column**
```sql
ALTER TABLE employees ADD COLUMN age INT;
```

### **2. Drop a Column**
```sql
ALTER TABLE employees DROP COLUMN age;
```

### **3. Modify Column Data Type**
```sql
ALTER TABLE employees MODIFY COLUMN age BIGINT;
```

### **4. Rename a Column**
```sql
ALTER TABLE employees RENAME COLUMN fname TO first_name;
```

### **5. Rename a Table**
```sql
ALTER TABLE employees RENAME TO staff;
```

### **6. Add a Constraint**
```sql
ALTER TABLE employees ADD CONSTRAINT unique_email UNIQUE (email);
```

### **7. Drop a Constraint**
```sql
ALTER TABLE employees DROP CONSTRAINT unique_email;
```


### **8. Set a Default Value for a Column**
```sql
ALTER TABLE employees ALTER COLUMN age SET DEFAULT 25;
```

### **9. Remove Default Value from a Column**
```sql
ALTER TABLE employees ALTER COLUMN age DROP DEFAULT;
```

### **10. Set a Column as NOT NULL**
```sql
ALTER TABLE employees MODIFY COLUMN age INT NOT NULL;
```

### **11. Remove NOT NULL Constraint from a Column**
```sql
ALTER TABLE employees MODIFY COLUMN age INT NULL;
```

## **CHECK Constraint in SQL**

The `CHECK` constraint ensures that all values in a column meet specific conditions.

### **1. Add a CHECK Constraint**
```sql
ALTER TABLE employees ADD CONSTRAINT check_salary CHECK (salary > 30000);
```

### **2. Add a CHECK Constraint with Multiple Conditions**
```sql
ALTER TABLE employees ADD CONSTRAINT check_age_salary CHECK (age >= 18 AND salary > 30000);
```

### **3. Drop a CHECK Constraint**
```sql
ALTER TABLE employees DROP CONSTRAINT check_salary;
```

### **4. Use CHECK Without a Named Constraint**
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary > 30000)
);
```

## **CASE Expression in SQL**

The `CASE` expression allows conditional logic in SQL queries.

### **1. Simple CASE Expression**
```sql
SELECT name, salary,
    CASE salary 
        WHEN 50000 THEN 'Average'
        WHEN 100000 THEN 'High'
        ELSE 'Other'
    END AS salary_category
FROM employees;
```

### **2. Searched CASE Expression**
```sql
SELECT name, age,
    CASE 
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 60 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM employees;
```



## **Relationships in SQL**

SQL relationships define how data in different tables is connected. The most common relationships are:

### **1. One-to-One Relationship**
```sql
CREATE TABLE employee_details (
    employee_id INT PRIMARY KEY,
    address VARCHAR(255),
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

### **2. One-to-Many Relationship**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

### **3. Many-to-Many Relationship (Using a Junction Table)**
```sql
CREATE TABLE employee_projects (
    employee_id INT,
    project_id INT,
    PRIMARY KEY (employee_id, project_id),
    FOREIGN KEY (employee_id) REFERENCES employees(id),
    FOREIGN KEY (project_id) REFERENCES projects(id)
);
```


## **Foreign Key in SQL**

A `FOREIGN KEY` is a field in one table that uniquely refers to the `PRIMARY KEY` in another table. It helps maintain referential integrity.

### **1. Adding a Foreign Key**
```sql
ALTER TABLE orders ADD CONSTRAINT fk_employee FOREIGN KEY (employee_id) REFERENCES employees(id);
```

### **2. Creating a Table with a Foreign Key**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

### **3. Dropping a Foreign Key**
```sql
ALTER TABLE orders DROP CONSTRAINT fk_employee

![image](https://github.com/user-attachments/assets/f982534a-6d61-492f-bd78-484b2b38e023)



## **CHECK Constraint in SQL**

The `CHECK` constraint ensures that all values in a column meet specific conditions.

### **1. Add a CHECK Constraint**
```sql
ALTER TABLE employees ADD CONSTRAINT check_salary CHECK (salary > 30000);
```

### **2. Add a CHECK Constraint with Multiple Conditions**
```sql
ALTER TABLE employees ADD CONSTRAINT check_age_salary CHECK (age >= 18 AND salary > 30000);
```

### **3. Drop a CHECK Constraint**
```sql
ALTER TABLE employees DROP CONSTRAINT check_salary;
```

### **4. Use CHECK Without a Named Constraint**
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary > 30000)
);
```

## **CASE Expression in SQL**

The `CASE` expression allows conditional logic in SQL queries.

### **1. Simple CASE Expression**
```sql
SELECT name, salary,
    CASE salary 
        WHEN 50000 THEN 'Average'
        WHEN 100000 THEN 'High'
        ELSE 'Other'
    END AS salary_category
FROM employees;
```

### **2. Searched CASE Expression**
```sql
SELECT name, age,
    CASE 
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 60 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM employees;
```

## **Relationships in SQL**

SQL relationships define how data in different tables is connected. The most common relationships are:

### **1. One-to-One Relationship**
```sql
CREATE TABLE employee_details (
    employee_id INT PRIMARY KEY,
    address VARCHAR(255),
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

### **2. One-to-Many Relationship**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

### **3. Many-to-Many Relationship (Using a Junction Table)**
```sql
CREATE TABLE employee_projects (
    employee_id INT,
    project_id INT,
    PRIMARY KEY (employee_id, project_id),
    FOREIGN KEY (employee_id) REFERENCES employees(id),
    FOREIGN KEY (project_id) REFERENCES projects(id)
);
```

when there is mant to many relation ,we need one extra table (junction table ) which will keep the matching enteries.to avoid data duplications
![many-to-many](https://github.com/user-attachments/assets/c6973454-c828-4f14-bba9-6ee64985d6fa)


## **Foreign Key in SQL**

A `FOREIGN KEY` is a field in one table that uniquely refers to the `PRIMARY KEY` in another table. It helps maintain referential integrity.

### **1. Adding a Foreign Key**
```sql
ALTER TABLE orders ADD CONSTRAINT fk_employee FOREIGN KEY (employee_id) REFERENCES employees(id);
```

### **2. Creating a Table with a Foreign Key**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    employee_id INT,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

### **3. Dropping a Foreign Key**
```sql
ALTER TABLE orders DROP CONSTRAINT fk_employee;
```

## **Joins in SQL**

Joins are used to combine rows from two or more tables based on a related column.

### **1. INNER JOIN** (Returns only matching records from both tables)
```sql
SELECT employees.id, employees.name, orders.order_id
FROM employees
INNER JOIN orders ON employees.id = orders.employee_id;
```

### **2. LEFT JOIN (or LEFT OUTER JOIN)** (Returns all records from the left table and matching records from the right table)
```sql
SELECT employees.id, employees.name, orders.order_id
FROM employees
LEFT JOIN orders ON employees.id = orders.employee_id;
```

### **3. RIGHT JOIN (or RIGHT OUTER JOIN)** (Returns all records from the right table and matching records from the left table)
```sql
SELECT employees.id, employees.name, orders.order_id
FROM employees
RIGHT JOIN orders ON employees.id = orders.employee_id;
```

### **4. FULL JOIN (or FULL OUTER JOIN)** (Returns all records when there is a match in either left or right table)
```sql
SELECT employees.id, employees.name, orders.order_id
FROM employees
FULL JOIN orders ON employees.id = orders.employee_id;
```

### **5. CROSS JOIN** (Returns the Cartesian product of both tables, meaning each row from one table is combined with all rows from the other)
```sql
SELECT employees.id, employees.name, orders.order_id
FROM employees
CROSS JOIN orders;
```

### **6. SELF JOIN** (Joins a table with itself)
```sql
SELECT e1.id, e1.name, e2.name AS manager_name
FROM employees e1
INNER JOIN employees e2 ON e1.manager_id = e2.id;
```

## Understanding SQL VIEW 

### What is a VIEW?  
A **VIEW** in SQL is like a **virtual table** that doesn’t store data itself but shows data from one or more real tables.

### Think of it like this:
Imagine a **restaurant menu** 📜. The menu lists dishes, but the food is actually in the kitchen (real tables). The menu simply displays a selected set of items for customers (users) to see.

Similarly, a **VIEW** in SQL:
- **Pulls data from real tables** but doesn’t store it permanently.
- **Acts like a saved query** that you can use like a table.
- **Automatically updates** when the original table changes.

### Example:
If you have an `employees` table but only want to see employees in the IT department, you can create a **VIEW**:

```sql
CREATE VIEW it_employees AS
SELECT name, department, salary
FROM employees
WHERE department = 'IT';
```

Now, you can simply query the view:
```sql
SELECT * FROM it_employees;
```
- Instead of writing the whole query again.  

### Displaying a View:
To check the structure of a view, use:
```sql
SELECT * FROM information_schema.views WHERE table_name = 'it_employees';
```
To see the SQL code used to create a view:
```sql
SELECT definition FROM pg_views WHERE viewname = 'it_employees';
```
To list all views in the database using `information_schema`:
```sql
SELECT table_name FROM information_schema.views WHERE table_schema = 'public';
```
To list all views using PostgreSQL's `\dv` command:
```sql
\dv
```  

### Benefits of Using Views:
✅ Simplifies complex queries  
✅ Improves security by restricting data access  
✅ Provides a consistent structure for reports  


### HAVING Clause in SQL Views:
The **HAVING** clause is used to filter results based on aggregate functions (e.g., `SUM`, `COUNT`, `AVG`). It works similarly to `WHERE`, but for grouped data.

#### Example:
Suppose you want to see departments with an average salary greater than 50,000 from the `employees` view:

```sql
SELECT department, AVG(salary) AS avg_salary
FROM it_employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### Can the HAVING Clause Be Used on Non-Aggregate Columns?
No, the **HAVING** clause is specifically designed for filtering grouped results using aggregate functions. If you need to filter rows based on non-aggregated columns, you should use the **WHERE** clause instead.

#### Incorrect Usage:
```sql
SELECT department, salary
FROM it_employees
GROUP BY department
HAVING salary > 50000; -- ❌ This will cause an error
```

#### Correct Usage:
```sql
SELECT department, salary
FROM it_employees
WHERE salary > 50000; -- ✅ Use WHERE for non-aggregated columns
```


### Understanding ROLLUP in SQL:
The **ROLLUP** operator is used to generate subtotals and grand totals in aggregate queries.

#### Example:
Suppose you want to calculate the total salary per department, along with a grand total:

```sql
SELECT department, SUM(salary) AS total_salary
FROM it_employees
GROUP BY ROLLUP(department);
```

#### Explanation:
- This query will return total salaries for each department.
- It will also add an extra row with the grand total (sum of all salaries).

### Why Use ROLLUP?
✅ Saves time by automatically generating subtotals and totals.  
✅ Reduces the need for multiple queries.  

### Understanding COALESCE in SQL:
The **COALESCE** function is used to return the first non-null value from a list of values.

#### Example:
If some employees do not have a department assigned, you can use `COALESCE` to replace `NULL` values with a default value:

```sql
SELECT name, COALESCE(department, 'Not Assigned') AS department
FROM employees;
```

#### Explanation:
- If `department` is NULL, it will be replaced with 'Not Assigned'.
- Otherwise, it will show the actual department name.

### Why Use COALESCE?
✅ Prevents NULL values from appearing in query results.  
✅ Helps provide meaningful default values.  

![rollup](https://github.com/user-attachments/assets/16c67de4-5252-4b81-bd37-1729bae1a10b)

### Understanding Stored Routines in SQL:
A **Stored Routine** in SQL is a set of SQL statements that are saved and executed as a unit. It includes:
- **Stored Procedures** (perform operations but do not return a value)
- **User-Defined Functions** (return a value)

#### Example - Stored Procedure:
A procedure to increase salaries by a percentage:
```sql
CREATE PROCEDURE IncreaseSalary (IN percentage DECIMAL)
LANGUAGE plpgsql
AS $$
BEGIN
    UPDATE employees
    SET salary = salary + (salary * percentage / 100);
END $$;
```
To execute it:
```sql
CALL IncreaseSalary(10);
```
![SP](https://github.com/user-attachments/assets/51fd9055-57ce-46fe-81d8-ce58d5e1f6fc)

#### Example - User-Defined Function:
A function to get the employee count:
```sql
CREATE FUNCTION GetEmployeeCount() RETURNS INT AS $$
DECLARE emp_count INT;
BEGIN
    SELECT COUNT(*) INTO emp_count FROM employees;
    RETURN emp_count;
END $$ LANGUAGE plpgsql;
```
To use it:
```sql
SELECT GetEmployeeCount();
```
![user defined function](https://github.com/user-attachments/assets/bd94f44e-6e9f-44b7-b4bc-eb21fda98bef)

### Benefits of Stored Routines:
✅ Reduces code duplication  
✅ Improves performance by pre-compiling SQL  
✅ Enhances security by restricting direct access to tables  



### Benefits of Using Views:
✅ Simplifies complex queries  
✅ Improves security by restricting data access  
✅ Provides a consistent structure for reports  

## Understanding the OVER Clause:
The **OVER** clause in SQL is used with window functions to perform calculations across a set of rows related to the current row.

### Example - Using OVER with ROW_NUMBER():
Assigns a unique row number to each row within a partition:
```sql
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```
#### Explanation:
- Groups rows by department.
- Orders them by salary within each department.
- Assigns a row number (rank) based on the order.

#### Output Example:
| name  | department | salary | rank |
|--------|------------|--------|------|
| Alice  | IT        | 70000  | 1    |
| Bob    | IT        | 65000  | 2    |
| Carol  | HR        | 60000  | 1    |
| Dave   | HR        | 55000  | 2    |

### Common Uses of the OVER Clause:
- **ROW_NUMBER()**: Assigns a unique row number.
- **RANK()**: Assigns a rank, allowing ties.
- **DENSE_RANK()**: Like `RANK()`, but without gaps.
- **LEAD() / LAG()**: Access values from previous or next rows.
![over](https://github.com/user-attachments/assets/7e579edb-6608-4bd7-b15d-c75ba9ca51a8)
![partition](https://github.com/user-attachments/assets/6e2b2f01-0c7f-4b6e-be2f-e13448174515)
![lead](https://github.com/user-attachments/assets/3b1c648a-5285-4623-92ce-e9351bc07e61)

### Why Use the OVER Clause?
✅ Allows row-level analysis without collapsing data.  
✅ Useful for ranking, cumulative sums, and accessing row-specific details.  


## Understanding Common Table Expressions (CTE)
A **Common Table Expression (CTE)** is a temporary result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.

### Example - Using a CTE:
```sql
WITH high_salary_employees AS (
    SELECT name, department, salary
    FROM employees
    WHERE salary > 60000
)
SELECT * FROM high_salary_employees;
```
#### Explanation:
- `WITH high_salary_employees AS (...)` creates a temporary result set.
- The main `SELECT` query retrieves data from this result set.

#### Output Example:
| name  | department | salary |
|--------|------------|--------|
| Alice  | IT        | 70000  |
| Chris  | Finance   | 75000  |

### Benefits of Using CTE:
✅ Improves readability and organization of complex queries.  
✅ Helps avoid subquery repetition.  
✅ Can be used recursively for hierarchical data.  


## Understanding SQL VIEW in Layman Terms

### What is a VIEW?  
A **VIEW** in SQL is like a **virtual table** that doesn’t store data itself but shows data from one or more real tables.

### Think of it like this:
Imagine a **restaurant menu** 🌟. The menu lists dishes, but the food is actually in the kitchen (real tables). The menu simply displays a selected set of items for customers (users) to see.

Similarly, a **VIEW** in SQL:
- **Pulls data from real tables** but doesn’t store it permanently.
- **Acts like a saved query** that you can use like a table.
- **Automatically updates** when the original table changes.

### Example:
If you have an `employees` table but only want to see employees in the IT department, you can create a **VIEW**:

```sql
CREATE VIEW it_employees AS
SELECT name, department, salary
FROM employees
WHERE department = 'IT';
```

Now, you can simply query the view:
```sql
SELECT * FROM it_employees;
```
- Instead of writing the whole query again.  

#### Output Example:
| name  | department | salary |
|--------|------------|--------|
| Alice  | IT        | 70000  |
| Bob    | IT        | 65000  |

### Displaying a View:
To check the structure of a view, use:
```sql
SELECT * FROM information_schema.views WHERE table_name = 'it_employees';
```
To see the SQL code used to create a view:
```sql
SELECT definition FROM pg_views WHERE viewname = 'it_employees';
```
To list all views in the database using `information_schema`:
```sql
SELECT table_name FROM information_schema.views WHERE table_schema = 'public';
```
To list all views using PostgreSQL's `\dv` command:
```sql
\dv
```

### Benefits of Using Views:
✅ Simplifies complex queries  
✅ Improves security by restricting data access  
✅ Provides a consistent structure for reports  

---

## Understanding the OVER Clause:
The **OVER** clause in SQL is used with window functions to perform calculations across a set of rows related to the current row.

### Example - Using OVER with ROW_NUMBER():
Assigns a unique row number to each row within a partition:
```sql
SELECT name, department, salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```
#### Explanation:
- Groups rows by department.
- Orders them by salary within each department.
- Assigns a row number (rank) based on the order.

#### Output Example:
| name  | department | salary | rank |
|--------|------------|--------|------|
| Alice  | IT        | 70000  | 1    |
| Bob    | IT        | 65000  | 2    |
| Carol  | HR        | 60000  | 1    |
| Dave   | HR        | 55000  | 2    |

### Common Uses of the OVER Clause:
- **ROW_NUMBER()**: Assigns a unique row number.
- **RANK()**: Assigns a rank, allowing ties.
- **DENSE_RANK()**: Like `RANK()`, but without gaps.
- **LEAD() / LAG()**: Access values from previous or next rows.

### Why Use the OVER Clause?
✅ Allows row-level analysis without collapsing data.  
✅ Useful for ranking, cumulative sums, and accessing row-specific details.  

---

## Understanding Common Table Expressions (CTE)
A **Common Table Expression (CTE)** is a temporary result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.

### Example - Using a CTE:
```sql
WITH high_salary_employees AS (
    SELECT name, department, salary
    FROM employees
    WHERE salary > 60000
)
SELECT * FROM high_salary_employees;
```
#### Explanation:
- `WITH high_salary_employees AS (...)` creates a temporary result set.
- The main `SELECT` query retrieves data from this result set.

#### Output Example:
| name  | department | salary |
|--------|------------|--------|
| Alice  | IT        | 70000  |
| Chris  | Finance   | 75000  |

### Benefits of Using CTE:
✅ Improves readability and organization of complex queries.  
✅ Helps avoid subquery repetition.  
✅ Can be used recursively for hierarchical data.  

![point](https://github.com/user-attachments/assets/01ff19d9-80e0-4b19-928c-aebdd336c63b)


---

## Understanding SQL Triggers
A **Trigger** in SQL is a special type of stored procedure that automatically executes in response to certain events on a table.

### Example - Creating a Trigger:
Automatically updates the `last_updated` column whenever an `employees` record is modified:

```sql
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON employees
FOR EACH ROW
EXECUTE FUNCTION update_last_updated_column();
```
![syntax](https://github.com/user-attachments/assets/8d4048a5-1a1b-4cc8-aa04-5e2079fd7a97)


![function](https://github.com/user-attachments/assets/40cc6db6-f06b-478a-9eba-13c0f83e9fa2)


![use case](https://github.com/user-attachments/assets/06268701-a7f6-4f9f-a1a6-7b6df314a5ae)

![function](https://github.com/user-attachments/assets/ed3453c8-2f73-4b3e-b830-01e13b2ea94d)


![trigger](https://github.com/user-attachments/assets/c426959d-3437-4912-87c7-bf3ab8a5fa12)

Where `update_last_updated_column` is a function that updates the `last_updated` field.

### Benefits of Using Triggers:
✅ Automates tasks like logging, validation, or calculations.  
✅ Ensures data integrity and consistency.  
✅ Reduces manual intervention and improves efficiency.  




