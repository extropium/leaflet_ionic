# Week 3 - Subqueries and Joins in SQL

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Module introduction](#module-introduction)
  - [Joins](#joins)
- [Using subqueries](#using-subqueries)
  - [What are subqueries?](#what-are-subqueries)
  - [Problem: Get regions for customers who have ordered freight >= 100](#problem-get-regions-for-customers-who-have-ordered-freight--100)
    - [Combined with a subquery](#combined-with-a-subquery)
  - [Working with subquery statements](#working-with-subquery-statements)
- [Subquery Best Practices and Considerations](#subquery-best-practices-and-considerations)
  - [Subquery in a Subquery](#subquery-in-a-subquery)
  - [Subqueries for calculations](#subqueries-for-calculations)
  - [The power of subqueries](#the-power-of-subqueries)
- [Joining Tables: An Introduction](#joining-tables-an-introduction)
  - [Benefits of breaking data into tables](#benefits-of-breaking-data-into-tables)
  - [Joins](#joins-1)
- [Cartesian (Cross) Joins](#cartesian-cross-joins)
  - [Cartesian / Cross Join Example](#cartesian--cross-join-example)
  - [Different ways to create cartesian joins](#different-ways-to-create-cartesian-joins)
  - [Takeaways](#takeaways)
- [Inner Joins](#inner-joins)
  - [Qualifying and aliasing](#qualifying-and-aliasing)
  - [Best practices](#best-practices)
- [Aliases and Self Joins](#aliases-and-self-joins)
  - [Aliases](#aliases)
    - [Example](#example)
  - [Self joins](#self-joins)
- [Advanced Joins: Left, Right, and Full Outer Joins](#advanced-joins-left-right-and-full-outer-joins)
  - [Left join](#left-join)
  - [Right join](#right-join)
  - [Full outer join](#full-outer-join)
- [Unions](#unions)
  - [Union syntax](#union-syntax)
- [Summary](#summary)
  - [Best practices using joins](#best-practices-using-joins)
  - [Slowly do](#slowly-do)
  - [Joins and database performance](#joins-and-database-performance)
  - [Join syntax](#join-syntax)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Module introduction

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/NDsRj/module-introduction)

Subqueries and joins are used to combine data from multiple tables.

### Joins

We'll learn about different types of joins:

- cartesian joins
- inner joins
- left and right joins
- full outer joins
- self joins

We'll also learn how to make queries cleaner and more efficient using aliases
and pre-qualifiers.

## Using subqueries

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/FChaS/using-subqueries)

Using one table is useful, but a lot of value comes from using data from
multiple tables.

One of the ways to combine data from multiple tables is by using subqueries.

### What are subqueries?

Subqueries are queries embedded in other queries.

Relational databases store data in multiple tables. Subqueries merge data from
multiple sources together.

Subqueries are useful for adding additional filtering criteria.

### Problem: Get regions for customers who have ordered freight >= 100

With our currently limited knowledge of single table queries we would have to:

1. retrieve customer IDs for orders with freight over 100 from the `orders`
   table
2. retrieve customer details from the `customers` table
3. combine the two queries

e.g.

```sql
-- get customer ids
SELECT customer_id
FROM orders
WHERE freight >= 100;

-- get regions
SELECT customer_id, company_name, region
FROM customers
WHERE customer_id in (1,2,3,...);
```

#### Combined with a subquery

```sql
SELECT customer_id, comppany_name, region
FROM customers
WHERE customer_id IN (
  SELECT customer_id
  FROM orders
  WHERE freight >= 100
);
```

### Working with subquery statements

With subqueries, SQL will be performing two operations. The subquery is always
performed first.

When troubleshooting, always evaluate the innermost query first, as that is what
SQL will be evaluating first.

## Subquery Best Practices and Considerations

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/3ubfD/subquery-best-practices-and-considerations)

- there is no limit to the depth subqueries one can use
- the more subqueries one uses, the more performance is impacted
- subquery `SELECT`s can only retrieve data for a single column at a time

### Subquery in a Subquery

1. get the order numbers for toothbrushes
2. get the customer ids for those orders
3. get the customer information for those orders

```sql
SELECT customer_name, customer_contact
FROM customers
WHERE customer_id IN (
  SELECT customer_id
  FROM orders
  WHERE order_number IN (
    SELECT order_number
    FROM order_items
    WHERE product_name = 'Toothbrush'
  )
)
```

[poorsql.com](http://poorsql.com) can be used to better format poorly formatted
SQL.

### Subqueries for calculations

Get the total number of orders for each customer:

```sql
SELECT
  customer_name
  ,customer_state
  (
    SELECT COUNT (*) AS total_orders
    FROM Orders
    WHERE Orders.customer_id = Customers.customer_id
  ) AS orders
FROM Customers
ORDER BY customer_nam