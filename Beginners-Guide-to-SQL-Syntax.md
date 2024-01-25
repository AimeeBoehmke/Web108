# Beginners Guide to SQL Syntax 

## Command to login to MySQL from the terminal

```
mysql -u root -p
```

## How to SHOW USERS

```
SELECT User, Host FROM mysql.user;
```

## How to CREATE USERS

```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

## How to GRANT PRIVILEGES, Show granted privileges and remove.

```
-- Granting privileges
GRANT ALL PRIVILEGES ON your_database.* TO 'username'@'localhost';

-- Show granted privileges
SHOW GRANTS FOR 'username'@'host';

-- Display privileges for current user
SHOW GRANTS;

-- Removing user privileges for a specific table
REVOKE privilege_type [, privilege_type ...] ON database_name.table_name FROM 'username'@'host';

-- Removing a user's privileges from an entire database
REVOKE ALL PRIVILEGES ON database_name.* FROM 'username'@'host';
```
*After executing the **REVOKE** statement, you should run **FLUSH PRIVILEGES** to apply the changes.

## How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES

```
-- Command to show all databases.
SHOW DATABASES;

-- Command to delete a database.
DROP DATABASE your_database_name;

-- Command to create a database.
CREATE DATABASE you_database_name;

-- Command to select a database.
USE your_database_name;
```

## How to CREATE a TABLE with Columns and their data types

The **CREATE TABLE** statement is used to create a new table in a database.

```
-- Syntax --
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);

-- Example --
CREATE TABLE employees (
    EmployeeID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    BirthDate DATE,
    SocialInsuranceNumber INT NOT NULL UNIQUE,
    Phone VARCHAR(15) NOT NULL UNIQUE,
    HireDate DATE NOT NULL,
    DepartmentID VARCHAR(50) NOT NULL,
    Salary INT NOT NULL
);
```
Each column in a database table is required to have a name and a data type. In MySQL there are three main data types: string, numeric, and date and time.

### String Data Types

| Data Type      | Description                                                                                                          |
| -------------- | -------------------------------------------------------------------------------------------------------------------- |
| `CHAR(size)`   | Fixed-length character string. Allocates a specified size, pads with spaces. Used for fixed-length strings.          |
| `VARCHAR(size)` | Variable-length character string. Allocates only the necessary space, no padding. Efficient for variable-length data. |
| `TEXT`         | Variable-length character string with no specified maximum length. Suitable for large amounts of text data.          |
| `NCHAR(size)`  | Fixed-length Unicode character string. Similar to `CHAR` but supports Unicode characters.                           |
| `NVARCHAR(size)`| Variable-length Unicode character string. Similar to `VARCHAR` but supports Unicode characters.                      |
| `NTEXT`        | Variable-length Unicode character string with no specified maximum length. Suitable for large Unicode text data.      |

### Numeric Data Types

| Data Type         | Description                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------- |
| `INT`             | Integer. Represents whole numbers without decimal places.                                          |
| `FLOAT(size, d)`  | Floating-point number. Represents approximate numeric data with specified precision and scale.  |
| `DOUBLE`          | Double-precision floating-point number. Provides higher precision than `FLOAT`.                    |
| `DECIMAL(size, d)`| Decimal. Represents fixed-point numeric data with specified precision and scale.                   |
| `NUMERIC(size, d)`| Numeric. Similar to `DECIMAL`, represents fixed-point numeric data.                                |
| `TINYINT`         | Small integer. Represents small whole numbers.                                                     |
| `SMALLINT`        | Medium-sized integer. Represents medium-sized whole numbers.                                       |
| `BIGINT`          | Large integer. Represents large whole numbers.                                                      |

### Date and Time Data Types

| Data Type          | Description                                                      |
| ------------------ | ---------------------------------------------------------------- |
| `DATE`             | Represents a date (year, month, day) in the format 'YYYY-MM-DD'.   |
| `TIME`             | Represents a time of day in the format 'HH:MM:SS'.                |
| `DATETIME`         | Represents a date and time in the format 'YYYY-MM-DD HH:MM:SS'.  |
| `TIMESTAMP`        | Similar to `DATETIME`, but often used for automatic timestamping. |
| `YEAR`             | Represents a year in the format 'YYYY'.                          |

### SQL Contraints

**NOT NULL** is used to specify that a column must have a value.

**UNIQUE** ensures that all values in a column are different.

**PRIMARY KEY** is a combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table.


**FOREIGN KEY** prevents actions that would destroy links between tables.

**CHECK** ensures that the values in a column satisfies a specific condition.

**DEFAULT** sets a default value for a column if no value is specified.

**CREATE INDEX** is used to create and retrieve data from the database very quickly.

## How to SHOW, DELETE & DROP Tables

```
-- Display a list of tables in a database
SHOW TABLES;

