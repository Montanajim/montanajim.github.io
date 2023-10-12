# PDO With No Named Placeholders

This example shows how to use SQL with no named placeholders.

```php+HTML
<!DOCTYPE html>
<html>
<head>
<title>function example</title>

	<!-- css styling -->
	<style>
		#div1{
			background-color:cornsilk;
			width:65%;
			margin-left:auto;
			margin-right:auto;
		}
	</style>

</head>
<body>
    <?php

        //database connection
        function newDB(){
            //returns a database object
            return new PDO('mysql:host=127.0.0.1;dbname=wp_cars','root','');
        }

        function pdoInsert(){

            // open new datbase connection
            $pdo = newDB();

            // instantiate variables
            // remember the don't come into existance
            // until a value has been assigned to them

            $ownerFN 	= "Bubba";
            $ownerLN	= "Smith";
            $make		= "Scion";
            $model		= "XB";
            $carYear	= rand(2000,2012);
            $color		= "Blue";

            try
            {
                // SQL Statement
                $sql_stmt = "INSERT INTO tbl_car(OwnerFN,OwnerLN,make,model,carYear,color) 
                        VALUES (?,?,?,?,?,?)";

                // prepare
                $pdo = $pdo->prepare($sql_stmt);

                // bind our parameters
                $pdo->bindParam(1,$ownerFN);
                $pdo->bindParam(2,$ownerLN);
                $pdo->bindParam(3,$make);
                $pdo->bindParam(4,$model);
                $pdo->bindParam(5,$carYear);
                $pdo->bindParam(6,$color);

                // generate some database
                // normally where you assign $_POST variable
                // which has been sanitized to variable

                // for this example auto generate some database

                $numRecs = rand(5,10);

                for($i = 0; $i < $numRecs; $i++)
                {
                    $arn 		= rand(0,1000);

                    // normally the $_POST variable is 
                    // sanitized and assigned a local variable

                    // $ownerFN = filter_var($_POST['ownerFN'],FILTER_SANITIZE_STRING);

                    $ownerFN 	= "Bubba".$arn;
                    $ownerLN 	= "Smith".$arn;
                    $make 		= "Ford".$arn;
                    $model 		= "Mach E".$arn;
                    $carYear 	= rand(2020,2024);
                    $color 		= "red";

                    // since the variables are already bound
                    // we can just call execute()

                    $pdo->execute();
                }

            }
            catch(PDOException $epdo)
            {
                // In production, errors be redirect to an error page
                echo($pdo->getMessage());
            }

            // always closse our connection
            $pdo = null;
        }

        function printCarTable(){
            
            echo('
            <div id="div1">
            <h1>Car Table</h1>
            <a href="default.php">
                <button type="Button">Refresh</button>
                </a><br><br>
            <table border="1" width="100%" align="center">
                <tr>
                    <td>Owner FN</td>
                    <td>Owner LN</td>
                    <td>Make</td>
                    <td>Model</td>
                    <td>Car Year</td>
                    <td>Color</td>
                    <td>Car ID</td>				
                </tr>
            ');

            // create a database connection
            $pdo = newDB();

            // setup our SQL
            $sql = "SELECT * FROM tbl_car";

            // executing the SQL - bring down the data
            $dataSet = $pdo->query($sql);

            // iterate through each dataSet row
            foreach($dataSet as $row)
            {
                echo('<tr>');
                echo('<td>'.$row['OwnerFN'].'</td>'.
                        '<td>'.$row['OwnerLN'].'</td>'.
                        '<td>'.$row['Make'].'</td>'.
                        '<td>'.$row['Model'].'</td>'.
                        '<td>'.$row['CarYear'].'</td>'.
                        '<td>'.$row['Color'].'</td>'.
                        '<td>'.$row['Car_Id'].'</td>'				
                    );
                echo('</tr>');

            }

            echo('</table>
            <br></div><br><br>');

            // close the db connection
            $pdo = null;

        }


        function clearDB()
        {
            try
            {
                // create new database connection
                $pdo = newDB();

                // execute the truncate SQL command
                $pdo->exec("TRUNCATE TABLE tbl_car");

            }
            catch(PDOException $epdo)
            {
                // In production, errors be redirect to an error page
                echo("Error<br>".$epdo->getMessage());
            }

            $pdo = null;
        }

        // function calls

        clearDB();
        pdoInsert();
        printCarTable();

    ?>
</body>
</html>
```

