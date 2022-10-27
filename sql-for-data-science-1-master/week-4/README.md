# Week 4 - Modifying and Analyzing Data with SQL

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Module Introduction](#module-introduction)
  - [Methods for modifying data](#methods-for-modifying-data)
  - [Case statements](#case-statements)
- [Working with Text Strings](#working-with-text-strings)
  - [Working with string variables](#working-with-string-variables)
  - [Concatenations](#concatenations)
  - [Trimming strings](#trimming-strings)
  - [Substring](#substring)
  - [Upper and Lower](#upper-and-lower)
- [Working with Date and Time Strings](#working-with-date-and-time-strings)
  - [Date formats](#date-formats)
  - [SQLite date time functions](#sqlite-date-time-functions)
  - [Timestrings](#timestrings)
  - [Modifiers](#modifiers)
- [Date and Time Strings Examples](#date-and-time-strings-examples)
  - [`STRFTIME`](#strftime)
  - [Compute current date](#compute-current-date)
  - [Compute dates and times for the current date](#compute-dates-and-times-for-the-current-date)
- [Case Statements](#case-statements)
  - [Search case statement](#search-case-statement)
- [Views](#views)
  - [Creating a view](#creating-a-view)
- [Data Governance and Profiling](#data-governance-and-profiling)
  - [What is data profiling?](#what-is-data-profiling)
    - [Object data profile](#object-data-profile)
    - [Column data profile](#column-data-profile)
  - [Governance best practises](#governance-best-practises)
- [Using SQL for Data Science, Part 1](#using-sql-for-data-science-part-1)
  - [Working through a problem](#working-through-a-problem)
  - [Data understanding](#data-understanding)
    - [Subject understanding](#subject-understanding)
  - [Business understanding](#business-understanding)
- [Using SQL for Data Science, Part 2](#using-sql-for-data-science-part-2)
  - [Profiling data](#profiling-data)
    - [Start with `SELECT`](#start-with-select)
    - [Test and troubleshoot](#test-and-troubleshoot)
    - [Format and comment](#format-and-comment)
    - [Review](#review)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Module Introduction

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/V9qBD/module-introduction)

### Methods for modifying data

- concatenating
- trimming
- changing case
- substring
- date and time strings

### Case statements

SQL's version of `IF`, `THEN`, and `ELSE` statements

## Working with Text Strings

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/yw49P/working-with-text-strings)

### Working with string variables

Manipulating strings on the server reduces work that needs to be done by the
client.

String functions:

- concatenate
- substring
- trim
- upper
- lower

### Concatenations

In SQLite one uses `||` to concatenate strings. SQL Server allows for `+` to
concatenate strings.

```sql
SELECT
  company_name
  ,contact_name
  ,compaany_name || ' (' || contact_name || ')'
FROM Customers
```

### Trimming strings

- `TRIM`
- `RTRIM`
- `LTRIM`

```sql
SELECT TRIM("   You the best ") AS trimmed_string;
```

### Substring

The `SUBSTR` command is 1-indexed. It accepts the string on which to operate,
the starting index, and the number of characters to return from that index.

```sql
-- SUBSTR([string name], [start pos], [num return chars])

SELECT first_name, SUBSTR(first_name, 2, 3)
FROM Employees
WHERE department_id = 69;
```

### Upper and Lower

```sql
-- make string uppercase
SELECT UPPER(first_name) FROM Customers
-- or
SELECT UCASE(first_name) FROM Customers

-- make string lowercase
SELECT LOWER(first_name) FROM Customers
```

## Working with Date and Time Strings

[video](https://www.coursera.org/learn/sql-for-data-science/lecture/kbIot/working-with-date-and-time-strings)

Dates are stored as `date` or `datetime` datatypes. The format of the date is
dependent on the RDMS you are working with.

If only the date portion of an entry is being queried, queries are generally
quite easy. As soon as the time portion is included in the query complexity
increases.

When inserting a date into a table, care must be taken to ensure that it is done
so in the correct format.

### Date formats

`DATE`: `YYYY-MM-DD`

`DATETIME`: `YYYY-MM-DD HH:MM:SS`

`TIMESTAMP`: `YYYY-MM-DD HH:MM:SS`

```sql
-- querying a DATETIME field with:
WHERE purchase_date = '2016-12-12'
-- will return no results because it's missing the _time_ portion of the data
```

### SQLite date time functions

SQLite supports 5 date and time functions:

```sql
DATE(timestring, [modifier, ...])
TIME(timestring, [modifier, ...])
DATETIME(timestring, [modifier, ...])
JULIANDAY(timestring, [modifier, ...])
STRFTIME(format, timestring, [modifier, ...])
```

### Timestrings

A time string can be in one of the following formats:

```
YYYY-MM-DD
YYYY-MM-DD HH:MM
YYYY-MM-DD HH:MM:SS
YYYY-MM-DD HH:MM:SS.SSS
# T here is a literal T delimiting the date from the time
YYYY-MM-DDTHH:MM
YYYY-MM-DDTHH:MM:SS
YYYY-MM-DDTHH:MM:SS.SSS
HH:MM
HH:MM:SS
HH:MM:SS.SSS
```

### Modifiers

Modifiers alter the date, and multiple modifiers can be applied to a date.
Modifiers are applied in the order they are provided, from left to right.

The following modifiers add a specified amount to the date:

```sql
NNN days
NNN hours
NNN minutes
NNN.NNN seconds
NNN months
NNN years
```

The following modifiers return a date "shifted back" from the provided date:

```sql
start of month
start of year
start of day
```

`weekday N` shifts the date forward to the 0-indexed day in the future, unless
the provided date is that index. Sunday is 0.

`localtime` modifies UTC dates by shifting the time to the localtime of where
the process is running. `utc` is the inverse of `localtime`.

`now` will r