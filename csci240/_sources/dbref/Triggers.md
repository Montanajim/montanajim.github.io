# Triggers

A trigger in MySQL is a stored program that is executed automatically in response to a specific event such as insertion, updation or deletion occurring in a table. There are 6 different types of triggers in MySQL:

* Before Insert Trigger: This trigger is executed before the row is inserted into the table.
* After Insert Trigger: This trigger is executed after the row is inserted into the table.
* Before Update Trigger: This trigger is executed before the row is updated in the table.
* After Update Trigger: This trigger is executed after the row is updated in the table.
* Before Delete Trigger: This trigger is executed before the row is deleted from the table.
* After Delete Trigger: This trigger is executed after the row is deleted from the table.

Triggers can be used to perform a variety of tasks such as:

* Validate data before it is inserted into a table.
* Automatically update other tables when data is changed in a table.
* Log all changes that are made to a table.
* Prevent unauthorized users from making changes to a table.

To create a trigger in MySQL, you use the `CREATE TRIGGER` statement. The syntax for the `CREATE TRIGGER` statement is as follows:

```sql
CREATE TRIGGER trigger_name
BEFORE | AFTER
insert | update | delete
ON table_name
FOR EACH ROW
BEGIN
  -- trigger body
END;
```

The `trigger_name` is the name of the trigger. The `BEFORE` or `AFTER` keyword specifies whether the trigger is executed before or after the event occurs. The `insert`, `update`, or `delete` keyword specifies the type of event that triggers the trigger. The `table_name` is the name of the table that the trigger is associated with. The `FOR EACH ROW` clause specifies that the trigger is executed for each row that is affected by the event.

The `trigger body` is the code that is executed by the trigger. The trigger body can contain any valid SQL statements.

Here is an example of a trigger that validates data before it is inserted into a table:

```sql
CREATE TRIGGER validate_data
BEFORE INSERT ON customers
FOR EACH ROW
BEGIN
  -- Check if the customer name is empty
  IF NEW.customer_name = '' THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Customer name cannot be empty.';
  END IF;

  -- Check if the customer email is in the correct format
  IF NOT NEW.customer_email REGEXP '^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z]+$' THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Customer email is not in the correct format.';
  END IF;
END;
```

This trigger will check if the customer's name and email are empty and if the customer's email is in the correct format. If either of these conditions is not met, the trigger will raise an error.

Triggers can be a powerful tool for controlling access to your data and ensuring the integrity of your database.



### More Examples

```mysql
-- CREATE TRIGGER CALLED trg_jgm
-- this assumes there is a table called tbl_car
-- and there is a 'make' field

-- if the user entered 'jgm' it would be replaced by 'Goudy Mobile'

delimiter //
CREATE TRIGGER trg_jgm BEFORE INSERT
ON tbl_car
FOR EACH ROW
    IF NEW.Make LIKE 'jgm' THEN
        SET NEW.MAKE = 'Goudy Mobile';
    END IF; 

//
delimiter ;

-- test
INSERT INTO tbl_trashme(make)
	VALUES('jgm');


```



#### Sources

[www.iditect.com/how-to/47387.html](https://www.iditect.com/how-to/47387.html)

[www.geeksforgeeks.org/different-types-of-mysql-triggers-with-examples/](https://www.geeksforgeeks.org/different-types-of-mysql-triggers-with-examples/)