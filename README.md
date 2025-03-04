# Sql-Notes

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

