# PDO - First Data Insert - Car Example



## Key Ideas



### Five Steps Of Inserting Data

1. Create the the insert SQL statement with placeholders (":").
2. Prepare the SQL statement.
3. Save the $_POST data to variables while sanitizing it.
4. Bind the placeholders with the variables of step 3.
5. Execute the SQL statement.



## Connection String

> A database connection string is a string that contains the information needed to connect an application to a database. The string includes parameters such as -  Server instance, Database name, Authentication details, Username, Password .



## dbconnect.php

```php
<!--  dbconnect.php --->
<?php
/*
-- Database - SQL Script
DROP DATABASE IF EXISTS wp_cars;

-- CREATE DATABASE
CREATE DATABASE IF NOT EXISTS wp_cars;

-- Use Database
USE wp_cars;

CREATE TABLE `wp_cars`.`tbl_car`(
    `OwnerFN` VARCHAR(20),
    `OwnerLN` VARCHAR(20),
    `Make` VARCHAR(20),
    `Model` VARCHAR(20),
    `Color` VARCHAR(20),
    `CarYear` CHAR(4),
    `Car_Id` INT(6) NOT NULL AUTO_INCREMENT,
    PRIMARY KEY(`Car_Id`)
) ENGINE = InnoDB;


*/

//connect database
try
{
	$pdo = new PDO('mysql:host=127.0.0.1;dbname=wp_cars','root','');
	$pdo->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);

	//only educational purposes
	$dbstatus = "Good database connection";

}
catch(PDOException $e)
{
	$dbstatus = "Database connection failed<br>".
				$e->getMessage();

	die();
}
SESSION_START();

?>

```



## default.php

```php
<?php
// page3.php

// require - all or nothing - will not tolerate an error
// include - will still try to run if there is an error

require('dbconnect.php');

// educational purposes / development purposes
echo($dbstatus."<br><hr><br>");

?>
<!DOCTYPE html>
<html>
<head>
	<title>Page 1</title>
	<style>
        .divpage1 {
          width: 50%;	
          background-color:cornsilk;
          margin-left: auto;
          margin-right: auto;
        } 
	</style>
</head>
<body>
<div class="divpage1">     

<?php

if(!isset($_POST['OwnerFN']))
{
    echo('
		<h1>Car Entry - form uses named place holders</h1>
        <form method="POST" action="default.php">
        <table border="1">
            <tr>
                <td>First Name</td>
                <td><input type="text" width="20" name="OwnerFN"
        required value="John"></td>
            </tr>

            <tr>
                <td>Last Name</td>
                <td><input type="text" width="20" name="OwnerLN"
        value="Doe"></td>
            </tr>

            <tr>
                <td>Make</td>
                <td><input type="text" width="20" name="Make"
        value="Ford"></td>
            </tr>

            <tr>
                <td>Model</td>
                <td><input type="text" width="20" name="Model"
        value="F150"></td>
            </tr>

            <tr>
                <td>Year</td>
                <td><input type="text" width="20" name="Year"
        value="1970"></td>
            </tr>

            <tr>
                <td>Color</td>
                <td><input type="text" width="20" name="Color"
        value="Red"></td>
            </tr>

            <tr>
                <td></td>
                <td><input type="submit" value="Enter"></td>
            </tr>

        </table>
        </form>
    ');

    }
    else
    {

        try
        {
        //Step 1 - create sql statement

        $sql_insert = "INSERT INTO tbl_car"
                ."(OwnerFN,OwnerLN,Make,Model,CarYear,Color) "
                ."VALUES(:OwnerFN,:OwnerLN,:Make,:Model,:Year,:Color)";

        //Step 2 - prepare our sql statement
        //This will box our information at the ":" placeholders

        $sqlp_insert = $pdo->prepare($sql_insert);


        //Step 3 - Sanitize the information from
        //from the input boxes using filter_var
        //other types of filters 
        //http://php.net/manual/en/filter.filters.sanitize.php

        $OwnerFN = filter_var($_POST['OwnerFN'], FILTER_SANITIZE_STRING);
        $OwnerLN = filter_var($_POST['OwnerLN'], FILTER_SANITIZE_STRING);
        $Make = filter_var($_POST['Make'], FILTER_SANITIZE_STRING);
        $Model = filter_var($_POST['Model'], FILTER_SANITIZE_STRING);
        $Year = filter_var($_POST['Year'], FILTER_SANITIZE_STRING);
        $Color = filter_var($_POST['Color'], FILTER_SANITIZE_STRING);

        //Step 4 - bind our boxes in the sql statement with our variables
        //bind parameters
        $sqlp_insert->bindparam(":OwnerFN",$OwnerFN);
        $sqlp_insert->bindparam(":OwnerLN",$OwnerLN);
        $sqlp_insert->bindparam(":Make",$Make);
        $sqlp_insert->bindparam(":Model",$Model);
        $sqlp_insert->bindparam(":Year",$Year);
        $sqlp_insert->bindparam(":Color",$Color);


        //Step 5 - Execute the query
        $sqlp_insert->execute();

        echo("<br>### input was successful ###<br><br><hr><br>");

        //-------------------------------------------------


        //Display our last car entered

        $sql_selectLastCar = 	"SELECT * " .
                        "FROM tbl_car " .
                        "WHERE Car_Id = (SELECT MAX(Car_Id) ".
        "FROM tbl_car )";

        //Run the Query
        $dataSet = $pdo->query($sql_selectLastCar);

        //loop through the columns in the row
        foreach($dataSet as $row)
        {
        echo($row['OwnerFN']." ".$row['OwnerLN']."<br>");
        echo($row['Make']." ".$row['Model']." ".$row['CarYear']."<br>");
        echo($row['Color']." ".$row['Car_Id']."<br><hr><br>");
        }

        //need to clear the $_POST because of the isset in if statement
        unset($_POST['OwnerFN']);
    }
    catch(PDOException $e)
    {
        echo("**** Input Error ****<br>".$e);
    }

    //add a button so we can add another car
    echo('<a href="default.php"><button type="button">'.
    'Add Another Car</button>');

}
?>
<br><hr><br>
    <br><a href="default.php"><button type="button">Home</button></a>&nbsp;&nbsp;
    <a href="page2.php"><button type="button">Page 2</button></a>&nbsp;&nbsp;
    <a href="page3.php"><button type="button">Page 3</button></a>&nbsp;&nbsp;
<br><br><br>
</div>
</body>
</html>
```



