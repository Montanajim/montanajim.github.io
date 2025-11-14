# Session Variable Homework Assignment Hint





## index.php

```html
<html>
<head>
<?php
session_start();
?>
</head>
<body>
<?php
	print_r($_SESSION);
	echo('<br><hr><br>');
?>

<form action="page2.php" method="POST">
<table>
		
		<tr>
		<td>First Name</td>
		<td><input type="text" name="fName"></td>
		</tr>
		
		<tr>
		<td>Last Name</td>
		<td><input type="text" name="lName"></td>
		<tr>
		
		<td></td>
		<td><input type="submit" name="submit" value="Submit">
		</td>
		</tr>
		
		</table>
		</form>
		
		<br>
		<a href="page2.php">Page2</a>

</body>
</html>
```



## page2.php

```php
<html>
<head>
<title>page2</title>
<?php
	session_start();
?>
</head>
<body>

<?php
	print_r($_SESSION);
	echo('<br><hr><br>');
	print_r($_POST);
	echo('<br><hr><br>');
	
	//1 need to see if there is an array in the session variable
	//  if not, then we create one.
	
	if(isset($_SESSION['arrPlayer']))
	{
		// we have an session variable array 
		// that is keep track of names
		array_push($_SESSION['arrPlayer'],$_POST['fName']);
		array_push($_SESSION['arrPlayer'],$_POST['lName']);
	}
	else
	{
		//There is no array in the session variable
		// so we create one
		
		// create an array
		$arrPlayer = array($_POST['fName'],$_POST['lName']);
		
		// add it to the session variable
		$_SESSION['arrPlayer']=$arrPlayer;
	}

	echo('<br><h1>Session contents</h1><br>');
	// NOTE in this example we only have 2 items fname, lname
	$xcntr = 0;
	
	for($c = 0; $c < count($_SESSION['arrPlayer']); $c++)
	{
		echo($_SESSION['arrPlayer'][$c]." ");
		
		$xcntr = $xcntr+1;
		// in this example we have two items
		// when the xcntr gets to 2
		// when enter a new line and reset the xcntr
		// back to 0
		if($xcntr == 2)
		{
			echo("<br>");
			$xcntr=0;
		}
	}

?>
<br><hr><br>
<a href="index.php">Home</a>
</body>
</html>
