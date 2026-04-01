
# Complete SQL Learning Guide for Beginners

## How to Use This Guide
This guide is organized into three modules:

- **Basics**: core ideas and first queries
- **Intermediate**: filtering, grouping, joins, and table design
- **Advanced**: analytics, security, transactions, optimization, and administration

For **every topic**, you will see:
1. Simple explanation  
2. Syntax  
3. Example  
4. Real-world use case  
5. Practice exercise  
6. Key takeaway  

---

## Sample Data Used in Examples

### customers
| customer_id | name | city   | email            |
|---|---|---|---|
| 1 | Asha | Delhi  | asha@email.com |
| 2 | Ben  | Mumbai | ben@email.com  |
| 3 | Cara | Delhi  | NULL           |

### orders
| order_id | customer_id | order_date  | amount | status    |
|---|---:|---|---:|---|
| 101 | 1 | 2026-01-10 | 500 | Shipped   |
| 102 | 2 | 2026-01-12 | 300 | Pending   |
| 103 | 1 | 2026-01-15 | 700 | Shipped   |
| 104 | 3 | 2026-01-18 | 200 | Cancelled |

### employees
| emp_id | emp_name | manager_id | department | salary |
|---|---|---:|---|---:|
| 1 | Ravi | NULL | Sales | 50000 |
| 2 | Neha | 1    | Sales | 40000 |
| 3 | Omar | 1    | Sales | 42000 |
| 4 | Isha | NULL | HR    | 55000 |

### products
| product_id | product_name | category | price |
|---|---|---|---:|
| 1 | Mouse | Electronics | 800 |
| 2 | Keyboard | Electronics | 1500 |
| 3 | Chair | Furniture | 4500 |

### order_items
| order_id | product_id | qty |
|---|---:|---:|
| 101 | 1 | 2 |
| 101 | 2 | 1 |
| 102 | 3 | 1 |

### Small diagram
```text
customers ----< orders ----< order_items >---- products
employees ---- employees (manager relationship)
```

---

# MODULE 1: BASICS

## 1) What is SQL?
**Explanation**  
SQL stands for Structured Query Language. It is used to talk to a database and work with data.

**Syntax**
```sql
SELECT column_name
FROM table_name;
```

**Example**
```sql
SELECT name
FROM customers;
```

**Real-world use case**  
A shopping app uses SQL to show customer names and orders.

**Practice**  
Show all columns from `customers`.

**Key Takeaway**  
SQL is the main language for working with relational databases.

---

## 2) DBMS vs RDBMS
**Explanation**  
A **DBMS** stores data. An **RDBMS** stores data in tables that can be related to each other.

**Syntax**  
No direct syntax. This is a concept.

**Example**
```text
DBMS  -> stores data
RDBMS -> stores data + relationships between tables
```

**Real-world use case**  
A school system uses an RDBMS to connect students, classes, and marks.

**Practice**  
Write one difference between DBMS and RDBMS.

**Key Takeaway**  
RDBMS is better for structured data with relationships.

---

## 3) Tables, rows, and columns
**Explanation**  
A **table** stores data. A **row** is one record. A **column** is one field.

**Syntax**
```sql
SELECT *
FROM customers;
```

**Example**
```text
Table: customers
Row: (1, Asha, Delhi, asha@email.com)
Column: name
```

**Real-world use case**  
An HR system stores each employee in one row.

**Practice**  
In `orders`, identify one row and one column.

**Key Takeaway**  
Tables organize data into rows and columns.

---

## 4) Schemas and databases
**Explanation**  
A **database** is a container for data. A **schema** is a logical group of tables inside a database.

**Syntax**
```sql
schema_name.table_name
```

**Example**
```sql
SELECT *
FROM sales.orders;
```

**Real-world use case**  
A company may keep finance tables in one schema and HR tables in another.

**Practice**  
Write a sample reference using schema and table name.

**Key Takeaway**  
A database contains schemas, and schemas contain objects like tables.

---

## 5) SQL syntax rules
**Explanation**  
SQL has rules for writing statements. Common rules: commands usually end with `;`, strings use quotes, and keywords are often written in uppercase for readability.

**Syntax**
```sql
SELECT name
FROM customers
WHERE city = 'Delhi';
```

**Example**
```sql
SELECT *
FROM orders;
```

**Real-world use case**  
Correct syntax prevents errors in production reports.

**Practice**  
Add a semicolon to a SQL statement.

**Key Takeaway**  
Good syntax helps SQL run correctly and stay readable.

---

## 6) SQL keywords and identifiers
**Explanation**  
**Keywords** are reserved words like `SELECT` and `FROM`. **Identifiers** are names you give to tables and columns.

**Syntax**
```sql
SELECT customer_id
FROM customers;
```

**Example**
```text
Keyword: SELECT
Identifier: customers
Identifier: customer_id
```

**Real-world use case**  
Clear names make team queries easier to understand.

**Practice**  
Mark the keyword and identifier in `SELECT amount FROM orders;`

**Key Takeaway**  
Keywords tell SQL what to do; identifiers tell SQL where to do it.

---

## 7) SQL data types
**Explanation**  
A data type tells the database what kind of value a column stores.

**Syntax**
```sql
column_name VARCHAR(50)
column_name INT
column_name DATE
```

**Example**
```sql
CREATE TABLE demo (
    id INT,
    name VARCHAR(50),
    joined_on DATE,
    salary DECIMAL(10,2)
);
```

**Real-world use case**  
Using `DATE` for dates makes filtering easier than storing dates as text.

**Practice**  
Choose a type for email, order amount, and order date.

**Key Takeaway**  
Pick the right type for better storage, speed, and accuracy.

---

## 8) Creating a database
**Explanation**  
You create a database before creating tables inside it.

**Syntax**
```sql
CREATE DATABASE shop_db;
```

**Example**
```sql
CREATE DATABASE training_db;
```

**Real-world use case**  
A new app starts with a dedicated database for its data.

**Practice**  
Write a command to create a database named `school_db`.

**Key Takeaway**  
A database is the top-level container for your data.

---

## 9) Using / selecting a database
**Explanation**  
After creating a database, you choose it before creating or querying objects.

**Syntax**
```sql
USE database_name;
```

**Example**
```sql
USE training_db;
```

**Real-world use case**  
Developers switch between test and production databases.

**Practice**  
Write the command to use `shop_db`.

**Key Takeaway**  
Select the correct database before running commands.

---

## 10) Creating a table
**Explanation**  
A table stores related data in columns.

**Syntax**
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype
);
```

**Example**
```sql
CREATE TABLE customers (
    customer_id INT,
    name VARCHAR(50),
    city VARCHAR(50),
    email VARCHAR(100)
);
```

**Real-world use case**  
An e-commerce site creates `customers`, `orders`, and `products` tables.

**Practice**  
Create a table `students` with `student_id`, `name`, and `class_name`.

**Key Takeaway**  
Tables define how data will be stored.

---

## 11) Inserting starter data
**Explanation**  
Use `INSERT` to add rows into a table.

**Syntax**
```sql
INSERT INTO table_name (col1, col2)
VALUES (val1, val2);
```

**Example**
```sql
INSERT INTO customers (customer_id, name, city, email)
VALUES (1, 'Asha', 'Delhi', 'asha@email.com');
```

**Real-world use case**  
A new store adds its first customer records.

**Practice**  
Insert one row into `students`.

**Key Takeaway**  
`INSERT` adds data to a table.

---

## 12) Comments in SQL
**Explanation**  
Comments explain your SQL and are ignored by the database.

**Syntax**
```sql
-- single-line comment

