# Form Validation

*This example uses a "flag" approach.*

## Lecture Code

index.html

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width">
        <title>Form Validation Example</title>
        <!-- Programmer: James Goudy -->
        
        <style>
            #theContent{
                width: 25%;
                margin: 100px auto; /* Combined margin properties */
                background-color: bisque;
                padding: 40px;
                color: black;
            }
            #errorDiv{
                background-color: khaki;
                color: navy;

            }
        </style>

    </head>
    <body>
        <div id="theContent">
        <h1>Form Validation Example</h1>

        <form name="demo" onsubmit="return validateFormOnSubmit(this)" action="test.html">
            <table summary="Demonstration form">
                <tbody>
                    <tr>
                        <td><label for="username">Username:</label></td>
                        <td><input  type="text" id="username" name="username" 
                                    size="35" maxlength="50" ></td>
                    </tr>   
                    <tr>
                        <td><label for="pwd">Password:</label></td>
                        <td><input  type="password" id="pwd" name="pwd" 
                                    size="35" maxlength="25" ></td>
                    </tr>   
                    <tr>
                        <td><label for="email">Email:</label></td>
                        <td><input  type="text" id="email" name="email" 
                                    size="35" maxlength="30"
                                    placeholder="xxx@domain.xxx"></td>
                    </tr>
                    <tr>
                        <td><label for="altemail">Alternate email:</label></td>
                        <td><input  type="text" id="altemail" name="altemail" 
                                    size="35" maxlength="30" 
                                    pattern="[a-z0-9._%+\-]+@[a-z0-9.\-]+\.[a-z]{2,}$" 
                                    placeholder="xxx@domain.xxx" required></td>
                    </tr>    
                    <tr>
                        <td><label for="phone">Phone:</label></td>
                        <td><input  type="text" id="phone" name="phone" size="35" 
                                    maxlength="25" placeholder="(555) 555-5555"></td>
                    </tr>   
                    <tr>
                        <td>
                            <label for="from">Where are you :</label></td>
                        <td><input  type="text" id="from" name="from" 
                                    size="35" maxlength="50" ></td>
                    </tr>   
                    <tr>
                        <td>&nbsp;</td>
                        <td><input name="Submit" value="Send" type="submit" ></td>
                        <td>&nbsp;</td>
                    </tr> 
                </tbody>
            </table>
        </form> 

        <div id="errorDiv">

        </div>

        </div>

        <script>
            /*
                This code defines a function that validates a form. 
                The function breaks down the form validation into 
                smaller functions, each of which checks 
                a single form element. If an element is valid, 
                the function checking it doesn't return any error message. 
                Otherwise, it returns an error message 
                describing the problem and highlights 
                the element in yellow for the user to see.
             */
            
            function validateFormOnSubmit(theForm) {
                let reason = "";

                
                reason += validateUsername(theForm.username);
                reason += validatePassword(theForm.pwd);
                reason += validateEmail(theForm.email);
                reason += validatePhone(theForm.phone);
                reason += validateEmpty(theForm.from);

                if(reason != "")
                {
                    reason = "<h2>Errors</h2><ul>" + reason + "</ul><br>";
                    document.getElementById("errorDiv").innerHTML = reason;
                    return false;
                }

                document.getElementById("errordiv").innerHTML = "";
                return true;
            }

            /* *
             The function below checks if a required field has been left 
             empty. If the required field is blank, 
             returned is the error string to the main function. 
             If it is not blank, the function returns an empty string.
             */

            function validateEmpty(fld) {
                let error = "";

                if (fld.value.length == 0) {
                    fld.style.background = 'Yellow';
                    error = "<li>The required field has not been filled in.</li>"
                } else {
                    fld.style.background = 'White';
                }
                return error;
            }

            /* 
            It first makes sure the username field isn't left empty. 
            Then, it checks if the username's length is between 5 and 15 characters. 
            If it passes those checks, it uses a special pattern 
            (called a regular expression) to make sure the username 
            only contains letters, numbers, and underscores. No other symbols or 
            characters are allowed.
            */
            function validateUsername(fld) {
                let error = "";
                let illegalChars = /\W/; // allow letters, numbers, and underscores

                if (fld.value == "") {
                    fld.style.background = 'Yellow';
                    error = "<li>You didn't enter a username.</li>";
                } else if ((fld.value.length < 5) || (fld.value.length > 15)) {
                    fld.style.background = 'Yellow';
                    error = "<li>The username is the wrong length.</li>";
                } else if (illegalChars.test(fld.value)) {
                    fld.style.background = 'Yellow';
                    error = "<li>The username contains illegal characters.</li>";
                } else {
                    fld.style.background = 'White';
                }
                return error;
            }
            /*
            The function below checks the password field for blankness
             and allow only letters and numbers - no underscopes this time. 
             So we should use a new regular expression to forbid underscopes. 
             This one /[\W_]/ allow only letters and numbers. 
             Next, we want to permit only passwords that contain letters 
             and at least one numeral. For that we use the seacrh() method and
              two more regular expressions: /(a-z)+/ and /(0-9)/.
            */
            function validatePassword(fld) {
                let error = "";
                let illegalChars = /[\W_]/; // allow only letters and numbers 

                if (fld.value == "") {
                    fld.style.background = 'Yellow';
                    error = "<li>You didn't enter a password.</li>";
                } else if ((fld.value.length < 7) || (fld.value.length > 15)) {
                    error = "<li>The password is the wrong length. </li>";
                    fld.style.background = 'Yellow';
                } else if (illegalChars.test(fld.value)) {
                    error = "<li>The password contains illegal characters.</li>";
                    fld.style.background = 'Yellow';
                } else if (!((fld.value.search(/(a-z)+/)) && (fld.value.search(/(0-9)+/)))) {
                    error = "<li>The password must contain at least one numeral.</li>";
                    fld.style.background = 'Yellow';
                } else {
                    fld.style.background = 'White';
                }
                return error;
            }
            
            
            // ---------------------------------------------------------------------
            /*
            "The following steps are undertaken to validate the user-provided email address:

            1. Empty Field Check: An initial check is performed to determine if the user 
            has entered any data in the email field.
            
            2. Regular Expression Validation: If the field is not empty, a regular expression is
            employed in conjunction with the test() method to verify if the email address 
            adheres to the following format:

                    * Presence of an "@" symbol, but not as the leading character.
                    * Presence of a dot (".") following the "@" symbol.

            It is acknowledged that this validation approach has limitations. While it may not 
            capture all non-compliant email addresses, it serves as a robust foundation for 
            initial validation purposes."
             * 
             */
            
            function trim(s)
            {
                return s.replace(/^\s+|\s+$/, '');
            }

            function validateEmail(fld) {
                let error = "";
                // value of field with whitespace trimmed off
                let tfld = trim(fld.value);
                let emailFilter = /^[^@]+@[^@.]+\.[^@]*\w\w$/;
                let illegalChars = /[\(\)\<\>\,\;\:\\\"\[\]]/;

                if (fld.value == "") {
                    fld.style.background = 'Yellow';
                    error = "<li>You didn't enter an email address.</li>";
                } else if (!emailFilter.test(tfld)) {
                    //test email for illegal characters
                    fld.style.background = 'Yellow';
                    error = "<li>Please enter a valid email address.</li>";
                } else if (fld.value.match(illegalChars)) {
                    fld.style.background = 'Yellow';
                    error = "<li>The email address contains illegal characters.</li>";
                } else {
                    fld.style.background = 'White';
                }
                return error;
            }

            //---------------------------------------------------------------------

            /*
            1. Clear Spacer Characters: It uses replace() to remove any extra spaces
               or characters that might be in the phone number.
            2. Check for Numbers Only: It calls isNaN() to make sure the phone number 
               contains only numbers, not letters or symbols.
            3. Check Length: It verifies that the phone number has exactly 10 digits, 
               as that's the standard length for many phone numbers.
             */

            function validatePhone(fld) {
                let error = "";
                let stripped = fld.value.replace(/[\(\)\.\-\ ]/g, '');
                console.log(stripped);
                if (fld.value === "") {
                    error = "<li>You didn't enter a phone number.</li>";
                    fld.style.background = 'Yellow';
                } else if (isNaN(stripped)) {
                    console.log(stripped);
                    error = "<li>The phone number contains illegal characters.</li>";
                    fld.style.background = 'Yellow';
                } else if (!(stripped.length == 10)) {
                    error = "<li>The phone number is the wrong length. " +
                            "Make sure you included an area code.</li>";
                    fld.style.background = 'Yellow';
                }
				else
				{
					fld.style.background = 'White';
				}
                return error;
            }
        </script>

    </body>
</html>
```

test.html

```html
<html>
<head>
<title>test success</title>
</head>
	<style>
		#theContent{
			width: 25%;
			margin: 100px auto; /* Combined margin properties */
			background-color: bisque;
			padding: 40px;
			color: black;
		}
	</style>
