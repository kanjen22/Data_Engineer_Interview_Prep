```sql
Link: https://medium.com/@msharma.ac.12/how-i-passed-the-hackerrank-sql-advanced-certification-questions-solutions-and-tips-a65baa6096d1

Que 1. The times that employees log in and out are recorded over the course of a month. For each employee, determine the number of hours worked during the weekends. For simplicity, hours worked in a day, hours are truncated to their integer part.
For example, there are 10 hours between ‘2000:01:01 00:45:00’ and ‘2000:01:01 10:45:00’. There are 9 hours between ‘2000:01:01 00:46:00’ and ‘2000:01:01 10:45:00’.
Return a list of employee IDs and weekend hours worked, descending by hours worked.

WITH hours_worked AS (
    SELECT
        emp_id,
    CASE
        WHEN MINUTE(TIMESTAMP) >= MINUTE(LAG(TIMESTAMP) OVER(PARTITION BY DATE(TIMESTAMP), emp_id ORDER BY TIMESTAMP)) THEN
        HOUR(TIMESTAMP) - HOUR(LAG(TIMESTAMP) OVER(PARTITION BY DATE(TIMESTAMP), emp_id ORDER BY TIMESTAMP))
    ELSE
        HOUR(TIMESTAMP) - HOUR(LAG(TIMESTAMP) OVER(PARTITION BY DATE(TIMESTAMP), emp_id ORDER BY TIMESTAMP)) - 1
    END AS hours_worked
    FROM
        attendance
    WHERE
        DAYOFWEEK(TIMESTAMP) IN (1, 7) - 1 is Sunday, 7 is Saturday
)
SELECT
    emp_id,
    SUM(hours_worked) AS hours_worked
FROM
    hours_worked
GROUP BY
    emp_id
ORDER BY
    hours_worked DESC;
```

```sql
Link: https://medium.com/@msharma.ac.12/how-i-passed-the-hackerrank-sql-advanced-certification-questions-solutions-and-tips-a65baa6096d1

Que 2. A number of algorithms are used to mine cryptocurrencies. As a part of comparison, create a query to return a list of algorithms and their volumes to each quarter of year 2020.

WITH cte AS (
    SELECT 
        algorithm, 
        SUM(volume) AS volume,
        QUARTER(dt) AS quarter
    FROM 
        coins
    JOIN 
        transactions
    ON 
        code = coin_code
    WHERE 
        YEAR(dt) = 2020
    GROUP BY 
        algorithm, QUARTER(dt)
)
SELECT 
    coins.algorithm,
    MAX(CASE WHEN cte.quarter = 1 THEN cte.volume ELSE 0 END) AS transactions_Q1,
    MAX(CASE WHEN cte.quarter = 2 THEN cte.volume ELSE 0 END) AS transactions_Q2,
    MAX(CASE WHEN cte.quarter = 3 THEN cte.volume ELSE 0 END) AS transactions_Q3,
    MAX(CASE WHEN cte.quarter = 4 THEN cte.volume ELSE 0 END) AS transactions_Q4
FROM 
    coins
JOIN 
    cte
ON 
    coins.algorithm = cte.algorithm
GROUP BY 
    coins.algorithm
ORDER BY 
    coins.algorithm;
```