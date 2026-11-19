# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
```
Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

Suppliers Table 

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
For example:

Test	Result
select changes();
changes()
----------
1
```

```sql
update Suppliers set address='58 Lakeview, Magnolia' where supplier_id=5;
```

**Output:**

<img width="1062" height="146" alt="image" src="https://github.com/user-attachments/assets/9fd6de26-863a-4a01-9623-83e6c789ced2" />

**Question 2**
---
```
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT * FROM EMPLOYEES WHERE DEPARTMENT_ID=80 AND COMMISSION_PCT=.25;
EMPLOYEE_ID  FIRST_NAME  LAST_NAME   EMAIL       PHONE_NUMBER        HIRE_DATE   JOB_ID      SALARY      COMMISSION_PCT  MANAGER_ID  DEPARTMENT_ID
-----------  ----------  ----------  ----------  ------------------  ----------  ----------  ----------  --------------  ----------  -------------
151          John        Bernstein   DBERNSTE    011.44.1344.345268  8/7/87      SA_REP      9500        0.25            145         80
152          John        Hall        PHALL       011.44.1344.478968  8/8/87      SA_REP      9000        0.25            145         80
161          John        Sewall      SSEWALL     011.44.1345.529268  8/17/87     SA_REP      7000        0.25            146         80
162          John        Vishney     CVISHNEY    011.44.1346.129268  8/18/87     SA_REP      10500       0.25            147         80
168          John        Ozer        LOZER       011.44.1343.929268  8/24/87     SA_REP      11500       0.25            148         80
175          John        Hutton      AHUTTON     011.44.1644.429266  8/31/87     SA_REP      8800        0.25            149         80
```
```sql
UPDATE Employees
SET FIRST_NAME = 'John'
WHERE DEPARTMENT_ID = 80 
  AND COMMISSION_PCT < 0.35
```

**Output:**

<img width="933" height="135" alt="image" src="https://github.com/user-attachments/assets/6b1756fc-45ec-4616-ac63-a18b4d03ef99" />

**Question 3**
---
```
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

For example:

Test	Result
select changes();
changes()
----------
2

```
```sql
UPDATE purchases
SET per_unit_price = 25,
    total_price = quantity * 25
WHERE purchase_date = '2022-08-15'
  AND product_id = 12;
```

**Output:**

<img width="1011" height="190" alt="image" src="https://github.com/user-attachments/assets/a2a59bcd-d15d-4fa0-8ae2-4fbfa8ff7195" />

**Question 4**
---
```
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
For example:

Test	Result
select changes();
changes()
-----------------
4
```
```sql
UPDATE products
SET reorder_lvl = 40
WHERE category = 'Grocery';
```

**Output:**

<img width="1018" height="141" alt="image" src="https://github.com/user-attachments/assets/abb07d67-fe1f-4ef5-a6f1-d4c5e7204aee" />

**Question 5**
---
```
Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID,FIRST_NAME,EMAIL,COMMISSION_PCT FROM EMPLOYEES 
WHERE DEPARTMENT_ID=110 LIMIT 1;
EMPLOYEE_ID  FIRST_NAME  EMAIL          COMMISSION_PCT
-----------  ----------  -------------  --------------
205          Shelley     not available  0.55
```
```sql
update Employees
set email = 'not available',COMMISSION_PCT = 0.55 where DEPARTMENT_ID = 110;
```

**Output:**

<img width="1196" height="224" alt="image" src="https://github.com/user-attachments/assets/c259f173-884f-4a7d-b680-bef304896335" />

