# DTA

* Relational Databases

## Relational Databases

Database: Database is a way of **storing information** in **an structured, logical way**.

A Relational Database has tables which are linked using key attributes.

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

### Foreign Keys

外键
An attribute in one table that uniquely identifies a row of annother table is a **foreign key**

一个表中的Foreign Key指向另一个表中的Primary Key

#### Referential Integrity

Each foreign key (advisor in the Student table)
needs to refer to an actual row in the table it
refers to (lecturer table), this is called referential integrity.

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

Common SQL:

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

### SELECT

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

### SQL Case Sensitivity

SQL commands are not case sensitive,**But data is.**

Convention(惯例)：
SQL commands (such as SELECT and FROM) are in
capitals.
Table names start with a capital letter (e.g.
Student)
Column names are in lower case (e.g. name)

### SELECT DISTINCT

```SQL
SELECT DISTINCT fname FROM People;
```

在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。
DISTINCT **关键词用于返回唯一不同的值**

### WHERE, IN, BETWEEN

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

### IS NULL, IS NOTNULL

NULL values represent **missing data**, it's different from an empty string or 0.

### AND, OR

```SQL
SELECT studentID FROM Student WHERE fname='Sally' AND address='12 Hope Street';

SELECT studentID FROM Student WHERE fname='Sally' OR fname='Lindsey';
```

### 结合 AND, OR

```SQL
SELECT * FROM Websites WHERE alexa>15 AND (country='CN' OR country='USA');
```

### ORDER BY

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

### Functions

SQL 拥有很多可用于计算和计数的内建函数

#### SQL Aggregate

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

### GROUP BY

Returns values for distinct groups, when used functions（GOURP BY语句需要结合一些聚合函数来使用，根据一个或多个列队结果来进行分组）

```SQL
SELECT school, COUNT(studentID) FROM Student GROUP BY school;
//注意这里的排列顺序是根据学校的字母顺序，而不是COUNT()的结果

```

### LIMIT

keywords LIMIT: only want a specific number of rows back.

```SQL
SELECT fname,sname FROM student WHERE sname < 'Black' LIMIT 10;
```

## More SQL

### Joins

连接（JOIN）
SQL JOIN 子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段。

最常见的 JOIN 类型：SQL INNER JOIN（简单的 JOIN）。 SQL INNER JOIN 从多个表中返回满足 JOIN 条件的所有行。

querying multiple tables 使用Join查询多个表格

#### 其他的 SQL JOIN

INNER JOIN: 如果表中有至少一个匹配，则返回行
LEFT JOIN: 即使右表中没有匹配，也从左表中返回所有的行
RIGHT JOIN: 即使左表中没有匹配，也从右表中返回所有的行
FULL JOIN: 只要其中一个表中存在匹配，则返回行

#### INNER JOIN ON

INNER JOIN 关键字在表中存在至少一个匹配时返回行。
Returns the rows where the join condition is met.

> INNER JOIN 可以简化为 JOIN

```SQL
SELECT Order.number, Customer.company FROM Order INNER JOIN Customer ON Order.companyID=Customer.ID;
```

#### LEFT JOIN

LEFT JOIN 关键字从左表（Websites）返回所有的行，即使右表（access_log）中没有匹配。

Returns all the rows of table1 (left table) with the corresponding rows of table2 if the condition is met, or null if not.
如果右表没有相对应的值，则返回NULL在结果表上。


```SQL
SELECT Website.name, access_log.count, access_log.date FROM Websites LEFT JOIN access_log ON Websites.id=access_log.site_id ORDER BY access_log.count DESC;
```

#### Aliases 别名

Aliases are used to temporarily rename a table or column.
创建别名是为了让命令的可读性更强

**特别注意**使用别名后，输出的结果表显示的attribute也是重新命名后的别名

```SQL
//rename a table
SELECT col FROM table1 AS temp_name;
```

