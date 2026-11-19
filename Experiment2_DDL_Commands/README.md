# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
```
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300
```

```sql
insert into Products(Name,Category,Price,Stock)
Values ('Smartphone', 'Electronics','800','150');
insert into Products(Name,Category,Price,Stock)
Values('Headphones','Accessories','200','300');
```

**Output:**

<img width="955" height="210" alt="image" src="https://github.com/user-attachments/assets/ee607457-d8ff-41fd-8d81-bcbfc4f5bb63" />

**Question 2**
---
```
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

For example:

Test	Result
SELECT ProductID, Name, Category, Price, Stock 
FROM Products 
WHERE ProductID = 104;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
104         Tablet      Electronics  100         50
```
```sql
INSERT INTO Products (ProductID, Name, Category)  
VALUES (104, 'Tablet', 'Electronics');```
```
**Output:**

<img width="1002" height="120" alt="image" src="https://github.com/user-attachments/assets/c66920e2-280c-4360-a98b-7760acfd576e" />

**Question 3**
---
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700
```
```sql
CREATE TABLE item(item_id TEXT PRIMARY KEY,item_desc TEXT NOT NULL,rate INTEGER NOT NULL,icom_id TEXT CHECK(length(icom_id)=4),FOREIGN KEY (icom_id) REFERENCES company(com_id)ON UPDATE SET NULL ON DELETE SET NULL);
```

**Output:**

<img width="942" height="191" alt="image" src="https://github.com/user-attachments/assets/eb5e6dd0-2414-4079-beed-48bce13645ff" />

**Question 4**
---
```
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5
```
```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4) CHECK (LENGTH(icom_id)=4),
    FOREIGN KEY (icom_id) REFERENCES company(com_id)
        ON UPDATE CASCADE
        ON DELETE CASCADE
    
);
```

**Output:**

<img width="957" height="183" alt="image" src="https://github.com/user-attachments/assets/d35359c4-20cc-4770-b582-029d65b92fe0" />

**Question 5**
---
```
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.
For example:

Test	Result
PRAGMA table_info(employee);
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           department  INTEGER     0                       0
3           manager_id  INTEGER     0           NULL        0
```
```sql
ALTER TABLE employee
ADD COLUMN department_id INTEGER;
ALTER TABLE employee
ADD COLUMN manager_id INTEGER DEFAULT NULL;
```

**Output:**

<img width="882" height="178" alt="image" src="https://github.com/user-attachments/assets/b1732abb-cd7b-4dac-b9ef-1d27d55ee02b" />

**Question 6**
---
```
Write a SQL query to Add a new column State as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           State       TEXT        0                       0
```
```sql
ALTER TABLE Student_details ADD State TEXT;
```

**Output:**

<img width="957" height="175" alt="image" src="https://github.com/user-attachments/assets/c5adfb64-ff94-49ba-875a-ef9ee88c265c" />

**Question 7**
---
```
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	Result
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000
```
```sql
CREATE TABLE jobs(
job_id int PRIMARY KEY,
job_title varchar(225) default'',
min_salary int default 8000,
max_salary int default null
);
```

**Output:**

<img width="818" height="117" alt="image" src="https://github.com/user-attachments/assets/db47048e-39fc-4436-b749-4b1bacc9f7f9" />

**Question 8**
---
```
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York
```
```sql
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT
);
```

**Output:**

<img width="953" height="97" alt="image" src="https://github.com/user-attachments/assets/4a3e5ec9-45cd-4e46-8ae0-de3aeb8240e7" />

**Question 9**
---
```
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE
For example:

Test	Result
pragma table_info('Tasks');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           TaskID      INTEGER     0                       0
1           TaskName    TEXT        0                       0
2           DueDate     DATE        0                       0
```
```sql
CREATE TABLE Tasks(TaskID INTEGER,TaskName TEXT,DueDate DATE);
```

**Output:**

<img width="965" height="173" alt="image" src="https://github.com/user-attachments/assets/b35aedf4-c0d8-473f-b6b3-c979ebdf5654" />

**Question 10**
---
```
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78

```
```sql
INSERT INTO Student_details
SELECT *
FROM Archived_students
```

**Output:**

<img width="812" height="130" alt="image" src="https://github.com/user-attachments/assets/7a34de00-2f64-4f68-94c2-25e6b53d097a" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