## Page2.php

```php
<?php
	// page2.php
	require('dbconnect.php');
?>
<!DOCTYPE html>
<html>
<head>
	<title>Inventory</title>
	<style>
        #div1 {
          width: 75%;	
          background-color:cornsilk;
          margin-left: auto;
          margin-right: auto;
        } 
	</style>
</head>
<body>
<div id="div1">
	<H1>Car Inventory</H1>

	<table align="center" border="1">
	<tr>
		<td>First Name</td>
		<td>Last Name</td>
		<td>Make</td>
		<td>Model</td>
		<td>Year</td>
		<td>Color</td>
		<td>Car_Id</td>
	</tr>
	<?php
		$sql = "SELECT * FROM tbl_car";
		$ds = $pdo->query($sql);

		foreach($ds as $row)
		{		
			echo('<tr>');
			echo('
				<td>'.$row['OwnerFN'].'</td>
				<td>'.$row['OwnerLN'].'</td>
				<td>'.$row['Make'].'</td>
				<td>'.$row['Model'].'</td>
				<td>'.$row['CarYear'].'</td>
				<td>'.$row['Color'].'</td>
				<td>'.$row['Car_Id'].'</td>
				');
			echo('</tr>');
}
	?>
	</table>


<br><hr><br>
    <br><a href="default.php"><button type="button">Home</button></a>&nbsp;&nbsp;
    <a href="page2.php"><button type="button">Page 2</button></a>&nbsp;&nbsp;
    <a href="page3.php"><button type="button">Page 3</button></a>&nbsp;&nbsp;
<br><br><br>
</div>
</body>
</html>

```