/* multi-line
   comment */
```

**Example**
```sql
-- Get Delhi customers
SELECT *
FROM customers;
```

**Real-world use case**  
Teams use comments to describe tricky business rules.

**Practice**  
Add a single-line comment above a `SELECT`.

**Key Takeaway**  
Comments improve readability and teamwork.

---

## 13) Operators in SQL
**Explanation**  
Operators compare or combine values.

**Syntax**
```sql
=, >, <, >=, <=, <>, AND, OR, NOT
```

**Example**
```sql
SELECT *
FROM orders
WHERE amount > 300 AND status = 'Shipped';
```

**Real-world use case**  
A finance report finds orders above a minimum amount.

**Practice**  
Find orders with amount less than 500.

**Key Takeaway**  
Operators help you filter and compare data.

---

## 14) NULL values
**Explanation**  
`NULL` means the value is missing or unknown. It is not the same as 0 or an empty string.

**Syntax**
```sql
WHERE column_name IS NULL
```

**Example**
```sql
SELECT *
FROM customers
WHERE email IS NULL;
```

**Real-world use case**  
A CRM finds customers missing email addresses.

**Practice**  
List employees whose `manager_id` is `NULL`.

**Key Takeaway**  
Use `IS NULL` and `IS NOT NULL` to check missing values.

---

## 15) Aliases
**Explanation**  
Aliases give temporary names to columns or tables to make results easier to read.

**Syntax**
```sql
SELECT column_name AS alias_name
FROM table_name AS t;
```

**Example**
```sql
SELECT name AS customer_name, city AS customer_city
FROM customers AS c;
```

**Real-world use case**  
Dashboards use friendly column names for reports.

**Practice**  
Rename `amount` as `order_amount`.

**Key Takeaway**  
Aliases improve readability without changing real table names.

---

## 16) SELECT statement
**Explanation**  
`SELECT` is used to read data from a table.

**Syntax**
```sql
SELECT column1, column2
FROM table_name;
```

**Example**
```sql
SELECT name, city
FROM customers;
```

**Real-world use case**  
An app page reads customer names and cities.

**Practice**  
Select `order_id` and `amount` from `orders`.

**Key Takeaway**  
`SELECT` is the most common SQL command.

---

## 17) SELECT DISTINCT
**Explanation**  
`DISTINCT` removes duplicate values from the result.

**Syntax**
```sql
SELECT DISTINCT column_name
FROM table_name;
```

**Example**
```sql
SELECT DISTINCT city
FROM customers;
```

**Real-world use case**  
A delivery team wants a unique list of cities.

**Practice**  
Show distinct order statuses.

**Key Takeaway**  
Use `DISTINCT` when you want unique values only.

---

## 18) WHERE clause
**Explanation**  
`WHERE` filters rows.

**Syntax**
```sql
SELECT *
FROM table_name
WHERE condition;
```

**Example**
```sql
SELECT *
FROM customers
WHERE city = 'Delhi';
```

**Real-world use case**  
A marketing team targets customers from one city.

**Practice**  
Find orders where status is `Pending`.

**Key Takeaway**  
`WHERE` helps you get only the rows you need.

---

## 19) ORDER BY
**Explanation**  
`ORDER BY` sorts results.

**Syntax**
```sql
SELECT *
FROM table_name
ORDER BY column_name ASC|DESC;
```

**Example**
```sql
SELECT *
FROM orders
ORDER BY amount DESC;
```

**Real-world use case**  
A sales report shows highest-value orders first.

**Practice**  
Sort customers by name.

**Key Takeaway**  
Use `ORDER BY` to control result order.

---

## 20) LIMIT / TOP / FETCH FIRST
**Explanation**  
These return only some rows. The exact keyword depends on the database.

**Syntax**
```sql
-- MySQL / PostgreSQL
SELECT * FROM orders LIMIT 2;

-- SQL Server
SELECT TOP 2 * FROM orders;

-- Standard / Oracle style
SELECT * FROM orders FETCH FIRST 2 ROWS ONLY;
```

**Example**
```sql
SELECT *
FROM orders
LIMIT 2;
```

**Real-world use case**  
A dashboard shows the latest 5 orders.

**Practice**  
Write a query to return 3 products only.

**Key Takeaway**  
Use row limits to reduce output.

---

## 21) Pattern matching with LIKE
**Explanation**  
`LIKE` searches using a pattern.

**Syntax**
```sql
SELECT *
FROM table_name
WHERE column_name LIKE pattern;
```

**Example**
```sql
SELECT *
FROM customers
WHERE name LIKE 'A%';
```

**Real-world use case**  
A support team searches names that start with a letter.

**Practice**  
Find customers whose city starts with `D`.

**Key Takeaway**  
`LIKE` is useful for simple text matching.

---

## 22) Wildcards
**Explanation**  
Wildcards are special pattern symbols used with `LIKE`.

**Syntax**
```sql
%  -> any number of characters
_  -> exactly one character
```

**Example**
```sql
SELECT *
FROM customers
WHERE name LIKE '_e%';
```

**Real-world use case**  
Search flexible name patterns in customer data.

**Practice**  
Find names ending with `a`.

**Key Takeaway**  
`%` and `_` make pattern matching flexible.

---

## 23) IN operator
**Explanation**  
`IN` checks if a value matches any value in a list.

**Syntax**
```sql
WHERE column_name IN (value1, value2)
```

**Example**
```sql
SELECT *
FROM customers
WHERE city IN ('Delhi', 'Mumbai');
```

**Real-world use case**  
A campaign targets multiple cities at once.

**Practice**  
Find orders with status in `('Pending', 'Cancelled')`.

**Key Takeaway**  
`IN` is cleaner than many `OR` conditions.

---

## 24) BETWEEN operator
**Explanation**  
`BETWEEN` filters values in a range, usually inclusive.

**Syntax**
```sql
WHERE column_name BETWEEN low AND high
```

**Example**
```sql
SELECT *
FROM orders
WHERE amount BETWEEN 200 AND 500;
```

**Real-world use case**  
Finance teams report mid-range orders.

**Practice**  
Find salaries between 40000 and 55000.

**Key Takeaway**  
`BETWEEN` is handy for ranges.

---

## 25) IS NULL / IS NOT NULL
**Explanation**  
These test whether a value is missing.

**Syntax**
```sql
WHERE column_name IS NULL
WHERE column_name IS NOT NULL
```

**Example**
```sql
SELECT *
FROM customers
WHERE email IS NOT NULL;
```

**Real-world use case**  
A company checks profile completion.

**Practice**  
List employees with a manager.

**Key Takeaway**  
Never use `= NULL`; use `IS NULL`.

---

## 26) Aggregate functions (COUNT, SUM, AVG, MIN, MAX)
**Explanation**  
Aggregate functions summarize many rows into one value.

**Syntax**
```sql
SELECT COUNT(*), SUM(amount), AVG(amount), MIN(amount), MAX(amount)
FROM orders;
```

**Example**
```sql
SELECT COUNT(*) AS total_orders,
       SUM(amount) AS total_sales,
       AVG(amount) AS avg_order,
       MIN(amount) AS min_order,
       MAX(amount) AS max_order
