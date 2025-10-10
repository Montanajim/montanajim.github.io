# Add Edit Delete







```{tableofcontents}
```
---

```{contents}
:local:
```
---

``` {mermaid}
graph TD

A[index.php]-->B[Inputdata_DisplayData.php]
A --> C[ Display_Edit.php]
C --> D[Edit_Data.php]
D --> C
```



## Database SQL

This SQL dump creates a small database named **`wp_dogdb`**, which is test database for storing information about dogs and U.S. states.

Here’s what it does in essence:

1. **Creates the database** `wp_dogdb` (if it doesn’t already exist).

2. **Defines two tables:**

   - **`tbl_doginfo`** — stores details about dogs and their owners, including:
     - `dogname`, `dogbreed`, `ownerfirstname`, `ownerlastname`, `city`, and `st` (state code).
     - Each record has a unique `dogid` (auto-incremented primary key).
   - **`tbl_state`** — a simple reference table listing all **U.S. state abbreviations**.

3. **Populates** `tbl_doginfo` with four sample dogs (all owned by “Joe Cool” from “Fluffy, AK”).

4. **Populates** `tbl_state` with the full list of 50 U.S. state abbreviations.

   

```sql
-- phpMyAdmin SQL Dump
-- version 4.7.0
-- https://www.phpmyadmin.net/
--
-- Host: 127.0.0.1
-- Generation Time: Nov 02, 2017 at 04:53 PM
-- Server version: 10.1.22-MariaDB
-- PHP Version: 7.1.4

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET AUTOCOMMIT = 0;
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `wp_dogdb`
--
CREATE DATABASE IF NOT EXISTS `wp_dogdb` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci;
USE `wp_dogdb`;

-- --------------------------------------------------------

--
-- Table structure for table `tbl_doginfo`
--

DROP TABLE IF EXISTS `tbl_doginfo`;
CREATE TABLE IF NOT EXISTS `tbl_doginfo` (
  `dogname` varchar(20) NOT NULL,
  `dogbreed` varchar(20) NOT NULL,
  `ownerfirstname` varchar(20) NOT NULL,
  `ownerlastname` varchar(20) NOT NULL,
  `city` varchar(20) NOT NULL,
  `st` varchar(2) NOT NULL,
  `dogid` int(7) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`dogid`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=latin1;

--
-- Dumping data for table `tbl_doginfo`
--

INSERT INTO `tbl_doginfo` (`dogname`, `dogbreed`, `ownerfirstname`, `ownerlastname`, `city`, `st`, `dogid`) VALUES
('Barky', 'Spaniel', 'Joe', 'Cool', 'Fluffy', 'AK', 1),
('Barky 3', 'Spaniel', 'Joe', 'Cool', 'Fluffy', 'AK', 2),
('Barky 3', 'Spaniel', 'Joe', 'Cool', 'Fluffy', 'AK', 3),
('Barky 4', 'Spaniel', 'Joe', 'Cool', 'Fluffy', 'AK', 4);

-- --------------------------------------------------------

--
-- Table structure for table `tbl_state`
--

DROP TABLE IF EXISTS `tbl_state`;
CREATE TABLE IF NOT EXISTS `tbl_state` (
  `st` varchar(2) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Dumping data for table `tbl_state`
--

INSERT INTO `tbl_state` (`st`) VALUES
('AL'),('AK'),('AZ'),('AR'),('CA'),('CO'),('CT'),('DE'),('FL'),('GA'),
('HI'),('ID'),('IL'),('IN'),('IA'),('KS'),('KY'),('LA'),('ME'),('MD'),
('MA'),('MI'),('MN'),('MS'),('MO'),('MT'),('NE'),('NV'),('NH'),('NJ'),
('NM'),('NY'),('NC'),('ND'),('OH'),('OK'),('OR'),('PA'),('RI'),('SC'),
('SD'),('TN'),('TX'),('UT'),('VT'),('VA'),('WA'),('WV'),('WI'),('WY');
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

```



## dbconnect.php

This PHP script attempts to **connect to the `wp_dogdb` MySQL database** using PDO.

