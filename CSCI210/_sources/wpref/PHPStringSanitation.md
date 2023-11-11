# PHP String Sanitation




PHP string sanitation is the process of removing or encoding malicious characters from a string to prevent them from being executed or displayed unexpectedly. This is an important security measure, as attackers can inject malicious code into strings through user input, cookies, and other sources.

There are a number of ways to sanitize strings in PHP. One common method is to use the `htmlspecialchars()` function. This function encodes special characters, such as `<`, `>`, and `&`, so that they are displayed as text instead of being executed as HTML.

Another way to sanitize strings is to use the `filter_var()` function with the `FILTER_SANITIZE_STRING` filter. This filter removes all characters from the string except for letters, digits, spaces, and a few other common characters.

You can also use regular expressions to sanitize strings. This can be a more complex method, but it gives you more control over the characters that are removed. 

---

## Sanitation Functions



###  htmlspecialchars()

The `htmlspecialchars()` function in PHP is used to convert special characters to HTML entities. This is useful for preventing cross-site scripting (XSS) attacks, which can occur when an attacker injects malicious code into a web page.

The following characters are converted to HTML entities by the `htmlspecialchars()` function:

- & (ampersand) becomes  ```&amp;```

- " (double quote) becomes ```&quot;```

- ' (single quote) becomes ```&apos;```

- < (less than) becomes ```&lt;```

- < (greater than) becomes ```&gt;```

The `htmlspecialchars()` function can also be used to convert other characters to HTML entities, such as the following:

- `\n` (newline) becomes `<br>`
- `\t` (tab) becomes `&nbsp;&nbsp;&nbsp;&nbsp;`

The `htmlspecialchars()` function takes two arguments:

- The string to be converted.
- An optional bitmask of flags that specify how to convert the string.

The following flags can be used with the `htmlspecialchars()` function:

- `ENT_QUOTES`: Convert both double and single quotes to HTML entities.
- `ENT_NOQUOTES`: Do not convert quotes to HTML entities.
- `ENT_SUBSTITUTE`: Replace invalid characters with HTML entities.
- `ENT_HTML401`: Use the HTML 4.01 character set.
- `ENT_XML1`: Use the XML 1.0 character set.

The default value for the bitmask is `ENT_QUOTES | ENT_SUBSTITUTE | ENT_HTML401`.

Here is an example of how to use the `htmlspecialchars()` function:



```php
$string = 'This is a string with special characters: &<>"';

// Convert all special characters to HTML entities.
$encodedString = htmlspecialchars($string);

// stores the following:  'This is a string with special characters: &amp;&lt;&gt;'
```



## filter_var()


The `filter_var()` function in PHP is used to filter a variable with a specified filter. This can be used to validate and sanitize user input, or to convert data from one format to another.

The `filter_var()` function takes two arguments:

- The variable to be filtered.
- The filter to apply.

The filter can be one of the following:

- `FILTER_VALIDATE_INT`: Validates the variable as an integer.
- `FILTER_VALIDATE_FLOAT`: Validates the variable as a floating-point number.
- `FILTER_VALIDATE_BOOLEAN`: Validates the variable as a boolean value.
- `FILTER_VALIDATE_EMAIL`: Validates the variable as an email address.
- `FILTER_VALIDATE_URL`: Validates the variable as a URL.
- `FILTER_SANITIZE_STRING`: Sanitizes the variable by removing all HTML and PHP tags.
- `FILTER_SANITIZE_NUMBER_INT`: Sanitizes the variable by converting it to an integer.
- `FILTER_SANITIZE_NUMBER_FLOAT`: Sanitizes the variable by converting it to a floating-point number.

You can also specify a set of options for the filter. For example, you can specify a minimum and maximum value for the filter. 

---

## PHP Sanitation Flags



###  FILTER_FLAG_STRIP_HIGH | FILTER_FLAG_STRIP_LOW

The `FILTER_FLAG_STRIP_HIGH` and `FILTER_FLAG_STRIP_LOW` flags are used to remove characters from a string based on their ASCII values.

- `FILTER_FLAG_STRIP_HIGH` removes all characters with an ASCII value greater than 127.
- `FILTER_FLAG_STRIP_LOW` removes all characters with an ASCII value less than 32.

These flags are often used to sanitize user input to prevent attacks that exploit non-ASCII characters or control characters.

For example, an attacker could inject a malicious script into a web application by submitting a form with a non-ASCII character or control character in the input field. If the application does not properly sanitize the input, the script could be executed and the attacker could gain control of the application.

The `FILTER_FLAG_STRIP_HIGH` and `FILTER_FLAG_STRIP_LOW` flags can be used to prevent this type of attack by removing all non-ASCII characters and control characters from the user input. However, it is important to note that these flags can also remove legitimate data, such as foreign language characters and control characters that are used in some programming languages.

Here is an example of how to use the `FILTER_FLAG_STRIP_HIGH` and `FILTER_FLAG_STRIP_LOW` flags to sanitize user input:

PHP

```
$input = filter_var($_GET['input'], FILTER_SANITIZE_STRING, FILTER_FLAG_STRIP_HIGH | FILTER_FLAG_STRIP_LOW);
```

