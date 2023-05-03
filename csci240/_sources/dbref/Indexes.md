# Indexes

In MySQL, an index is a data structure that helps the database find rows quickly. It is a copy of one or more columns of a table, plus a pointer to the actual row data. When you create an index, MySQL stores the values of the indexed columns in a tree-like structure. This makes it very fast for MySQL to find rows that match a certain criteria, such as a WHERE clause in a SELECT statement.

There are two main types of indexes in MySQL:

- **Primary key indexes** are used to uniquely identify rows in a table. Each row in a table can only have one value for the primary key column.
- **Non-unique indexes** allow multiple rows in a table to have the same value for the indexed column.

Indexes can be created on one or more columns. The more columns that are indexed, the more efficient the index will be. However, creating too many indexes can slow down inserts and updates, so it is important to choose the right indexes for your needs.

Indexes are a powerful tool for improving the performance of your MySQL database. By understanding how indexes work, you can use them to make your queries faster and more efficient.

Here are some of the benefits of using indexes in MySQL:

- **Improved performance:** Indexes can significantly improve the performance of queries that need to find specific rows in a table. This is because MySQL can use the index to quickly locate the rows that match the criteria in the query, without having to scan the entire table.
- **Reduced disk I/O:** Indexes can also help to reduce disk I/O, which can further improve the performance of queries. This is because MySQL can use the index to read the data that it needs from the disk, without having to read the entire table.
- **Improved data integrity:** Indexes can also help to improve data integrity. This is because they can help to prevent duplicate data from being inserted into a table.

Overall, indexes are a valuable tool for improving the performance and data integrity of your MySQL database. By understanding how indexes work, you can use them to make your queries faster, more efficient, and more reliable.



To define an index in MySQL, you use the `CREATE INDEX` statement. The syntax for the `CREATE INDEX` statement is as follows:

```
CREATE INDEX index_name
ON table_name (column_name, column_name, ...);
```

The `index_name` is the name of the index. The `table_name` is the name of the table that the index will be created on. The `column_name` is the name of the column that the index will be created on. You can specify multiple columns for the index, separated by commas.

For example, the following statement creates an index called `idx_name` on the `name` and `age` columns of the `users` table:

```
CREATE INDEX idx_name
ON users (name, age);
```

Once you have created an index, you can use it in your queries. For example, the following query will only return rows where the `name` column contains the value `John`:

```
SELECT *
FROM users
WHERE name = 'John';
```

MySQL will use the index to quickly locate the rows that match the criteria in the query, without having to scan the entire table. This can significantly improve the performance of the query.

It is important to note that creating too many indexes can slow down inserts and updates, so it is important to choose the right indexes for your needs.