# PDO Connections



## Introduction

> The PHP Data Objects (PDO) extension defines a lightweight, consistent interface for accessing databases in PHP. Each database driver that implements the PDO interface can expose database-specific features as regular extension functions. Note that you cannot perform any database functions using the PDO extension by itself; you must use a database-specific PDO driver to access a database server.
>
> *PDO provides a data-access abstraction layer, which means that, regardless of which database you're using, you use the same functions to issue queries and fetch data.* PDO does not provide a database abstraction; it doesn't rewrite SQL or emulate missing features. You should use a full-blown abstraction layer if you need that facility.
>
> PDO ships with PHP.  [php introduction 10/2023](https://www.php.net/manual/en/intro.pdo.php)



## Database Connections

Connection strings do the following:

* identify what type of database they are connecting to
* where the database/host is located on the web
* the database name
* username with the appropriate privileges
  * NOTE: when going to production, **No username facing the public internet should have admin rights!**
* password for the username





> **NONE OF THE EXAMPLES INCLUDE SANITIZING THE DATA.  IN PRODUCTION, ALWAYS SANITIZE AND VALIDATE THE DATA BEFORE INSERTING IT INTO A DATABASE!** 



```php 
try {

 // MSSQL Server, Sybase, and Oracle

 $pdo = new PDO("sqlsrv:host=$host;dbname=$dbname, $user, $password");
 $pdo = new PDO("sybase:host=$host;dbname=$dbname, $user, $password");
 $pdo = new PDO("oci:host=$host;dbname=$dbname, $user, $password");
 
 // MySQL with PDO_MYSQL
 $pdo = new PDO("mysql:host=$host;dbname=$dbname", $user, $password);

 // SQLite Database
 $pdo = new PDO("sqlite:my/database/path/database.db");
    
 // ODBC
 $pdo = new PDO("odbc:host=$host;dbname=$dbname", $user, $password);
}

catch(PDOException $e) {

  echo $e->getMessage();

}
```



## PDO Drivers

 

- [ ] | Driver name  | Supported databases                                          |
  | :----------- | :----------------------------------------------------------- |
  | PDO_CUBRID   | Cubrid                                                       |
  | PDO_DBLIB    | FreeTDS / Microsoft SQL Server / Sybase                      |
  | PDO_FIREBIRD | Firebird                                                     |
  | PDO_IBM      | IBM DB2                                                      |
  | PDO_INFORMIX | IBM Informix Dynamic Server                                  |
  | PDO_MYSQL    | MySQL 3.x/4.x/5.x/8.x                                        |
  | PDO_OCI      | Oracle Call Interface                                        |
  | PDO_ODBC     | ODBC v3 (IBM DB2, unixODBC and win32 ODBC)                   |
  | PDO_PGSQL    | PostgreSQL                                                   |
  | PDO_SQLITE   | SQLite 3 and SQLite 2                                        |
  | PDO_SQLSRV   | Microsoft SQL Server / SQL Azure                             |
  |              | From [php.org](https://www.php.net/manual/en/pdo.drivers.php) |



## Close Connection



```php
// close the connection

$pdo = null;
```

 

## Error Modes

PDO::ERRMODE_SILENT

This is the default error mode. It does not show any error exceptions

 

PDO::ERRMODE_WARNING

This mode will issue a standard PHP warning, and allow the program to continue execution. It's useful for debugging.



PDO::ERRMODE_EXCEPTION 

This is the mode you should want in most situations. It fires an exception, allowing you to handle errors gracefully and hide data that might help someone exploit your system. Here's an example of taking advantage of exceptions:



```php
$pdo->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_SILENT );

$pdo->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_WARNING );

$pdo->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
```

 

## Insert / Update

 

Prepare -> Sanitize -> Bind _->_ Execute

 

## Prepared Statements

A prepared statement is a precompiled SQL statement that can be executed multiple times by sending just the data to the server. It has the added advantage of automatically making the **data used in the placeholders safe from SQL injection attacks**.

 

```php
$pdo= $pdo->prepare("INSERT INTO tbl_names(first_name,last_name) VALUES(:first_name,:last_name )");

$pdo->execute();
```



### Placeholders

```php
// no placeholders - ripe for SQL Injection!

$STH = $pdo->prepare("INSERT INTO folks (name, addr, city) values ($name, $addr, $city)");

 

// unnamed placeholders

$STH = $pdo->prepare("INSERT INTO folks (name, addr, city) values (?, ?, ?);

 

// named placeholders

$STH = $pdo->prepare("INSERT INTO folks (name, addr, city) value (:name, :addr, :city)");
```



### Unnamed Place Holders

```php
// unnamed placeholders

$STH = $pdo->("INSERT INTO folks (name, addr, city) values (?, ?, ?);

// assign variables to each place holder, indexed 1-3

$STH->bindParam(1, $name);

$STH->bindParam(2, $addr);

$STH->bindParam(3, $city);

 

// insert one row

$name = "Moe"

$addr = "1 Wicked Way";

$city = "Arlington Heights";

$STH->execute();

 

// insert another row with different values

$name = "Curly"

$addr = "Schmuck Drive";

$city = "Schaumburg";

$STH->execute();
```

 

### Use an array

```php
// the data we want to insert

$data = array('Cathy', '9 Dark and Twisty Road', 'Cardiff');

$STH = $pdo->prepare("INSERT INTO folks (name, addr, city) values (?, ?, ?);

$STH->execute($data);
```





 

### Named Place Holders

 ```php
 // the first argument is the named placeholder name - notice named
 
 // placeholders always start with a colon.
 
 $pdo->bindParam(':name', $name);
 
 
 // the data we want to insert
 $data = array( 'name' => 'Cathy', 'addr' => '9 Dark and Twisty', 'city' => 'Cardiff' );
 
 
 // the shortcut!
 
 $pdo = $pdo->("INSERT INTO folks (name, addr, city) value (:name, :addr, :city)");
 
 $STH->execute($data);
 ```



 

## Fetching Data

 

PDO::FETCH_ASSOC: returns an array indexed by column name

PDO::FETCH_BOTH (default): returns an array indexed by both column name and number

PDO::FETCH_BOUND: Assigns the values of your columns to the variables set with the ->bindColumn() method

PDO::FETCH_CLASS: Assigns the values of your columns to properties of the named class. It will create the properties if matching properties do not exist

PDO::FETCH_INTO: Updates an existing instance of the named class

PDO::FETCH_LAZY: Combines PDO::FETCH_BOTH/PDO::FETCH_OBJ, creating the object variable names as they are used

PDO::FETCH_NUM: returns an array indexed by column number

PDO::FETCH_OBJ: returns an anonymous object with property names that correspond to the column names

 

 

### FETCH_ASSOC

This fetch type creates an associative array, indexed by column name

```php
// using the shortcut ->query() method here since there are no variable

// values in the select statement.
$STH = $pdo->query('SELECT name, addr, city from folks');

// setting the fetch mode
$STH->setFetchMode(PDO::FETCH_ASSOC);

while($row = $STH->fetch()) {

  echo $row['name'] . "\n";

  echo $row['addr'] . "\n";

  echo $row['city'] . "\n";

}
```

### FETCH_OBJ

This fetch type creates an object of std class for each row of fetched data. Here's an example:

```php
// creating the statement
$STH = $DBH->query('SELECT name, addr, city from folks');

 
// setting the fetch mode
$STH->setFetchMode(PDO::FETCH_OBJ);

// showing the results
while($row = $STH->fetch()) {

  echo $row->name . "\n";

  echo $row->addr . "\n";

  echo $row->city . "\n";

}
```



 

## Last Insert ID

The ->lastInsertId() method is always called on the database handle, not the statement handle, and will return the auto-incremented id of the last inserted row by that connection.

 

## Delete Files

```php
$pdo->exec('DELETE FROM folks WHERE 1');
```





 

 