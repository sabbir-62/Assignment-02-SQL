# Interview Questions

## 1. What is PostgreSQL?

PostgreSQL is an open source, relational database management system. It has some key features 

1. It runs on Windows, Linux, MacOS etc any platform.
2. It is a open source software. That means users can freely contribute on this software.
3. It supports `ACID` properties. `ACID` means `Atomicity`, `Consistency`, `Isolation` and `Durability`.
4. It support `SQL` for quering and managing data.
5. It allows complex queries, joins, aggregations.
6. Support modern data types like JSON, JSONB, array and custom types.

---


## 2. What is the purpose of a database schema in PostgreSQL?

Database schema is like a blue print that defines how datas are organized in database. It organizes database objects like table, views and functions. It separates the objects to avoid the conflicts and manage the permissions. Whe can group related tables, views inside a schema.

Generally when we create a table without mension any schema then it creates inside the public schema. Example:

```ts
// Create a rangers table inside public schema
CREATE TABLE rangers (
    ranger_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    region VARCHAR(100) NOT NULL
);
```

But when we create a schema and mension the schema, then table create inside this schema:

```ts
// Create conversation schema
CREATE SCHEMA conservation;

// Create a rangers table inside conversation schema
CREATE TABLE conservation.rangers (
    ranger_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    region VARCHAR(100) NOT NULL
);
```

---


## 3. What is the difference between the VARCHAR and CHAR data types?

### VARCHAR

1. When we declare a column with VARCHAR then it takes only these characters size that we provided. Suppose we declare a column with VARCHAR(n) the it takes upto n characters size. 
2.  It does not pad for shorter strings with spaces.

```ts
CREATE TABLE example_varchar (
    name VARCHAR(50)
);
INSERT INTO example_varchar VALUES ('Sabbir');
```
3. In `VARCHAR(50)`, `Sabbir` stores just `6` characters.

### CHAR

1. When we declare a column with CHAR then it takes only these characters size that we provided. Suppose we declare a column with CHAR(n) the it takes always n characters size.
2. If we insert a string that is shorter than n then PostgreSQL will pad the string with trailing spaces to reach the specified n length.

```ts
CREATE TABLE example_char (
    code CHAR(50)
);
INSERT INTO example_char VALUES ('Sabbir');
```
3. In `CHAR(5)`, `Sabbir` is stored as 50 characters. 6 Character + 44 trailing spaces.

---


## 4. Explain the purpose of the WHERE clause in a SELECT statement.

### WHERE

1. The `WHERE` clause is used to filter rows from a table based on a condition.

```ts
// Retrive a customer based on email
SELECT *
FROM customers
WHERE email = 'sabbir@gmail.com';
```

2. Without where statement, query return all rows.
3. We can use mathematical logics with where statement for fetching specific data. 

```ts
// Find sightings after May 1, 2024
SELECT * FROM sightings
WHERE sighting_time > '2024-05-01';

// Rangers in 'River Delta' OR 'Mountain Range'
SELECT * FROM rangers
WHERE region = 'River Delta' OR region = 'Mountain Range';
```

### SELECT

`SELECT` specify which columns we want to retrive

```ts
// Retrive all columns
SELECT * FROM rangers;

// Retrive only name and region column
SELECT name, region FROM rangers;
```

---


## 5. How can you modify data using UPDATE statements?

`UPDATE` statements is used for modifing existing record based on condition. Without conditon, all records will be modified.

```ts
// Basic syntax
UPDATE table_name
SET column1 = value1,
    column2 = value2,
WHERE condition;
```

```ts
// Updates the region of "Alice Green" to "Eastern Hills".
UPDATE rangers
SET region = 'Eastern Hills'
WHERE name = 'Alice Green';

// Update all rows
UPDATE rangers
SET region = 'Unknown';
```

---

## 6. How can you calculate aggregate functions like COUNT(), SUM(), and AVG() in PostgreSQL?

```ts
// Basic syntax
SELECT aggregate_function(column)
FROM table_name
WHERE condition;
```

Examples:

```ts
// Suppose we have a rangers table. Counts the total number of rangers.
SELECT COUNT(*) AS total_rangers FROM rangers;

// Suppose we have a table sales with a revenue column. Calculates total revenue.
SELECT SUM(revenue) AS total_revenue FROM sales;

// Calculates the average revenue.
SELECT AVG(revenue) AS average_revenue FROM sales;
```