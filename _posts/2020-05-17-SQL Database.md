---
layout: page
title: SQL Database
tags: SQL
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->

## SQL Database

- SQL CREATE DATABASE

`CREATE DATABASE databasename;`

- SQL DROP DATABASE

`DROP DATABASE databasename;`

- SQL BACKUP DATABASE for SQL Server

`BACKUP DATABASE databasename TO DISK = ‘filepath’;`

- SQL CREATE TABLE

```
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) 
);
```

-SQL DROP TABLE

`DROP TABLE tablename;`

**TRUNCATE**

> The TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself.

`TRUNCATE TABLE table_name;`

- SQL ALTER TABLE

Alter table - add column

```
ALTER TABLE Customers
ADD Email varchar(255);
```

Alter table - drop column

```
ALTER TABLE Customers
DROP COLUMN Email;
```

- SQL Constraints

- NOT NULL

```
ALTER TABLE Persons
MODIFY Age int NOT NULL;
```

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

- UNIQUE

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    UNIQUE (ID)
);
```

- PRIMARY KEY

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID)
);
```

- FOREIGN KEY

> A FOREIGN KEY is a key used to link two tables together.

> A FOREIGN KEY is a field (or collection of fields) in one table that refers to the PRIMARY KEY in another table.

> The table containing the foreign key is called the child table, and the table containing the candidate key is called the referenced or parent table.

```
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
```

```
ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

```
ALTER TABLE Orders
DROP FOREIGN KEY FK_PersonOrder;
```

- CHECK

> The CHECK constraint is used to limit the value range that can be placed in a column.
> If you define a CHECK constraint on a single column it allows only certain values for this column.
> If you define a CHECK constraint on a table it can limit the values in certain columns based on values in other columns in the row.

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);
```

- DEFAULT

> The DEFAULT constraint is used to provide a default value for a column.

> The default value will be added to all new records IF no other value is specified.

```
CREATE TABLE Orders (
    ID int NOT NULL,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT GETDATE()
);
```

- INDEX

```
CREATE INDEX idx_pname
ON Persons (LastName, FirstName);
```

```
ALTER TABLE table_name
DROP INDEX index_name;
```

- AUTO INCREMENT

```
CREATE TABLE Persons (
    Personid int NOT NULL AUTO_INCREMENT,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (Personid)
);
```

**let the sequence start with 100**

```
ALTER TABLE Persons AUTO_INCREMENT=100;
```

- SQL Dates

> MySQL comes with the following data types for storing a date or a date/time value in the database:
> DATE - format YYYY-MM-DD
> DATETIME - format: YYYY-MM-DD HH:MI:SS
> TIMESTAMP - format: YYYY-MM-DD HH:MI:SS
> YEAR - format YYYY or YY

```
SELECT * FROM Orders WHERE OrderDate='2008-11-11'
```

- SQL VIEW

```
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = "Brazil";
```