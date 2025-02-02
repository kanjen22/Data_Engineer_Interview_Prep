### Behavioral:

```
Q: Introduce
```



### Technical:
#### Part a. Data Modeling
Design a database for a company to store its employee's information and their historical data.
```sql
step 1: what information to store?
step 2: ask question, ex: Show historical data of an employee
step 3:
    schema:
    Employee Table:
        employee_id: int (PK)
        name: vchar
        age: int
        address: vchar
        DOB: datetime

    History:
        history_id: int (PK)
        employee_id: int (FK)
        department: vchar
        salary: float
        start_date: datetime
        end_date: datetime
        current: bool


    Explanation:
        Separate information into two table, based their data change frequency. Employee table stores data that does not change much while History table stores data that changes more frequently.

Follow up:
Q1. Ruin a scenario for an employee?
A1: 
    Employee: (1, Kevin, 21, [some address], 1996-03-19)
    History:
        (1, 1, Business, $100000, 2024-10, 2024-11, False)
        (1, 1, Engineering, $120000, 2024-11, Null, True)

Q2: The employee head count change between two consecutive years?
A2: Use different joins to get the headcount of first year, then another for the second year. Then, compare the headcount.
```



