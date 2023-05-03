# Creating Databases and Tables



## Classification of SQL Commands

All of the SQL commands can be broken into several groups.

*DDL - Data Definition Language* - These are the SQL commands that are responsible for creating, deleting, and updating database schema, tables and relations.

*DML - Data Manipulation Language* - These are the SQL commands that are responsible for inserting, updating, and deleting data

*DQL - Data Query language* - These are the SQL commands that are responsible for selecting data.

*DCL - Data Control Language -* These are the SQL commands that are responsible for creating user groups, creating users, granting and revoking privileges, and deleting users.



## Database Creation and Deletion

### Helpful SQL commands

```sql
-- at the command prompt type 'mysql' to start

--  Record all command activities to a file
TEE c:\myfolder\myfilename.sql;

-- Stop recording all activities to a file
NOTEE;

-- Load a sql file into the databae
SOURCE C:\myfolder\myfilename.sql;

-- Exit mysql command prompt
EXIT

```



### SQL comments

```sql
/*
This is a multi
line comment.
*/

-- Single line comment (two dashes and a space)
```

### Case Sensitivity

> Whether objects are case-sensitive or not is partly determined by the underlying operating system. Unix-based systems are case-sensitive, Windows is not, while Mac OS X is usually case-insensitive by default, but devices can be configured as case-sensitive using Disk Utility.
>
> https://mariadb.com/kb/en/identifier-case-sensitivity/#:~:text=Database%2C%20table%2C%20table%20aliases%20and,group%20name%20are%20case%20sensitive.



### Database Commands

```sql
-- Creating a database
CREATE DATABASE  db_myDatabaseName;

CREATE DATABASE IF NOT EXISTS db_myDatabaseName;

CREATE OR REPLACE DATABASE db_myDatabaseName;

-- Show Databases
SHOW DATABASES;

-- Delete Database
DROP DATABASE db_myDatabaseName;

DROP DATABASE IF EXISTS db_myDatabaseName;

-- Select / Use a specific database
USE db_myDatabaseName

-- Show Schema
-- Schema is characteristics of a database
SELECT * FROM INFORMATION_SCHEMA.SCHEMATA\G

SELECT TABLE_NAME, COLUMN_NAME, DATA_TYPE, CHARACTER_MAXIMUM_LENGTH  
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE TABLE_SCHEMA='databaseName' 
    AND TABLE_NAME='tableName';
    
-- https://mariadb.com/kb/en/information-schema-columns-table/

```

## Create and Delete Tables

```sql
-- Create table
CREATE TABLE  tb_Person
(
  FirstName VARCHAR(40),
  LastName  VARCHAR(40) NOT NULL,
  Street    VARCHAR(40),
  City      VARCHAR(40),
  State     CHAR(2) ,
  Zip       INT(5),
  Person_ID INT(5) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (Person_ID)
);

CREATE TABLE IF NOT EXISTS  tb_Person2
(
  FirstName VARCHAR(40),
  LastName  VARCHAR(40) NOT NULL,
  Street    VARCHAR(40),
  City      VARCHAR(40) DEFAULT 'Kalispell',
  State     CHAR(2) DEFAULT 'MT',
  Zip       INT(5) DEFAULT '59901',
  Person_ID INT(5) NOT NULL  AUTO_INCREMENT PRIMARY KEY
);

-- Sometimes we need to recreate a table
CREATE OR REPLACE TABLE  tb_Person
(
  FirstName VARCHAR(40),
  LastName  VARCHAR(40) NOT NULL,
  Street    VARCHAR(40),
  City      VARCHAR(40),
  State     CHAR(2) ,
  Zip       INT(5),
  Person_ID INT(5) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (Person_ID)
);

-- Alternative
DROP TABLE IF EXISTS tb_Person;
CREATE TABLE  tb_Person
(
  FirstName VARCHAR(40),
  LastName  VARCHAR(40) NOT NULL,
  Street    VARCHAR(40),
  City      VARCHAR(40),
  State     CHAR(2) ,
  Zip       INT(5),
  Person_ID INT(5) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (Person_ID)
)ENGINE = InnoDB;


-- Delete Table
DROP TABLE tbl_mytableName;

```

### Describe Table

