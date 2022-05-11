# Week 2 - Filtering, Sorting, and Calculating Data with SQL

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Module Introduction](#module-introduction)
- [Basics of Filtering with SQL](#basics-of-filtering-with-sql)
  - [Why filter](#why-filter)
  - [`WHERE` clause](#where-clause)
- [Advanced Filtering: `IN`, `OR`, and `NOT`](#advanced-filtering-in-or-and-not)
  - [`IN` operator](#in-operator)
  - [`OR` operator](#or-operator)
  - [`IN` vs `OR`](#in-vs-or)
  - [`NOT` operator](#not-operator)
- [Using Wildcards in SQL](#using-wildcards-in-sql)
  - [Using wildcards](#using-wildcards)
  - [Underscore wildcard](#underscore-wildcard)
  - [Implications of using wildcards](#implications-of-using-wildcards)
- [Sorting with `ORDER BY`](#sorting-with-order-by)
  - [Sort direction](#sort-direction)
  - [Sorting by columns position](#sorting-by-columns-position)
- [Math operations](#math-operations)
- [Aggregate Functions](#aggregate-functions)
  - [`AVG` function](#avg-function)
  - [`COUNT` function](#count-function)
  - [`MAX` and `MIN` functions](#max-and-min-functions)
  - [`SUM` function](#sum-function)
  - [`DISTINCT`](#distinct)
- [Grouping Data with SQL](#grouping-data-with-sql)
  - [Using `GROUP BY`](#using-group-by)
  - [`WHERE`, `HAVING`, and `GROUP BY`](#where-having-and-group-by)
  - [`GROUP BY` and `ORDER BY`](#group-by-and-order-by)
- [Putting it all together](#putting-it-all-together)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Module Introduction

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/GAA9h/module-introduction)

This module introduces a number of operators and clauses to query data:

- `WHERE`
- `BETWEEN`
- `IN`
- `OR`
- `NOT`
- `LIKE`
- `ORDER BY`
- `GROUP BY`

It also introduces wildcards, and math operators which can be used to aggregate
data:

- `AV