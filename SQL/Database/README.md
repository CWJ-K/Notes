<!-- omit in toc -->
# Introduction
How to use SQL Database statements?

<br />

<!-- omit in toc -->
# Table of Contents
- [Fundamental Concepts](#fundamental-concepts)
  - [1. Injection](#1-injection)
    - [1.1. Protection](#11-protection)
  - [2. **hosting**](#2-hosting)
  - [3. Data types](#3-data-types)
  - [4. Schema](#4-schema)
    - [4.1. Constraints](#41-constraints)
- [SQL Statements](#sql-statements)
  - [1. Drop](#1-drop)
  - [2. Delete](#2-delete)
  - [3. Truncate](#3-truncate)
  - [4. Create](#4-create)
    - [4.1. CREATE OR REPLACE TABLE](#41-create-or-replace-table)
  - [5. Backup](#5-backup)
    - [5.1. backup with differential](#51-backup-with-differential)
  - [6. Alter](#6-alter)
  - [7. View](#7-view)
  - [8. Constraints](#8-constraints)
    - [8.1. Not Null](#81-not-null)
    - [8.2. Unique](#82-unique)
    - [8.3. Primary key](#83-primary-key)
    - [8.4. Foreign Key](#84-foreign-key)
    - [8.5. check](#85-check)
    - [8.6. Default](#86-default)
    - [8.7. index](#87-index)
    - [8.8. auto increment](#88-auto-increment)
- [Comparison](#comparison)
  - [1. Drop vs Delete vs Truncate](#1-drop-vs-delete-vs-truncate)

<br />

# Fundamental Concepts

## 1. Injection
* Web Page - code injection
  * web hacking techniques that may destroy databases
  * use `or` and `functions are true` to get all data <br />
    e.g. where user = '' or ''='' 
    >                      '1'='1'
* Batched SQL Statements
  * use semi-column  to create another statement
  ```SQL
  SELECT * FROM Users WHERE UserId = 105; DROP TABLE Suppliers;
  ```

<br />

### 1.1. Protection
* SQL Parameters
  * parameters are represented in the SQL statement by a @ marker
  * SQL engine checks each parameter to ensure that it is correct for its column and is treated literally

```sql
txtNam = getRequestString("CustomerName");
txtAdd = getRequestString("Address");
txtCit = getRequestString("City");
txtSQL = "INSERT INTO Customers (CustomerName,Address,City) Values(@0,@1,@2)";
db.Execute(txtSQL,txtNam,txtAdd,txtCit);
```

<br />

## 2. **hosting**
* store (a website or other data) on a server or other computer so that it can be accessed over the internet
* e.g. MS SQL sever, oracle, mysql

<br />

## 3. Data types
> Data types might have different names in different database. And even if the name is the same, the size and other details may be different! Always check the documentation!

* data types affect [memory usage](https://shanewelgama.com/2020/08/16/tinyint-vs-smallint-vs-int-vs-bigint-does-size-matter/) a lot, be careful to choose
* [industries](https://stackoverflow.com/questions/803225/when-should-i-use-double-instead-of-decimal) affect which type to be used
  
* memory and range: `tinyint` < `smallint` < `int` < `bigint`
* memory and precision: `Float` <  `Double` < `Decimal`

<br />

## 4. Schema
> Postgre: `set schema myschema` is an alias to `SET search_path TO myschema`; is not available in POSTGRES 8.x.

<br />

### 4.1. Constraints
* limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.
  
|Constraint|Meaning|
|:---:|:---|
|`NOT NULL`|Ensures that a column cannot have a NULL value|
|`UNIQUE`|Ensures that all values in a column are different|
|`PRIMARY KEY`|A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table. only one PRIMARY KEY
 constraint per table|
|`FOREIGN KEY`|Prevents actions that would destroy links between tables|
|`CHECK`|Ensures that the values in a column satisfies a specific condition|
|`DEFAULT`|Sets a default value for a column if no value is specified|
|`CREATE INDEX`|Used to create and retrieve data from the database very quickly|

<br />

# SQL Statements

## 1. Drop
* affect schema and data
  * delete a column in a table
  * others related to schema changes

  ```SQL
  ALTER TABLE Customers
  DROP COLUMN ContactName;

  DROP Database testDB

  DROP Table snippers
  ```

<br />

## 2. Delete
* only for data, no schema affected
  * delete existing records in a table 
  * deletes all rows in the "Customers" table, without deleting the table. This means that the table structure, attributes, and indexes will be intact

  ```sql
  DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste'
  DELETE FROM Customers
  ```

<br />

## 3. Truncate
* drop all data, not affect schemas
  ```SQL
  TRUNCATE TABLE categories
  ```

<br />


## 4. Create
* new database, new table

### 4.1. CREATE OR REPLACE TABLE

```SQL
CREATE DATABASE testDB

CREATE TABLE Persons(
	PersonID int,
	Lastname varchar(255),
	FirstName varchar(255
)
```

<br />

## 5. Backup
* Backup Database: create a full backup of an existing SQL database

```SQL
/* backup to disk-D, the filename extension is .bak (backup) */
BACKUP DATABASE testDB
TO DISK = 'D\backup\testDB.bak'   

```

### 5.1. backup with differential
* only backs up the parts of the database that have changed since the last full database backup.

```SQL
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak'
WITH DIFFERENTIAL  
```
<br />

## 6. Alter
* add, delete, or modify columns or constraints in an existing table 
> not data itself
* **modify**: change the data type of a column

```sql
/* add column */
ALTER TABLE Customers
ADD Email varchar(255)

/* delete column */
ALTER TABLE Customers
DROP COLUMN Email

/* modify column */
ALTER TABLE Customers
MODIFY COLUMN column_name datatype

```

## 7. View
* a virtual table based on the result-set of an SQL statement
* Commonly used by analysts 

```SQL
/*CREATE VIEW: create a new view*/
             /* table name */
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil'

/*CREATE OR REPLACE VIEW: update a view*/
CREATE OR REPLACE VIEW [Brazil Customers] AS 
SELECT CustomerName, ContactName, City
FROM Customers 
WHERE Country = 'Brazil'

/*DROP VIEW*/
DROP VIEW [Brazil Customers]
```

<br />

## 8. Constraints

### 8.1. Not Null
```sql
ALTER TABLE Persons
MODIFY Age int NOT NULL

```
<br />

### 8.2. Unique

<br />

### 8.3. Primary key

<br />

### 8.4. Foreign Key

<br />

### 8.5. check

<br />

### 8.6. Default

<br />

### 8.7. index

<br />

### 8.8. auto increment

<br />

# Comparison

## 1. Drop vs Delete vs Truncate
|Statement|Meaning|
|:---:|:---|
|drop|affect schema and data|
|delete|only for data, no schema affected|
|truncate|drop all data, not affecting schema|