FROM orders;
```

**Real-world use case**  
Managers view total sales and average order value.

**Practice**  
Count customers in `customers`.

**Key Takeaway**  
Aggregates summarize data quickly.

---

## 27) GROUP BY
**Explanation**  
`GROUP BY` groups rows so aggregates can be calculated per group.

**Syntax**
```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name;
```

**Example**
```sql
SELECT status, COUNT(*) AS total_orders
FROM orders
GROUP BY status;
```

**Real-world use case**  
Track number of orders by status.

**Practice**  
Group customers by city.

**Key Takeaway**  
`GROUP BY` creates summary rows.

---

## 28) HAVING
**Explanation**  
`HAVING` filters groups after `GROUP BY`.

**Syntax**
```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

**Example**
```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 500;
```

**Real-world use case**  
Find customers whose spending passes a target.

**Practice**  
Show statuses with more than 1 order.

**Key Takeaway**  
Use `WHERE` for rows and `HAVING` for groups.

---

## 29) CASE expression
**Explanation**  
`CASE` adds if-else style logic inside SQL.

**Syntax**
```sql
CASE
    WHEN condition THEN result
    ELSE result
END
```

**Example**
```sql
SELECT order_id,
       amount,
       CASE
           WHEN amount >= 500 THEN 'High'
           ELSE 'Low'
       END AS order_size
FROM orders;
```

**Real-world use case**  
Classify orders into small, medium, and large buckets.

**Practice**  
Label salaries above 50000 as `High Pay`.

**Key Takeaway**  
`CASE` adds conditional labels and logic.

---

## 30) INSERT
**Explanation**  
`INSERT` adds new rows.

**Syntax**
```sql
INSERT INTO table_name (col1, col2)
VALUES (val1, val2);
```

**Example**
```sql
INSERT INTO orders (order_id, customer_id, order_date, amount, status)
VALUES (105, 2, '2026-01-20', 900, 'Shipped');
```

**Real-world use case**  
A new order is stored when a customer checks out.

**Practice**  
Insert one product row.

**Key Takeaway**  
Use `INSERT` to add records.

---

## 31) CREATE TABLE
**Explanation**  
Defines a new table.

**Syntax**
```sql
CREATE TABLE table_name (
    col1 datatype,
    col2 datatype
);
```

**Example**
```sql
CREATE TABLE products (
    product_id INT,
    product_name VARCHAR(50),
    category VARCHAR(30),
    price DECIMAL(10,2)
);
```

**Real-world use case**  
A product catalog starts with a `products` table.

**Practice**  
Create a `departments` table.

**Key Takeaway**  
`CREATE TABLE` defines structure.

---

## 32) ALTER TABLE
**Explanation**  
Changes an existing table, such as adding or changing a column.

**Syntax**
```sql
ALTER TABLE table_name
ADD column_name datatype;
```

**Example**
```sql
ALTER TABLE customers
ADD phone VARCHAR(20);
```

**Real-world use case**  
A business later decides to store phone numbers.

**Practice**  
Add `dob DATE` to a `students` table.

**Key Takeaway**  
`ALTER TABLE` changes structure without recreating the table.

---

## 33) DROP TABLE
**Explanation**  
Deletes a table completely.

**Syntax**
```sql
DROP TABLE table_name;
```

**Example**
```sql
DROP TABLE old_backup;
```

**Real-world use case**  
Unused temporary tables are removed after migration.

**Practice**  
Write the command to drop `test_table`.

**Key Takeaway**  
`DROP TABLE` removes both structure and data.

---

## 34) TRUNCATE TABLE
**Explanation**  
Removes all rows quickly but keeps the table.

**Syntax**
```sql
TRUNCATE TABLE table_name;
```

**Example**
```sql
TRUNCATE TABLE staging_orders;
```

**Real-world use case**  
A staging table is emptied before the next daily load.

**Practice**  
What remains after `TRUNCATE`: table structure or data?

**Key Takeaway**  
`TRUNCATE` clears data fast and keeps the table.

---

## 35) RENAME TABLE / COLUMN
**Explanation**  
Renames a table or a column. Syntax varies by database.

**Syntax**
```sql
-- Example styles
ALTER TABLE old_name RENAME TO new_name;
ALTER TABLE customers RENAME COLUMN name TO customer_name;
```

**Example**
```sql
ALTER TABLE customers
RENAME COLUMN name TO full_name;
```

**Real-world use case**  
A team renames columns to match business language.

**Practice**  
Rename column `city` to `customer_city`.

**Key Takeaway**  
Renaming improves clarity without changing the data.

---

## 36) CREATE SCHEMA
**Explanation**  
Creates a schema to organize database objects.

**Syntax**
```sql
CREATE SCHEMA sales;
```

**Example**
```sql
CREATE SCHEMA reporting;
```

**Real-world use case**  
A company separates app tables and reporting tables.

**Practice**  
Create a schema named `hr`.

**Key Takeaway**  
Schemas help organize large databases.

---

# MODULE 2: INTERMEDIATE

## 37) Subqueries
**Explanation**  
A subquery is a query inside another query.

**Syntax**
```sql
SELECT *
FROM table_name
WHERE column_name = (SELECT ...);
```

**Example**
```sql
SELECT *
FROM orders
WHERE amount > (
    SELECT AVG(amount)
    FROM orders
);
```

**Real-world use case**  
Find orders above the average order value.

**Practice**  
Find employees whose salary is above average.

**Key Takeaway**  
Subqueries let one query use the result of another.

---

## 38) Correlated subqueries
**Explanation**  
A correlated subquery depends on the current row of the outer query.

**Syntax**
```sql
SELECT *
FROM t1
WHERE EXISTS (
    SELECT 1
    FROM t2
    WHERE t2.col = t1.col
);
```

**Example**
```sql
SELECT c.customer_id, c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

**Real-world use case**  
Find customers who have placed at least one order.

**Practice**  
Find employees who manage someone.

**Key Takeaway**  
Correlated subqueries run row by row using outer-row values.

---

## 39) EXISTS / NOT EXISTS
**Explanation**  
`EXISTS` checks whether a subquery returns any rows.

**Syntax**
```sql
WHERE EXISTS (subquery)
WHERE NOT EXISTS (subquery)
```

**Example**
```sql
SELECT c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

**Real-world use case**  
Find customers with no orders.

**Practice**  
Use `EXISTS` to list customers with orders.

**Key Takeaway**  
`EXISTS` is great for yes/no matching.

---

## 40) ANY / ALL
**Explanation**  
`ANY` compares with at least one value from a subquery. `ALL` compares with every value.

**Syntax**
```sql
WHERE value > ANY (subquery)
WHERE value > ALL (subquery)
```

**Example**
```sql
SELECT *
FROM orders
WHERE amount > ALL (
    SELECT amount
    FROM orders
    WHERE status = 'Cancelled'
);
```

**Real-world use case**  
Compare current sales with values from another group.

**Practice**  
Write a sentence explaining `> ANY`.

**Key Takeaway**  
`ANY` means at least one match; `ALL` means all matches.

---

## 41) Derived tables
**Explanation**  
A derived table is a subquery used in the `FROM` clause.

**Syntax**
```sql
SELECT *
FROM (subquery) AS alias;
```

**Example**
```sql
SELECT avg_data.customer_id, avg_data.total_spent
FROM (
    SELECT customer_id, SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id
) AS avg_data;
```

**Real-world use case**  
Create a summary first, then query the summary.

**Practice**  
Build a derived table that counts orders per status.

**Key Takeaway**  
Derived tables let you break a problem into steps.

---

## 42) SELECT INTO / CREATE TABLE AS
**Explanation**  
Creates a new table from the result of a query. Syntax depends on the database.

