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
How many doctors specialize in each medical specialty?

Sample table:Doctors Table

For example:

Result
Specialty          TotalDocto
-----------------  ----------
Gastroenterology   1
Neurology          1
Obstetrics         3
Ophthalmology      1
Orthopedics        1
Pediatrics         2
Urology            1


```sql
FROM Doctors
GROUP BY Specialty;
```

**Output:**

<img width="527" height="518" alt="image" src="https://github.com/user-attachments/assets/5cfbcbc1-dfe2-4da8-a6c7-421038685043" />

**Question 2**
---
```
How many appointments are scheduled in each hour of the day?

Sample table:Appointments Table

name                              type
--------------------          ----------
AppointmentID               INTEGER
PatientID                         INTEGER
DoctorID                         INTEGER
AppointmentDateTime   DATETIME
Purpose                           TEXT
Status                              TEXT     

For example:

Result
HourOfDay   TotalAppointments
----------  -----------------
09          2
10          5
11          1
14          1
16          1
```
```sql
GROUP BY HourOfDay
ORDER BY HourOfDay;
```

**Output:**

<img width="522" height="396" alt="image" src="https://github.com/user-attachments/assets/c4a7f92a-a13e-40c3-a3b3-b9b61efe43f0" />

**Question 3**
---
```
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table

For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1
```
```sql
FROM Appointments
GROUP BY DoctorID;
```

**Output:**

<img width="522" height="473" alt="image" src="https://github.com/user-attachments/assets/bfa0dc50-2361-4cd5-8238-0a28e573a506" />

**Question 4**
---
```
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8
```
```sql
select count(*) as COUNT
FROM customer;
```

**Output:**

<img width="257" height="220" alt="image" src="https://github.com/user-attachments/assets/2cecec4e-9c0f-482c-aeb7-33319b55a682" />

**Question 5**
---
```
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
AVERAGE
----------
1461.765
```
```sql
select avg(purch_amt) as AVERAGE from orders
```

**Output:**

<img width="252" height="223" alt="image" src="https://github.com/user-attachments/assets/52fedb21-c8a6-4b71-ad7a-eb21b28f353d" />

**Question 6**
---
```
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8
```
```sql
SELECT COUNT(*) AS COUNT
FROM customer
```

**Output:**

<img width="253" height="220" alt="image" src="https://github.com/user-attachments/assets/7c3e62fb-7927-4dd5-a9f0-87def1a70964" />

**Question 7**
---
```
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4
```
```sql
SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**

<img width="254" height="231" alt="image" src="https://github.com/user-attachments/assets/df547c3f-8406-439a-a23a-533d1b44ce51" />

**Question 8**
---
```
Write the SQL query that achieves the selection of product names and the maximum price for each category from the "products" table, and includes only those products where the maximum price is greater than 15.

For example:

Result
category_id  product_name  Price
-----------  ------------  ----------
1            Orange        15.5
2            Monitor       25
```
```sql
select category_id,product_name,max(price) as Price from products group by category_id having max(price)>15;
```

**Output:**


<img width="641" height="283" alt="image" src="https://github.com/user-attachments/assets/9e33defc-028e-4486-9ae9-e7ddc68fa707" />

**Question 9**
---
```
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1

For example:

Result
address     AVG(salary)
----------  -----------
Bhopal      8500.0
Indore      10000.0
Mumbai      6500.0
```
```sql
select address,avg(salary) as 'AVG(salary)' from customer1
group by address
```

**Output:**


<img width="446" height="319" alt="image" src="https://github.com/user-attachments/assets/78998254-0480-451d-b966-1a1fa1236e09" />

**Question 10**
---
```
Write the SQL query that accomplishes the selection of average price for each category from the "products" table and includes only those products where the average price

falls between 10 and 15.

For example:

Result
category_id  AVG(Price)
-----------  ----------
1            12.375
```
```sql
SELECT category_id, AVG(price) AS "AVG(Price)"
FROM products
```

**Output:**


<img width="442" height="238" alt="image" src="https://github.com/user-attachments/assets/abb0debc-cdba-495e-aa5a-4284d110a010" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
