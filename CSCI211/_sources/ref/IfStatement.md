# If Statement



A **JavaScript `if` statement** is a fundamental construct that allows you to make decisions in your code based on specified conditions. It enables you to execute a block of code **only if a particular condition is true**. Here’s how it works:

1. **Syntax**:

   - The basic structure of an

     ```javascript
     if
     ```

     statement looks like this:

     ```javascript
     if (condition) {
         // Block of code to be executed if the condition is true
     }
     ```

     

   - The `condition` is an expression that evaluates to either `true` or `false`.

1. **Execution Flow**:

   - When your program encounters an `if` statement, it checks whether the specified condition is true.
   - If the condition is true, the code inside the curly braces `{ ... }` is executed.
   - If the condition is false, the code block is skipped, and the program moves on to the next statement.

1. **Example**: Let’s say we want to greet users based on the time of day. Here’s how we can use an `if` statement:

   JavaScript

   

   ```javascript
   let hour = new Date().getHours();
   
   if (hour < 10) {
       console.log("Good morning");
   } else if (hour < 20) {
       console.log("Good day");
   } else {
       console.log("Good evening");
   }
   ```

   

   - In this example:
     - If the current hour is less than 10, it prints “Good morning.”
     - If the hour is between 10 and 20 (exclusive), it prints “Good day.”
     - Otherwise, it prints “Good evening.”

1. **Additional Notes**:

   - You can use `else` to specify an alternative block of code to execute when the condition is false.
   - The `else if` statement allows you to test multiple conditions sequentially.
   - Remember that JavaScript is case-sensitive, so use lowercase `if`, `else`, and `else if`.

## Lecture Code

```javascript
< !DOCTYPE html >
   <
   !--
If Examples by Jim Goudy
-- >
<
html >
   <
   head >
   <
   title > If Example < /title> <
   meta charset = "UTF-8" >
   <
   meta name = "viewport"
content = "width=device-width, initial-scale=1.0" >

   <
   style >
   .zbox {
      float: left;
      width: 200 px;
      height: 200 px;
      border - width: 3 px;
      border - style: solid;
      margin: 5 px;
      text - align: center;
      font - size: 24 pt;

   }
#warningColor {
   font - style: italic;
   color: red;
}

<
/style>

<
script >
   function setBoxColor() {
      //this demostrates an else if statement
      var userInput = Number(document.getElementById("inputC").value);
      var message = "Please enter a number between 0 and 100";

      //reset boxes, error message and inputbox
      resetBoxes();

      //example of else if 
      if (userInput < 0) {
         document.getElementById("warningColor").innerHTML = message;

      } else if (userInput > 0 && userInput <= 50) {
         document.getElementById("boxGreen").style.backgroundColor = "green";
      } else if (userInput >= 51 && userInput <= 65) {
         document.getElementById("boxGreen").style.backgroundColor = "green";
         document.getElementById("boxYellow").style.backgroundColor = "yellow";
      } else if (userInput >= 66 && userInput <= 74) {
         document.getElementById("boxGreen").style.backgroundColor = "green";
         document.getElementById("boxYellow").style.backgroundColor = "yellow";
         document.getElementById("boxOrange").style.backgroundColor = "orange";
      } else if (userInput >= 75 && userInput <= 100) {
         document.getElementById("boxGreen").style.backgroundColor = "green";
         document.getElementById("boxYellow").style.backgroundColor = "yellow";
         document.getElementById("boxOrange").style.backgroundColor = "orange";
         document.getElementById("boxRed").style.backgroundColor = "red";

      } else {
         document.getElementById("warningColor").innerHTML = message;
      }
   }

function resetBoxes() {
   //get all of the boxs and store them into an array call boxes
   var boxes = document.getElementsByClassName("zbox");

   //loop through each box and change the color back to white
   //note: you cannot change them all at once
   for (var cntr = 0; cntr < boxes.length; cntr++) {
      boxes[cntr].style.backgroundColor = 'white';
   }
   //reset inputbox
   document.getElementById("inputC").value = "";

   //Reset the warning message
   document.getElementById("warningColor").innerHTML = "";

}

function checkAge() {
   //Store Age To variable
   var nAge = document.getElementById("inputAge").value;

   if (nAge > 17) {
      var ageMess = "  You are old enough to vote";
      document.getElementById("ageMessage").innerHTML = ageMess;
   }

}

function clearAge() {
   document.getElementById("inputAge").value = null;
   document.getElementById("ageMessage").innerHTML = null;

}

<
/script>


<
/head> <
body >

   <
   h1 > If Example < /h1> <
   p > This is an
if example < /p> <
   p > Enter Your Age < input type = "text"
id = "inputAge"
onfocus = "clearAge()" / >
   <
   input type = "button"
onclick = "checkAge()"
value = "Check Age" / >
   <
   span id = "ageMessage" > < /span> </p >
   <
   h1 > Else If < /h1>

   <
   p > < br / > Enter Value
for boxes:
   <
   input type = "text"
id = "inputC"
size = "25"
placeholder = "Enter a value between 0 and 100" / >
   <
   input type = "button"
value = "Enter"
onclick = "setBoxColor()" / >
   <
   input type = "button"
value = "Reset"
onclick = "resetBoxes()" / >
   <
   span id = "warningColor" > < /span> </p >
   <
   div id = "boxGreen" class = "zbox" > 0 - 50 < /div> <
   div id = "boxYellow" class = "zbox" > 51 - 65 < /div> <
   div id = "boxOrange" class = "zbox" > 66 - 74 < /div> <
   div id = "boxRed" class = "zbox" > 75 - 100 < /div> <
   p > < /p> <
   /body> <
   /html>
```

