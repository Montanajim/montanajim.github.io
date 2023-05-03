# Data Query Language - DQL

In MySQL, DQL stands for Data Query Language. It is a subset of SQL that is used to retrieve data from a database. The SELECT statement is the most common DQL command. 

DQL commands can be used to retrieve data from a database in a variety of ways. For example, you can use DQL to:

- Retrieve all rows from a table
- Retrieve only certain columns from a table
- Retrieve rows that meet certain criteria
- Retrieve rows in a specific order

 By understanding the different DQL commands, you can use them to retrieve the data that you need.

Here are some examples of DQL statements:

```sql
SELECT * FROM customers;

SELECT name, email FROM customers;

SELECT name, email FROM customers WHERE country = 'USA';

SELECT name, email FROM customers ORDER BY name DESC;
```

These statements will retrieve all rows from the `customers` table, only the `name` and `email` columns from the `customers` table, only rows where the `country` column is equal to `USA`, and all rows from the `customers` table sorted by the `name` column in descending order, respectively.