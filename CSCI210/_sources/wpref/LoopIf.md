# Loops and If



## Example code

```php+HTML
<?php

echo "hello php";
print "Hello Amigos";
print("http://localhost/wp/page1");
print("\n");

$output = 0;
$counter = 0;

print("For Loop\n");
for ($counter = 0; $counter <= 20; $counter++) {
    echo("for: ".$counter."\n");
}
$counter = 0;
print("\nWhile Loop\n");
while ($counter < 10) {
    echo("while: ".$counter."\n");
    $counter += 1;
}

$num = 12;

if ($num < 10) {
    echo "This was less than ten";
} else if ($num < 15) {
    echo "This was less than 15";
} else {
    echo "This was greater than 15";
}

?>
```

**Purpose:** Demonstrate basic output, looping structures, and conditional statements.

**Breakdown:**

1. **Output Statements:**
   - `echo "hello php";`: Prints the string "hello php" to the output.
   - `print "Hello Amigos";`: Prints the string "Hello Amigos" to the output.
   - `print("http://localhost/wp/page1");`: Prints the URL "http://localhost/wp/page1" to the output.
   - `print("\n");`: Prints a newline character to the output.
1. **Variable Initialization:**
   - `$output = 0;`: Initializes a variable named `$output` with the value 0.
   - `$counter = 0;`: Initializes a variable named `$counter` with the value 0.
1. **For Loop:**
   - `for ($counter = 0; $counter <= 20; $counter++) { ... }`: Iterates from `$counter` equal to 0 up to 20 (inclusive), incrementing `$counter` by 1 in each iteration. Inside the loop, it prints the current value of `$counter`.
1. **While Loop:**
   - `while ($counter < 10) { ... }`: Continues to execute as long as `$counter` is less than 10. Inside the loop, it prints the current value of `$counter` and increments `$counter` by 1.
1. **Conditional Statements:**
   - `if ($num < 10) { ... } else if ($num < 15) { ... } else { ... }`: Checks the value of `$num` and executes the appropriate code block based on the comparison.

**Summary:** The code demonstrates the following PHP concepts:

- Output using `echo` and `print`.
- Variable declaration and assignment.
- Looping structures: `for` and `while`.
- Conditional statements: `if`, `else if`, and `else`.

The code effectively illustrates how to use these concepts to perform basic operations and control the flow of execution in a PHP script.