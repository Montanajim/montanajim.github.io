# First Forms - POST and GET



## Key Ideas

* POST and GET
* isset()
* empty()
* print_r() and var_dump()
* Use isset() and empty() to write a submit and POST on one PHP page



```{admonition} Definition - GET
__GET__ is used to request data from a specified resource. Note that the query string (name/value pairs) is sent in the URL of a GET request:

demo_form.php?name1=value1&name2=value2

https://www.w3schools.com/tags/ref_httpmethods.asp
```

**Some notes on GET requests:**

- GET requests can be cached

- GET requests remain in the browser history

- GET requests can be bookmarked

- GET requests should never be used when dealing with sensitive data

- GET requests have length restrictions

- GET requests are only used to request data (not modify)

  https://www.w3schools.com/tags/ref_httpmethods.asp



```{admonition} Definition - POST
__POST__ is used to send data to a server to create/update a resource.

The data sent to the server with POST is stored in the request body of the HTTP request:
https://www.w3schools.com/tags/ref_httpmethods.asp
```



**Some notes on POST requests:**

- POST requests are never cached
- POST requests do not remain in the browser history
- POST requests cannot be bookmarked
- POST requests have no restrictions on data length

https://www.w3schools.com/tags/ref_httpmethods.asp



## Code Examples



```{mermaid}
flowchart TD
A[Home page\nindex.html] --> B[Form1\nform1.html]
A --> C[Form2\nform2.html]
A --> D[Form & Results\nForm3.php]
A --> E[Form & Results\nForm4.php]
B --> B1[Form Results\nform1a.php]
C --> C1[Form Results\nform2a.php]
```

### Home Page - index.html

```html
<!-- index.html -->
<html>
<head>
<title>Home Page</title>

</head>
<body>
<h1>POST and GET Examples</h1>

<a href="form1.html">Form 1</a><br>
<a href="form2.html">Form 2</a><br>
<a href="form3.php">Form 3</a><br>
<a href="form4.php">Form 4</a><br>

</body>
</html>

```



### First Form - form1.html

```html
<!-- form1.html -–>
<!DOCTYPE html>
<html>
<head>
<title>Home Page</title>

</head>
<body>

<h1>Form 1</h1>

	<form action="form1a.php" method="POST">
	<table border="1">
		<tr>
		<td>Name</td>
		<td><input type="text" name="stuName" value="Bubba"></td>
		</tr>

		<tr>
		<td>Major</td>
		<td><input type="text" name="stuMajor" value="Whisky Making"></td>
		</tr>


		<tr>
		<td></td>
		<td><input type="submit" value="Click Me"></td>
		</tr>

	</table>
	</form>
</body>
</html>

```

### Results from Form1 - form1a.php

```php
<!-- form1a.php -->
<html>
<head>
<title>Form1a</title>
</head>
<body>

<h1> Results from form1</h1>

<?php
    echo("var dump<br>");
    var_dump($_POST);

    echo("<br><hr><br>");

    print_r($_POST);

    echo("<br><hr><br>");

    echo("<br>Hello ".$_POST['stuName']."<br>");
    echo("Your major is ".$_POST['stuMajor']."<br>");

?>

<br><br>
<a href="index.html">Home</a>
</body>
</html>

```



### Form2 (GET) - form1.html

```html
<!-- form2.html -->
<!DOCTYPE html>
<html>
<head>
<title>Home Page</title>

</head>
<body>

<h1>Form 2</h1>

	<form action="form2a.php" method="GET">
	<table border="1">
		<tr>
		<td>Name</td>
		<td><input type="text" name="stuName" value="Brandy">
		</td>
		</tr>

		<tr>
		<td>Major</td>
		<td><input type="text" name="stuMajor" value="Wine Making"></td>
		</tr>


		<tr>
		<td></td>
		<td><input type="submit" value="Click Me"></td>
		</tr>

	</table>
	</form>
</body>
</html>

```

### Results - form2a.php

```php
<!-- form2a.php -->
<html>
<head>
<title>Form2a</title>
</head>
<body>

<h1> Results from form2a</h1>

<?php
    echo("var dump<br>");
    var_dump($_GET);

    echo("<br><hr><br>");

    print_r($_GET);

    echo("<br><hr><br>");

    echo("<br>Hello ".$_GET['stuName']."<br>");
    echo("Your major is ".$_GET['stuMajor']."<br>");
?>

<br><br>
<a href="index.html">Home</a>
</body>
</html>

```



### Form and Results - _isset()_ and _empty_ - form3.php

```php
<!-- form3.php -->
<!DOCTYPE html>
<html>
<head>
<title>Form 3</title>

</head>
<body>

<h1>Form 3</h1>

	<form action="form3.php" method="POST">
	<table border="1">
		<tr>
            <td>Name</td>
            <td><input type="text" name="stuName" value="Joe"></td>
		</tr>

		<tr>
            <td>Major</td>
            <td><input type="text" name="stuMajor" value="Bagpipe Making"></td>
		</tr>


		<tr>
            <td></td>
            <td><input type="submit" value="Click Me"></td>
		</tr>

	</table>
	</form>
    
    <?php
        echo("var dump<br>");
        var_dump($_POST);

        echo("<br><hr><br>");

        print_r($_POST);

        echo("<br><hr><br>");

        echo("<h3>isset</h3>");
        if(isset($_POST['stuName']))
        {
            echo("<br>Hello ".$_POST['stuName']."<br>");
            echo("Your major is ".$_POST['stuMajor']."<br>");
        }

        echo("<br><hr><br>");

        echo("<h3>Not Empty</h3>");
        if(!empty($_POST['stuName']))
        {
            echo("<br>Hello ".$_POST['stuName']."<br>");
            echo("Your major is ".$_POST['stuMajor']."<br>");
        }

    ?>

<a href="index.html">Home</a>
</body>
</html>

```



### Form4 - form4.php

This is the standard format for doing PHP pages with one page.

```php
<!-- form4.php -->

<!DOCTYPE html>
<html>
<head>
<title>Form 4</title>
</head>
<body>

<?php

if(!isset($_POST['stuName']) || empty($_POST['stuName'])){
    echo('
    <form action="form4.php" method="POST">
        <table border="1">
            <tr>
                <td>Name</td>
                <td><input type="text" name="stuName" value="Randy"></td>
            </tr>

            <tr>
                <td>Major</td>
                <td><input type="text" name="stuMajor" value="Basket Weaving"></td>
            </tr>


            <tr>
                <td></td>
                <td><input type="submit" value="Click Me"></td>
            </tr>
        </table>
        </form>
    ');
}
else
{
    echo("<br>Hello ".$_POST['stuName']."<br>");
    echo("Your major is ".$_POST['stuMajor']."<br>");
}
?>

<a href="index.html">Home</a>
</body>
</html>

```

<div style="page-break-after: always; break-after: page;"></div>