**Syntax**
```sql
-- SQL Server
SELECT *
INTO new_table
FROM old_table;

-- PostgreSQL / others
CREATE TABLE new_table AS
SELECT * FROM old_table;
```

**Example**
```sql
CREATE TABLE shipped_orders AS
SELECT *
FROM orders
WHERE status = 'Shipped';
```

**Real-world use case**  
Create a backup or reporting table.

**Practice**  
Create a new table with Delhi customers.

**Key Takeaway**  
Useful for quick copies and reporting tables.

---

## 43) Common Table Expressions (CTE)
**Explanation**  
A CTE is a temporary named result used in one query.

**Syntax**
```sql
WITH cte_name AS (
    SELECT ...
)
SELECT *
FROM cte_name;
```

**Example**
```sql
WITH customer_totals AS (
    SELECT customer_id, SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM customer_totals
WHERE total_spent > 500;
```

**Real-world use case**  
Make complex queries easier to read.

**Practice**  
Create a CTE that lists total orders by customer.

**Key Takeaway**  
CTEs improve readability and step-by-step logic.

---

## 44) Recursive CTE
**Explanation**  
A recursive CTE repeats itself to work through hierarchical data.

**Syntax**
```sql
WITH RECURSIVE cte_name AS (
    SELECT ...
    UNION ALL
    SELECT ...
    FROM cte_name
)
SELECT * FROM cte_name;
```

**Example**
```sql
WITH RECURSIVE emp_tree AS (
    SELECT emp_id, emp_name, manager_id, 1 AS level_no
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT e.emp_id, e.emp_name, e.manager_id, et.level_no + 1
    FROM employees e
    JOIN emp_tree et
      ON e.manager_id = et.emp_id
)
SELECT *
FROM emp_tree;
```

**Real-world use case**  
Show company org charts or category trees.

**Practice**  
What type of data is best for recursive CTEs?

**Key Takeaway**  
Recursive CTEs are useful for hierarchical data.

---

## 45) Window functions overview
**Explanation**  
Window functions calculate values across related rows without collapsing them into one row like `GROUP BY` does.

**Syntax**
```sql
function_name() OVER (PARTITION BY ... ORDER BY ...)
```

**Example**
```sql
SELECT order_id,
       customer_id,
       amount,
       SUM(amount) OVER (PARTITION BY customer_id) AS customer_total
FROM orders;
```

**Real-world use case**  
Show each order plus the customer’s total spend.

**Practice**  
Name one difference between `GROUP BY` and window functions.

**Key Takeaway**  
Window functions keep detail rows and add extra calculations.

---

## 46) Ranking functions (ROW_NUMBER, RANK, DENSE_RANK)
**Explanation**  
These assign rank numbers to rows.

**Syntax**
```sql
ROW_NUMBER() OVER (...)
RANK() OVER (...)
DENSE_RANK() OVER (...)
```

**Example**
```sql
SELECT emp_name,
       department,
       salary,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_num,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rnk,
       DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dense_rnk
FROM employees;
```

**Real-world use case**  
Find top earners in each department.

**Practice**  
Which function leaves gaps after ties: `RANK` or `DENSE_RANK`?

**Key Takeaway**  
Use ranking functions for leaderboards and top-N analysis.

---

## 47) Analytic functions (LAG, LEAD, FIRST_VALUE, LAST_VALUE)
**Explanation**  
These compare rows with previous, next, first, or last rows in a window.

**Syntax**
```sql
LAG(column) OVER (...)
LEAD(column) OVER (...)
```

**Example**
```sql
SELECT order_id,
       order_date,
       amount,
       LAG(amount) OVER (ORDER BY order_date) AS previous_amount,
       LEAD(amount) OVER (ORDER BY order_date) AS next_amount
FROM orders;
```

**Real-world use case**  
Compare today’s sales with the previous day.

**Practice**  
Which function shows the previous row value?

**Key Takeaway**  
Analytic functions help with comparisons across rows.

---

## 48) Window frames and running totals
**Explanation**  
A window frame defines which rows are included in the calculation.

**Syntax**
```sql
SUM(amount) OVER (
    ORDER BY order_date
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
)
```

**Example**
```sql
SELECT order_id,
       order_date,
       amount,
       SUM(amount) OVER (
           ORDER BY order_date
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS running_total
FROM orders;
```

**Real-world use case**  
Track cumulative sales over time.

**Practice**  
What does `CURRENT ROW` mean in a running total?

**Key Takeaway**  
Frames control how much of the window is used in a calculation.

---

## 49) PIVOT / UNPIVOT
**Explanation**  
`PIVOT` turns row values into columns. `UNPIVOT` does the opposite. Syntax differs by database.

**Syntax**
```sql
-- Conceptual only: syntax varies by platform
```

**Example**
```text
Before:
status     total
Shipped    2
Pending    1

After pivot:
Shipped | Pending
2       | 1
```

**Real-world use case**  
Create report-style summaries for dashboards.

**Practice**  
Would pivoting turn cities into rows or columns?

**Key Takeaway**  
Pivot reshapes data for reporting.

---

## 50) Set operators (UNION, UNION ALL, INTERSECT, EXCEPT / MINUS)
**Explanation**  
Set operators combine results from multiple queries.

**Syntax**
```sql
query1 UNION query2
query1 UNION ALL query2
query1 INTERSECT query2
query1 EXCEPT query2
```

**Example**
```sql
SELECT city FROM customers
UNION
SELECT department FROM employees;
```

**Real-world use case**  
Combine customer and lead lists.

**Practice**  
What is the difference between `UNION` and `UNION ALL`?

**Key Takeaway**  
Use set operators to combine query results.

---

## 51) INSERT INTO SELECT
**Explanation**  
Copies rows from one table into another.

**Syntax**
```sql
INSERT INTO target_table (col1, col2)
SELECT col1, col2
FROM source_table;
```

**Example**
```sql
INSERT INTO shipped_orders (order_id, customer_id, order_date, amount, status)
SELECT order_id, customer_id, order_date, amount, status
FROM orders
WHERE status = 'Shipped';
```

**Real-world use case**  
Move selected data into a reporting table.

**Practice**  
Copy Delhi customers into another table.

**Key Takeaway**  
Useful for copying query results into tables.

---

## 52) UPDATE
**Explanation**  
Changes existing rows.