**Question 6**
---
```
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_country' must be 'India',

2. 'cus_city' must not be 'Chennai',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
SELECT * FROM customer WHERE cust_country='India';
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00025      Ravindran   Bangalore   Bangalore     India         2           5000         7000         4000         8000             AVAVAVA     A011
C00019      Yearannaid  Chennai     Chennai       India         1           8000         7000         7000         8000             ZZZZBFV     A010
C00005      Sasikant    Mumbai      Mumbai        India         1           7000         11000        7000         11000            147-258963  A002
C00007      Ramanathan  Chennai     Chennai       India         1           7000         11000        9000         9000             GHRDWSD     A010
C00022      Avinash     Mumbai      Mumbai        India         2           7000         11000        9000         9000             113-123456  A002
C00017      Srinivas    Bangalore   Bangalore     India         2           8000         4000         3000         9000             AAAAAAB     A007
C00009      Ramesh      Mumbai      Mumbai        India         3           8000         7000         3000         12000            Phone No    A002
C00014      Rangarappa  Bangalore   Bangalore     India         2           8000         11000        7000         12000            AAAATGF     A001
C00016      Venkatpati  Bangalore   Bangalore     India         2           8000         11000        7000         12000            JRTVFDD     A007
C00011      Sundariya   Chennai     Chennai       India         3           7000         11000        7000         11000            PPHGRTS     A010
CUST_CODE   CUST_NAME    CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  -----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00019      Yearannaidu  Chennai     Chennai       India         1           8000         7000         7000         8000             ZZZZBFV     A010
C00007      Ramanathan   Chennai     Chennai       India         1           7000         11000        9000         9000             GHRDWSD     A010
C00011      Sundariya    Chennai     Chennai       India         3           7000         11000        7000         11000            PPHGRTS     A010
```
```sql
DELETE FROM customer
WHERE cust_country = 'India'
AND cust_city <> 'Chennai';
```

**Output:**

<img width="905" height="217" alt="image" src="https://github.com/user-attachments/assets/07bf601d-797e-42c2-9f3d-0be876fa9d3e" />

**Question 7**
---
```
Write a SQL query to Delete customers from 'customer' table where 'OPENING_AMT' is between 4000 and 6000.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
SELECT * FROM customer
WHERE OPENING_AMT BETWEEN 4000 AND 6000;
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00013      Holmes      London      London        UK            2           6000         5000         7000         4000             BBBBBBB     A003
C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB     A008
C00025      Ravindran   Bangalore   Bangalore     India         2           5000         7000         4000         8000             AVAVAVA     A011
C00024      Cook        London      London        UK            2           4000         9000         7000         6000             FSDDSDF     A006
C00015      Stuart      London      London        UK            1           6000         8000         3000         11000            GFSGERS     A003
C00002      Bolt        New York    New York      USA           3           5000         7000         9000         3000             DDNRDRH     A008
C00004      Winston     Brisban     Brisban       Australia     1           5000         8000         7000         6000             AAAAAAA     A005
C00023      Karl        London      London        UK            0           4000         6000         7000         3000             AAAABAA     A006
C00010      Charles     Hampshair   Hampshair     UK            3           6000         4000         5000         5000             MMMMMMM     A009
C00012      Steven      San Jose    San Jose      USA           1           5000         7000         9000         3000             KRFYGJK     A012
```
```sql
delete from customer 
where OPENING_AMT BETWEEN 4000 AND 6000;
```

**Output:**

<img width="878" height="143" alt="image" src="https://github.com/user-attachments/assets/8b05ebf9-b64a-48de-b868-913f5eff63d2" />

**Question 8**
---
```
Write a SQL query to Delete customers whose 'GRADE' is greater than 2 and have a 'PAYMENT_AMT' less than the average 'PAYMENT_AMT' for all customers, or whose 'OUTSTANDING_AMT' is greater than 8000:

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
12
```
```sql
delete from customer 
where (GRADE > 2 AND PAYMENT_AMT < (SELECT AVG (PAYMENT_AMT) FROM CUSTOMER))
OR OUTSTANDING_AMT > 8000;
```

**Output:**

<img width="822" height="154" alt="image" src="https://github.com/user-attachments/assets/00767e13-4c66-44ce-b058-b7f3ccaae2e1" />

**Question 9**
---
```
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```
```sql
delete from Doctors
where specialization like '%Pediatric%'
and first_name ='Michael';
```

**Output:**

<img width="667" height="154" alt="image" src="https://github.com/user-attachments/assets/ea70b545-2cdc-4965-b6e3-8394bbd277cd" />

**Question 10**
---
```
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
4
```
```sql
DELETE FROM Customer
WHERE CUST_COUNTRY = 'UK'
  AND WORKING_AREA = 'London'
  AND GRADE < 3;
```

**Output:**

<img width="823" height="106" alt="image" src="https://github.com/user-attachments/assets/46dc9cae-67e1-425d-b3b2-49e347bf8bac" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
