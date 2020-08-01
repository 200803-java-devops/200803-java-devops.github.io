# Week 2 - SQL
# SQL
## Concepts
- RDBMS
- Sublanguages: DDL, DML, DQL
- Set Operators: Union, Intersect, Except
- Subqueries
- Normalization: 1st vs 2nd vs 3rd Normal Forms
- Multiplicity: Foreign keys
- Joins: Inner, Outer, Cross
- Functions: Aggregate vs Scalar

## Syntax
- [DDL](https://www.postgresql.org/docs/12/ddl.html): 
  - [CREATE TABLE](https://www.postgresql.org/docs/12/sql-createtable.html)
  - [ALTER TABLE](https://www.postgresql.org/docs/12/sql-altertable.html)
  - [DROP TABLE](https://www.postgresql.org/docs/12/sql-droptable.html)
- [DML](https://www.postgresql.org/docs/12/dml.html): 
  - [INSERT](https://www.postgresql.org/docs/12/sql-insert.html)
  - [UPDATE](https://www.postgresql.org/docs/12/sql-update.html)
  - [DELETE](https://www.postgresql.org/docs/12/sql-delete.html)
- [DQL](https://www.postgresql.org/docs/12/queries.html):
  - [SELECT](https://www.postgresql.org/docs/12/sql-select.html)
  - Combining Queries: [UNION/INTERSECT/EXCEPT](https://www.postgresql.org/docs/12/queries-union.html)
  - [Scalar Subqueries](https://www.postgresql.org/docs/12/sql-expressions.html#SQL-SYNTAX-SCALAR-SUBQUERIES)
  - [Subquery Expressions](https://www.postgresql.org/docs/12/functions-subquery.html)
  - [Joined Tables](https://www.postgresql.org/docs/12/queries-table-expressions.html#QUERIES-JOIN)
- [Functions](https://www.postgresql.org/docs/12/functions.html):
  - [Aggregate Functions](https://www.postgresql.org/docs/12/functions-aggregate.html)
  - Scalar Functions:
    - [Date/Time](https://www.postgresql.org/docs/12/functions-datetime.html)
    - [Math](https://www.postgresql.org/docs/12/functions-math.html)
    - [Strings](https://www.postgresql.org/docs/12/functions-string.html)

# JDBC
## Concepts
- [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)

## Standard Library
- [java.sql](https://docs.oracle.com/javase/8/docs/api/java/sql/package-summary.html)
  - [DriverManager](https://docs.oracle.com/javase/8/docs/api/java/sql/DriverManager.html)
  - [Connection](https://docs.oracle.com/javase/8/docs/api/java/sql/Connection.html)
  - [Statement](https://docs.oracle.com/javase/8/docs/api/java/sql/Statement.html)
    - [PreparedStatement](https://docs.oracle.com/javase/8/docs/api/java/sql/PreparedStatement.html)
    - [CallableStatement](https://docs.oracle.com/javase/8/docs/api/java/sql/CallableStatement.html)
  - [ResultSet](https://docs.oracle.com/javase/8/docs/api/java/sql/ResultSet.html)
  - [SQLException](https://docs.oracle.com/javase/8/docs/api/java/sql/SQLException.html)

# Linux
## Concepts
- Unix
- Red Hat Enterprise Linux (RHEL)
- Open Source Software
- Unix philosophy: pipelines
- Linux file system: Root[/] vs Home[~]
- User management: groups, permissions
- Linux Kernel: [scheduler](https://www.kernel.org/doc/html/latest/scheduler/index.html)
- Hardware: CPU, RAM, Storage
- Problems: fragmentation, access time, deadlock, starvation, capacity

## Tools
- GNU Core Utilities: `mkdir`, `rm`, `cp`, `mv`, `cd`, `ls`, `cat`, `echo`, `chmod`, `df`
- Package management: `rpm`, `yum`
- `Bash`: Environment variables, shell scripting
- Editors: `vim`, `nano`
- `ssh`: private/public key
- procps-ng proc filesystem utilities: `free`, `watch`, `vmstat`
- util-linux utilities: `fallocate`, `mkswap`, `swapon`, `fdisk`, `sfdisk`, `lsblk`, `blkid`
- Managing RAID: `mdadm`

# Questions
## SQL
- What is SQL?
- What are its sublanguages?
- What is multiplicity?
- What is cardinality?
- What is a candidate key?
- What is referential integrity?
- What are the different constraints of a column?
- what are the differences between GROUP BY and ORDER BY?
- What is the difference between IN and EXISTS?
- What are subqueries?
- What is the differenece between an aggregate function and a scalar function?
- What are the different joins in SQL?
- What are the different set operations in SQL?
- What is the difference between joins and set operations?
- What is normalization?
- What are the requirements for the first three normal forms?

## JDBC
- What is JDBC?
- What dependencies are required to connect to an RDBMS?
- What are the main interfaces of JDBC?
- In what order are they used?
- What are the different types of statements?
- What is SQL Injection?
- What is a DAO?
- Describe client-server communication: how does it apply to PostgreSQL?
- What does a connection URL for PostgreSQL look like?
- How do you connect to a PostgreSQL server with a client? With Java?
- Why is connection pooling important?

## Linux
- What is Unix?
- What is Linux?
- What are Linux pipelines?
- What distribution of Linux are you familiar with? Which distributions are in the same family?
- What is a shell? Which shell are you familiar with?
- What is shell scripting?
- What is a package manager? Which one is used on RHEL?
- What is grep? man?
- Explain basic Unix commands for file creation and directory navigation.
- Where is the home directory located? Where is root?
- How is the Linux filesystem structured and organized? What are some important directories?
- What is vim? Nano?
- How do I change file permissions?
- How do I create local and global environment variables?
- What utilities can help you monitor a system's processes? It's filesystem?
- What is ssh? How can you use it to connect to a Linux system?
- What is a private and public key?
