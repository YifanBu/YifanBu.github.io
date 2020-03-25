---
title: "PostgreSQL"
date: 2020-02-07
tags: [SQL, PostgreSQL]
header:
image:
excerpt: "Database"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# Intro

Databases are systems that allow users to *store* and *organize* data. They are useful when dealing with massive amounts of data.

PostgreSQL is open source, widely used on internet, and multi platform.

SQL(Structured Query Language) is the programming language used to communicate with the database.

# Creating Databases and Tables

## Data Types

- Boolean: true, false, NULL
- Character: char, char(n), varchar(n)
- Number: integers, floating-point numbers
- Temporal: data and time related data
- Special types
- Array

## Primary Keys & Foreign Keys

A primary key is a column or a group of columns that is used to identify a row uniquely in a table.

A foreign key is a field or group of fields in a table that uniquely identifies a row in another table. In other words, a foreign key is defined in a table that refers to the primary key of the other table.

<!-- 
## Create Table

-->

# SQL Fundamentals

## SELECT

SELECT: retrieve information from table.

```sql
SELECT column_name FROM table_name;

SELECT c1, c3 FROM table_1;

SELECT * FROM table_1;
```

Use an asterisk(*) in the SELECT will automatically query everything, which increases traffic between the data base server and the application, which can slow down the retrieval of results.


## SELECT DISTINCT

Sometimes a table contains a column that has duplicate values, and you may find yourself in a situation where you only want to list the distinct values.

DISTINCT: return only the distinct values in a column.

```sql
SELECT DISTINCT column_name FROM table_name;

SELECT DISTINCT(column_name) FROM table_name;
```

## COUNT

The COUNT function returns the number of input rows in the table that match a specific condition of a query.

```sql
SELECT COUNT(DISTINCT column_name) FROM table_name;
```

## SELECT WHERE

```sql
SELECT column1, column2 FROM table1 WHERE conditions;
```

The conditions are used to filter the rows returned from the SELECT statement.


```sql
SELECT name, choice FROM table
WHERE name='David' AND choice='Red';
```

## ORDER BY

Sometimes PostgreSQL returns the same request query results in a different order.

You can use *ORDER BY* to sort rows based on a column value, in either ascending or descending order.

```sql
SELECT column_1, column_2
FROM table
ORDER BY column_1 ASC/DESC;
```

If you leave it blank, ORDER BY uses ASC by default.

You can also *ORDER BY* multiple columns:

```sql
SELECT company, name, sales
FROM table
ORDER BY company, sales;
```

## LIMIT

The LIMIT command allows us to limit the number of rows returned for a query to get an idea of the table layout.

LIMIT goes at the very end of a query request and is the last command to be executed.


## BETWEEN

The BETWEEN operator is the same as:

- ```value >= low AND value <= high```
- ```value BETWEEN low AND high```

The NOT BETWEEN operator is the same as: 

- ```value < low OR value > high```
- ```value NOT BETWEEN low AND high```

## IN

Create a condition that checks to see if a value is included in a list of multiple options.

```sql
SELECT color FROM table
WHERE color IN/NOT IN ('red', 'blue', 'green');
```

## LIKE and ILIKE

The LIKE allows us to perform **pattern matching** against string data with the use of **wildcard** characters:

- %: matches any sequence of characters
- _: matches any single character

LIKE is case-sensitive, while ILIKE is not.

# GROUP BY

GROUP BY: aggregate data and apply functions to better understand how data is distributed per category.

## Aggregation Functions

Take multiple inputs and return a single output.

Aggregate function calls happen only in the SELECT clause or the HAVING clause.

Most common aggregate functions:
- AVG(): returns a floating point value, use ROUND() ro specify precision after the decimal.
- COUNT()
- MAX()
- MIN()
- SUM()

```sql
SELECT ROUND(AVG(replacement_cost), 4)
FROM film;
```

## GROUP BY

GROUP BY allows us to aggregate columns per some category.

We need to choose a categorical column to GROUP BY.

The GROUP BY clause must appear right after a **FROM**  or **WHERE** statement.


```sql
SELECT category_col, AGG(data_col)
FROM table1
GROUP BY category-col;
```

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
```

```sql
SELECT DATE(payment_date), SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC
```

## HAVING

HAVING allows us to filter after an aggregation has already taken place.

```sql
SELECT company, SUM(sales)
FROM finance_table
GROUP BY company
HAVING SUM(sales) > 1000;
```

# JOINS

**JOINS** allows us to combine information from multiple tables.

## AS

**AS** allows us to create an "alias" for a column or result.

```sql
SELECT SUM(amount) AS rental_price
FROM payment;
```

**AS** operator gets executed at the very end of a query, meaning that we can not use the ALIAS inside a WHERE operator.

## INNER JOINS

```sql
SELECT * FROM TableA
INNER JOIN TableB
ON TableA.col_match = TableB.col_match;
```

## FULL OUTER JOINS

Just grabs everything.

```sql
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON TableA.col_match = TableB.col_match;
```

## LEFT OUTER JOINS

```sql
SELECT * FROM TableA
LEFT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match;
```

## RIGHT OUTER JOINS

```sql
SELECT * FROM TableA
RIGHT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match;
```

## UNIONS

UNION combines result sets of two or more SELECT statements into a single result set.

The UNION operator is often used to combine data from similar tables that are not perfectly normalized. Those tables are often found in the reporting or data warehouse system.

```sql
SELECT column_1, column_2
FROM tbl_name_1
UNION
SELECT column_1, column_2
FROM tbl_name_2;
```

# Advanced SQL Commands

- Timestamps and EXTRACT
- Math Functions
- String Functions
- Sub-query
- Self-Join

# PostgreSQL with Python


