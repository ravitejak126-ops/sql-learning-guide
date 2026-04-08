# SQL Study Notes: Stored Procedures, Parameters, and Indexing

## 1. Stored Procedures

### Definition
A stored procedure is a saved set of SQL statements that can be executed whenever needed.

### Syntax
```sql
CREATE PROCEDURE procedure_name
AS
BEGIN
    -- SQL statements
END;
```

### Example
```sql
CREATE PROCEDURE GetAllEmployees
AS
BEGIN
    SELECT * FROM employees;
END;

EXEC GetAllEmployees;
```

### Common Mistakes
- Using stored procedures for very simple one-line queries without need
- Not handling errors or edge cases
- Writing procedures that are too large and hard to maintain

### When to Use
- When logic needs to be reused
- When you want to centralize business logic in the database
- When you want controlled access to data

### Key Interview Points
- Stored procedures are reusable database programs
- They can accept parameters
- They can improve maintainability and reduce repeated SQL code

---

## 2. Input Parameters

### Definition
Input parameters let you pass values into a stored procedure.

### Syntax
```sql
CREATE PROCEDURE procedure_name
    @param_name datatype
AS
BEGIN
    -- SQL statements
END;
```

### Example
```sql
CREATE PROCEDURE GetEmployeeById
    @emp_id INT
AS
BEGIN
    SELECT *
    FROM employees
    WHERE id = @emp_id;
END;

EXEC GetEmployeeById @emp_id = 101;
```

### Common Mistakes
- Forgetting to pass the parameter
- Using the wrong datatype
- Confusing parameter names with column names

### When to Use
- When the same query is reused with different values
- When filtering results based on user input

### Key Interview Points
- Input parameters make procedures flexible
- Multiple input parameters can be used in the same procedure

---

## 3. Output Parameters

### Definition
Output parameters return a value from a stored procedure back to the caller.

### Syntax
```sql
CREATE PROCEDURE procedure_name
    @param_name datatype OUTPUT
AS
BEGIN
    -- SQL statements
END;
```

### Example
```sql
CREATE PROCEDURE GetEmployeeCount
    @total INT OUTPUT
AS
BEGIN
    SELECT @total = COUNT(*)
    FROM employees;
END;

DECLARE @result INT;
EXEC GetEmployeeCount @total = @result OUTPUT;
SELECT @result;
```

### Common Mistakes
- Forgetting the `OUTPUT` keyword in procedure definition
- Forgetting the `OUTPUT` keyword while executing
- Not declaring a variable to store the returned value

### When to Use
- When returning a single calculated value
- When returning summary values like count, sum, or average

### Key Interview Points
- Output parameters return values differently from result sets
- A procedure can have both input and output parameters

---

## 4. Dynamic Stored Procedures

### Definition
Dynamic stored procedures build and execute SQL statements at runtime.

### Syntax
```sql
DECLARE @sql VARCHAR(500);
SET @sql = 'SELECT ...';
EXEC(@sql);
```

### Example
```sql
CREATE PROCEDURE GetTableData
    @table_name VARCHAR(100)
AS
BEGIN
    DECLARE @sql VARCHAR(500);
    SET @sql = 'SELECT * FROM ' + @table_name;
    EXEC(@sql);
END;

EXEC GetTableData 'employees';
```

### Better Safer Version
```sql
DECLARE @sql NVARCHAR(500);
SET @sql = N'SELECT * FROM employees WHERE department_id = @dept_id';

EXEC sp_executesql
    @sql,
    N'@dept_id INT',
    @dept_id = 10;
```

### Common Mistakes
- Creating SQL injection risks
- Concatenating user input directly into SQL
- Making dynamic SQL harder to debug and maintain

### When to Use
- When table names, filters, or conditions must be decided at runtime
- When query structure changes dynamically

### Key Interview Points
- Dynamic SQL is flexible but risky if not handled safely
- `sp_executesql` is usually preferred over plain `EXEC`
- Always mention SQL injection in interviews

---

## 5. Indexing

### Definition
An index is a database object that speeds up data retrieval.

### Syntax
```sql
CREATE INDEX index_name
ON table_name(column_name);
```

### Example
```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

### Common Mistakes
- Creating too many indexes
- Indexing columns that are rarely searched
- Ignoring the effect on INSERT, UPDATE, and DELETE operations

### When to Use
- On columns frequently used in `WHERE`
- On columns frequently used in `JOIN`
- On columns frequently used in `ORDER BY`

### Key Interview Points
- Indexes improve read performance
- Indexes can slow down write operations
- Good indexing is a trade-off between read speed and write cost

---

## 6. Clustered Index

### Definition
A clustered index determines the physical order of rows in a table.

### Syntax
```sql
CREATE CLUSTERED INDEX idx_emp_id
ON employees(id);
```

### Example
```sql
CREATE CLUSTERED INDEX idx_emp_id
ON employees(id);
```

### Common Mistakes
- Choosing a column that changes often
- Using a large key column
- Forgetting that a table can have only one clustered index

### When to Use
- On primary key columns
- On columns used in range searches
- When sorted storage helps performance

### Key Interview Points
- Only one clustered index per table
- Data rows are stored in clustered index order
- Good for range queries like `BETWEEN`, `<`, and `>`

---

## 7. Non-Clustered Index

### Definition
A non-clustered index stores index data separately from the actual table rows and points to the data.

### Syntax
```sql
CREATE NONCLUSTERED INDEX idx_emp_name
ON employees(name);
```

### Example
```sql
CREATE NONCLUSTERED INDEX idx_emp_name
ON employees(name);
```

### Common Mistakes
- Adding too many non-clustered indexes
- Creating indexes on low-selectivity columns without reason
- Not reviewing index usage over time

### When to Use
- On columns frequently used for search and filtering
- On columns used in joins and sorting
- When you need multiple indexes on one table

### Key Interview Points
- A table can have multiple non-clustered indexes
- Non-clustered indexes do not change physical row order
- Think of it like an index at the back of a book

---

## Clustered vs Non-Clustered Index

| Feature | Clustered Index | Non-Clustered Index |
|---|---|---|
| Physical row order | Yes | No |
| Number per table | One | Many |
| Best for | Range queries | Lookups and filtering |
| Data storage | Rows stored in index order | Separate structure with pointers |

---

## Quick Revision

- **Stored Procedure**: Saved SQL program
- **Input Parameter**: Sends value into procedure
- **Output Parameter**: Returns value from procedure
- **Dynamic Stored Procedure**: Builds SQL at runtime
- **Indexing**: Speeds up data retrieval
- **Clustered Index**: Sorts actual table data
- **Non-Clustered Index**: Separate index structure pointing to data
