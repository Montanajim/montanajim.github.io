# String Sanitation - filter_var()

This code demonstrates the different sanitation conditions. 

In order to see the htmlspecialcharacters,  you must look at the source code.  There one will see that the special characters have been encoded. 



# Lecture Code

```php
<!DOCTYPE html>
<html>
<head>
<title>PHP Sanitization</title>

    <style>
        main,header,footer{
            margin-left: auto;
            margin-right: auto;
            width: 80%;
        }
    </style>
</head>
<body>

  <header>
    <h1>Sanitization Examples</h1>
  </header>

  <main>

  <!-- --------------------------------------------- -->

  <?php


$testString = "ASDasd1234.99!@#$%^&*()_+-,./\";\'<>?:[]{}\|`~ ";
$testString2 = "<h1><p>This is a test</p></h1>";
$testString_Int = "+- 123,456,789";
$testString_Float = "+- 123,456,789.8899";

echo('<font face="Courier New">');

echo('<h2>');
echo("Test Strings<br>");
echo($testString."<br>");
echo($testString_Int."<br>");
echo($testString_Float."<br>");
$test1 = $testString;
$space = "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";

echo('<br><hr><br>');
echo(" FILTER_SANITIZE_EMAIL<br>");
$test1 = filter_var($test1,FILTER_SANITIZE_EMAIL);
echo($testString.'<br>');
echo($test1.$space."  ");
echo('<br><hr><br>');


$test1 = $testString_Float;
echo('FILTER_SANITIZE_NUMBER_FLOAT<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_NUMBER_FLOAT);
echo($testString_Float.'<br>');
echo($test1.$space." ");
echo('<br><hr><br>');

$test1 = $testString_Float;
echo('FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_THOUSAND<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_NUMBER_FLOAT,FILTER_FLAG_ALLOW_THOUSAND);
echo($testString_Float.'<br>');
echo($test1.$space." ");
echo('<br><hr><br>');

$test1 = $testString_Float;
echo('FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_FRACTION<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_NUMBER_FLOAT,FILTER_FLAG_ALLOW_FRACTION);
echo($testString_Float.'<br>');
echo($test1.$space." ");
echo('<br><hr><br>');

$test1 = $testString_Float;
echo('FILTER_SANITIZE_NUMBER_FLOAT, 
        FILTER_FLAG_ALLOW_THOUSAND | FILTER_FLAG_ALLOW_FRACTION<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_NUMBER_FLOAT,
                    FILTER_FLAG_ALLOW_THOUSAND | FILTER_FLAG_ALLOW_FRACTION);
echo($testString_Float.'<br>');
echo($test1.$space." ");
echo('<br><hr><br>');

$test1 = $testString_Int;
echo('FILTER_SANITIZE_NUMBER_INT<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_NUMBER_INT);
echo($testString_Int.'<br>');
echo($test1.$space."  ");
echo('<br><hr><br>');



$test1 = $testString;
echo('FILTER_SANITIZE_SPECIAL_CHARS<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_SPECIAL_CHARS,
                array('flags'=>  FILTER_FLAG_STRIP_HIGH  ));
echo($testString.'<br>');
echo($test1.$space."  ");
echo('<br><hr><br>');

$test1 = $testString;
echo('FILTER_SANITIZE_STRING<br>');
$test1 = filter_var($test1,FILTER_SANITIZE_STRING);
echo($testString.'<br>');
echo($test1.$space."  ");
echo('<br><hr><br>');
//echo('<br><br><hr><br>');

$test1 = $testString;
echo('<br>');
$test1 = htmlspecialchars($test1,ENT_COMPAT);
//$test1 = filter_var($test1,FILTER_SANITIZE_STRING);
echo($test1.$space." htmlspecialchars");


echo('</h2>');
echo('</font');

?>

 <!-- --------------------------------------------- -->
  </main>

  <footer>
    <p>&copy; 2023 Jim Goudy</p>
  </footer>

</body>
</html>
```



## Output

### Sanitization Examples

Test Strings
ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~
+- 123,456,789
+- 123,456,789.8899


FILTER_SANITIZE_EMAIL
ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~
ASDasd1234.99!@#$%^&*_+-.'?[]{}|`~   

FILTER_SANITIZE_NUMBER_FLOAT
+- 123,456,789.8899
+-1234567898899   

FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_THOUSAND
+- 123,456,789.8899
+-123,456,7898899   

FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_FRACTION
+- 123,456,789.8899
+-123456789.8899   

FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_THOUSAND | FILTER_FLAG_ALLOW_FRACTION
+- 123,456,789.8899
+-123,456,789.8899   

FILTER_SANITIZE_NUMBER_INT
+- 123,456,789
+-123456789   

FILTER_SANITIZE_SPECIAL_CHARS
ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~
ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~    

FILTER_SANITIZE_STRING
ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~
ASDasd1234.99!@#$%^&*()_+-,./";\'?:[]{}\|`~    


ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~    htmlspecialchars

©  Jim Goudy