```SQL
//rename a column
SELECT col  AS temp_name FROM table1;
```

```SQL
SELECT name AS n, country AS c FROM Websites;
```

```SQL
SELECT w.name, w.url, a.count, a.date FROM Websites AS w, access_log AS a WHERE a.site_id=w.id and w.name='tutorial';
```

在下面的情况下，使用别名很有用：

在查询中涉及超过一个表
在查询中使用了函数
列名称很长或者可读性差
需要把两个列或者多个列结合在一起

### RIGHT JOIN

Returns all the rows of table2 (to the right of the JOIN) with corresponding rows of table1 where the condition is met, null otherwise.

其实与 LEFT JOIN 类似，只是保留的是JOIN右侧的表格

```SQL
SELECT s.name, l.name FROM Student AS s RIGHT JOIN Lecture AS l ON s.advisor=l.staffID;
```

### FULL OUTER JOIN

Combines the results of left and right joins
Returns all the rows from the left (table1) and right (table2) tables.

FULL OUTER JOIN 关键字结合了 LEFT JOIN 和 RIGHT JOIN 的结果。
> 注意使用FULL OUTER JOIN 的结果表中，表中行的排列应该按照同一个顺序，而不是简单的把LEFT JOIN 和RIGHT JOIN的结果结合起来（根据attribute来对应）。

### SELF JOIN

You can join a table to itself: i.e. compare a column in the table to another column in the same table
Useful where a column is a foreign key corresponding to the table’s own primary key

```SQL
SELECT l.name, m.name FROM Lecture AS l SELF JOIN Lecture AS m ON l.manager = m.staffID;
```

### Sub-queries

```SQL
SELECT * FROM lecturer WHERE salary=(SELECT max(salary) FROM lecturer);
```

```SQL
SELECT staffNo, fname,lname FROM Staff WHERE dept=(SELECT deptNum FROM departments WHERE address='14 Addison Road');
```

> 使用= 和 （） 来内嵌另一个SQL语句

#### IN / NOT IN

IN allows you to use multiple values in a
WHERE clause

```SQL
SELECT fname, sname FROM Student WHERE programme IN(SELECT programmeid FROM programme WHERE name='Information Technology' OR name='Bioinformatics');
```

similar to NOT IN

### Views

A view is a virtual table based on the result-set of a SQL statement.

They don't contain any data themselves.

#### Views Syntax

```SQL
CREATE VIEW CSstaffView AS SELECT * FROM Lecturer WHERE school='Computing Science';
```

#### Using Views

Once a view has been created, it can be queried like a table.

```SQL
SELECT * FROM CSstaffView;
```

## Entity Relationship Diagrams

ER Diagrams(实体关系图): A graphical representation of an entity relationship model.

### Entity Type

An entity type is a real world object we want to store information about, e.g. a Student, Course, Staff

All entity types have some properties that give
them their identity e.g.
– Staff -name, address, staff number, national
insurance number
– Course- the title, the director, the set of modules,
– Module - the lecturer, the meeting room, the
times of the lecture

### Relationships

Identify the relationships from the Company Example:
Department controls Project
Employee works for Department
Employee manages Department
Employee works on Project
Employee supervises Employee
Employee has Dependents

### Attributes（属性，特性）

Characteristics of the entities which can be used
to describe the entity
– E.g. student has a name, student ID, DOB etc.

#### Different types of attribute

simple(automic): such as age, sex 由单个不可分割的值组成
composite: address, DOB 由多个成分的值组成

OR

single-valued(contains one value): age, title
multi-valued(contain more than one value): locations

不同类型的attribute 有不同的图例表示

 ![drawing attributes](http://kkimages.oss-cn-shanghai.aliyuncs.com/18-4-20/13569100.jpg)

### Basics Summary

Entity – a real world object we wish to model

Attribute – a characteristic which describes an entity

Relationship – links two or more entities

### Weak Entity Types