If the connection is successful, it sets a status message saying **“Good database connection.”**
If the connection fails, it catches the exception and stores an error message containing the failure reason.

Finally, it **starts a PHP session**—likely to maintain user or application state across pages.

```php
<?php

try
{
    $pdo=new PDO("mysql:host=127.0.0.1;dbname=wp_dogdb",'root','');
    $pdo->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);

    $dbstatus = "Good database connection";
}
 catch (PDOException $e)
 {
     $dbstatus = "Database connection failed <br>".
             $e->getMessage();    
 }
 session_start()

?>

```



## index.php

This PHP and HTML code creates a simple web form for entering dog information into a database. It begins by including the `dbconnect.php` file to establish a connection with the `wp_dogdb` database and displays the current connection status. The script then retrieves a list of U.S. state abbreviations from the `tbl_state` table, sorting them alphabetically, and stores the results for use in the form. The webpage presents an input form where users can enter details about a dog—such as its name, breed, and the owner’s first and last name, as well as the city and state. The state field is dynamically generated from the database query, ensuring the dropdown list reflects accurate state data. When the user submits the form, the entered information is sent via POST to `Inputdata_DisplayData.php` for further processing or display.

```php
<!DOCTYPE html>
<html>
<head>
<title>Home Page</title>


<?php
	require 'dbconnect.php';
	
	echo $dbstatus;
	
    // used for building the select statement
	$sql_st = "SELECT * ".
			"FROM tbl_state ".
			"ORDER BY 	st";
    
	//retreive the states and store them ind $dataset_st
	$dataset_st = $pdo->query($sql_st);

?>

</head>
<body>

	<form method="POST" action = "Inputdata_DisplayData.php">
	<table border="1">
		<tr>
			<td colspan="2">Dog Information</td>
		</tr>
		<tr>
			<td>Dog Name
            </td>
            <td>
            <input type="text" name="dogname" value="Barky">
            </td>
		</tr>
		<tr>
			<td>Dog Breed
            </td>
            <td>
            <input type="text" name="dogbreed" value="Mutt">
            </td>
		</tr>
		<tr>
			<td>Owner First Name
            </td>
            <td>
            <input type="text" name="ownerfirstname" value="Bubba">
            </td>
		</tr>
		<tr>
			<td>Owner Last Name
            </td>
            <td>
            <input type="text" name="ownerlastname" value="Smith">
            </td>
		</tr>
		<tr>
			<td>City
            </td>
            <td>
            <input type="text" name="city" value="Chicago">
            </td>
		</tr>
		<tr>
			<td>State
            </td>
            <td>
            <select name="st">
                <?php
                    while($row = $dataset_st->fetch())
                    {
                    echo('<option value="'.$row['st'].'">'.$row['st'].'</option>');
                    }
                ?>
            </select>
            </td>
		</tr>
		<tr>
			<td>
            </td>
            <td><input type="submit" value="Enter">
            </td>
		</tr>
	</table>
	</form>
</body>
</html>

```



## Inputdata_DisplayData.php

This PHP script, **`Inputdata_DisplayData.php`**, processes the dog information form submission from the previous page. It begins by including the database connection file `dbconnect.php`, then prints the submitted form data for debugging purposes. The script defines a `sanitize()` function to clean user input by trimming whitespace, removing HTML/PHP tags, and encoding special characters—ensuring the data is safe for database insertion.

Inside a `try` block, it prepares an SQL `INSERT` statement to add a new record into the `tbl_doginfo1` table, binding the sanitized form values (`dogname`, `dogbreed`, `ownerfirstname`, `ownerlastname`, `city`, and `st`) to named placeholders. After executing the insert command, the script displays a formatted confirmation message showing the details entered by the user. If any database or general errors occur, they are caught and displayed in a clear error message.

