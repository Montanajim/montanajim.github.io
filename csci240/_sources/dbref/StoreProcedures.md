# Store Procedures

## Definition

A stored procedure is a set of SQL statements that are stored in a database and can be called by name. They are used to group together SQL statements that are executed frequently, which can improve performance and reduce errors. Stored procedures can also be used to enforce security and encapsulate business logic, making it easier to maintain and update the database.

## Advantages

* Code reusability.

* Lesser Network transfer

* More secure – The Database Administrator 
	can GRANT or REVOKE privileges at a procedure level.
	
* Modularised code structure.
  
  https://www.softwaretestinghelp.com/mysql-stored-procedure/#Advantages
  
  

```mysql
-- Stored Procedures
 
-- We change the delimiter to indicate what is 
-- part of the store procedure vs what is an SQL command
-- outside a stored procedure
-- We can change the delimiter to anything we want.

DELIMITER $$

CREATE OR REPLACE PROCEDURE pro_Payments()

  BEGIN 
	  -- SQL Statements Go Here
	  -- These can also include SQL statements to 
	  -- create tables, views, users, and set priviledges
	  
      SELECT * 
      FROM payments
      LIMIT 25;

  END $$

-- change the delimiter back to 
DELIMITER ;

-- excecute the stored procedure
CALL pro_Payments();

-- ------------- Another Example -------------------------

DELIMITER $$

-- here we are creating a stored procedure that will 
-- take input. Note the key word "IN" which means input
-- we then define a variable name and the data type

CREATE PROCEDURE pro_Payments2(IN payAmount DECIMAL)

  BEGIN 

  	SELECT * FROM payments
    	WHERE amount >= payAmount;
  END $$

DELIMITER ;

call pro_Payments2(70000);

-- ------------- Another Example -------------------------

-- Here is a query to show stored procedures
SELECT  routine_schema,  
        routine_name,  
        routine_type 
FROM information_schema.routines 
WHERE routine_schema = 'classicmodels' 
ORDER BY routine_name;

-- Turn this into a stored procedure

DELIMITER //

CREATE OR REPLACE PROCEDURE pro_ListProcedures(IN procName VARCHAR(255))

  BEGIN 

    SELECT  routine_schema,  
            routine_name,  
            routine_type 
    FROM information_schema.routines 
    WHERE routine_schema = 'classicmodels' 
    ORDER BY routine_name;
  
END //

DELIMITER ;

CALL pro_ListProcedures('classicmodels');


-- -------------- Helpful  query ----------------------------------
SHOW FULL TABLES IN classicmodels WHERE TABLE_TYPE LIKE 'VIEW';


-- -------- Here is an example of a stored procedure to  list views --------------


DELIMITER //



CREATE OR REPLACE PROCEDURE proc_ListViews(IN theDBName VARCHAR(255))

  BEGIN 

      SELECT TABLE_SCHEMA, TABLE_NAME 
      FROM information_schema.tables 
      WHERE TABLE_TYPE LIKE 'VIEW'
          AND TABLE_SCHEMA LIKE theDBName;

	END //

DELIMITER ;

CALL proc_ListViews('classicmodels');


-- Another example --

DELIMITER

```

