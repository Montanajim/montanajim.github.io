# Functions



## Code Breakdown and Comments

**Purpose:** This PHP code demonstrates various programming concepts, including functions, loops, and conditional statements.

**Functions:**

- **`myfunc1()`:** A simple function that prints "Func1" to the page
- **`add2($n1, $n2)`:** Takes two numbers as input, adds them together, and returns the sum.
- **`loops()`:** A function that demonstrates different types of loops (while, do-while) and conditional statements.

**Variables:**

- **`$n1`, `$n2`:** Used in the `add2()` function to store the input numbers.
- **`$sum`:** Stores the calculated sum in the `add2()` function.
- **`$run`, `$cntr`, `$stop`, `$status`:** Variables used in the `loops()` function for loop control, counting, and status tracking.

**Loops:**

- **`while` loop:** Continues to execute as long as a given condition is true.
- **`do-while` loop:** Executes at least once, then continues as long as a given condition is true.

**Conditional Statements:**

- **`if-else` statements:** Used to make decisions based on conditions.

**Code Breakdown:**

1. **Function Definitions:**
   - `myfunc1()` is defined to print a message.
   - `add2()` takes two numbers, adds them, and returns the result.
   - `loops()` demonstrates different loop types and conditional logic.
1. **Main Execution:**
   - Calls the `myfunc1()` function.
   - Calculates the sum using `add2()` and prints the result.
   - Calls the `loops()` function to demonstrate loop and conditional concepts.

**Comments within `loops()`:**

- **`while` loop:** Demonstrates a basic `while` loop with a counter and a stopping condition.
- **`while` loop with `if`:** Shows how to use an `if` statement inside a loop to break out of the loop based on a condition.
- **`do-while` loop:** Demonstrates a `do-while` loop that executes at least once.
- **`if-else` statements:** Shows how to use `if-else` statements to check conditions and set a status based on the result.



```php
<!doctype html>
<html>
    <head>
        <title>functions</title>

        <?php
        
        function myfunc1()
        {
            echo("<br><br>Func1<br><br>");
        }

        function add2($n1,$n2)
        {
            $sum = $n1 + $n2;

            return $sum;
        }

        function loops()
        {
            
            $run = TRUE;

            $cntr = 1;
            $stop = 11;

            // Example of a while loop
            while($cntr < $stop)
            {
                echo($cntr.". Item".$cntr."<br>");
                $cntr +=1;
            }
            echo("<br><hr><br>");
			// excample of while loop using
            // a boolean and if statement
            $cntr = 0;
            while($run)
            {
                echo($cntr.". Item 22 ".$cntr."<br>");
                $cntr +=1;

                if($cntr == $stop)
                {
                    $run=FALSE;
                }
            }

            echo("<br><hr><br>");
            // Example of do loop - always runs once
            $cntr = 0;
            do{
                echo($cntr.".  Item Do".$cntr."<br>");
                $cntr +=1;  
            }while($cntr < $stop);
        

        echo("<br><hr><br><h2>Status If</h2><br>");

        $cntr = 0;
        $status = "";
        $run = True;

        while($run)
        {

			// example of else if statement
            if($cntr == $stop)
            {
                $run=FALSE;
            }
            else if(($cntr % 2) == 0)
            {
                $status = "Even";
            }
            else{
                $status = "Odd";
            }

            echo($cntr.". Item 22 ".$cntr." ".$status."<br>");
            $cntr +=1;
        }
        }
        ?>
        
    </head>
<body>
    <?php
        
        myfunc1();

        echo("<br><br><hr><br><br>");
    ?>
    <h2>Sum Example - 60 + 40</h2>
    <?php 
        $x = 40;
        $xx = 60;
        $total = add2($x,$xx);
        echo("The sum = ".$total."<br>");

        echo("<br><br><hr><br><br>");

        loops();
    ?>
</body>
</html>
```