<body>
	<div id="theContent">
		<h1>Good test</h1>
		<p>There was good form validation</p>
	</div>

</body>
</html>
```



## Explanation

The code you provided is a basic HTML form with Javascript validation. Let's break it down into sections:

**HTML Structure:**

- **DOCTYPE declaration:** This line specifies the document type as HTML.

- **HTML tag:** This is the root element of the HTML document.

- Head section:

   This section contains meta information about the document.

  - **Meta charset:** This specifies the character encoding used in the document (UTF-8 in this case).
  - **Meta viewport:** This sets how the document should be scaled on different screen sizes (set to device width here).
  - **Title:** This defines the title of the webpage displayed on the browser tab.

- Style section:

   This section contains CSS code that styles the HTML elements.

  - In this case, styles are defined for two divs with ids `theContent` and `errorDiv`. The content div has a width of 50%, centered with margin, background color, padding, and text color. The error div has a background color and text color.

- Body section:

   This section contains the visible content of the webpage.

  - `Div` with `id` "theContent"

    : This div contains the form and the error message area.

    - **Heading:** This displays the title "Form Validation Example".

    - Form:

       This is the HTML form element that users will interact with to submit data.

      - Form attributes:

        - name: "demo" (specifies a name for the form)
        - `onsubmit: "return validateFormOnSubmit(this)"` (calls the validateFormOnSubmit function when the form is submitted and prevents default form submission behavior).
        - `action: "test.html"`  (specifies the file where the form data will be submitted, but not used in this example since validation is done with Javascript).

      - Table:

         This creates a table layout for the form elements.

        - Each row represents an input field and its label.
        - Input elements have different types (`text`, `password`) and attributes like size, maxlength, and placeholder.

      - **Submit button:** This button triggers the form submission when clicked.

    - `Div` with `id` "errorDiv": This div will be used to display any error messages from the form validation.

- Script section:

   This section contains Javascript code that adds interactivity to the webpage.

  - The script defines several functions for form validation:
    - `validateFormOnSubmit`: This function is called when the form is submitted. It calls other validation functions for each form element and builds an error message string if any errors are found. If there are errors, it displays them in the error div and prevents the form from being submitted. Otherwise, it clears the error div and allows form submission.
    - `validateEmpty`: This function checks if a required field is empty. If empty, it sets the background color of the field to yellow and adds an error message to the error string.
    - `validateUsername`: This function checks the username field for validity. It checks for blank input, length restrictions, and illegal characters. It sets the background color of the field based on the validation result and adds an error message to the error string if needed.
    - `validatePassword`: This function checks the password field for validity. It checks for blank input, length restrictions, illegal characters, and presence of at least one numeral. It sets the background color of the field based on the validation result and adds an error message to the error string if needed.
    - `trim`: This function removes leading and trailing whitespace from a string (used in email validation).
    - `validateEmail`: This function checks the email field for validity. It checks for blank input, format using a regular expression, and illegal characters. It sets the background color of the field based on the validation result and adds an error message to the error string if needed.
    - `validatePhone`: This function checks the phone number field for validity. It removes non-numeric characters, checks if the remaining string contains only numbers, and checks the length of the number. It sets the background color of the field based on the validation result and adds an error message to the error string if needed.

Overall, this code demonstrates a simple form with client-side validation using Javascript. When the user submits the form, the Javascript code validates each field and provides feedback to the user if there are any errors.