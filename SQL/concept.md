- [1. Comparison of SQL Procedures and Functions:](#1-comparison-of-sql-procedures-and-functions)

#### 1. Comparison of SQL Procedures and Functions:

| Feature                      | Stored Procedure 🏛️                                                                     | Function 📜                                                            |
| ---------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **Purpose**                  | Used to perform operations (e.g., modifying data).                                      | Used to compute and return a single value or table.                    |
| **Return Type**              | Can return multiple values via `OUT` parameters.                                        | Must return a single value or table.                                   |
| **Can Modify Data?**         | ✅ Yes (can use `INSERT`, `UPDATE`, `DELETE`).                                          | ❌ No (cannot modify database state).                                  |
| **Can be Used in SELECT?**   | ❌ No, cannot be used directly in a `SELECT` statement.                                 | ✅ Yes, can be used in `SELECT` and `WHERE` clauses.                   |
| **Parameters**               | Supports `IN`, `OUT`, and `INOUT` parameters.                                           | Only `IN` parameters allowed.                                          |
| **Can Handle Transactions?** | ✅ Yes, can use `COMMIT` and `ROLLBACK`.                                                | ❌ No, functions cannot manage transactions.                           |
| **Execution**                | Executed using `EXEC` or `CALL`.                                                        | Called within SQL statements like `SELECT my_function()`.              |
| **Performance**              | Generally faster for complex operations.                                                | Optimized for calculations and queries.                                |
| **Use Case**                 | Best for procedural operations like batch updates, logging, and complex business logic. | Best for calculations, transformations, and reusable logic in queries. |

> **Key Takeaway**:
>
> - Use **Functions** for computations and data retrieval.
> - Use **Procedures** for operations that modify data or involve complex logic.

🏛️ Example: Stored Procedure

```sql
CREATE PROCEDURE GetEmployeeDetails(IN emp_id INT)
BEGIN
    SELECT * FROM employees WHERE id = emp_id;
END

-- Execute the procedure
CALL GetEmployeeDetails(101);
```

🏛️ Example: Function

```sql
CREATE FUNCTION GetTotalSalary(dept_id INT)
RETURNS DECIMAL(10,2)   -- dtype
BEGIN ( -- query main body
    DECLARE total_salary DECIMAL(10,2);
    SELECT SUM(salary) INTO total_salary FROM employees WHERE department_id = dept_id;
    RETURN total_salary;
)
END

-- Function call
SELECT GetTotalSalary(3) AS total_salary;
```
