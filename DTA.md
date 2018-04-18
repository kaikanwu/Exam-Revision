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

> 注意结尾的分号 **;** （有些数据库系统要求SQL语句末端使用分号，来分隔每条SQL，我们这里默认使用）

#### SELECT

SELECT 语句用于从数据库中选取数据。
**结果被存储在一个结果表中，称为结果集**。

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
SELECT * FROM Websites WHERE country='CN';
SELECT * FROM Websites WHERE id=1;
```

注意**文本信息**这里使用的是**单引号**
数值则不需要加单引号

```SQL
SELECT fname FROM People WHERE studentID IN(1,3,7);
```

```SQL
SELECT fname FROM People WHERE studentID BETWEEN 1 AND 30;
```

> The range is inclusive, so in this example, 1 and 30 are in the range.
**we can also use NOT IN and NOT BETWEEN**

#### IS NULL, IS NOTNULL

NULL values represent **missing data**, it's different from an empty string or 0.

#### AND, OR

```SQL
SELECT studentID FROM Student WHERE fname='Sally' AND address='12 Hope Street';

SELECT studentID FROM Student WHERE fname='Sally' OR fname='Lindsey';
```

#### 结合 AND, OR

```SQL
SELECT * FROM Websites WHERE alexa>15 AND (country='CN' OR country='USA');
```

#### ORDER BY

ORDER BY 默认按照**升序**对记录进行排序 **ASC**
**降序**： 使用 **DESC**关键字

```SQL
//默认升序： 从小到大
SELECT * FROM Websites ORDER BY alexa;
```

```SQL
//使用DESC关键字降序： 从大到小
SELECT * FROM Websites ORDER BY alexa DESC;
```

ORDER BY 多列
可以使用多个条件

```SQL
SELECT * FROM Websites ORDER BY country, alexa;
```

> 注意这里的输出结果，如果是条件是英文的时候，会按照ABC->XYZ的顺序排列。

#### Functions

SQL 拥有很多可用于计算和计数的内建函数

##### SQL Aggregate

Aggregate functions **return a single value.**

AVG()
MAX()
MIN()
SUM()
COUNT()

```SQL
SELECT AVG(salary) FROM Lecturer;
```

COUNT( ) Examples:

```SQL
SELECT COUNT(*) FROM Employee;
 //Returns the number of rows in the table

SELCT COUNT(salary) FROM Employee;
// returns the number of rows in which salary is not null

SELECT COUNT(DISTINCT salary) FROM Employee;
//returns the number of rows of different salaries in the table

SELECT COUNT(staffID) FROM Lecturer WHERE school='Philosophy';
```

#### GROUP BY

Returns values for distinct groups, when used functions（GOURP BY语句需要结合一些聚合函数来使用，根据一个或多个列队结果来进行分组）

```SQL
SELECT school, COUNT(studentID) FROM Student GROUP BY school;
//注意这里的排列顺序是根据学校的字母顺序，而不是COUNT()的结果

```

#### LIMIT

keywords LIMIT: only want a specific number of rows back.

```SQL
SELECT fname,sname FROM student WHERE sname < 'Black' LIMIT 10;
```

