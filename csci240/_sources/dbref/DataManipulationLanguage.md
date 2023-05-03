# Data Manipulation Language - DML



DML stands for Data Manipulation Language. It is a subset of SQL that is used to manipulate data in a database. The four main DML commands are:

- INSERT - Used to insert new rows into a table
- UPDATE - Used to update existing rows in a table
- DELETE - Used to delete rows from a table
- REPLACE - Used to insert or update rows in a table

DML commands can be used to manipulate data in a database in a variety of ways. For example, you can use DML to:

- Insert new rows into a table
- Update existing rows in a table
- Delete rows from a table
- Replace rows in a table

DML is a powerful tool that can be used to manipulate data in a database. By understanding the different DML commands, you can use them to manipulate the data that you need.

Here are some examples of DML statements:

```mysql
INSERT INTO customers (name, email) VALUES ('John Doe', 'johndoe@example.com');

UPDATE customers SET email = 'janedoe@example.com' WHERE name = 'Jane Doe';

DELETE FROM customers WHERE name = 'John Doe';

REPLACE INTO customers (name, email) VALUES ('John Doe', 'johndoe@example.com');
```

These statements will insert a new row into the `customers` table, update the email address for the row where the `name` column is equal to `Jane Doe`, delete the row where the `name` column is equal to `John Doe`, and replace the row where the `name` column is equal to `John Doe` with a new row with the same `name` column value but a different `email` column value, respectively.