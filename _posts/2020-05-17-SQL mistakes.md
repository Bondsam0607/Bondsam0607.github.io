---
layout: page
title: SQL mistakes
tags: SQL
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

## SQL mistakes

1. Select all the *different* values from the `Country` column in the `Customers` table.

```mysql
SELECT DISTINCT Country FROM Customers;
```

2. Use the `NOT` keyword to select all records where `City` is NOT "Berlin".

```mysql
SELECT * FROM Customers
WHERE NOT City = 'Berlin';
```

3. Select all records where the `CustomerID` column has the value 32.

```mysql
SELECT * FROM Customers
WHERE CustomerID = 32;
```

4. Select all records from the `Customers` table, sort the result alphabetically by the column `City`.

```mysql
SELECT * FROM Customers
ORDER BY City;
```

5. Select all records from the `Customers` table, sort the result *reversed* alphabetically by the column `City`.

```mysql
SELECT * FROM Customers
ORDER BY City DESC;
```

6. Select all records from the `Customers` table, sort the result alphabetically, first by the column `Country`, then, by the column `City`.

```mysql
SELECT * FROM Customers
ORDER BY Country, City;
```

7. Delete all the records from the `Customers` table.

```mysql
DELETE FROM Customers;
```

8. Select all records where the value of the `City` column does NOT start with the letter "a".

```mysql
SELECT * FROM Customers
WHERE City NOT LIKE 'a%';
```

9. Select all records where the first letter of the `City` is an "a" or a "c" or an "s".

```mysql
SELECT * FROM Customers
WHERE City LIKE '[acs]%';
```

10. Select all records where the first letter of the `City` starts with anything from an "a" to an "f".

```mysql
SELECT * FROM Customers
WHERE City LIKE '[a-f]%';
```

11. Select all records where the first letter of the `City` is NOT an "a" or a "c" or an "f".

```mysql
SELECT * FROM Customers
WHERE City LIKE '[^acf]%';
```

12. Use the `IN` operator to select all the records where `Country` is either "Norway" or "France".

```mysql
SELECT * FROM Customers
WHERE Country IN ('Norway', 'France');
```

13. When displaying the `Customers` table, make an ALIAS of the `PostalCode` column, the column should be called `Pno` instead.

```mysql
SELECT CustomerName,
Address,
PostalCode AS Pno
FROM Customers;
```

14. Add a column of type `DATE` called `Birthday`.

```mysql
ALTER TABLE Persons
ADD Birthday DATE;
```

15. Delete the column `Birthday` from the `Persons` table.

```mysql
ALTER TABLE Persons
DROP COLUMN Birthday;
```