**Syntax**
```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

**Example**
```sql
UPDATE orders
SET status = 'Shipped'
WHERE order_id = 102;
```

**Real-world use case**  
Update order status after shipping.

**Practice**  
Change `Cara`'s city to `Pune`.

**Key Takeaway**  
Always use `WHERE` carefully with `UPDATE`.

---

## 53) DELETE
**Explanation**  
Removes rows from a table.

**Syntax**
```sql
DELETE FROM table_name
WHERE condition;
```

**Example**
```sql
DELETE FROM orders
WHERE status = 'Cancelled';
```

**Real-world use case**  
Remove test data from a table.

**Practice**  
Delete products where price is below 100.

**Key Takeaway**  
Without `WHERE`, all rows can be deleted.

---

## 54) Constraints overview
**Explanation**  
Constraints are rules that keep data accurate.

**Syntax**
```sql
NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, DEFAULT
```

**Example**
```sql
CREATE TABLE demo_constraints (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18)
);
```

**Real-world use case**  
Prevent bad customer records.

**Practice**  
Name two constraints.

**Key Takeaway**  
Constraints protect data quality.

---

## 55) NOT NULL constraint
**Explanation**  
Prevents empty values in a column.

**Syntax**
```sql
column_name datatype NOT NULL
```

**Example**
```sql
CREATE TABLE students (
    student_id INT,
    name VARCHAR(50) NOT NULL
);
```

**Real-world use case**  
A customer name must always exist.

**Practice**  
Make `email` required.

**Key Takeaway**  
`NOT NULL` makes a field mandatory.

---

## 56) UNIQUE constraint
**Explanation**  
No duplicate values are allowed.

**Syntax**
```sql
column_name datatype UNIQUE
```

**Example**
```sql
CREATE TABLE users (
    user_id INT,
    email VARCHAR(100) UNIQUE
);
```

**Real-world use case**  
Two users should not share the same email.

**Practice**  
Which field is often unique in login systems?

**Key Takeaway**  
`UNIQUE` stops duplicates.

---

## 57) PRIMARY KEY
**Explanation**  
A primary key uniquely identifies each row.

**Syntax**
```sql
column_name datatype PRIMARY KEY
```

**Example**
```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50)
);
```

**Real-world use case**  
Each customer needs a unique ID.

**Practice**  
Pick a primary key for `orders`.

**Key Takeaway**  
A primary key is unique and not null.

---

## 58) FOREIGN KEY
**Explanation**  
A foreign key links one table to another.

**Syntax**
```sql
FOREIGN KEY (column_name) REFERENCES other_table(other_column)
```

**Example**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

**Real-world use case**  
Every order should belong to a valid customer.

**Practice**  
Which column in `orders` should reference `customers`?

**Key Takeaway**  
Foreign keys create relationships and protect references.

---

## 59) CHECK constraint
**Explanation**  
Limits allowed values using a condition.

**Syntax**
```sql
CHECK (condition)
```

**Example**
```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    salary DECIMAL(10,2) CHECK (salary > 0)
);
```

**Real-world use case**  
Prevent negative salary values.

**Practice**  
Write a check for age >= 18.

**Key Takeaway**  
`CHECK` enforces simple business rules.

---

## 60) DEFAULT constraint
**Explanation**  
Automatically uses a value when none is given.

**Syntax**
```sql
column_name datatype DEFAULT value
```

**Example**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'Pending'
);
```

**Real-world use case**  
New orders start as `Pending` by default.

**Practice**  
Set a default city as `Unknown`.

**Key Takeaway**  
`DEFAULT` saves time and keeps values consistent.

---

## 61) AUTO_INCREMENT / IDENTITY / SEQUENCE
**Explanation**  
These generate automatic numeric IDs. The name depends on the database.

**Syntax**
```sql
-- MySQL
id INT AUTO_INCREMENT PRIMARY KEY

-- SQL Server
id INT IDENTITY(1,1) PRIMARY KEY

-- PostgreSQL / Oracle concept
CREATE SEQUENCE seq_name;
```

**Example**
```sql
CREATE TABLE products (
    product_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    product_name VARCHAR(50)
);
```

**Real-world use case**  
A new customer gets an automatic ID when inserted.

**Practice**  
Why are generated IDs useful?

**Key Takeaway**  
Automatic keys reduce manual mistakes.

---

## 62) CREATE INDEX
**Explanation**  
An index helps the database find data faster.

**Syntax**
```sql
CREATE INDEX index_name
ON table_name (column_name);
```

**Example**
```sql
CREATE INDEX idx_orders_customer_id
ON orders (customer_id);
```

**Real-world use case**  
Speed up searches on frequently filtered columns.

**Practice**  
Which column in `orders` would be a good index for joins?

**Key Takeaway**  
Indexes improve read speed, especially on searched columns.

---

## 63) DROP / ALTER / REBUILD INDEX
**Explanation**  
You can remove or maintain indexes. Syntax depends on the database.

**Syntax**
```sql
DROP INDEX index_name;
-- ALTER / REBUILD syntax varies
```

**Example**
```sql
DROP INDEX idx_orders_customer_id;
```

**Real-world use case**  
Remove unused indexes that slow down writes.

**Practice**  
Why should you not create too many indexes?

**Key Takeaway**  
Indexes need maintenance and should be used wisely.

---

## 64) CREATE VIEW
**Explanation**  
A view is a saved query that acts like a virtual table.

**Syntax**
```sql
CREATE VIEW view_name AS
SELECT ...
```

**Example**
```sql
CREATE VIEW customer_order_totals AS
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id;
```

**Real-world use case**  
Simplify common reports for business users.

**Practice**  
Create a view of shipped orders.

**Key Takeaway**  
Views hide complexity and improve reuse.

---

## 65) ALTER / DROP VIEW
**Explanation**  
Changes or removes a view. Syntax depends on the database.

**Syntax**
```sql
CREATE OR REPLACE VIEW view_name AS ...
DROP VIEW view_name;
```

**Example**
```sql
DROP VIEW customer_order_totals;
```

**Real-world use case**  
Update a reporting view when business logic changes.

**Practice**  
Write the command to drop `shipped_orders_view`.

**Key Takeaway**  
Views can be maintained like other database objects.

---

## 66) Temporary tables
**Explanation**  
Temporary tables store short-term data for the current session or process.

**Syntax**
```sql
CREATE TEMP TABLE temp_name (...);
```

**Example**
```sql
CREATE TEMP TABLE temp_delhi_customers AS
SELECT *
FROM customers
WHERE city = 'Delhi';
```

**Real-world use case**  
Break a big process into smaller steps.

**Practice**  
Why might a temp table be useful in reporting?

**Key Takeaway**  
Temporary tables are useful for short-lived intermediate data.

---

## 67) INNER JOIN
**Explanation**  
Returns only matching rows from both tables.

**Syntax**
```sql
SELECT ...
FROM table1
INNER JOIN table2
  ON table1.col = table2.col;
```

**Example**
```sql
SELECT c.name, o.order_id, o.amount
FROM customers c
INNER JOIN orders o
  ON c.customer_id = o.customer_id;
```

**Real-world use case**  
Show customers and their orders.

**Practice**  
Join `orders` and `customers`.

**Key Takeaway**  
`INNER JOIN` keeps only matches.

---

## 68) LEFT JOIN
**Explanation**  
Returns all rows from the left table and matching rows from the right table.

**Syntax**
```sql
SELECT ...
FROM left_table
LEFT JOIN right_table
  ON left_table.col = right_table.col;
```

**Example**
```sql
SELECT c.name, o.order_id
FROM customers c
LEFT JOIN orders o
  ON c.customer_id = o.customer_id;
```

**Real-world use case**  
Show all customers, even those without orders.

**Practice**  
Which side’s rows are always kept in a left join?

**Key Takeaway**  
`LEFT JOIN` keeps every row from the left table.

---

## 69) RIGHT JOIN
**Explanation**  
Returns all rows from the right table and matching rows from the left table.

**Syntax**
```sql
SELECT ...
FROM left_table
RIGHT JOIN right_table
  ON left_table.col = right_table.col;
```

**Example**
```sql
SELECT c.name, o.order_id
FROM customers c
RIGHT JOIN orders o
  ON c.customer_id = o.customer_id;
```

**Real-world use case**  
Keep all orders, even if customer data is missing.

**Practice**  
How is right join related to left join?

**Key Takeaway**  
`RIGHT JOIN` keeps every row from the right table.

---

## 70) FULL OUTER JOIN
**Explanation**  
Returns all rows from both tables, matching where possible.

**Syntax**
```sql
SELECT ...
FROM t1
FULL OUTER JOIN t2
  ON t1.col = t2.col;
```

