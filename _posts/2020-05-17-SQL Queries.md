---
layout: page
title: SQL Queries
tags: SQL
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->

## SQL SYNTAX

- SQL SELECT

```
select Column
select *
```

- SQL SELECT DISTINCT

```
select distinct
select COUNT(distinct column_name)
```

- SQL WHERE

```where clause```
		

- SQL AND,OR AND NOT Operators

```
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

```
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

```
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

- SQL ORDER BY
  **ASC:ascending**/
  **DESC:descending**

```
order by
order by desc
order by several column
```

```
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

- SQL INSERT INTO

```
INSERT INTO
```

> If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query.

```
INSERT INTO table_name
VALUES (value1, value2, value3, ...)
```

**Insert Data Only in Specified Columns**

> The following SQL statement will insert a new record, but only insert data in the "CustomerName", "City", and "Country" columns (CustomerID will be updated automatically):

```
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

- SQL NULL Values

> We will have to use the IS NULL and IS NOT NULL operators instead.

```
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

```
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```

- SQL Updates

**Updating table**

```
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```

**Updating multiple Records**

> The following SQL statement will update the contactname to "Juan" for all records where country is "Mexico":

```
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico’;
```

- SQL DELECT Statement

```
DELETE FROM Customers 
WHERE CustomerName='Alfreds Futterkiste';
```

**Delete All Records**

```
DELETE FROM Customers;
```

- SQL TOP, LIMIT or ROWNUM Clause

**TOP**

`select TOP 3 * from costumers;`

**LIMIT**

```
SELECT * from Costumers
LIMIT 3`
```

**ROWNUM**

```
SELECT * FROM Customers
WHERE ROWNUM <= 3;
```

**The three syntaxes above are equivalent.**

**TOP PERCENT**

```
SELCT TOP 50 PERCENT *
FROM Costumers;
```

**With a WHERE clause**

```
SELECT * FROM Customers
WHERE Country='Germany' 
AND ROWNUM <= 3;
```

- SQL MIN() AND MAX()

```
SELECT MIN(Price) AS
SmallestPrice
From Products;
```

- SQL COUNT(),AVG() and SUM() Functions

**COUNT()**

```
SELECT COUNT(ProductID)
FROM Products;
```


RESULT:

| COUNT(ProductID) |
| :--------------- |
| 77               |

**AVG()**

```
SELECT AVG(Price)
FROM Products;
```

Result:

| AVG(Price)           |
| :------------------- |
| 28.86636363636363637 |

**SUM()**

```
SELECT SUM(Quantity)
FROM OrderDetails;
```

- SQL LIKE
  - % The percent sign represents zero, one, or multiple characters
  - _ The underscore represents a single character

```
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%';
```

- SQL Wildcards

REG

- SQL IN

```
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```

- SQL BETWEEN

```
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;
```

- SQL Aliases

```
SELECT CustomerID AS ID, CustomerName AS Customer
FROM Customers;
```

- SQL Joins

> A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

**Inner Join**

> Inner Join vs. Outer Join. In SQL, a join is used to compare and combine — literally join — and return specific rows of data from two or more tables in a database. An inner join finds and returns matching data from tables, while an outer join finds and returns matching data and some dissimilar data from tables.

```
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```


**Different types of SQL JOINs**
	- (INNER) JOIN: Returns records that have matching values in both tables
	- LEFT (OUTER) JOIN: Return all records from the left table, and the matched records from the right table
	- RIGHT (OUTER) JOIN: Return all records from the right table, and the matched records from the left table
	- FULL (OUTER) JOIN: Return all records when there is a match in either left or right table<br />
![](https://www.w3schools.com/sql/img_innerjoin.gif)<br />
![](https://www.w3schools.com/sql/img_leftjoin.gif)<br />
![](https://www.w3schools.com/sql/img_rightjoin.gif)<br />
![](https://www.w3schools.com/sql/img_fulljoin.gif)<br />

- SQL UNIONS

The SELECT statement within UNION has to fulfill the following 3 features:

* Each SELECT statement within UNION must have the same number of columns
* The columns must also have similar data types
* The columns in each SELECT statement must also be in the same order

```
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

**UNION ALL Syntax**

> allow duplicate values

```
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

- SQL GROUP BY

```
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

Result:

| COUNT(CostumerID) | Country |
| :---------------- | :------ |
| 5                 | Germany |
| 3                 | England |
| 1                 | China   |

- SQL HAVING

> The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions.

```
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

- SQL EXISTS

> The EXISTS operator is used to test for the existence of any record in a subquery.

> The EXISTS operator returns true if the subquery returns one or more records.

```
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

- SQL ANY and ALL

> The ANY and ALL operators are used with a WHERE or HAVING clause.

> The ANY operator returns true if any of the subquery values meet the condition.

> The ALL operator returns true if all of the subquery values meet the condition.

```
SELECT ProductName
FROM Products
WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
```

- SQL INSERT INTO SELECT

> The INSERT INTO SELECT statement copies data from one table and inserts it into another table.

```
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers;
```

- SQL CASE

```
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN "The quantity is greater than 30"
    WHEN Quantity = 30 THEN "The quantity is 30"
    ELSE "The quantity is under 30"
END AS QuantityText
FROM OrderDetails;
```


Above are the basic syntaxes of SQL language, some of them may differ in different SQLs.