```php
<?php
//Inputdata_DisplayData.php
require 'dbconnect.php';

print_r($_POST);
echo('<br><hr><br>');

function sanitize($value){

    // strip of any excess white spaces on the ends
    $value = trim($value);

    // get rid of any html or php tags
    $value = strip_tags($value);

    // convert special characters
    $value = htmlspecialchars($value,ENT_QUOTES,'UTF-8');

    // return the value
    return $value;

}

// alternative
function sanitize2($value){
    return htmlspecialchars(strip_tags(trim($value)),ENT_QUOTES,'UTF-8');
}

try{
    // write insert sql statement
    $sql_insert = 	"INSERT INTO tbl_doginfo1("
                ."dogname,"
                ."dogbreed,"
                ."ownerfirstname,"
                ."ownerlastname,"
                ."city,"
                ."st)"
                ."VALUES("
                .":dogname,"
                .":dogbreed,"
                .":ownerfirstname,"
                .":ownerlastname,"
                .":city,"
                .":st)";

    // prepare the sql statement
    $sql_insert = $pdo->prepare($sql_insert);

    // sanitize the information
    $dogname = sanitize($_POST['dogname'] ?? '');
    $dogbreed = sanitize($_POST['dogbreed'] ?? '');
    $ownerfirstname = sanitize($_POST['ownerfirstname'] ?? '');
    $ownerlastname = sanitize($_POST['ownerlastname'] ?? '');
    $city = sanitize($_POST['city'] ?? '');
    $st = sanitize($_POST['st'] ?? '');

    //bind variable name to placeholders
    $sql_insert->bindparam(":dogname",$dogname);
    $sql_insert->bindparam(":dogbreed",$dogbreed);
    $sql_insert->bindparam(":ownerfirstname",$ownerfirstname);
    $sql_insert->bindparam(":ownerlastname",$ownerlastname);
    $sql_insert->bindparam(":city",$city);
    $sql_insert->bindparam(":st",$st);

    //execute
    $sql_insert->execute();

    //--Alternative Binding Method using an array
    /*
    $sql_params=array(':dogname'=> $dogname,
                    ':dogbreed' => $dogbreed,
                    ':ownerfirstname' => $ownerfirstname ,
                    ':ownerlastname' => $ownerlastname,
                    ':city' => $city,
                    ':st' => $st);

    $sql_insert->execute($sql_params);
     */    




    echo("
            <h2>Dog Infomation Confirmation</h2>
            Dog Name: $dogname<br>
            Dog Breed: $dogbreed<br>
            Owner First Name: $ownerfirstname<br>
            Owner Last Name: $ownerlastname<br>
            City: $city<br>
            State: $st<br>
        ");
}
catch(PDOException $err)
{
	echo('<h2>Error</h2>'.
		$err->getMessage()
		);
	
}
catch(Exception $e)
{
	echo('<h2>Error</h2>'.
		$e->getMessage()
		);
}

?>

```



## Display_Edit.php

This PHP script displays and manages a **list of dogs** from the `tbl_doginfo` database table, allowing users to **edit or delete records** directly from a web interface.

It begins by including the `dbconnection.php` file to establish a database connection. When a form is submitted, the script checks the `action` value in the POST data:

- If the action is **“Delete”**, it sanitizes the `dogid` and executes a SQL `DELETE` command to remove the corresponding record.
- If the action is **“Edit”**, it stores the selected dog’s ID in a session variable and redirects the user to `edit_data.php` to update that record.

After handling any actions, the script retrieves all existing dog records—showing each dog’s name, breed, owner’s name, city, and state—and dynamically generates an HTML table with **Edit** and **Delete** buttons for each entry.

In short: 🐕 *This code powers a simple admin-style dashboard for managing dog records—complete with live database actions and a clean, table-based interface.*