**Example**
```sql
SELECT c.name, o.order_id
FROM customers c
FULL OUTER JOIN orders o
  ON c.customer_id = o.customer_id;
```

**Real-world use case**  
Compare two lists and see matches and non-matches.

**Practice**  
When would a full outer join be useful?

**Key Takeaway**  
It shows matches and unmatched rows from both sides.

---

## 71) CROSS JOIN
**Explanation**  
Returns every combination of rows from both tables.

**Syntax**
```sql
SELECT ...
FROM t1
CROSS JOIN t2;
```

**Example**
```sql
SELECT c.name, p.product_name
FROM customers c
CROSS JOIN products p;
```

**Real-world use case**  
Generate all customer-product combinations for testing.

**Practice**  
If one table has 3 rows and another has 2, how many rows after cross join?

**Key Takeaway**  
Cross join creates all possible combinations.

---

## 72) SELF JOIN
**Explanation**  
A table joined to itself.

**Syntax**
```sql
SELECT ...
FROM table_name a
JOIN table_name b
  ON a.col = b.col;
```

**Example**
```sql
SELECT e.emp_name AS employee,
       m.emp_name AS manager
FROM employees e
LEFT JOIN employees m
  ON e.manager_id = m.emp_id;
```

**Real-world use case**  
Show employees and their managers.

**Practice**  
Which table in our sample is good for a self join?

**Key Takeaway**  
Self joins are useful for hierarchical relationships.

---

## 73) Multi-table joins
**Explanation**  
Joins can include more than two tables.

**Syntax**
```sql
SELECT ...
FROM t1
JOIN t2 ON ...
JOIN t3 ON ...;
```

**Example**
```sql
SELECT c.name, o.order_id, p.product_name, oi.qty
FROM customers c
JOIN orders o
  ON c.customer_id = o.customer_id
JOIN order_items oi
  ON o.order_id = oi.order_id
JOIN products p
  ON oi.product_id = p.product_id;
```

**Real-world use case**  
Show customer, order, and product details in one report.

**Practice**  
How many joins are needed to include customers, orders, and products?

**Key Takeaway**  
Complex reports often need several joined tables.

---

## 74) Joining aggregated data
**Explanation**  
You can join a detail table to an aggregated result.

**Syntax**
```sql
SELECT ...
FROM table1 t
JOIN (
    SELECT key, aggregate_function(...)
    FROM table2
    GROUP BY key
) x
  ON t.key = x.key;
```

**Example**
```sql
SELECT c.name, totals.total_spent
FROM customers c
JOIN (
    SELECT customer_id, SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id
) totals
  ON c.customer_id = totals.customer_id;
```

**Real-world use case**  
Show each customer with total spend.

**Practice**  
Build a total orders per customer subquery.

**Key Takeaway**  
Aggregate first, then join to detail or master data.

---

## 75) Join conditions and join order
**Explanation**  
Join conditions tell SQL how tables relate. A wrong join condition can duplicate or lose rows.

**Syntax**
```sql
... JOIN table2 ON table1.key = table2.key
```

**Example**
```sql
SELECT *
FROM customers c
JOIN orders o
  ON c.customer_id = o.customer_id;
```

**Real-world use case**  
Correct joins keep reports accurate.

**Practice**  
Which columns connect `customers` and `orders`?

**Key Takeaway**  
Good joins depend on correct matching columns.

---

## 76) Referential integrity basics
**Explanation**  
Referential integrity means related data stays valid. For example, an order should not point to a customer that does not exist.

**Syntax**
```sql
FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
```

**Example**
```text
Allowed: orders.customer_id = 1 when customer 1 exists
Not allowed: orders.customer_id = 999 when no such customer exists
```

**Real-world use case**  
Prevents broken links in business data.

**Practice**  
Why is referential integrity important?

**Key Takeaway**  
It keeps relationships correct and trusted.

---

## 77) Many-to-many relationships
**Explanation**  
Many records in one table can match many records in another. This is handled using a bridge table.

**Syntax**
```text
orders >----< products
using order_items(order_id, product_id, qty)
```

**Example**
```sql
SELECT *
FROM order_items;
```

**Real-world use case**  
One order can include many products, and one product can appear in many orders.

**Practice**  
Name the bridge table in our sample data.

**Key Takeaway**  
Many-to-many relationships need a linking table.

---

## 78) String functions
**Explanation**  
String functions work with text.

**Syntax**
```sql
UPPER(), LOWER(), LENGTH(), SUBSTRING(), TRIM(), CONCAT()
```

**Example**
```sql
SELECT UPPER(name) AS upper_name,
       LENGTH(name) AS name_len
FROM customers;
```

**Real-world use case**  
Clean names and format text for reports.

**Practice**  
Convert all customer names to lowercase.

**Key Takeaway**  
String functions help clean and transform text.

---

## 79) Numeric functions
**Explanation**  
Numeric functions work with numbers.

**Syntax**
```sql
ROUND(), ABS(), CEILING(), FLOOR()
```

**Example**
```sql
SELECT amount,
       ROUND(amount / 3.0, 2) AS split_amount,
       ABS(-10) AS abs_value
FROM orders;
```

**Real-world use case**  
Round totals in invoices.

**Practice**  
Round product prices to 0 decimal places.

**Key Takeaway**  
Numeric functions help calculate and format values.

---

## 80) Date and time functions
**Explanation**  
These functions work with dates and timestamps. Exact names vary by database.

**Syntax**
```sql
CURRENT_DATE
CURRENT_TIMESTAMP
EXTRACT(YEAR FROM date_col)
DATEADD(...)
DATEDIFF(...)
```

**Example**
```sql
SELECT order_date,
       EXTRACT(YEAR FROM order_date) AS order_year
FROM orders;
```

**Real-world use case**  
Create monthly sales reports.

**Practice**  
Extract the year from `order_date`.

**Key Takeaway**  
Date functions are essential for time-based analysis.

---

## 81) Conversion / CAST / CONVERT
**Explanation**  
These change a value from one data type to another.

**Syntax**
```sql
CAST(value AS datatype)
CONVERT(datatype, value)   -- SQL Server style
```

**Example**
```sql
SELECT CAST(amount AS INT) AS amount_int
FROM orders;
```

**Real-world use case**  
Convert imported text data into numbers or dates.

**Practice**  
Cast product price to integer.

**Key Takeaway**  
Type conversion helps when data types do not match.

---

## 82) COALESCE / IFNULL / ISNULL
**Explanation**  
These replace `NULL` with another value. The exact function depends on the database.

**Syntax**
```sql
COALESCE(col, replacement)
IFNULL(col, replacement)
ISNULL(col, replacement)
```

**Example**
```sql
SELECT name,
       COALESCE(email, 'no_email@example.com') AS fixed_email
FROM customers;
```

**Real-world use case**  
Show fallback values in reports instead of blanks.

**Practice**  
Replace null city with `Unknown`.

**Key Takeaway**  
Use null-handling functions to avoid empty results.

---

## 83) Conditional logic with CASE / IF / IIF
**Explanation**  
These add conditions inside SQL. `CASE` is the most portable.

**Syntax**
```sql
CASE WHEN condition THEN result ELSE result END
```

**Example**
```sql
SELECT emp_name,
       salary,
       CASE
           WHEN salary >= 50000 THEN 'Senior'
           ELSE 'Junior'
       END AS level_name
FROM employees;
```

**Real-world use case**  
Bucket customers, products, or salaries.

**Practice**  
Label order status `Pending` as `Open`.

