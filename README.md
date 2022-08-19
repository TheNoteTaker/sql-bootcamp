# <u>MySQL Master Bootcamp</u>

## General Notes

- Wildcards in __SQL__:
  - `%` (Any character)
  - `_` (Any character, but only results where there are the same amount of
    characters as there are underscores)
  - Escape the character if you need to use either
- To comment in __SQL__, use `--`, `/* */`, or `#`

# Section 2: Overview

## General Notes

- Some of the most common __DBMS's__ _(Database Management Systems)_:
    - PostgreSQL
    - MySQL
    - Oracle Database
    - SQLite
- _Types_ cannot be mixed and are specified upon creation. (Statically Typed)

## What is a Database?

1. A collection of data
    - I.e. a phone book
2. A method of accessing and manipulating that data
3. A structured set of computerized data with an accessible interface

## Database vs Database Management System

- __DMS__ or __Relational Database Management System__ refers to an interface
  for the data.
    - The database is the data itself and all of it. The __DBMS__ is the UI for it.
    - They're often referred to as the same thing

## MySQL vs SQL

### __SQL _(Structured Query Language)___

- The language we use to "talk" to our databases
- SQL is used to write inside of DBMS's such as MySQL
- There is a standard for how SQL should work, and all DBMS's are tasked with
  implementing that standard and making them work.

#### Two Takeaways

- It's very easy to switch after learning SQL
- What makes databases (DBMS) unique are the features they offer, not the language.

## Using __Goorm__ and __SQL__

- `mysql-ctrl {command}`
    - `start` (will start mysql)
    - `stop` (will stop mysql)
    - `cli` (Will stop and then start mysql)
        - Stands for ___Command Line Interface___
- `use {database_name}` (Changes the database being used)
- `source {database_filename}` (Run code from a query file)
- `desc {table}` (Shows the contents of a table)
    - Shorthand for `SHOW COLUMNS FROM {tablename}`
- `create {database_name}` (Creates a database)
- `drop {database_name}` (permanently destroys a database)
- `SELECT database()` (Tells you the current database being used)
- `show {tables | databases}` (Shows all tables or databases)

## What is a Table?

A table is a collection of related data held in a structured format within a
database.

- __Columns__ (Headers)

## Different __Types__ in SQL

|  Numeric  |   String   |   Date    |
|:---------:|:----------:|:---------:|
|    INT    |    CHAR    |   DATE    |
| SMALLINT  |  VARCHAR   | DATETIME  |
|  TINYINT  |   BINARY   | TIMESTAMP |
| MEDIUMINT | VARBINARY  |   TIME    |
|  BIGINT   |    BLOB    |   YEAR    |
|  DECIMAL  |  TINYBLOB  |           |
|  NUMERIC  | MEDIUMBLOB |           |
|   FLOAT   |  LONGBLOB  |           |
|  DOUBLE   |    TEXT    |           |
|    BIT    |  TINYTEXT  |           |
|           | MEDIUMTEXT |           |
|           |  LONGTEXT  |           |
|           |    ENUM    |           |

### SQL Types

- __INT__ (whole number)
- __varchar__ (variable-length string between 1-255 characters)

## Creating Tables

- Table names should be pluralized. It's because a table describes multiple of
  the thing, not just one.

```SQL
CREATE TABLE tablename
(
    column_name data_type,
    column_name data_type,
);

/* Example: */
CREATE TABLE cats
(
    name VARCHAR(100),
    age  INT
);
```

# Section 4: Inserting Data (And More)

## General Notes

- `SHOW WARNINGS` (Shows all warnings)
- `size` is a reserved word. Don't use it for a column name.

### Syntax

Incorrect syntax:

```sql
INSERT INTO <tablename>(column, column)
VALUES (value, value);
```

The preferred way of writing:

```sql
INSERT INTO <tablename>
            (column,
            column)
VALUES      (value,
            value);
```

- The order which the columns are used matters, as the order for the values being
  inserted must be in the same order.

## Multiple Inserts