-- Remove an existing table
DROP TABLE table_name;
```

Be careful when you **'DROP TABLE'** because it removes data permanently. 

## How to Insert ROWS & RECORDS (single and multiple)

### Inserting a Single Row:

```
-- Syntax --
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

-- Example --
INSERT INTO users (username, email, age)
VALUES ('aimee_b', 'aimee@gmail.com', 40);
```

### Inserting Multiple Rows:

```
-- Syntax --
INSERT INTO table_name (column1, column2, column3, ...)
VALUES
    (value1_row1, value2_row1, value3_row1, ...),
    (value1_row2, value2_row2, value3_row2, ...),
    ...;

-- Example --
INSERT INTO users (username, email, age)
VALUES
    ('aimee_b', 'aimee@gmail.com', 40),
    ('jesse_w', 'jesse@gmail.com', 47),
    ('sherrill_p', 'sherrill@gmail.com', 69);
```

## How to SELECT with the WHERE Clause

```
-- Syntax --
SELECT column_list FROM table_name WHERE condition;

-- Example --
SELECT FirstName, LastName, HireDate FROM Employees WHERE Salary > 6000;
```

## How to SELECT with the WHERE Clause using a range

```
-- Syntax --
SELECT column1, column2, ...
FROM table_name
WHERE column_name BETWEEN value1 AND value2;

-- Example --
SELECT * FROM employees
WHERE Salary BETWEEN 5000 AND 7000;
```

## How to DELETE an individual ROW

```
-- Syntax --
DELETE FROM your_table_name
WHERE your_condition_column = your_condition_value;


-- Example --
DELETE FROM employees
WHERE EmployeeID = 129;
```

## How to UPDATE a ROW

```
-- Syntax --
UPDATE your_table_name
SET column1 = value1, column2 = value2, ...
WHERE your_condition_column = your_condition_value;

-- Example --
UPDATE employees
SET Salary = 5000, DepartmentID = 3
WHERE EmployeeID = 115;
```

## How to add a new column and modify it

```
-- Syntax --
ALTER TABLE your_table_name
ADD COLUMN new_column_name data_type;

-- Example --
ALTER TABLE employees
ADD COLUMN PositionID INT;
```

## How to Order by and use Distinct

```
-- Syntax --
SELECT DISTINCT column1, column2, ...
FROM your_table_name
ORDER BY column_name [ASC|DESC];

-- Example --
SELECT DISTINCT job_title
FROM employees
ORDER BY salary ASC;
```

## How to Concatenate Columns

```
-- Using CONCAT function --

-- Syntax --
SELECT CONCAT(column1, ' ', column2) AS concatenated_columns
FROM your_table_name;

-- Example --
SELECT CONCAT(firstName, ' ', lastName) AS concatenated_columns
FROM persons;

-- Using Concatenation Operator (||) --

-- Syntax --
SELECT column1 || ' ' || column2 AS concatenated_columns
FROM your_table_name;

-- Example --
SELECT firstName || ' ' || lastName AS concatenated_columns
FROM persons;
```

## How to Select Distinct Rows

```
-- Syntax --
SELECT DISTINCT column1, column2, ...
FROM table_name;

-- Example --
SELECT DISTINCT firstName, lastName
FROM persons;
```

## LIKE Operator

The **LIKE** operator is used in a **WHERE** clause to search for a specific pattern in a column.

```
-- Syntax --
SELECT column1, column2, ...
FROM table_name
WHERE column LIKE pattern;