**Key Takeaway**  
Use conditional logic to create categories and custom outputs.

---

## 84) Regular expressions in SQL
**Explanation**  
Regular expressions allow more advanced text matching than `LIKE`. Syntax varies by database.

**Syntax**
```sql
-- Example concept
WHERE column_name REGEXP 'pattern'
```

**Example**
```sql
SELECT *
FROM customers
WHERE email REGEXP '^[a-zA-Z0-9._%+-]+@';
```

**Real-world use case**  
Validate email-like patterns in data cleaning.

**Practice**  
When would regex be better than `LIKE`?

**Key Takeaway**  
Regex is powerful for complex text patterns.

---

## 85) User-defined functions (UDFs)
**Explanation**  
A UDF is a custom function you create to reuse logic.

**Syntax**
```sql
CREATE FUNCTION function_name(...)
RETURNS ...
AS
BEGIN
    ...
END;
```

**Example**
```sql
-- Example idea
CREATE FUNCTION get_tax_amount (@amt DECIMAL(10,2))
RETURNS DECIMAL(10,2)
AS
BEGIN
    RETURN @amt * 0.18;
END;
```

**Real-world use case**  
Reuse tax or discount calculations.

**Practice**  
What kind of repeated logic could fit in a UDF?

**Key Takeaway**  
UDFs make repeated logic reusable.

---

## 86) Stored procedures
**Explanation**  
A stored procedure is a saved set of SQL statements that can be run as one unit.

**Syntax**
```sql
CREATE PROCEDURE procedure_name
AS
BEGIN
    ...
END;
```

**Example**
```sql
-- Example idea
CREATE PROCEDURE GetShippedOrders
AS
BEGIN
    SELECT *
    FROM orders
    WHERE status = 'Shipped';
END;
```

**Real-world use case**  
Apps call procedures to run standard business operations.

**Practice**  
Would a stored procedure be good for a daily report? Why?

**Key Takeaway**  
Stored procedures package SQL steps together.

---

## 87) Dynamic SQL
**Explanation**  
Dynamic SQL builds SQL as text and runs it. It is flexible but must be used carefully.

**Syntax**
```sql
-- Conceptual
SET @sql = 'SELECT * FROM ' + @table_name;
EXEC(@sql);
```

**Example**
```sql
-- Example idea only
```

**Real-world use case**  
Admin tools may query different tables based on input.

**Practice**  
Why can dynamic SQL be risky?

**Key Takeaway**  
Dynamic SQL is powerful, but unsafe string building can cause problems.

---

## 88) GRANT
**Explanation**  
`GRANT` gives permissions to users or roles.

**Syntax**
```sql
GRANT privilege ON object TO user_or_role;
```

**Example**
```sql
GRANT SELECT ON customers TO analyst_role;
```

**Real-world use case**  
Allow analysts to read reports but not change data.

**Practice**  
Grant select on `orders` to `report_user`.

**Key Takeaway**  
Use `GRANT` to control access safely.

---

## 89) REVOKE
**Explanation**  
`REVOKE` removes permissions.

**Syntax**
```sql
REVOKE privilege ON object FROM user_or_role;
```

**Example**
```sql
REVOKE UPDATE ON customers FROM analyst_role;
```

**Real-world use case**  
Remove extra access when a role changes.

**Practice**  
Revoke delete permission from a user.

**Key Takeaway**  
Use `REVOKE` to reduce or remove access.

---

## 90) Roles and privileges
**Explanation**  
A **role** is a group of permissions. **Privileges** are the individual permissions such as `SELECT`, `INSERT`, or `UPDATE`.

**Syntax**
```text
Role -> collection of privileges
```

**Example**
```text
analyst_role -> SELECT on reporting tables
admin_role   -> full access
```

**Real-world use case**  
Give the same access to many employees by role.

**Practice**  
Which is easier to manage for many users: direct grants or roles?

**Key Takeaway**  
Roles make permission management simpler.

---

## 91) COMMIT
**Explanation**  
`COMMIT` saves transaction changes permanently.

**Syntax**
```sql
COMMIT;
```

**Example**
```sql
UPDATE accounts
SET balance = balance - 100
WHERE account_id = 1;

COMMIT;
```

**Real-world use case**  
After a successful payment transfer, save the changes.

**Practice**  
What happens if you commit after an update?

**Key Takeaway**  
`COMMIT` makes transaction changes final.

---

## 92) ROLLBACK
**Explanation**  
`ROLLBACK` undoes uncommitted changes.

**Syntax**
```sql
ROLLBACK;
```

**Example**
```sql
UPDATE orders
SET amount = amount * 10;

ROLLBACK;
```

**Real-world use case**  
Undo a mistaken update before saving it.

**Practice**  
When is rollback useful?

**Key Takeaway**  
`ROLLBACK` is a safety button during transactions.

---

## 93) SAVEPOINT
**Explanation**  
A savepoint marks a point inside a transaction that you can roll back to.

**Syntax**
```sql
SAVEPOINT savepoint_name;
ROLLBACK TO savepoint_name;
```

**Example**
```sql
SAVEPOINT before_discount;

UPDATE orders
SET amount = amount * 0.9;

ROLLBACK TO before_discount;
```

**Real-world use case**  
Undo only part of a multi-step transaction.

**Practice**  
What is the advantage of a savepoint over full rollback?

**Key Takeaway**  
Savepoints give finer control inside transactions.

---

## 94) ACID properties
**Explanation**  
ACID describes reliable transactions:
- **Atomicity**: all or nothing
- **Consistency**: rules stay valid
- **Isolation**: transactions do not interfere badly
- **Durability**: committed data stays saved

**Syntax**  
No direct syntax. This is a concept.

**Example**
```text
Bank transfer:
debit + credit must both happen or neither happens
```

**Real-world use case**  
Critical systems like banking rely on ACID.

**Practice**  
Which ACID property means changes stay saved after commit?

**Key Takeaway**  
ACID makes database transactions reliable.

---

## 95) Concurrency control / MVCC
**Explanation**  
Concurrency control manages many users working at the same time. MVCC lets readers see a stable version of data without blocking as much.

**Syntax**  
Mostly controlled by the database engine.

**Example**
```text
User A reads row version 1
User B updates same row to version 2
User A can still finish reading version 1 safely
```

**Real-world use case**  
Large apps need many users to read and write at once.

**Practice**  
Why is MVCC helpful for readers?

**Key Takeaway**  
Concurrency control keeps simultaneous work safe and efficient.

---

# MODULE 3: ADVANCED

## 96) Transaction isolation levels
**Explanation**  
Isolation level controls how much one transaction can see from another transaction’s changes.

**Syntax**
```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

**Example**
```text
Common levels:
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

**Real-world use case**  
A finance system may use stricter isolation for accuracy.

**Practice**  
Which level is usually stricter: `READ COMMITTED` or `SERIALIZABLE`?

**Key Takeaway**  
Higher isolation usually means safer results but more blocking.

---

## 97) Locks and blocking
**Explanation**  
A lock protects data while it is being changed. Blocking happens when one transaction waits for another to release a lock.

**Syntax**  
Usually managed automatically by the database.

**Example**
```text
User A updates order 101 -> row is locked
User B tries to update order 101 -> waits
```

**Real-world use case**  
Busy systems can slow down when long transactions hold locks.

**Practice**  
What causes blocking?

**Key Takeaway**  
Long-running transactions can block other work.

---

## 98) Deadlocks
**Explanation**  
A deadlock happens when two transactions wait on each other and neither can continue.

