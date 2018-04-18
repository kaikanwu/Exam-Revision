# DTA

* Relational Databases

## Relational Databases

Database: Database is a way of **storing information** in **an structured, logical way**.

Database Model:
such as Relational Model

* Database consist of tables, which are linked
* Each table has a name

### Attributes and Attributes Type

|Attributes  |Attributes Type  |
|---------|---------|
|Student Number     |     Number    |
|Name     |    Text     |
|Address     |      Text   |
|DOB     |    Data     |

### Table

* each row should be unique(no duplicate rows)

### Primary key

A primary key is **an attribute** in the table which can **be used to uniquely identify each row.**

* only one primary key in a table, and each talbe must have a primary key.
* cannot have a null entry for the primary key

Candidate Keys:
Each table will normaly have several potential primary keys called candidate keys.

### Database Schema

**A description of the columns** in a table can be called the table schema.

Such as:
Table(col,col,col,…) Table(col,col,..)
– E.g. **Student (studentNumber, name, address, DOB)**

> Talbes can be empty(no rows of data), but must have a schema.

## SQL

Relational databases use SQL **(Structured query language) 结构化查询语言** to get information

SQL
A standard language for accessing and manipulating information in relational databases.

The language consists of SQL commands.

SQL is an ANSI (American National Standards
Institute) Standard, but there are slightly
different versions (flavours).

###Common SQL:

* Oracle
* MySQL
* SQLite
* **PostgreSQL**
* MSQL(Micosoft)
* Microsoft Access

Most implementations do not implement the
entire standard.

But they all implement the basics。

### SQL Queries

SQL Commands with **a specific format** which
**potentially return rows of a database.**

Start with SELECT command
e.g.

```SQL
SELECT name FROM student;
```

#### Basic form

```SQL
SELECT column_name FROM table_name WHERE condition_is_true;
```

> SELECT * will return the complete rows

SELECT – Get the data you want, normally column names, sometimes a function of a column.

FROM – Find the table first.

WHERE – Find the rows which satisfy
the condition.

#### SQL Case Sensitivity

SQL commands are not case sensitive,**But data is.**

Convention(惯例)：

SQL commands (such as SELECT and FROM) are in
capitals.
Table names start with a capital letter (e.g.
Student)
Column names are in lower case (e.g. name)

#### SELECT DISTINCT

```SQL
SELECT DISTINCT fname FROM People;
```

在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。
DISTINCT **关键词用于返回唯一不同的值**

#### WHERE, IN, BETWEEN

```SQL
SELECT fname FROM People WHERE studentID IN(1,3,7);
```

```SQL
SELECT fname FROM People WHERE studentID BETWEEN 1 AND 30;
```