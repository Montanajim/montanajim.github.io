# PHP Basics



## Starting out

 PHP files are run on the server. In Apache the are usually placed in a folder within the HTDOCS folder.

 PHP code is placed between the 

```php
 <?php

   ....

  ?>
```

 This can be placed anywhere - in the head or body and multiple times



##  Syntax

-  Statements end with ;
-  PHP statements, key words, classes etc are NOT case sensitive
-  Variables **_are_** case sensitive



## Comments 

``` php
//  single line
# single line
    
/* multiple line
Comments
*/

```



## Variables

-  Start with $

-  Followed by a letter or underscore 

-  Cannot start with a number

-  Variables are case sensitive

-  No special characters except for underscore _

-  Variables are created  when a value is assigned to it

- VARIABLES ARE LOOSELY TYPE

  - They can hold anything

  ```php
  $salary = 20000;
  $_salary = 1000000;
  ```



## Constant

```php
//Note constants do not use $ and the convention is to use all caps
//use the define command

        define('PI', 3.1415);
        define('CODEGURU', "Jim Goudy");

```



## Variable Scope - Local

```php
<?php
 // The variable can only be accessed within the function   
    
function myfunc()
{
	$x=42; 			//local scope
	echo (“This is value x is $x”);	//note that the variable is within the string
}

myfunc();
?>

```



## Variable Scope - Global

```php
<?php
// The variable can only be accessed from outside the function

//global scope
$x=42; 				

function myfunc()
{
    //note that the variable is within the string
	echo “This is value x is $x”;	
}

myfunc();
?>

Global is also a keyword - supervariable

```



## Variable Scope - Static

The variable will retain its value after it's been called by a function.

Usually when a function is called the variables are cleared and reinitialized

```php
<?php

function myfunc2()

{

 static $xx=42;  //local scope

 echo “This is value x is $x”; //note that the variable is within the string

$xx = $xx + 100;

echo("<br>This is value x is $xx<br><hr><br>");

}

myfunc2();

myfunc2();

?>
    
```



