# SQL Reference



```mysql
     /*
   This is a 
   multi line
   comment
*/

-- This is single line comment

-- Creating a database
CREATE DATABASE  myDatabaseName;

CREATE DATABASE IF NOT EXISTS db_myDatabaseName;

-- show databases
SHOW DATABASES;

-- Use
USE db_myDatabaseName;

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
)ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS  tb_Person2
(
  FirstName VARCHAR(40),
  LastName  VARCHAR(40) NOT NULL,
  Street    VARCHAR(40),
  City      VARCHAR(40),
  State     CHAR(2) DEFAULT 'MT',
  Zip       INT(5),
  Person_ID INT(5) NOT NULL  AUTO_INCREMENT PRIMARY KEY
)ENGINE = InnoDB;


CREATE TABLE IF NOT EXISTS tbl_Author
(
  aFname    VARCHAR(30),
  aLname    VARCHAR(30),
  a_id      INT(5) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (a_id)
);

DROP TABLE IF EXISTS tbl_book;








CREATE TABLE IF NOT EXISTS tbl_book
(
  bTitle    VARCHAR(30),
  bGenre    VARCHAR(30),
  a_id      INT(5),
  book_id   INT(5) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY(book_id),
  FOREIGN KEY (a_id) REFERENCES tbl_Author(a_id)
);


DROP TABLE  IF EXISTS tbl_book2;

CREATE TABLE IF NOT EXISTS tbl_book2
(
  bTitle    VARCHAR(30),
  bGenre    VARCHAR(30),
  a_id      INT(5),
  book_id   INT(5)
);


-- Delete table
DROP TABLE myTablname;

-- Delete database
DROP DATABASE myDatabaseName;

-- drop a column
ALTER TABLE tableName
DROP COLUMN columnName;

ALTER TABLES tableName
CHANGE COLUMN badColumnName goodColumnName VARCHAR(40);


-- Add a column --
ALTER TABLE tableName
ADD COLUMN columName VARCHAR(50);

ALTER TABLE tableName
ADD COLUMN columName VARCHAR(50) FIRST;

ALTER TABLE tableName
ADD COLUMN columName VARCHAR(50) AFTER otherColumnName;



-- Add a column with a primary key
ALTER TABLE tablename
ADD COLUMN  column_id INT(7)
NOT NULL AUTO_INCREMENT  PRIMARY KEY;








--
ALTER TABLE tbl_book2
ADD FOREIGN KEY tbl_book2(a_id) REFERENCES tbl_author(a_id);

ALTER TABLE tbl_book2
ADD PRIMARY KEY tbl_book2(book_id);

ALTER TABLE tbl_book2
MODIFY COLUMN  book_id INT(5)  NOT NULL AUTO_INCREMENT PRIMARY KEY;


-- add a not null

ALTER TABLE tbl_book2
MODIFY COLUMN  bTitle VARCHAR(30)  NOT NULL;

-- delete primary key
ALTER TABLE tablename
DROP PRIMARY KEY;

-- DELETE foreign key
ALTER TABLE tablename
DROP FOREIGN KEY;

-- Enable or disable keys - used when deleting tables  or data
ALTER TABLE tablename
DISABLE KEYS;

ALTER TABLE tablename
ENABLE KEYS;

-- Deletes all data out a table
TRUNCATE TABLE tablename;

--  Record all command activies to a file
TEE c:\myfolder\myfilename.sql;

-- Stop recording all activites to a file
NOTEE;

-- Load a sql file into the databae
SOURCE C:\myfolder\myfilename.sql;

-- Exit mysql command prompt
EXIT

-- Show a description of the table
DESCRIBE tablename;

-- 
SELECT `COLUMN_NAME` 
FROM `INFORMATION_SCHEMA`.`COLUMNS` 
WHERE `TABLE_SCHEMA`='db_customer' 
    AND `TABLE_NAME`='customer';
    
    
    
-- show foreign keys
select
    concat(table_name, '.', column_name) as 'foreign key',  
    concat(referenced_table_name, '.', referenced_column_name) as 'references'
from
    information_schema.key_column_usage
where
    referenced_table_name is not null;
    
    
    
select
    concat(table_name, '.', column_name) as 'foreign key',  
    concat(referenced_table_name, '.', referenced_column_name) as 'references'
from
    information_schema.key_column_usage
where
    referenced_table_name is not null
    and table_schema = 'my_database' 
```

