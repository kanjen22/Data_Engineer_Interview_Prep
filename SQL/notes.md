
- [1. Table declaration:](#1-table-declaration)
- [2. Syntax for `INSERT`, `UPDATE`, and `DELETE`:](#2-syntax-for-insert-update-and-delete)
- [3. `NULL` handling:](#3-null-handling)
- [4. `DATETIME` object operation:](#4-datetime-object-operation)
- [5. Use `SET` to change variable value:](#5-use-set-to-change-variable-value)
- [6. `While` loop in SQL:](#6-while-loop-in-sql)


##### 1. Table declaration:

```sql
-- Table declaration
CREATE TABLE students (
    student_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
)
```

##### 2. Syntax for `INSERT`, `UPDATE`, and `DELETE`:

```sql
-- INSERT
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);

-- UPDATE
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

-- DELETE
DELETE FROM table_name
WHERE condition;
```

##### 3. `NULL` handling:

```sql
-- LIMIT will NOT return NULL if nothing is in the result
OFFSET 1 LIMIT 1

-- If want to return NULL, use
IFNULL(something, NULL)
-- or
SELECT () AS [alias]
```

##### 4. `DATETIME` object operation:

```sql
-- use DATEDIFF to do operations for datetime objects
DATEDIFF(date1, date2) = date1 - date2
DATEADD(interval, number, date)
```

##### 5. Use `SET` to change variable value:

```sql
-- `SET` to change variable
-- ** within function, you CANNOT change variable value directly using
-- regular operation, EX: `N - 1` does not work
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
SET N = N - 1; -- ** has to have a ";"
RETURN ( # Write your MySQL query statement below.
    SELECT DISTINCT salary
    FROM Employee
    ORDER BY salary DESC
    LIMIT 1 OFFSET N
)
```

##### 6. `While` loop in SQL:

```sql
-- SQL While loop
DECLARE i INT DEFAULT 0;
DECLARE max_num DEFAULT 10;

WHILE i <= max_num DO
   SELECT i;
   SET i = i + 1;
END WHILE;
```