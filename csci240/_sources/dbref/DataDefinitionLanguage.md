# Data Definition Language - DDL



DDL (Data Definition Language) is a set of SQL statements that are used to create, alter, and drop database objects. DDL statements are used to define the structure of a database, such as the tables, columns, and indexes that it contains.

Here are some of the most common DDL statements:

- **CREATE DATABASE:** This statement creates a new database.
- **CREATE TABLE:** This statement creates a new table.
- **ALTER TABLE:** This statement modifies an existing table.
- **DROP TABLE:** This statement deletes an existing table.
- **CREATE INDEX:** This statement creates an index on a column or columns in a table.
- **DROP INDEX:** This statement deletes an index from a table.
- **CREATE VIEW:** This statement creates a view, which is a virtual table that is based on one or more base tables.
- **DROP VIEW:** This statement deletes a view.
- **CREATE PROCEDURE:** This statement creates a stored procedure, which is a collection of SQL statements that can be executed as a single unit.
- **DROP PROCEDURE:** This statement deletes a stored procedure.
- **CREATE TRIGGER:** This statement creates a trigger, which is a stored procedure that is executed automatically when a specific event occurs, such as an insert, update, or delete.
- **DROP TRIGGER:** This statement deletes a trigger.
- **GRANT:** This statement grants permissions to a user or role.
- **REVOKE:** This statement revokes permissions from a user or role.
- **BACKUP DATABASE:** This statement backs up a database.
- **RESTORE DATABASE:** This statement restores a database from a backup.

Here are some examples of DDL statements:

```sql
-- Create a database
CREATE DATABASE mydb;

-- Create a table
CREATE TABLE mytable (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  age INT NOT NULL,
  PRIMARY KEY (id)
);

-- Alter a table
ALTER TABLE mytable ADD COLUMN email VARCHAR(255);

-- Drop a table
DROP TABLE mytable;

-- Create an index
CREATE INDEX myindex ON mytable (name);

-- Drop an index
DROP INDEX myindex ON mytable;

-- Create a view
CREATE VIEW myview AS
SELECT name, age
FROM mytable;

-- Drop a view
DROP VIEW myview;

-- Create a stored procedure
CREATE PROCEDURE myproc()
BEGIN
  SELECT * FROM mytable;
END;

-- Drop a stored procedure
DROP PROCEDURE myproc;

-- Grant permissions
GRANT SELECT ON mydb.* TO myuser;

-- Revoke permissions
REVOKE SELECT ON mydb.* FROM myuser;

-- Backup a database
BACKUP DATABASE mydb TO DISK = '/path/to/mydb.bak';

-- Restore a database
RESTORE DATABASE mydb FROM DISK = '/path/to/mydb.bak';
```