-- Example --
SELECT * FROM persons
WHERE lastName LIKE 'Sm%';
```
There are two wildcards often used in conjunction with the **LIKE** operator: 
The **%** wildcard represents any number of characters, even zeros.

```
-- Example 1: Putting % at the end of a condition --
SELECT * FROM persons
WHERE lastName LIKE 'Sm%';

-- Returns all persons with a last name that starts with "Sm" (aka Smith, or Smee).


-- Example 2: Putting % at the beginning of a condition --
SELECT * FROM persons
WHERE lastName LIKE '%son';

-- Returns all persons with a last name that ends with "son" (aka Johnson, or Erickson).
```

The **_** wildcard represents a single character.

```
-- Example --
SELECT * FROM persons
WHERE firstName LIKE 'L_nd_';

-- Returns all persons with a first name that starts with "L" and has a "nd" as the third and fourth character (aka Linda, or Lyndi).
```

## IN Operator

The **IN** operator allows you to specify multiple values in a **WHERE** clause.

The **IN** operator is a shorthand for multiple OR conditions.

```
-- Syntax --
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);

-- Example --
SELECT * FROM employees
WHERE department IN ('Sales', 'Administration', 'Accounting');

-- Result will yeild all employees who work in the Sales, Administrative, or Accounting departments of the company.
```

## How to Create & Remove Index

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

**Note:** Updating a table with indexes takes more time than updating a table without (because the indexes also need an update). So, only create indexes on columns that will be frequently searched against.

The CREATE INDEX statement is used to create indexes in tables.

The DROP INDEX statement is used to remove indexes in tables.

```
-- CREATE INDEX Syntax --
CREATE INDEX index_name
ON table_name (column1, column2, ...);

-- Example --
CREATE INDEX idx_department_salary
ON employees (department, salary);

-- DROP INDEX Syntax --
DROP INDEX table_name.index_name;

-- Example --
DROP INDEX employees.idx_department_salary;
```


#### Create Two Tables demonstrating a one to many relationship that shows a PK & FK How to use Inner Join How to JOIN Multiple Tables

In the example below, the Employees table would be considered a **"many"** table because each employee can belong to only one department.

The Department table is considered a **"one"** table because a department can have many employees.


```
-- The 'many' table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(255),
    LastName VARCHAR(255),
    DepartmentID INT,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

-- The 'one' table
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(255)
);
```
### Using INNER JOIN

**INNER JOIN** returns records that have matching values in both tables. By using this keyword, you can select rows from both tables as long as there is a match between the columns. If there are records in the "Department" table that do not have matches in "Employees", these employees won't be shown.

```
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

This query retrieves a list of employees along with the name of the department they belong to, based on the matching "DepartmentID" values in both tables.

### JOIN Multiple Tables

In this example, we're going to create a new table called "Positions", and add a new column to the Employees table called "PositionID". This new "PositionID" column will be a FOREIGN KEY in the Employees table.
We will then JOIN the Positions table to the Employees table.

```
-- Creating a "Positions" table
CREATE TABLE Positions (
    PositionID INT PRIMARY KEY,
    PositionTitle VARCHAR(255)
);

-- Adding the PositionID column to the Employees table
ALTER TABLE Employees
ADD COLUMN PositionID INT;

-- Defining the FOREIGN KEY constraint for "PositionID" on the Employees table
ALTER TABLE Employees
ADD CONSTRAINT fk_PositionID
FOREIGN KEY (PositionID) REFERENCES Positions(PositionID);

-- Updated Employees table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(255),
    LastName VARCHAR(255),
    DepartmentID INT,
    PositionID INT,  -- New column for job title
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID),
    FOREIGN KEY (PositionID) REFERENCES Positions(PositionID)
);

-- Creating a JOIN from the Department and Positions tables to the Employees table.
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName, Positions.PositionTitle
FROM Employees
INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID
INNER JOIN Positions ON Employees.PositionID = Positions.PositionID;
```
The above example with the joins will now retrieve employees with their departments and positions.
