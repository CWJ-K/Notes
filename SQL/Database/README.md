<!-- omit in toc -->
# Introduction

<br />

<!-- omit in toc -->
# Table of Contents

<br />


# Fundamental Concepts
## Injection
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

### Protection
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

## **hosting**
* store (a website or other data) on a server or other computer so that it can be accessed over the internet
* e.g. MS SQL sever, oracle, mysql

<br />

## Data types
> Data types might have different names in different database. And even if the name is the same, the size and other details may be different! Always check the documentation!

* data types affect [memory usage](https://shanewelgama.com/2020/08/16/tinyint-vs-smallint-vs-int-vs-bigint-does-size-matter/) a lot, be careful to choose
* [industries](https://stackoverflow.com/questions/803225/when-should-i-use-double-instead-of-decimal) affect which type to be used
  
* memory and range: `tinyint` < `smallint` < `int` < `bigint`
* memory and precision: `Float` <  `Double` < `Decimal`

<br />

## Schema
> Postgre: `set schema myschema` is an alias to `SET search_path TO myschema`; is not available in POSTGRES 8.x.

### Constraints
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





# SQL Statements

## Drop
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

## Delete
* only for data, no schema affected
  * delete existing records in a table 
  * deletes all rows in the "Customers" table, without deleting the table. This means that the table structure, attributes, and indexes will be intact

  ```sql
  DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste'
  DELETE FROM Customers
  ```

<br />

## Truncate
* drop all data, not affect schemas
  ```SQL
  TRUNCATE TABLE categories
  ```

<br />


## Create
* new database, new table

### CREATE OR REPLACE TABLE

```SQL
CREATE DATABASE testDB

CREATE TABLE Persons(
	PersonID int,
	Lastname varchar(255),
	FirstName varchar(255
)
```

<br />

## Backup
* Backup Database: create a full backup of an existing SQL database

```SQL
/* backup to disk-D, the filename extension is .bak (backup) */
BACKUP DATABASE testDB
TO DISK = 'D\backup\testDB.bak'   

```

### backup with differential
* only backs up the parts of the database that have changed since the last full database backup.

```SQL
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak'
WITH DIFFERENTIAL  
```
<br />

## Alter
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

## View
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

## Constraints
### Not Null
```sql
ALTER TABLE Persons
MODIFY Age int NOT NULL

```
<br />

### Unique

<br />

### Primary key

<br />

### Foreign Key

<br />

### check

<br />

### Default

<br />

### index

<br />

### auto increment

<br />

# Comparison
## Drop vs Delete vs Truncate
|Statement|Meaning|
|:---:|:---|
|drop|affect schema and data|
|delete|only for data, no schema affected|
|truncate|drop all data, not affecting schema|



