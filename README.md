# <u>MySQL Master Bootcamp</u>

## General Notes:

# Section 2: Overview

## General Notes

- Some of the most common __DBMS's__ _(Database Management Systems)_:
  - PostgreSQL
  - MySQL
  - Oracle Database
  - SQLite

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
    - Stands for _Command Line Interface_
- `use {database_name}` (Changes the database being used)
- `source {database_filename}` (Run code from a query file)
- `desc {table}`
- `create {database_name}` (Creates a database)
- `drop {database_name}` (permanently destroys a database)
- `SELECT database()` (Tells you the current database being used)