```sql
INSERT INTO <tablename>
            (column type, column type)
VALUES      (value, value),
            (value, value),
            (value, value);
```

## NULL and NOT NULL

- When a value is not given for a column, `NULL` is put in its place.
- To require a value for a field:
```sql
CREATE TABLE <tablename>(column type NOT NULL);
```
  - The `NOT NULL` part throws a `warning` if the value is empty when being inserted.

## Setting Default Values
```sql
CREATE TABLE <tablename>
    (
        column type DEFAULT <default_value>
)
```

- It's important to specify `NOT NULL` as a value can still manually be set to 
  `NULL`.

## Primary Keys

- If you have multiple entries, you need to be able to tell them apart. That's
  when you use a __Primary Key__ ___(A unique identifier)___.

```sql
CREATE TABLE unique_cats (cat_id INT AUTO_INCREMENT NOT NULL
                         ,name VARCHAR(100)
                         ,age INT
                         ,PRIMARY KEY(cat_id)  /* Give the name of the field */
                          );

/* The second way to write it is to put PRIMARY KEY at the end */

CREATE TABLE unique_cats (cat_id INT AUTO_INCREMENT NOT NULL PRIMARY KEY
                         ,name VARCHAR(100)
                         ,age INT
                          );
```

- `AUTO_INCREMENT` will automatically increase the value for each entry.
  - It will appear under `EXTRA` when `DESC` is used.

## CRUD

- __C__ reate
  - ```sql
    INSERT INTO
    ```
- __R__ ead
  - ```sql
    SELECT
    ```
    - Can use `*` or the name of a `column` or multiple `columns`
    - ```sql
      SELECT column, column from <table>;
      ```
- __U__ pdate
  - ```sql
    UPDATE <table> SET <column>=<value> WHERE <column>=<value>
    ```
- __D__ elete
- ```sql
    DELETE FROM <table> WHERE column=<value>;
    ```

Common in many areas of web development, not just databases.

### WHERE clause

Used to find specific information, not just check in on the table

  - I.e. Finding someone by their username and checking that their password matches
- Used almost everywhere
- **Case-insensitive**

```sql
SELECT * FROM <table> WHERE <column>=<value>;

/* Example */

SELECT * FROM cats WHERE age=4;
```

### Aliases

Specify how our data should be displayed back to us. Changes the name of the 
column temporarily to what's specified when it's displayed in a table.

```sql
SELECT column AS <temporary name>, column FROM <table>

/* Example */
SELECT cat_id AS id, name FROM cats;
```

- In this example `cat_id` has been changed to `id`. It's useful for when there
  are two databases with the same column. This way, you can tell them apart.

### Update

Good rule of thumb before updating is to run the equivalent `SELECT` to make sure
you're updating the correct data.

```sql
UPDATE table SET column=<value>
WHERE column=<value>;

/* Example */
UPDATE cats SET breed='Shorthair'
WHERE breed='Tabby';
```

### Delete

Same syntax as `SELECT`, except without a `column` after `DELETE`.

```sql
    DELETE FROM <table> WHERE column=<value>;
```

- The IDs will not shift when an item is deleted, as they're generated at
  creation.
  - This can be problematic if they were changed, as the IDs are often stored 
    in multiple tables.

# Section 7: String Functions

## General Notes

## Concat

`CONCAT` Combine data for cleaner output

```sql
SELECT CONCAT(column, column, 'text', ...) FROM <table>;
    
/* Example s*/
    
SELECT CONCAT(author_fname, ' ', author_lname) AS 'Full Name' FROM books;


SELECT author_fname AS first, author_lname AS last, 
CONCAT(author_fname, ' ', author_lname) AS 'Full Name' 
FROM books;
```

When dealing with multiple values that will all need a separator, using `CONCAT_WS` 
will save time:
```sql
SELECT CONCAT_WS(<separator>, column, column, ...) FROM <table>
```

## Substring

Work with parts of a string. `SUBSTR()` is the shorthand.

```sql
SELECT SUBSTRING(column, start, end) FROM <table>;

SELECT SUBSTRING('Hello World', 1, 4);
SELECT SUBSTR('Hello World', 1, 4);
```

