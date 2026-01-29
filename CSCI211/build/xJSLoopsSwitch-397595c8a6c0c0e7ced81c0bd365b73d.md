# Loops and Switch



1. For Loop:

   - Ideal for known iteration counts.

     ```javascript
     for (initialization; condition; afterthought) {
         // Code to execute
     }
     ```

     

   - Example:

     ```javascript
     for (let i = 0; i < 5; i++) {
         console.log("Walking east one step");
     }
     ```

     

1. While Loop:

   - Best for unknown iteration counts based on a condition.

     ```javascript
     while (condition) {
         // Code to execute
     }
     ```

     

1. Do…While Loop:

   - Executes at least once, even if the condition is initially false.

     ```javascript
     do {
         // Code to execute
     } while (condition);
     ```

     

1. For…In Loop:

   - Perfect for iterating over object properties.

     ```javascript
     for (const key in object) {
         // Code to execute
     }
     ```




# Switch Statement

 **switch statement** is a powerful construct used for making decisions in code based on different conditions. It provides an organized and concise alternative to using multiple `if-else` statements. Here’s how it works:

1. **Syntax**:

   ```javascript
   switch (expression) {
       case value1:
           // Code block executed if expression matches value1
           break;
       case value2:
           // Code block executed if expression matches value2
           break;
       // More cases...
       default:
           // Code block executed if no case matches the expression
   }
   ```

   

1. **How It Works**:

   - The `switch` expression is evaluated once.
   - The value of the expression is compared with the values of each `case`.
   - If there’s a match, the associated block of code is executed.
   - If no match is found, the `default` code block is executed.

1. **Example**: Let’s say we want to determine the day of the week based on the current day number (0 for Sunday, 1 for Monday, etc.). We can use the `switch` statement like this:

   JavaScript

   

   ```javascript
   switch (new Date().getDay()) {
       case 0:
           day = "Sunday";
           break;
       case 1:
           day = "Monday";
           break;
       // ... other cases ...
       default:
           day = "Unknown day";
   }
   ```

   AI-generated code. Review and use carefully. [More info on FAQ](https://www.bing.com/new#faq).

1. **Break Keyword**:

   - When JavaScript encounters a `break` keyword inside a `case`, it exits the `switch` block.
   - It’s not necessary to break the last case; the block ends there anyway.

1. **Default Keyword**:

   - The `default` keyword specifies the code to run if no case matches.
   - It’s like a fallback option.

1. **Common Code Blocks**:

   - Sometimes different `case` values share the same code block.

   - For example:

     JavaScript

     

     ```javascript
     switch (new Date().getDay()) {
         case 4:
         case 5:
             text = "Soon it is Weekend";
             break;
         case 0:
         case 6:
             text = "It is Weekend";
             break;
         default:
             text = "Looking forward to the Weekend";
     }
     ```

     



## Lecture Code

```html
<!DOCTYPE html>
<!--
Loops, if's and switch examples
-->
<html>
    <head>
        <title>TODO supply a title</title>
        <script>

            function loops()
            {
                //do loop
                let dostring = "do1 ";
                let cntr = 2;
                do {
                    dostring = dostring + "do" + cntr + " ";
                    cntr++;
                } while (cntr <= 10);

                //while loop
                let whilestring = "while1 "
                cntr = 1;

                while (cntr <= 10)
                {
                    whilestring = whilestring + "while" + cntr + " ";
                    cntr++;
                }

                //for loop
                let forstring = "";
                for (let i = 1; i <= 10; i++)
                {
                    forstring = forstring + "for" + i + " ";

                }
                document.getElementById("p1").innerHTML =
                        dostring + "<br><br>" +
                        whilestring + "<br><br>" +
                        forstring + "<br><br>";
            }

            function rbutton()
            {
                //checking radio buttons with an if
                let rbttns = document.getElementsByName("rbgroup1");
                for (let i = 0; i < rbttns.length; i++)
                {
                    if (rbttns[i].checked)
                    {
                        document.getElementById("p2").innerHTML =
                                rbttns[i].value + " was selected <br>";
                        document.getElementById("p2").style.color = 
                        rbttns[i].value;
                    }
                }
            }

            function numrange()
            {
                //example of an if
                let x;

                x = document.getElementById("nbox1").value;


                if (x <= 25)
                {
                    document.getElementById("p3").innerHTML =
                            "Your number is less than or equal to 25";
                }
                else if (x <= 50)
                {
                    document.getElementById("p3").innerHTML =
                            "Your number is less than or equal to 50";
                }
                else if (x <= 75)
                {
                    document.getElementById("p3").innerHTML =
                            "Your number is less than or equal to 75";
                }
                else if (x <= 100)
                {
                    document.getElementById("p3").innerHTML =
                            "Your number is less than or equal to 100";
                }
                else
                {
                    document.getElementById("p3").innerHTML =
                            "Your number is greater than 100";
                }

                //example of a range
                if ((x > 0 && x < 25) || (x > 75 && x < 100))
                {
                    document.getElementById("p4").innerHTML =
                            "Your number must be near \n\
                            one of the ends of the range";
                }
                else
                {
                    document.getElementById("p4").innerHTML = "";
                }

            }

            function switchexample()
            {
                //Example of a switch
                let x = document.getElementById('nbox2').value;

                switch (x)
                {
                    case "1":
                        document.getElementById("p5").innerHTML = 
                        "You chose 1 - you win a new car";
                        break;
                    case "2":
                       document.getElementById("p5").innerHTML = 
                        "You chose 2 - you win a new boat";
                        break; 
                    case "3":
                        document.getElementById("p5").innerHTML = 
                        "You chose 3 - you win a vacation to Italy";
                        break;
                    default:
                        document.getElementById("p5").innerHTML = 
                        "You did not choose correctly - are destined to\n\
                        roam the world aimlessly";
                        break;
                }
            }

        </script>

    </head>
    <body>

        <br>
        <hr>
        <H2>Loops</H2>
        <input type="submit" value="Run" name="btnRun" onclick="loops()" />
        <p  id="p1"></p>
        <br>
        <hr>

        <h2>If example with radio buttons</h2>
        <input type="radio" name="rbgroup1" value="red" checked="checked"
               onclick="rbutton()" />
        Red<br>
        <input type="radio" name="rbgroup1" value="brown"  
               onclick="rbutton()"/>
        Brown<br>
        <input type="radio" name="rbgroup1" value="blue" 
               onclick="rbutton()"/>
        Blue<br>

        <p id="p2"></p>

        <hr>

        <h2>If else example</h2>
        Enter a number between 1- 100
        <input type="text" name="numberbox" value="" size="15" id="nbox1" />
        <input type="submit" value="Number Enter" name="bttnnumber" 
               onclick="numrange()"/>
        <p id="p3"></p>
        <p id = "p4"></p>

        <hr>
        <h2>Switch statement</h2>
        Enter 1, 2 or 3<br>
        <input type="text" name="nbox2" value="" size="15" id="nbox2" />
        <input type="submit" value="Number Enter" name="bttnnumber2" 
               onclick="switchexample()"/>
        <p id="p5"></p>

    </body>
</html>
```