```sql
DESCRIBE tableName;

-- output
/*
DESCRIBE tb_person2;
MariaDB [z_test]> describe tb_person2;
+-----------+-------------+------+-----+-----------+----------------+
| Field     | Type        | Null | Key | Default   | Extra          |
+-----------+-------------+------+-----+-----------+----------------+
| FirstName | varchar(40) | YES  |     | NULL      |                |
| LastName  | varchar(40) | NO   |     | NULL      |                |
| Street    | varchar(40) | YES  |     | NULL      |                |
| City      | varchar(40) | YES  |     | Kalispell |                |
| State     | char(2)     | YES  |     | MT        |                |
| Zip       | int(5)      | YES  |     | 59901     |                |
| Salary    | double(9,2) | YES  |     | NULL      |                |
| Person_ID | int(5)      | NO   | PRI | NULL      | auto_increment |
+-----------+-------------+------+-----+-----------+----------------+
8 rows in set (0.008 sec)
*/

-- alternate

CREATE VIEW VTABLE AS 
SELECT 	TABLE_SCHEMA AS 'DB',
		TABLE_NAME AS 'TABLE', 
		COLUMN_NAME AS 'FIELD',
		DATA_TYPE AS 'TYPE',
		COLUMN_DEFAULT AS 'DEFAULT',
		CHARACTER_MAXIMUM_LENGTH AS 'MAX LENGTH',
		NUMERIC_PRECISION AS 'PRECISION',
		NUMERIC_SCALE AS 'SCALE',
		COLUMN_KEY AS 'KEY', 
		EXTRA
FROM 	INFORMATION_SCHEMA.COLUMNS 
WHERE 	TABLE_SCHEMA='z_test' 
		AND TABLE_NAME='tb_person2';
		
-- to use
SELECT * FROM VTABLE;
/*
MariaDB [z_test]> select * from vtable;
+--------+------------+-----------+---------+-------------+------------+-----------+-------+-----+----------------+
| DB     | TABLE      | FIELD     | TYPE    | DEFAULT     | MAX LENGTH | PRECISION | SCALE | KEY | EXTRA          |
+--------+------------+-----------+---------+-------------+------------+-----------+-------+-----+----------------+
| z_test | tb_person2 | FirstName | varchar | NULL        |         40 |      NULL |  NULL |     |                |
| z_test | tb_person2 | LastName  | varchar | NULL        |         40 |      NULL |  NULL |     |                |
| z_test | tb_person2 | Street    | varchar | NULL        |         40 |      NULL |  NULL |     |                |
| z_test | tb_person2 | City      | varchar | 'Kalispell' |         40 |      NULL |  NULL |     |                |
| z_test | tb_person2 | State     | char    | 'MT'        |          2 |      NULL |  NULL |     |                |
| z_test | tb_person2 | Zip       | int     | 59901       |       NULL |        10 |     0 |     |                |
| z_test | tb_person2 | Salary    | double  | NULL        |       NULL |         9 |     2 |     |                |
| z_test | tb_person2 | Person_ID | int     | NULL        |       NULL |        10 |     0 | PRI | auto_increment |
+--------+------------+-----------+---------+-------------+------------+-----------+-------+-----+----------------+
8 rows in set (0.006 sec)
*/

```



### Temporary Tables

> Use the TEMPORARY keyword to create a temporary table that is only available to the current session. Temporary tables are dropped when the session ends. Temporary table names are specific to the session. They will not conflict with other temporary tables from other sessions even if they share the same name.  https://mariadb.com/kb/en/create-table/

```sql
-- Temporary Tables
CREATE TEMPORARY TABLE  tb_Person
(
  FirstName VARCHAR(40),
  LastName  VARCHAR(40) NOT NULL,
  Street    VARCHAR(40),
  City      VARCHAR(40),
  State     CHAR(2) ,
  Zip       INT(5),
  Person_ID INT(5) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (Person_ID)
)ENGINE = InnoDB;
```



## Alter Tables

```sql
-- rename table
ALTER TABLE tablename
RENAME TO newtablename;

-- drop / delete a column
ALTER TABLE tableName
DROP COLUMN columnName;

-- change a column / field
ALTER TABLES tableName
CHANGE COLUMN badColumnName goodColumnName VARCHAR(40);


-- Add a column / field --
ALTER TABLE tableName
ADD COLUMN columName VARCHAR(50);

-- Add Column AS First Field
ALTER TABLE tableName
ADD COLUMN columName VARCHAR(50) FIRST;

-- Add Column After A Specific Field
ALTER TABLE tableName
ADD COLUMN columName VARCHAR(50) AFTER otherColumnName;

-- Add a column with a primary key
ALTER TABLE tablename
ADD COLUMN  column_id INT(7)
NOT NULL AUTO_INCREMENT  PRIMARY KEY;

-- Add Primary Key
ALTER TABLE tablename
ADD CONSTRAINT websites_pk
    PRIMARY KEY (website_id);

-- Drop / Delete Primary Key
ALTER TABLE tablename
DROP PRIMARY KEY;

-- Delete Column
ALTER TABLE tablename
DROP columnname

```