```php
<?php
require ('./dbconnection.php');

if (isset($_POST)) {
    
    if (!empty($_POST['action'])) {
        if ($_POST['action'] === 'Delete') {
            $dID = filter_var($_POST['dogid'], FILTER_SANITIZE_STRING);
            $sql_delete = "DELETE FROM tbl_doginfo WHERE dogid = " . $dID;
            $pdo->exec($sql_delete);
        }

      if ($_POST['action'] === 'Edit')
      {
          //NOTE: you cannot send any output to the current page (Display_Edit.php
          //You must go directly to the new page.
          $_SESSION['dogEditID'] = filter_var($_POST['dogid'], FILTER_SANITIZE_NUMBER_INT);  
          header("Location:edit_data.php");
      }       
   }
}


$sql_selectEdit = "SELECT dogname, dogbreed, ownerfirstname, ownerlastname, city, st, dogid"
        . " FROM tbl_doginfo "
        . " ORDER BY dogname";

$result_edit = $pdo->query($sql_selectEdit);
?>

<html>
    <head>
        <title></title>
    </head>
    <body>
<?php
include 'menu.php';
?>


        <table border="1">
            <thead>
                <tr>
                    <th>Dog Name</th>
                    <th>Dog Breed</th>
                    <th>First Name</th>
                    <th>Last Name</th>
                    <th>Owner First Name</th>
                    <th>Owner Last Name</th>
                    <th>Edit</th>
                </tr>
            </thead>
            <tbody>
<?php
while ($row = $result_edit->fetch()) {
    echo('<tr>'
    . '<td>' . $row['dogname'] . "</td>"
    . "<td>" . $row['dogbreed'] . "</td>"
    . "<td>" . $row['ownerfirstname'] . "</td>"
    . "<td>" . $row['ownerlastname'] . "</td>"
    . "<td>" . $row['city'] . "</td>"
    . "<td>" . $row['st'] . "</td>"
    . '<td><form method="POST" action="Display_Edit.php" 
    		onsubmit="return confirm('."'".'Are U Sure'."')".'">
    		<input type="hidden" name="dogid" value="'.$row['dogid'].'"/>'
    . '<input type="submit" value="Edit" name="action" />&nbsp;&nbsp;'
    . '<input type="submit" value="Delete" name="action"/>'
    . '</form></td></tr>');
}
?>
            </tbody>
        </table>
    </body>
</html>
```



## Edit_data.php

This PHP script provides an **edit interface for updating existing dog records** in the `tbl_doginfo` database.

It begins by including the database connection file and defining two `sanitize()` functions that clean user input by trimming whitespace, stripping HTML/PHP tags, and encoding special characters—ensuring the data is secure before being stored. If the user submits the form, the script prepares an SQL `UPDATE` statement with named placeholders and binds the sanitized input values (dog name, breed, owner info, city, and state) to those placeholders. It then executes the update and redirects the user back to the main display page.

If the form hasn’t been submitted yet, the script retrieves the selected dog’s record—based on a session-stored `dogEditID`—and queries the list of U.S. states from `tbl_state`. It then displays a pre-filled form that allows the user to modify the existing information, with the current state automatically selected.

In essence: 🐾 *This page is the heart of the “edit dog” workflow—securely fetching, displaying, and updating canine records with clean, user-friendly precision.*

