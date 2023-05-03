# Foreign Keys and Cascading



```sql
-- delete the database
DROP DATABASE IF EXISTS zdbcasdemo;

-- create database
CREATE OR REPLACE DATABASE zdbcasdemo;

USE zdbcasdemo;

-- delete the tables
DROP TABLE IF EXISTS tbl_author;
DROP TABLE IF EXISTS tbl_book;

-- create new table
CREATE TABLE IF NOT EXISTS tbl_author
(
    Fname VARCHAR(255),
    Lname VARCHAR(255),
    Author_ID INT(7) NOT NULL AUTO_INCREMENT PRIMARY KEY
);

-- comment
SELECT 'Describe tbl_author ' as 'Describe';

-- display the table
DESCRIBE tbl_author;

-- create new table
CREATE TABLE IF NOT EXISTS tbl_book
(
    Title VARCHAR(255),
    Author_ID INT(7),
    Book_ID     INT(7) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    CONSTRAINT fk_bkAuth FOREIGN KEY (Author_ID) REFERENCES tbl_author(Author_ID) 
    ON DELETE CASCADE 
);

/*NOTE: we here are the other options
[CONSTRAINT [symbol]] FOREIGN KEY
    [index_name] (index_col_name, ...)
    REFERENCES tbl_name (index_col_name,...)
    [ON DELETE reference_option]
    [ON UPDATE reference_option]

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT

 https://mariadb.com/kb/en/foreign-keys/   
*/

-- comment
SELECT 'Describe tbl_book' as 'Describe';

-- displayl the table
DESCRIBE tbl_book;

-- inserting values into the author table
INSERT INTO tbl_Author(Fname,Lname,Author_ID) 
VALUES  ('Bubba','Brown',1),
        ('Sally','Smith',2),
        ('Charle','Coolidge',3);

-- comment
SELECT 'Display the author table ' as 'Comment';

-- displaying the selected records
SELECT * FROM tbl_author;

-- inserting values into the book table
-- NOTE: the author id's correspond to the
-- author that wrote the book

INSERT INTO tbl_book(Title,Author_ID) 
VALUES  ('Baking Brownies', 1),
        ('Basting Beef', 1),
        ('Surfing', 2),
        ('Sailing', 2),
        ('Snowboarding',2),
        ('Caving',3),
        ('Carving Wood',3),
        ('Cycling',3);

-- comment
SELECT 'Display the book table ' as 'Comment';

-- displaying all the books in the book table
SELECT * from tbl_book;

-- comment
SELECT 'Showing the data Combined ' as 'Comment';

-- showing the data combined from both tables
SELECT Fname,Lname, Title,tbl_author.Author_ID,Book_ID
FROM tbl_author JOIN tbl_book
     ON tbl_Author.Author_ID = tbl_book.Author_ID;

-- Since the tbl_books constraint has the cascade delete
-- when an author is deleted, it will cascade to the
-- tbl_book table and all of the corresponding 
-- books will be deleted

DELETE FROM tbl_Author
WHERE Author_ID = 2;

-- comment
SELECT 'Delete Sally Smith From Table ' as 'Comment';

-- Notice that all of Sally Smith's data has
-- been deleted from the database

SELECT Fname,Lname, Title,tbl_author.Author_ID,Book_ID
FROM tbl_author JOIN tbl_book
     ON tbl_Author.Author_ID = tbl_book.Author_ID;

-- OUTPUT 

/*
Database changed
Query OK, 0 rows affected, 1 warning (0.000 sec)

Query OK, 0 rows affected, 1 warning (0.000 sec)

Query OK, 0 rows affected (0.006 sec)

+----------------------+
| Describe             |
+----------------------+
| Describe tbl_author  |
+----------------------+
1 row in set (0.000 sec)

+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Fname     | varchar(255) | YES  |     | NULL    |                |
| Lname     | varchar(255) | YES  |     | NULL    |                |
| Author_ID | int(7)       | NO   | PRI | NULL    | auto_increment |
+-----------+--------------+------+-----+---------+----------------+
3 rows in set (0.009 sec)

Query OK, 0 rows affected (0.016 sec)

+-------------------+
| Describe          |
+-------------------+
| Describe tbl_book |
+-------------------+
1 row in set (0.000 sec)

+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Title     | varchar(255) | YES  |     | NULL    |                |
| Author_ID | int(7)       | YES  | MUL | NULL    |                |
| Book_ID   | int(7)       | NO   | PRI | NULL    | auto_increment |
+-----------+--------------+------+-----+---------+----------------+
3 rows in set (0.003 sec)

Query OK, 3 rows affected (0.001 sec)
Records: 3  Duplicates: 0  Warnings: 0

+---------------------------+
| Comment                   |
+---------------------------+
| Display the author table  |
+---------------------------+
1 row in set (0.000 sec)

+--------+----------+-----------+
| Fname  | Lname    | Author_ID |
+--------+----------+-----------+
| Bubba  | Brown    |         1 |
| Sally  | Smith    |         2 |
| Charle | Coolidge |         3 |
+--------+----------+-----------+
3 rows in set (0.000 sec)

Query OK, 8 rows affected (0.001 sec)
Records: 8  Duplicates: 0  Warnings: 0

+-------------------------+
| Comment                 |
+-------------------------+
| Display the book table  |
+-------------------------+
1 row in set (0.000 sec)

+-----------------+-----------+---------+
| Title           | Author_ID | Book_ID |
+-----------------+-----------+---------+
| Baking Brownies |         1 |       1 |
| Basting Beef    |         1 |       2 |
| Surfing         |         2 |       3 |
| Sailing         |         2 |       4 |
| Snowboarding    |         2 |       5 |
| Caving          |         3 |       6 |
| Carving Wood    |         3 |       7 |
| Cycling         |         3 |       8 |
+-----------------+-----------+---------+
8 rows in set (0.000 sec)

+----------------------------+
| Comment                    |
+----------------------------+
| Showing the data Combined  |
+----------------------------+
1 row in set (0.000 sec)

+--------+----------+-----------------+-----------+---------+
| Fname  | Lname    | Title           | Author_ID | Book_ID |
+--------+----------+-----------------+-----------+---------+
| Bubba  | Brown    | Baking Brownies |         1 |       1 |
| Bubba  | Brown    | Basting Beef    |         1 |       2 |
| Sally  | Smith    | Surfing         |         2 |       3 |
| Sally  | Smith    | Sailing         |         2 |       4 |
| Sally  | Smith    | Snowboarding    |         2 |       5 |
| Charle | Coolidge | Caving          |         3 |       6 |
| Charle | Coolidge | Carving Wood    |         3 |       7 |
| Charle | Coolidge | Cycling         |         3 |       8 |
+--------+----------+-----------------+-----------+---------+
8 rows in set (0.000 sec)

Query OK, 1 row affected (0.001 sec)

+--------------------------------+
| Comment                        |
+--------------------------------+
| Delete Sally Smith From Table  |
+--------------------------------+
1 row in set (0.000 sec)

+--------+----------+-----------------+-----------+---------+
| Fname  | Lname    | Title           | Author_ID | Book_ID |
+--------+----------+-----------------+-----------+---------+
| Bubba  | Brown    | Baking Brownies |         1 |       1 |
| Bubba  | Brown    | Basting Beef    |         1 |       2 |
| Charle | Coolidge | Caving          |         3 |       6 |
| Charle | Coolidge | Carving Wood    |         3 |       7 |
| Charle | Coolidge | Cycling         |         3 |       8 |
+--------+----------+-----------------+-----------+---------+
5 rows in set (0.001 sec)
*/
```

