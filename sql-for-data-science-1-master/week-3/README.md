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
- [Aliases a