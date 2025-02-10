## Interview with Amazon Jr. Data Engineer

- [Interview with Amazon Jr. Data Engineer](#interview-with-amazon-jr-data-engineer)
  - [Overview](#overview)
  - [Position Link \& Details](#position-link--details)
  - [Behavioral](#behavioral)
  - [Technical](#technical)
    - [Part a. Data Modeling](#part-a-data-modeling)
    - [Part b. Python](#part-b-python)
    - [Part c. SQL Challenge](#part-c-sql-challenge)
  - [Extra Questions](#extra-questions)
  - [Result](#result)


### Overview
- Got the interview via referral of a senior SDE friend
- Got SQL online assessment from recruiter. 5 sections, first 4 were 20 multiple selection questions involving concepts of SQL last section was 4 (or 5?) SQL query challenges. Medium difficulty.
- Phone interview with recruiter going through interview details, packages. Later disclosed the OA was just to get candidate used to SQL questions, but not regraded (huh??)
- recruiter send links to schedule phone interview 
- Phone interview 75 minute with senior engineer. Consist of 4 parts: Behavorial, Technical (data modeling, Python, SQL).

### Position Link & Details
Link: https://amazon.jobs/en/jobs/2804399/data-engineer

```
Data Engineer
Job ID: 2804399 | Amazon.com Services LLC

DESCRIPTION
Come build the future as a Data Engineer at Amazon, where you will be inspired working along best-in-class inventors and innovators! You will have the opportunity to create meaningful experiences that deliver on the ever-evolving needs of our customers, and your work will impact millions of people around the world.

As an Amazon Data Engineer, you will solve unique and complex problems at a rapid pace, utilizing the latest technologies to create solutions that are highly scalable. You will find that there is an unlimited number of opportunities within Amazon, where developing your career across a wide range of teams is highly supported. We are committed to making your work experience as enjoyable as the experiences you’ll be creating for our customers.

Apply now and you will be eligible for Amazon Data Engineer positions that are based on your preferred location, team, and more. We’re hiring across Amazon Stores in the United States and Canada.

Teams with available positions include, but are not limited to:

• Consumer Technology: Build new generation features and products for amazon.com, constantly improving the Customer and Seller experience for billions around the globe. Whether building site wide features such as reviews and recommendations, category specific software for the likes of Pharmacy, Electronics, Digital Software and Video Games or seller infrastructure, there are a variety of complex problems to tackle using a range of technologies in the design of your technical solutions.

• Operations Technology: Shape the future of transportation planning and execution on a global scale, that impacts hundreds of fulfillment centers, thousands of Amazonians, and millions of customers across the world. Your technology will support thousands of operators worldwide to design, build and run the best-in-class Amazon transportation network. We are building intelligent software to make transportation more reliable, faster, and less costly, providing a better and less expensive experience for our customers.

• Human Resources Technology: Create a seamless experience for millions of Amazonians and/or candidates. Whether supporting technologies for onboarding, time and attendance, compensation, amazon.jobs, or recruiting, you’ll deliver robust feature sets, elegant designs, intuitive user interfaces and systems that make it easy for Amazonians to excel at performing critical business functions.


Key job responsibilities
Design, implement and support an analytical data infrastructure using AWS technologies
Build robust and scalable data integration (ETL) pipelines using SQL, and AWS data storage technologies like Aurora, Red Shift etc.
Design and develop Analytics applications using modern scripting languages (Python, R, PHP, etc) supporting critical business functions.
Gather business and functional requirements and translate these requirements into robust, scalable, operable solutions with a flexible and adaptable data architecture.
Lead architecture design and implementation of next generation BI solution
Continually improve ongoing reporting and analysis processes, automating or simplifying self-service modeling and production support for customers.

BASIC QUALIFICATIONS
- 1+ years of data engineering experience
- Experience with data modeling, warehousing and building ETL pipelines
- Experience with one or more query language (e.g., SQL, PL/SQL, DDL, MDX, HiveQL, SparkSQL, Scala)
- Experience with one or more scripting language (e.g., Python, KornShell)

PREFERRED QUALIFICATIONS
- Experience with big data technologies such as: Hadoop, Hive, Spark, EMR
- Experience with any ETL tool like, Informatica, ODI, SSIS, BODI, Datastage, etc.

Amazon is committed to a diverse and inclusive workplace. Amazon is an equal opportunity employer and does not discriminate on the basis of race, national origin, gender, gender identity, sexual orientation, protected veteran status, disability, age, or other legally protected status.

Our inclusive culture empowers Amazonians to deliver the best results for our customers. If you have a disability and need a workplace accommodation or adjustment during the application and hiring process, including support for the interview or onboarding process, please visit https://amazon.jobs/content/en/how-we-hire/accommodations for more information. If the country/region you’re applying in isn’t listed, please contact your Recruiting Partner.

Our compensation reflects the cost of labor across several US geographic markets. The base pay for this position ranges from $91,200/year in our lowest geographic market up to $185,000/year in our highest geographic market. Pay is based on a number of factors including market location and may vary depending on job-related knowledge, skills, and experience. Amazon is a total compensation company. Dependent on the position offered, equity, sign-on payments, and other forms of compensation may be provided as part of a total compensation package, in addition to a full range of medical, financial, and/or other benefits. For more information, please visit https://www.aboutamazon.com/workplace/employee-benefits. This position will remain posted until filled. Applicants should apply via our internal or external career site.
```



### Behavioral
```
Interviewer introduce his own background:
Linkedin: https://www.linkedin.com/in/soumyachatterjee-6714/
title: Amazon Data Engineer II (Glen Allen, VA)
- Worked 18 years in data Engineering
```
```
Q: Introduce yourself
A: First went through my background. Not traditional CS background, but got interested in data analysis/engineering during grad school. Now working as a Data Engineer and pursuing CS Masters.
Most current project (Sigicom DataHandler Desktop App). Explained the function, tools used are
(SQLite, Python PyQt5, transform manufacturers' API service json returned data to local database...)
Also explains the entire workflow of the data (I did not explain this part well, but eventually the interviewer got the idea):
Manufacturers' API service -> 
My Tool -> 
generate datafile on company server and store data in server local database (temperary) ->
FTP send datafiles to company software and store data in software database (permanent destination)
```
```
Q: Tell me an obstacle while creating the tool and how you overcame it?
A: Manufacturers' API service is not reliable to send hourly trigger for construction site monitoring devices.
Instead of actively sending API requests to retrieve data, built an socket to listen to most up-to-date database status
to check for new data.
```
```
Q: If redo the project, what would you have done differently.
A: The current version of database uses SQLite since it is lightweight and can be packaged easily whe other offices
need the tool running. But downside is it has a weekly cleanup routine to avoid database from growing. Could have used
online service like MongoDB (TTL: time-to-live) for automatic data cleanup and cloud service allows data sharing. 
```

### Technical
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
```
Follow up:
```sql
Q1. Run a scenario for an employee?
A1: 
    Employee:
        (1, Kevin, 21, [some address], 1996-03-19)
    History:
        (1, 1, Business, $100000, 2024-10, 2024-11, False)
        (1, 1, Engineering, $120000, 2024-11, Null, True)

Q2: The employee head count change between two consecutive years?
A2: Use different joins to get the headcount of first year, then another for the second year. Then, compare the headcount.
```

#### Part b. Python
```
Given a log, return all the users who have logged in to the server twice.
User can log in at most once every calendar day.
Logging in twice means the user has logged in to the server for at least two consecutive days.
Write a Python code, no external libraries allowed.

**Example log:
logtime             | user_id  
--------------------|---------
2024-02-01 08:15:32 | user_001  
2024-02-02 09:20:45 | user_001  (Consecutive)  
2024-02-03 07:55:12 | user_001  (Consecutive)  
2024-02-05 10:05:22 | user_001  
2024-02-01 12:30:14 | user_002  
2024-02-03 14:10:09 | user_002  
2024-02-04 09:45:50 | user_002  (Consecutive)  
2024-02-04 18:20:33 | user_003  
2024-02-05 08:05:17 | user_003  (Consecutive)  
2024-02-06 07:50:10 | user_003  (Consecutive)  
2024-02-08 11:15:55 | user_003  
2024-02-05 06:40:30 | user_004  
2024-02-07 13:25:48 | user_004  
2024-02-10 16:10:12 | user_005  

**Answer:
user_id  
---------
user_001
user_002
user_003
```
```python
def get_consecutive_users(records) -> list:
    # seperate log records based on user_id
    logs = collections.defaultdict(list)
    for record in records:
        time, user_id = record
        logs[user_id].append(time)

    # get all user_id who logged in at least twpo consecutive days
    user_ids = []
    for user_id, times in logs.items():
        # sort the time
        times = time.sort()
        # get consecutive user_ids
        for i in range(1, len(times)):
            if 1-day <= times[i] - times[i - 1] < 2-days:
                user_ids.append(user_id)
                break
    
    return user_ids
```
#### Part c. SQL Challenge
```sql
Given the following two tables, return all product_groups that covers the US market but has no sell.
The US area_id = 1.

Orders:
 product_id | sell_in_area | sold_unit
------------+-------------+-------------
       101  |      1      |   10
       102  |      1      |    5
       103  |      2      |    7
       105  |      3      |    8

Products:
 area | product_id | name | product_group
------+------------+------+---------------
   1  |    101    |   A   |   Group 1
   1  |    102    |   B   |   Group 1
   2  |    103    |   C   |   Group 2
   1  |    104    |   D   |   Group 3
   3  |    105    |   E   |   Group 3

Output:
 product_group
---------------
 Group 3

```
```sql
-- get all product_groups whose US sold_unit > 0
WITH HasUSSellGroup AS (
    SELECT p.product_group
    FROM Orders o JOIN Product p ON o.product_id = p.product_id
    WHERE o.sell_in_area = 1
    GROUP BY p.product_group
    HAVING SUM(o.sold_unit) > 0
-- get all product_groups who covers US market
), CoverUSGroup AS (
    SELECT DISTINCT product_group
    FROM Product
    WHERE area = 1
)

-- get all product_groups that covers US market but has no sell
SELECT product_group
FROM CoverUSGroup
WHERE product_group NOT IN (
    SELECT * FROM HasUSSellGroup
)
```

### Extra Questions
- Q: Later steps for the interview?
- A: One day on-site with 5 back-to-back interviews (can find this on Youtube: https://www.youtube.com/results?search_query=amazon+data+engineer+interview).
   
- Q: When will I hear back?
- A: In one or two days.

- Q: Peroformance of the interview and possible imporvement?
- A: Nothing wrong, enjoyed the interviewing preocess. Loved the way I communicate :(


### Result
Rejected the very next day by recruiter via email.
