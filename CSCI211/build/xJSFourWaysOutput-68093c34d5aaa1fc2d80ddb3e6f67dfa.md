# Four Ways To Display Output



there are **four primary ways** to display output:

1. **Using `innerHTML` Property**:

   - You can modify the content of an HTML element using the `innerHTML` property.

   - For example:

     ```text
     <p id="demo"></p>
     <script>
       document.getElementById("demo").innerHTML = 5 + 6;
     </script>
     ```

     This sets the content of the paragraph with the ID “demo” to the result of

     ```
     5 + 6
     ```

     , which is 11.

1. **Using `document.write()` Method**:

   - For testing purposes, you can use `document.write()` to directly write content to the HTML output.

   - Example:

     ```text
     <script>
       document.write(5 + 6);
     </script>
     ```

     

     > **Caution:** 
     >
     > Note that using  
     >     
     >    document.write() 
     >     
     >     after the HTML document is loaded will replace all existing HTML content.  

      

1. **Using `window.alert()`**:

   - You can display data in an alert box using `window.alert()`.

   - Example:

  &lt;script&gt;
        // window.alert(5 + 6);
  &lt;/script&gt;

     (Note: remove the comment when code is in production)

You can also skip the

     window

keyword, as it’s optional:
    
     ```text
     <script>
       // alert(5 + 6);
      </script>
     ```


​     

1. **Using `console.log()`**:

   - For debugging purposes, you can log data to the browser console using `console.log()`.

   - Example:

     ```text
     <script>
       console.log(5 + 6);
     </script>
     ```
     
     This won’t display anything on the page but will log the result to the browser console.
     
     



## Lecture Code

```html
<!DOCTYPE html>
<!--
Four ways to output information.
Example by James Goudy
-->
<html>
    <head>
        <title>Four Ways To Output</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">


    </head>
    <body>
        <h1>Four Ways To Output In JavaScript</h1>
        
        <script>
            /*
             * In this example, we cannont put the script here. The body
             * runs top down.  Since our script examples writes to specific
             * tags - at this moment in time or location of the code,
             * the h3, p and span tags have not been created yet, 
             * so the script would fail - not knowing where to put the tags..
             */
        </script>
        
        
        <br>
        <h3 id="myH3"></h3>
        <p id="myParagraph"></p>
        <p>The message is the following: "<span id="mySpan"></span>"</p>
        
        
        <script>

            var myMessage = "JavaSript is Fun!";

            //First way is by a popup window using alert            
            alert(myMessage);

            //Second way is by using document doc write.  
            //NOTE: This way destroys html - use is with caution.
            //It writes excatly where the physical location of the script
            //tag is located in the html.
            document.write(myMessage);

            //The third way is using innerHTML.  This puts the output
            //in between two html tags like span, paragraph, headings, etc.
            //NOTE: You have to identify the tag by id when usign innerHTML
            document.getElementById("myH3").innerHTML = myMessage;
            document.getElementById("myParagraph").innerHTML = myMessage;
            document.getElementById("mySpan").innerHTML = myMessage;
            
            /*
             * NOTE: innerHTML works with getElementByID. getElementByID
             * identifies the exact tag to use with innerHTML. Also the 
             * page runs top down.  With the script tag located here, the
             * h3, p and span tags have already been created so the 
             * script knows where to put the code.
             */

            
            //The fourth way to output information is to the console.
            //This is handy if you wish to test values, but not
            //display them on the page. In most browsers you can bring
            //the console up by clicking the F12 key and then clicking
            //the console tab. 
            
            console.log("In order to read this you have to open the console");

        </script>
    </body>
</html>

```