This code will sanitize the variable `$_GET['input']` and remove all non-ASCII characters and control characters. The sanitized input will then be stored in the variable `$input`.

It is important to note that the `FILTER_FLAG_STRIP_HIGH` and `FILTER_FLAG_STRIP_LOW` flags are not a replacement for input validation. You should always validate user input before sanitizing it. This will help to ensure that the input is valid and that it cannot be used to exploit your application. (AIBRDJG)



### FILTER_FLAG_ENCODE_LOW | FILTER_FLAG_ENCODE_HIGH

The `FILTER_FLAG_ENCODE_LOW` and `FILTER_FLAG_ENCODE_HIGH` flags are used to encode characters in a string based on their ASCII values.

- `FILTER_FLAG_ENCODE_LOW` encodes all characters with an ASCII value less than 32.
- `FILTER_FLAG_ENCODE_HIGH` encodes all characters with an ASCII value greater than 127.

These flags are often used to sanitize user input to prevent attacks that exploit control characters or non-ASCII characters.

For example, an attacker could inject a malicious script into a web application by submitting a form with a control character or non-ASCII character in the input field. If the application does not properly sanitize the input, the script could be executed and the attacker could gain control of the application.

The FILTER_FLAG_ENCODE_LOW and FILTER_FLAG_ENCODE_HIGH flags can be used to prevent this type of attack by encoding all control characters and non-ASCII characters in the user input. However, it is important to note that these flags can also encode legitimate data, such as foreign language characters and control characters that are used in some programming languages.  (AIBRDJG)

```php
// Encode all control characters and non-ASCII characters in a string.
$encodedString = filter_var($string, FILTER_SANITIZE_STRING, FILTER_FLAG_ENCODE_LOW | FILTER_FLAG_ENCODE_HIGH);
```



### FILTER_FLAG_ALLOW_FRACTION  | FILTER_FLAG_ALLOW_THOUSAND  | FILTER_FLAG_ALLOW_SCIENTIFIC


The `FILTER_FLAG_ALLOW_FRACTION`, `FILTER_FLAG_ALLOW_THOUSAND`, and `FILTER_FLAG_ALLOW_SCIENTIFIC` flags are used to control the validation and sanitation of numbers in PHP.

- `FILTER_FLAG_ALLOW_FRACTION` allows decimal points in numbers.
- `FILTER_FLAG_ALLOW_THOUSAND` allows thousands separators in numbers.
- `FILTER_FLAG_ALLOW_SCIENTIFIC` allows scientific notation in numbers.

These flags can be used with the `FILTER_VALIDATE_NUMBER_INT` and `FILTER_SANITIZE_NUMBER_INT` filters to validate and sanitize integer numbers. They can also be used with the `FILTER_VALIDATE_NUMBER_FLOAT` and `FILTER_SANITIZE_NUMBER_FLOAT` filters to validate and sanitize floating-point numbers. (AIBRDJG)



```php
// Validate a number with a decimal point.
$number = filter_var('123.45', FILTER_VALIDATE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_FRACTION);

// Validate a number with a thousands separator.
$number = filter_var('1,234,567', FILTER_VALIDATE_NUMBER_INT, FILTER_FLAG_ALLOW_THOUSAND);

// Validate a number in scientific notation.
$number = filter_var('1.23e+10', FILTER_VALIDATE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_SCIENTIFIC);

// Sanitize a number with a decimal point.
$number = filter_var('123.45', FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_FRACTION);

// Sanitize a number with a thousands separator.
$number = filter_var('1,234,567', FILTER_SANITIZE_NUMBER_INT, FILTER_FLAG_ALLOW_THOUSAND);

// Sanitize a number in scientific notation.
$number = filter_var('1.23e+10', FILTER_SANITIZE_NUMBER_FLOAT, FILTER_FLAG_ALLOW_SCIENTIFIC);
```



### FILTER_FLAG_STRIP_BACKTICK

The FILTER_FLAG_STRIP_BACKTICK flag is used to remove the backtick (&grave;) character from a string. This flag is often used to sanitize user input to prevent attacks that exploit the backtick character like SQL Injection Attacks.

For example, an attacker could inject a malicious script into a web application by submitting a form with a backtick character in the input field. If the application does not properly sanitize the input, the script could be executed and the attacker could gain control of the application.

The FILTER_FLAG_STRIP_BACKTICK flag can be used to prevent this type of attack by removing all backtick characters from the user input. However, it is important to note that this flag can also remove legitimate data, such as backticks used in code.

Here is an example of how to use the FILTER_FLAG_STRIP_BACKTICK flag to sanitize user input:

```php
$input = filter_var($_GET['input'], FILTER_SANITIZE_STRING, FILTER_FLAG_STRIP_BACKTICK);
```



source for page(AIBRDJG)

### Code Example

```php+HTML
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



### Output

```
Sanitization Examples
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


ASDasd1234.99!@#$%^&*()_+-,./";\'<>?:[]{}\|`~       htmlspecialchars
© 2023 Jim Goudy
```

