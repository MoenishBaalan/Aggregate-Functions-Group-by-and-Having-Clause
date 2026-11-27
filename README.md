# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
What is the total number of appointments scheduled by each doctor?

```sql
SELECT
    DoctorID,
    COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID
ORDER BY DoctorID;
```

**Output:**

<img width="1222" height="750" alt="image" src="https://github.com/user-attachments/assets/e04d0046-aa0a-45bb-a217-e234daec1599" />

**Question 2**
---
What is the total number of medications prescribed for each patient?

```sql
SELECT
    PatientID,
    COUNT(*) AS TotalMedications
FROM Prescriptions
GROUP BY PatientID
ORDER BY PatientID;
```

**Output:**

<img width="1233" height="887" alt="image" src="https://github.com/user-attachments/assets/d54bc7a6-7a35-4d54-99e7-35d0d7605486" />


**Question 3**
---
What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE

```sql
SELECT
    InsuranceCompany,
    ROUND(AVG(
        (JULIANDAY(EndDate) - JULIANDAY(StartDate)) / 365.0
    )) AS AvgCoverageDurationDays
FROM Insurance
GROUP BY InsuranceCompany
ORDER BY InsuranceCompany;
```

**Output:**

<img width="1235" height="811" alt="image" src="https://github.com/user-attachments/assets/135e11f8-5d91-4d5d-967e-11784c267338" />

**Question 4**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```sql
SELECT
    AVG(income) AS avg_income
FROM employee
WHERE name LIKE 'A%';
```

**Output:**

<img width="1237" height="453" alt="image" src="https://github.com/user-attachments/assets/3957a720-22ec-45a4-8d4e-63a6e2bdd93f" />

**Question 5**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 
```sql
SELECT
    SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

<img width="1245" height="431" alt="image" src="https://github.com/user-attachments/assets/1bed163f-abb6-408e-b3e1-4fd76a1eb798" />

**Question 6**
---
Write a SQL query to find the number of employees whose age is greater than 32.

```sql
SELECT COUNT(*) AS COUNT
FROM employee
WHERE age > 32;
```

**Output:**

<img width="1252" height="412" alt="image" src="https://github.com/user-attachments/assets/7e5d1a41-510a-4578-9db7-8f0225c82ddc" />

**Question 7**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
SELECT COUNT(DISTINCT salesman_id) AS COUNT
FROM orders;
```

**Output:**

<img width="1222" height="432" alt="image" src="https://github.com/user-attachments/assets/8968c0fc-4d8b-47d0-95bd-7eac4b48ce9d" />

**Question 8**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the maximum work hours for each date, and excludes dates where the maximum work hour is not greater than 12.
```sql
SELECT
    jdate,
    MAX(workhour) AS "MAX(workhour)"
FROM employee1
GROUP BY jdate
HAVING MAX(workhour) > 12;
```

**Output:**

<img width="1243" height="505" alt="image" src="https://github.com/user-attachments/assets/edd8874a-6301-45e4-b6f5-2357408ff3cc" />

**Question 9**
---
Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

name        type
----------  ----------
RecordID    INTEGER
PatientID   INTEGER
DoctorID    INTEGER
Date        DATE
Diagnosis   TEXT
Treatment   TEXT
Medication  TEXT

```sql
SELECT
    PatientID,
    COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(*) > 3;
```

**Output:**

<img width="1215" height="453" alt="image" src="https://github.com/user-attachments/assets/0eccc02f-c475-446b-9a42-9ec0f58953a1" />

**Question 10**
---
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.
```sql
SELECT
    (age / 5) * 5 AS age_group,
    MIN(salary) AS "MIN(salary)"
FROM customer1
GROUP BY age_group
HAVING MIN(salary) < 2000
ORDER BY age_group;
```

**Output:**

<img width="1233" height="458" alt="image" src="https://github.com/user-attachments/assets/e1bc06c3-7ec1-432c-b8b7-820176c90deb" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
