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

        <style>
            #theContent{
                width: 50%;
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
                        <td><label for="username">Your user name:</label></td>
                        <td><input name="username" size="35" maxlength="50" type="text"></td>
                    </tr>   
                    <tr>
                        <td><label for="pwd">Your password</label></td>
                        <td><input name="pwd" size="35" maxlength="25" type="password"></td>
                    </tr>   
                    <tr>
                        <td><label for="email">Your email:</label></td>
                        <td><input name="email" size="35" maxlength="30" type="text"></td>
                    </tr>   
                    <tr>
                        <td><label for="phone">Your telephone number:</label></td>
                        <td><input name="phone" size="35" maxlength="25" type="text"
								placeholder="(555) 555-5555"></td>
                    </tr>   
                    <tr>
                        <td>
                            <label for="from">Where are you :</label></td>
                        <td><input name="from" size="35" maxlength="50" type="text"></td>
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
             * This is a main function that calls a series of subfunctions,
             *  each of which checks a single form element for compliance. 
             *  If the element complies than sufunction returns an empty string.
             *   Otherwise it returns a message describing the error and 
             *   highlight appropriate element with yellow.
             */
            
            function validateFormOnSubmit(theForm) {
                var reason = "";

                
                reason += validateUsername(theForm.username);
                reason += validatePassword(theForm.pwd);
                reason += validateEmail(theForm.email);
                reason += validatePhone(theForm.phone);
                reason = reason + validateEmpty(theForm.from);

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
             * The function below checks if a required field has been left 
             * empty. If the required field is blank, 
             * we return the error string to the main function. 
             * If it’s not blank, the function returns an empty string.
             */

            function validateEmpty(fld) {
                var error = "";

                if (fld.value.length == 0) {
                    fld.style.background = 'Yellow';
                    error = "<li>The required field has not been filled in.</li>"
                } else {
                    fld.style.background = 'White';
                }
                return error;
            }

            /* 
             *The function below checks if the user entered anything at all 
             *in the username field. If it’s not blank, we check the length of
             * the string and permit only usernames that are between 5 and 15
             *  characters. Next, we use the JavaScript 
             *  regular expression /\W/ to forbid illegal characters from 
             *  appearing in usernames. 
             *  We want to allow only letters, numbers and underscopes. 
            */
            function validateUsername(fld) {
                var error = "";
                var illegalChars = /\W/; // allow letters, numbers, and underscores

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
                var error = "";
                var illegalChars = /[\W_]/; // allow only letters and numbers 

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
             * Next we want to see if the email address the user entered 
             * is real. This means that the input data must contain at 
             * least an @ sign and a dot (.). Also, the @ must not be the 
             * first character of the email address, and the last dot must 
             * at least be one character after the @ sign.  At first we check
             *  if the user entered anything at all in the email field. 
             *  Next, we use regular expression and the test() method to check 
             *  the field for a compliance. 
             *  Also we will use trim() function that will 
             *  trim leading whitespace off the string. 
             *  This won’t be perfect validation — it is possible to slip 
             *  not compliant addresses by it — but it's normally good enough.
             * 
             */
            
            function trim(s)
            {
                return s.replace(/^\s+|\s+$/, '');
            }

            function validateEmail(fld) {
                var error = "";
                var tfld = trim(fld.value); // value of field with whitespace trimmed off
                var emailFilter = /^[^@]+@[^@.]+\.[^@]*\w\w$/;
                var illegalChars = /[\(\)\<\>\,\;\:\\\"\[\]]/;

                if (fld.value == "") {
                    fld.style.background = 'Yellow';
                    error = "<li>You didn't enter an email address.</li>";
                } else if (!emailFilter.test(tfld)) { //test email for illegal characters
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
             * The function below checks if the phone number is valid. 
             * At first we use regular expression and the replace() method 
             * to clear out any spacer characters. Next, we use the 
             * isNaN() function to check if the phone number contain 
             * only numbers. At last we check the length of the string 
             * and permit only phone numbers with 10 digits.
             * 
             */

            function validatePhone(fld) {
                var error = "";
                var stripped = fld.value.replace(/[\(\)\.\-\ ]/g, '');
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
			width: 50%;
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
        - onsubmit: "return validateFormOnSubmit(this)" (calls the validateFormOnSubmit function when the form is submitted and prevents default form submission behavior).
        - action: "test.html" (specifies the file where the form data will be submitted, but not used in this example since validation is done with Javascript).

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