**Syntax**  
Managed by the database engine.

**Example**
```text
Transaction A locks row 1, waits for row 2
Transaction B locks row 2, waits for row 1
```

**Real-world use case**  
Can happen in high-write systems with poor update order.

**Practice**  
How can consistent update order reduce deadlocks?

**Key Takeaway**  
Deadlocks happen when transactions block each other in a circle.

---

## 99) Normalization (1NF, 2NF, 3NF, BCNF)
**Explanation**  
Normalization organizes data to reduce duplication and improve consistency.

**Syntax**  
No direct syntax. This is a design concept.

**Example**
```text
1NF  -> atomic values, no repeating groups
2NF  -> remove partial dependency
3NF  -> remove transitive dependency
BCNF -> stronger form of 3NF
```

**Real-world use case**  
Split customer and order data into separate tables instead of repeating customer details in every order row.

**Practice**  
Why is storing the same customer address in every order row a problem?

**Key Takeaway**  
Normalization reduces repeated data and update problems.

---

## 100) Denormalization
**Explanation**  
Denormalization means intentionally adding some duplication to improve read speed.

**Syntax**  
No single syntax; it is a design choice.

**Example**
```text
Store customer_name directly in a reporting table for faster dashboards
```

**Real-world use case**  
Reporting systems may duplicate some data for speed.

**Practice**  
What is the trade-off of denormalization?

**Key Takeaway**  
Denormalization can speed reads but may increase duplication.

---

## 101) Indexes and indexing strategy
**Explanation**  
An indexing strategy decides which columns should be indexed based on query patterns.

**Syntax**
```sql
CREATE INDEX idx_name ON table_name(column_name);
```

**Example**
```text
Good index candidates:
- join columns
- frequently filtered columns
- frequently sorted columns
```

**Real-world use case**  
Index `customer_id` on `orders` for joins and search.

**Practice**  
Name one bad reason to add an index.

**Key Takeaway**  
Index what you query often, not everything.

---

## 102) Clustered vs non-clustered indexes
**Explanation**  
A clustered index affects the physical order of table data. A non-clustered index is a separate lookup structure.

**Syntax**  
Syntax varies by database.

**Example**
```text
Clustered index -> table data stored in index order
Non-clustered   -> separate structure pointing to data rows
```

**Real-world use case**  
A table may be clustered by `order_id` and have a non-clustered index on `customer_id`.

**Practice**  
How many clustered indexes can a table usually have?

**Key Takeaway**  
Clustered changes storage order; non-clustered does not.

---

## 103) Execution plans / EXPLAIN
**Explanation**  
An execution plan shows how the database will run a query.

**Syntax**
```sql
EXPLAIN
SELECT ...
```

**Example**
```sql
EXPLAIN
SELECT *
FROM orders
WHERE customer_id = 1;
```

**Real-world use case**  
Used to find slow steps like full table scans.

**Practice**  
What is one thing you might look for in an execution plan?

**Key Takeaway**  
Execution plans help explain why a query is fast or slow.

---

## 104) Query optimization
**Explanation**  
Query optimization means writing SQL in a way that runs efficiently.

**Syntax**  
No single syntax. It is a method.

**Example**
```text
Better:
- select only needed columns
- filter early
- index searched columns
- avoid unnecessary functions on indexed columns
```

**Real-world use case**  
A slow report is improved by indexing and rewriting joins.

**Practice**  
Why is `SELECT *` not always ideal?

**Key Takeaway**  
Fast queries save time and resources.

---

## 105) Views for security
**Explanation**  
Views can hide sensitive columns and expose only allowed data.

**Syntax**
```sql
CREATE VIEW safe_customer_view AS
SELECT customer_id, name, city
FROM customers;
```

**Example**
```sql
CREATE VIEW customer_public_view AS
SELECT customer_id, name, city
FROM customers;
```

**Real-world use case**  
Analysts may see customer names but not private email addresses.

**Practice**  
Which column from `customers` might be hidden for privacy?

**Key Takeaway**  
Views can simplify and secure data access.

---

## 106) SQL injection prevention
**Explanation**  
SQL injection is a security problem where unsafe input changes a query. The safest fix is to use parameterized queries.

**Syntax**
```text
Use parameters / prepared statements instead of string-building SQL
```

**Example**
```text
Unsafe:
"SELECT * FROM users WHERE name = '" + user_input + "'"

Safe:
SELECT * FROM users WHERE name = ?
```

**Real-world use case**  
Login forms must not build SQL with raw user input.

**Practice**  
What is safer: concatenating input or parameterized queries?

**Key Takeaway**  
Never build SQL directly from untrusted input.

---

## 107) Backup and restore
**Explanation**  
A backup is a saved copy of the database. Restore brings data back from that copy.

**Syntax**  
Commands vary by database tool and platform.

**Example**
```text
Backup -> save current database safely
Restore -> recover after data loss or system failure
```

**Real-world use case**  
Recover data after accidental deletion or server failure.

**Practice**  
Why should backups be tested, not just created?

**Key Takeaway**  
Backups matter only if you can restore successfully.

---

# QUICK REVISION: COMMON QUERY ORDER

```text
SELECT
FROM
JOIN
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT / FETCH
```

---

# MINI CHEAT SHEET

## Basic select
```sql
SELECT name, city
FROM customers
WHERE city = 'Delhi'
ORDER BY name;
```

## Aggregate with group
```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 500;
```

## Join
```sql
SELECT c.name, o.order_id, o.amount
FROM customers c
JOIN orders o
  ON c.customer_id = o.customer_id;
```

## Window function
```sql
SELECT order_id,
       customer_id,
       amount,
       SUM(amount) OVER (PARTITION BY customer_id) AS customer_total
FROM orders;
```

## CTE
```sql
WITH totals AS (
    SELECT customer_id, SUM(amount) AS total_spent
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM totals;
```

---

# PRACTICE BLOCKS

## Practice Set 1: Basics
1. Show all customers.
2. Show distinct cities.
3. Find shipped orders.
4. Sort orders by amount descending.
5. Find customers with null emails.

## Practice Set 2: Intermediate
1. Count orders by status.
2. Show customers and their orders using an inner join.
3. Show all customers even if they have no orders.
4. Create a CTE for customer totals.
5. Copy shipped orders into a new table.

## Practice Set 3: Advanced
1. Rank employees by salary within department.
2. Show a running total of order amounts by date.
3. Use `EXPLAIN` on a filtered query.
4. Create a view hiding customer email.
5. Write one rule to prevent SQL injection.

---

# FINAL LEARNING PATH

```text
Step 1  -> Learn tables, rows, columns, SELECT, WHERE
Step 2  -> Learn ORDER BY, LIKE, IN, BETWEEN, NULL
Step 3  -> Learn aggregates, GROUP BY, HAVING, CASE
Step 4  -> Learn INSERT, UPDATE, DELETE, constraints
Step 5  -> Learn joins and relationships
Step 6  -> Learn subqueries, CTEs, window functions
Step 7  -> Learn transactions, indexes, optimization, security
```

---

# FINAL SUMMARY
SQL helps you:
- store data
- read data
- change data
- connect related tables
- summarize information
- secure and optimize databases

For beginners, the best order is:
1. Basics of tables and queries  
2. Filtering and sorting  
3. Grouping and aggregates  
4. Joins and relationships  
5. Data modification and table design  
6. Advanced analytics and performance  
7. Security, transactions, and administration  

The most important habit is: **practice every topic with small queries**.
