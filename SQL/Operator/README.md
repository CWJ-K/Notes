<!-- omit in toc -->
# Introduction
How to use SQL Operators statements?

<br />

<!-- omit in toc -->
# Table of Contents
- [SQL Statements](#sql-statements)
  - [1. Insert](#1-insert)
    - [1.1. MySQL: INSERT ON DUPLICATE KEY UPDATE](#11-mysql-insert-on-duplicate-key-update)
    - [1.2. INSERT INTO SELECT](#12-insert-into-select)
    - [INSERT INTO](#insert-into)
  - [2. Select](#2-select)
    - [2.1. SELECT INTO](#21-select-into)
  - [3. ANY, ALL, EXISTS, Some](#3-any-all-exists-some)
  - [UPDATE](#update)
  - [LIKE](#like)
    - [Character](#character)
  - [Stored Procedures](#stored-procedures)
    - [without parameters](#without-parameters)
    - [with parameters](#with-parameters)
- [Comparison](#comparison)
  - [1. INSERT INTO SELECT vs SELECT INTO](#1-insert-into-select-vs-select-into)
  - [2. UPDATE vs INSERT INTO](#2-update-vs-insert-into)
<br />

# SQL Statements

<br />

## 1. Insert

### 1.1. MySQL: INSERT ON DUPLICATE KEY UPDATE
* update the existing row with the new values instead

  ```sql
  INSERT INTO table (column_list)
  VALUES (value_list)
  ON DUPLICATE KEY UPDATE
  c1 = v1, 
  c2 = v2,
  ...;
  ```

<br />

### 1.2. INSERT INTO SELECT
* copies data from one table and inserts it into **another** table
  
  ```sql
  /*             table    columns*/
  INSERT INTO Customers (CustomerName, City, Country)
  SELECT SupplierName, City, Country FROM Suppliers
  ```

<br />

### INSERT INTO
* insert new records in an existing table

  ```sql
  INSERT INTO Customers (CustomerName, ContactName)
  VALUES ('Car', 'Tom')
  ```

<br />

## 2. Select

### 2.1. SELECT INTO
* copies data from one table into a new table. The new table will be created with the column-names and types as defined in the **old** table.

  ```sql
  SELECT c.customerName as name, o.orderID
  INTO CustomerOrderBackup2018
  FROM Customers c
  LEFT JOIN Orders o ON c.ID = o.ID
  
  ```

<br />

## 3. ANY, ALL, EXISTS, Some
* ALL: returns TRUE if ALL of the subquery values meet the condition

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ALL(SELECT ProductID FROM OrderDetails WHERE Quantity = 10) 
```

* ANY: returns TRUE if ANY of the subquery values meet the condition

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY(SELECT ProductID FROM OrderDetails WHERE Quantity = 10) 
```

* EXIST: test for the existence of any record in a subquery. same as any, the execution time is less. Since `any` execute every column to check if it fits the conditions, `exist` checks the all table at first and execute commands.
> `ANY`, `EXIST` do not return values fitting the conditions, but return all values if any value fits the conditions in the table.

```sql
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
```

<br />

## UPDATE 
* to modify the **existing** records in an existing table.
  
```sql
UPDATE Customers
SET ContactName = 'hi', City = 'ho'
WHERE CustomerID = 1
```

<br />

## LIKE
### Character
* different SQL with different characters. It is required to see documents before using characters.

|Character|Meaning|Example|Result|
|:---:|:---|:---:|:---:|
|%|Select words with specific characters|bl%|bl, black, blue, and blob|
|_|Represents any single character|h_t|hot, hat, and hit|
|[]|Represents any single character within the brackets|h[oa]t|hot and hat, but not hit|
|[^]|Represents any character not in the brackets|h[^oa]t|hit, but not hot and hat|
|[-]|Represents any single character within the specified range|c[a-b]t|cat and cbt|

<br />

## Stored Procedures
* a prepared SQL code that you can save, so the code can be reused over and over again
* if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it

<br />

### without parameters
```sql
## procedure
CREATED PROCEDURE SelectAllCustomers
AS
SELECT * FROM Custoomers
GO
## 執行儲存的指令碼
EXEC SelectAllCustomers
```

<br />

### with parameters
```sql
CREATED PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
AS
SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
GO
## Execute
EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP'
```


<br />

# Comparison

## 1. INSERT INTO SELECT vs SELECT INTO
* INSERT INTO: **copies** data from one table and inserts it into **another** table
* SELECT into: **copies** data from one table into a **new** table. The new table will be created with the column names and types as defined in the old table.

## 2. UPDATE vs INSERT INTO