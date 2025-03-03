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