- Unlike other programming languages like Python, the index does not start at 0.
- Only giving one number will produce all letters from there to the end.
  - i.e. `SELECT SUBSTRING('Hello World', 7)` will give `World`
  - Negative numbers are also applicable

### Combination Query Example

```sql
SELECT CONCAT
    (
        SUBSTRING(column, start, end),
        column/text,
        column/text
     ) AS 'My Concat'
FROM <table>;
```

## Replace

Replace parts of a string

```sql
SELECT REPLACE(text, text_to_replace, replacement_text)
FROM <table>;
```

- Replaces __all__ occurrences of `text_to_replace` with `replacement_text` in 
  the string
- It __is__ case-sensitive

## Reverse

Reverses a string

```sql
SELECT REVERSE(column) FROM <table>;
```

## Char_Length

Counts characters in a string. The long-form is `CHARACTER_LENGTH`.

```sql
SELECT CHAR_LENGTH(column) FROM <table>;
```

## UPPER and LOWER

Converts the string to either upper or lower-case.

```sql
SELECT UPPER(column) FROM <table>;

SELECT LOWER(column) FROM table;
```

# Section 8: Refining Our Selections

## Distinct

Used in conjunction with `SELECT`. If there's duplicates, it will only give the
unique ones.

- Comes right after `SELECT`

```sql
SELECT DISTINCT column FROM <table>;

-- Example

SELECT DISTINCT author_lname FROM books;
```

- To get a `DISTINCT` of multiple columns, you can either:
  - Use `CONCAT`
  - Use multiple columns:
    - ```sql
      SELECT DISTINCT column, column FROM <table>
      ```
      - Will only select unique columns where both values are unique. Applies 
        it to the entire row.

## ORDER BY

Sorting our results

```sql
SELECT column FROM <table> ORDER BY column;

-- Example

SELECT DISTINCT author_lname, author_fname 
FROM books 
ORDER BY author_lname;
```

- Ascending by default. Can be changed by assing `DESC` after the columns to sort
  by:
  - ```sql
    SELECT DISTINCT author_lname, author_fname 
    FROM books 
    ORDER BY author_lname DESC;
    ```
- Each selected column is given an index number starting from 1 that can be used
  as a shortcut, rather than typing the column:
  - ```sql
    SELECT DISTINCT author_lname, author_fname 
    FROM books 
    ORDER BY 2;
    -- This is ordering by author_fname
    ```
- It's possible to `ORDER BY` multiple columns. They will be ordered from left to
  right, prioritizing the column before it.
  - ```sql
    SELECT DISTINCT title, author_lname, author_fname 
    FROM books 
    ORDER BY title, author_lname;
    ```
    
## Limit

Specify a number for how many results to select.

- Used in conjunction with `ORDER BY`

```sql
SELECT column FROM <table> LIMIT <int>;

-- Examples

SELECT * FROM books LIMIT 3;

SELECT title, released_year FROM books
ORDER BY released_year DESC LIMIT 5;
```

- A range `<int>, <int>` can be given instead of a single number. The first number
  is the offset, and the second number is how many rows to fetch starting
  there _(including that row)_
  - An example of when to use this is a blog site for pagination.
  - To retrieve all rows from a certain offset, a number larger than the amount
    of rows can be given _(i.e. 99999999999999)_

## Like

Better searching. Allows the use of wildcards and partial matches using patterns.

```sql
SELECT * FROM <table> WHERE column LIKE '%<value>%';

-- Examples

-- Find all rows where author_fname contains 'da'
SELECT title, author_fname FROM books WHERE author_fname LIKE '%da%';

-- Find all rows where author_fname starts with 'da'
SELECT title, author_fname FROM books WHERE author_fname LIKE 'da%';

-- Find all rows where author_fname ends with 'da'
SELECT title, author_fname FROM books WHERE author_fname LIKE 'da%';

SELECT "(235)234-0987" LIKE '(___)___-____' ;
```

- This is __not__ case-sensitive