```php
<?php
// page3.php

// require - all or nothing - will not tolerate an error
// include - will still try to run if there is an error

require('dbconnect.php');

// educational purposes / development purposes
echo($dbstatus."<br><hr><br>");

?>
<!DOCTYPE html>
<html>
<head>
	<title>Page 3</title>
	<style>
        .divpage3 {
          width: 75%;	
          background-color:cornsilk;
          margin-left: auto;
          margin-right: auto;
        } 
	</style>
</head>
<body>
<div class="divpage3">      
<?php
  
if(!isset($_POST['OwnerFN']))
{
    echo('
    <h1>Car Entry - form uses ? for place holders</h1>
    <form method="POST" action="page3.php">
    <table border="1" align="center">
        <tr>
            <td>First Name</td>
            <td><input type="text" width="20" name="OwnerFN" required value="Roger"></td>
        </tr>
        <tr>
            <td>Last Name</td>
            <td><input type="text" width="20" name="OwnerLN" value="Smith"></td>
        </tr>
        <tr>
            <td>Make</td>
            <td><input type="text" width="20" name="Make" required value="AMC"></td>
        </tr>
        <tr>
            <td>Model</td>
            <td><input type="text" width="20" name="Model" required value="Gremlin"></td>
        </tr>
        <tr>
            <td>Year</td>
            <td><input type="text" width="20" name="CarYear" required value="1970"></td>
        </tr>
        <tr>
            <td>Color</td>
            <td><input type="text" width="20" name="Color" required value="Green"></td>
        </tr>
        <tr>
            <td></td>
            <td><input type="submit" value="Enter"></td>
        </tr>
    </table>
    </form>
    ');

}
else
{
    echo('');
	print_r($_POST);
	echo("<br><hr><br>");
	try
	{
	//Step 1 - create sql statement
	$sql_Insert =  	"INSERT INTO tbl_car".
				"(OwnerFN,OwnerLN,Make,Model,CarYear,Color) ".
				"VALUES(?,?,?,?,?,?)";

	//Step2 - prepare our sql statement
	//This will box our information at the ":" placeholders

	$sql_Insert =  $pdo->prepare($sql_Insert);


	//Step 3 - Sanitize the information
	// use filter_var
	$OwnerFN = filter_var($_POST['OwnerFN'],FILTER_SANITIZE_STRING);
	$OwnerLN = filter_var($_POST['OwnerLN'],FILTER_SANITIZE_STRING);
	$Make = filter_var($_POST['Make'],FILTER_SANITIZE_STRING);
	$Model = filter_var($_POST['Model'],FILTER_SANITIZE_STRING);
	$CarYear = filter_var($_POST['CarYear'],FILTER_SANITIZE_STRING);
	$Color = filter_var($_POST['Color'],FILTER_SANITIZE_STRING);



	//Step 4 - Bind our placeholders to our clean variables

	// 
	// $sql_Insert->bindparam(1,$OwnerFN);
	// $sql_Insert->bindparam(2,$OwnerLN);
	// $sql_Insert->bindparam(3,$Make);
	// $sql_Insert->bindparam(4,$Model);
	// $sql_Insert->bindparam(5,$CarYear);
	// $sql_Insert->bindparam(6,$Color);
	
	$data = array($_POST['OwnerFN'],
				$_POST['OwnerLN'],
				$_POST['Make'],
				$_POST['Model'],
				$_POST['CarYear'],
				$_POST['Color'],);
	
	$data = array($OwnerFN,$OwnerLN,$Make,$Model,$CarYear,$Color);
	

	//Step 5 - Execute the SQL Statement
	$sql_Insert->execute($data);
	//$sql_Insert->execute();
	echo("<br>### input was successful # # # <br><hr><br>");

	// ---------------------------------------------

	$sql_SelectLastCar = 	
        			"SELECT * ".
					"FROM tbl_car ".
					"WHERE Car_Id = ".
					"(SELECT MAX(Car_Id) FROM tbl_car) ";

	// run the query
	$dataSet = $pdo->query($sql_SelectLastCar);

	// loop the columns
	foreach($dataSet as $row)
	{
	echo($row['OwnerFN']." ".$row['OwnerLN']."<br>");
	echo($row['Make']." ".$row['Model']." ".$row['CarYear']."<br>");
	echo($row['Color']." ".$row['Car_Id']."<br>");
	}

	//-----------------------------------------------

	unset($_POST);

	}
	catch(PDOExcept $eio)
	{
		echo("**** Input Error<br>".$eio);
	}
	
	// add a button
	echo('<a href="default.php"><button type="button">'.
'Add Another Car</button></a>');


}
?>
<br><hr><br>
    <br><a href="default.php"><button type="button">Home</button></a>&nbsp;&nbsp;
    <a href="page2.php"><button type="button">Page 2</button></a>&nbsp;&nbsp;
    <a href="page3.php"><button type="button">Page 3</button></a>&nbsp;&nbsp;
<br><br><br>
</div>
</body>
</html>
```

