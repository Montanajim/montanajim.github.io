# PHP Arrays

## Key ideas

* array()
* count()
* Array Positions
* Printing arrays via for statement
* Associative arrays
* var_dump()
* print_r()
* sorting
  * sort()
  * rsort()
  * asort()
  * arsort()
  * ksort()
  * krsort()



## Lecture Code

```php
<?php
// Arrays

//Some data
$myVar = 42;

//--------------- Create An Array ------------------------------
echo "<br><br><hr><br><br>";

// Note that we declare array using the array keyword
// Also, since PHP is loosely typed, we can store any type of 
// data in the array.  Notice how we have strings, numbers and 
// a variable in the same array. 

$arrayName = array("Hitch Hikers Guide", 3, $myVar);

//Get the actual number of elements using the count function
echo "Count of array elements<br>".count($arrayName); 			//display the count on screen
$arrayCount = count($arrayName);	//Store the count in a variable


//---------------Access Array Data By Element Number ----------
echo "<br><br><hr><br><br>";

//print the elements of the array by specific element
echo $arrayName[0]."<br>";
echo $arrayName[1]."<br>";
echo $arrayName[2]."<br>";


//---------- Check To See If Variable Is An Array--------------
echo "<br><br><hr><br><br>";
echo "Check if variable is array<br><br>";
///check if the variable is an array
if(is_array($arrayName))
{
	echo(" is an array<br><br>");
}
else
{
	echo(" is not an array<br><br>");
}
echo "<br><br><hr><br><br>";

//Print the array in a for loop
for ($cnt = 0; $cnt < $arrayCount; $cnt++ )
{
	echo ("*".$arrayName[$cnt]."<br>");
}


//---------- Create an associative array  ---------------------
echo "<br><br><hr><br><br>";
$asscArray = array("key1" => "the first element",
					  "key2" => "the second element",
					  "key3" => "the third element");
//add a new key and value to $asscArray
$asscArray["bubba"] = 1000;					  


//access data via key value					  
echo ($asscArray["key1"]."<br>");
echo ($asscArray['key3']."<br>");
echo ($asscArray["key2"]."<br>");
echo ($asscArray["bubba"]."<br>");


//print associative array via a foreach loop
foreach($asscArray as $xkey => $xvalue)
{
	echo ($xkey." --- ".$xvalue."<br>");
}

//print associative array via a foreach loop as a table
echo("<table border = 2>");
foreach($asscArray as $xkey => $xvalue)
{
	echo ("<tr><td>".$xkey."</td><td>".$xvalue."</td></tr>");
}
echo("</table>");


//--------- Create A Two Dimensional Array ------------------------------------------
$product  = array(array("S6E",1250,6),
				  array("S6A", 900,6),
				  array("S5",  500, 5.7),
				  array("S4",   80, 5)
				  );
				  
echo ("<br><hr><br>Access Array Data Via Element Number<br><br>");
echo ($product[0][0]." costs $".$product[0][1]." screen = ". $product[0][2]."<br>" );
echo ($product[1][0]." costs $".$product[1][1]." screen = ". $product[1][2]."<br>" );
echo ($product[2][0]." costs $".$product[2][1]." screen = ". $product[2][2]."<br>" );
echo ($product[3][0]." costs $".$product[3][1]." screen = ". $product[3][2]."<br>" );


//Print the two dimensional array using two FOR loops
echo("<br><br>Loop<br><br>");
echo("<table border=1>");
for($row = 0; $row < 4; $row++)
{
	echo("<tr>");
	for($col = 0;$col < 3; $col++)
	{
		echo ("<td>".$product[$row][$col]."</td>" );
	}
	echo("</tr>");

}
echo("</table>");

//-----------  Create A 2 Dimensional Associative Array  --------------------------------
echo("<br><br>Multi Associative<br><br>");
$product2  = array(array("Model"=>"S6E","Price"=>1250,"Screen"=>6),
				  array("Model"=>"S6A","Price"=> 900,"Screen"=>6),
				  array("Model"=>"S5", "Price"=> 500, "Screen"=>5.7),
				  array("Model"=>"S4", "Price"=>  80, "Screen"=>5)
				  );

				  
//Print 2 Dimensional Array Using For Loop
for($row = 0;$row < 4; $row++)
{
	echo($product2[$row]["Model"]." -- ".$product2[$row]["Price"]." -- ".
		$product2[$row]["Screen"]." <br>");
}

//Print 2 Dimensional Array Using For Loop As A Table
echo("<br><br>");
echo("<table border=1>");
for($row = 0;$row < 4; $row++)
{
	echo("<tr>");
	echo("<td>".$product2[$row]["Model"]."</td><td>".$product2[$row]["Price"]."</td><td>".
		$product2[$row]["Screen"]." </td>");
	echo("</tr>");
}
echo("</table>");

echo ("<br><br><br><br><br>");


//---------------------   Sorting  --------------------------------------------
//Create Sample Array for sorting
$array3 = array(42, 3, 54, 9, 88, 6, 33, 2, 11, 1);

//print the array with var_dump - shows array, data and data types
var_dump($array3);
echo("<br><br>");

//print the array using print_r - shows the array and the values in the array
print_r($array3);
echo("<br><br>");

//print the array using a for statement
for($i = 0; $i < count($array3); $i++)
{
	echo ($array3[$i]."&nbsp;&nbsp;");
}

//Sort the array
sort($array3);

echo("<br><br>");
//print out the array
for($i = 0; $i < count($array3); $i++)
{
	echo ($array3[$i]."&nbsp;&nbsp;");
}

//Reverse the array sort
rsort($array3);

echo("<br><br>");

//Print the reverse display
for($i = 0; $i < count($array3); $i++)
{
	echo ($array3[$i]."&nbsp;&nbsp;");
}

echo("<br><br><br><br>");
$product3  = array(array("Model"=>"X6E","Price"=>1250,"Screen"=>6),
				  array("Model"=>"S6A","Price"=> 900,"Screen"=>6),
				  array("Model"=>"J5B", "Price"=> 500, "Screen"=>5.7),
				  array("Model"=>"A4C", "Price"=>  80, "Screen"=>5)
				  );


$product3  = array(	"X6E"=>1250,
					"S6A"=> 300,
					"J5B"=> 500,
					"A4C"=>  80
				  );

				  
asort($product3);
				
echo("<br><br>Associative Array - value sort<br><br>");
echo("<table border = 2>");
foreach($product3 as $xkey => $xvalue)
{
	echo ("<tr><td>".$xkey."</td><td>".$xvalue."</td></tr>");
}
echo("</table>");

arsort($product3);
				
echo("<br><br>Associative Array - value Reverse sort<br><br>");
echo("<table border = 2>");
foreach($product3 as $xkey => $xvalue)
{
	echo ("<tr><td>".$xkey."</td><td>".$xvalue."</td></tr>");
}
echo("</table>");

//zzzzzzzzzzzzzzzzz
ksort($product3);
				
echo("<br><br>Associative Array - key sort<br><br>");
echo("<table border = 2>");
foreach($product3 as $xkey => $xvalue)
{
	echo ("<tr><td>".$xkey."</td><td>".$xvalue."</td></tr>");
}
echo("</table>");

krsort($product3);
				
echo("<br><br>Associative Array - key reverse sort<br><br>");
echo("<table border = 2>");
foreach($product3 as $xkey => $xvalue)
{
	echo ("<tr><td>".$xkey."</td><td>".$xvalue."</td></tr>");
}
echo("</table>");
echo ("<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>");
?>

```