```php
<?php
require ('./dbconnection.php');


function sanitize($value){

    // strip of any excess white spaces on the ends
    $value = trim($value);

    // get rid of any html or php tags
    $value = strip_tags($value);

    // convert special characters
    $value = htmlspecialchars($value,ENT_QUOTES,'UTF-8');

    // return the value
    return $value;

}

// alternative
function sanitize2($value){
    return htmlspecialchars(strip_tags(trim($value)),ENT_QUOTES,'UTF-8');
}


if (!empty($_POST['dogname'])) {
    
    //write the sql statement with placehonders
    $sql_edit = "UPDATE  tbl_doginfo "
            . "SET dogname = :dogname, "
            . "dogbreed = :dogbreed, "
            . "ownerfirstname = :ownerfirstname, "
            . "ownerlastname = :ownerlastname, "
            . "city = :city, "
            . "st = :st  "
            . "WHERE dogid = :dogid";

    //prepare the squel statement
    $sql_edit = $pdo->prepare($sql_edit);


    //Sanitize Information
    $dogname = sanitize($_POST['dogname'] ?? '');
    $dogbreed = sanitize($_POST['dogbreed'] ?? '');
    $ownerfirstname = sanitize($_POST['ownerfirstname'] ?? '');
    $ownerlastname = sanitize($_POST['ownerlastname'] ?? '');
    $city = sanitize($_POST['city'] ?? '');
    $st = sanitize($_POST['st'] ?? '');


    //bind parameters
    $sql_edit->bindparam(":dogname", $dogname);
    $sql_edit->bindparam(":dogbreed", $dogbreed);
    $sql_edit->bindparam(":ownerfirstname", $ownerfirstname);
    $sql_edit->bindparam(":ownerlastname", $ownerlastname);
    $sql_edit->bindparam(":city", $city);
    $sql_edit->bindparam(":st", $st);
    $sql_edit->bindparam(":dogid", $dogid);

	//input data
    $sqlh_edit->execute();

	//open display data page
    header("Location: Display_Edit.php");
}


$sql_editData = "Select * "
        . " From tbl_doginfo"
        . " Where dogid="
        . $_SESSION['dogEditID'];

$result_editData = $pdo->query($sql_editData);

$row_edit = $result_editData->fetch();

//----States
//Query to select states
$sql_st = "SELECT st " .
        "FROM tbl_state " .
        "Order by st";

//execute the select query       
$result_st = $pdo->query($sql_st);
?>

<html>
<head>
    <meta charset="UTF-8">
    <title>Edit Data</title>
</head>
<body>
    <?php
    include 'menu.php';
    ?>

    <h2>Edit Data</h2>
    <form method="POST" action="edit_data.php"  
          onsubmit="return confirm('Are you sure you want to continue')">
        <table border="1">
            <thead>
                <tr>
                    <th colspan="2">Dog Information</th>
                </tr>
            </thead>
            <tbody>

                <tr>
                    <td>Dog Name</td>
                    <td><input type="text" name="dogname" 
                               value="<?php echo $row_edit['dogname'] ?>" size="20" />						</td>
                </tr>
                <tr>
                    <td>Dog Breed</td>
                    <td><input type="text" name="dogbreed" 
                               value="<?php echo $row_edit['dogbreed'] ?>" size="20" />						</td>
                </tr>
                <tr>
                    <td>Owner First Name</td>
                    <td><input type="text" name="ownerfirstname" 
                           value="<?php echo $row_edit['ownerfirstname'] ?>" size="20" />					</td>
                </tr>
                <tr>
                    <td>Owner Last Name</td>
                    <td><input type="text" name="ownerlastname" 
                               value="<?php echo $row_edit['ownerlastname'] ?>" 
        								size="20" /></td>
                </tr>
                <tr>
                    <td>City</td>
                    <td><input type="text" name="city" 
                               value="<?php echo $row_edit['city'] ?>" size="20" /></td>
                </tr>
                <tr>
                    <td>ST</td>
                    <td><select name="st" size="1" width = 5>

                            <?php
                            while ($row = $result_st->fetch()) {
                                if ($row['st'] === $row_edit['st']) {
                                    echo('<option value="'.$row['st']
                                         .'" selected>'.$row['st'].'</option>');
                                } else {
                                    echo('<option value="'.$row['st'] 
                                         . '">'.$row['st'].'</option>');
                                }
                            }
                            ?>
                        </select></td>
                </tr>
                <tr>
                    <td>Record Id: <?php echo $row_edit['dogid'] ?>  
                        <input type="hidden" name="dogid" value="<?php 
                        echo $row_edit['dogid'] ?> "/></td>
                    <td><input type="submit" value="Enter"/></td>
                </tr>
            </tbody>
        </table>
    </form>
</body>
</html>

```



## menu.php

This short HTML snippet creates a simple **navigation menu** with two links: one leading to the **home page (`index.php`)** and another to the **data display page (`Display_Edit.php`)**. The links are separated by a small space and followed by line breaks for visual spacing.

In essence:  *It’s a minimalist navigation bar that helps users hop between the homepage and the dog data management page.*

```html
<div>    
    <a href="index.php">Home</a>&nbsp;
    <a href="Display_Edit.php">Display Data</a><br><br>
</div>

```

10/2025

