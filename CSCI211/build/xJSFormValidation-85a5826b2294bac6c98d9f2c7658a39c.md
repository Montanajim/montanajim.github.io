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
        margin: 100px auto;
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
              <td>
                <input type="text" id="username" name="username" size="35" maxlength="50">
              </td>
            </tr>
            <tr>
              <td><label for="pwd">Password:</label></td>
              <td>
                <input type="password" id="pwd" name="pwd" size="35" maxlength="25">
              </td>
            </tr>
            <tr>
              <td><label for="email">Email:</label></td>
              <td>
                <input type="text" id="email" name="email" size="35" maxlength="30"
                       placeholder="xxx@domain.xxx">
              </td>
            </tr>

            <!-- Leave altEmail as HTML validation example (pattern + required) -->
            <tr>
              <td><label for="altemail">Alternate email:</label></td>
              <td>
                <input type="text" id="altemail" name="altemail" size="35" maxlength="30"
                       pattern="[a-z0-9._%+\-]+@[a-z0-9.\-]+\.[a-z]{2,}$"
                       placeholder="xxx@domain.xxx" required>
              </td>
            </tr>

            <tr>
              <td><label for="phone">Phone:</label></td>
              <td>
                <input type="text" id="phone" name="phone" size="35" maxlength="25"
                       placeholder="(555) 555-5555">
              </td>
            </tr>
            <tr>
              <td><label for="from">Where are you:</label></td>
              <td>
                <input type="text" id="from" name="from" size="35" maxlength="50">
              </td>
            </tr>
            <tr>
              <td>&nbsp;</td>
              <td><input name="Submit" value="Send" type="submit"></td>
              <td>&nbsp;</td>
            </tr>
          </tbody>
        </table>
      </form>

      <div id="errorDiv"></div>
    </div>

    <script>
      /*
        Demo form validation.
        - One function per field
        - Each validator returns "" (no error) or "<li>...</li>" (error)
        - Invalid fields are highlighted yellow
        - On submit, errors are collected and displayed
      */

      function trim(s) {
        return s.replace(/^\s+|\s+$/, '');
      }

      function validateFormOnSubmit(theForm) {
        let reason = "";

        // Clear previous errors every submit attempt (fixed casing)
        document.getElementById("errorDiv").innerHTML = "";

        reason += validateUsername(theForm.username);
        reason += validatePassword(theForm.pwd);
        reason += validateEmail(theForm.email);
        reason += validatePhone(theForm.phone);
        reason += validateEmpty(theForm.from);

        if (reason !== "") {
          reason = "<h2>Errors</h2><ul>" + reason + "</ul><br>";
          document.getElementById("errorDiv").innerHTML = reason;
          return false;
        }

        // no errors
        return true;
      }

      /*
        Checks if a required field is blank.
      */
      function validateEmpty(fld) {
        let error = "";
        let value = trim(fld.value);

        if (value.length === 0) {
          fld.style.background = 'Yellow';
          error = "<li>The required field has not been filled in.</li>";
        } else {
          fld.style.background = 'White';
        }
        return error;
      }

      /*
        Username rules:
        - Not empty
        - Length 5..15
        - Only letters, numbers, underscores
      */
      function validateUsername(fld) {
        let error = "";
        let value = trim(fld.value);
        let illegalChars = /\W/; // anything other than [A-Za-z0-9_]

        if (value === "") {
          fld.style.background = 'Yellow';
          error = "<li>You didn't enter a username.</li>";
        } else if (value.length < 5 || value.length > 15) {
          fld.style.background = 'Yellow';
          error = "<li>The username is the wrong length.</li>";
        } else if (illegalChars.test(value)) {
          fld.style.background = 'Yellow';
          error = "<li>The username contains illegal characters.</li>";
        } else {
          fld.style.background = 'White';
        }
        return error;
      }

      /*
        Password rules:
        - Not empty
        - Length 7..15
        - Only letters and numbers (no underscores, no symbols)
        - Must contain at least one letter and at least one digit
      */
      function validatePassword(fld) {
        let error = "";
        let value = trim(fld.value);
        let illegalChars = /[\W_]/; // forbid non-word chars and underscore

        if (value === "") {
          fld.style.background = 'Yellow';
          error = "<li>You didn't enter a password.</li>";
        } else if (value.length < 7 || value.length > 15) {
          fld.style.background = 'Yellow';
          error = "<li>The password is the wrong length.</li>";
        } else if (illegalChars.test(value)) {
          fld.style.background = 'Yellow';
          error = "<li>The password contains illegal characters.</li>";
        } else if (!(/[A-Za-z]/.test(value) && /\d/.test(value))) {
          fld.style.background = 'Yellow';
          error = "<li>The password must contain at least one letter and one numeral.</li>";
        } else {
          fld.style.background = 'White';
        }
        return error;
      }

      /*
        Email rules (simple demo):
        - Not empty
        - Basic pattern check
        - Reject a few "illegal" punctuation characters
      */
      function validateEmail(fld) {
        let error = "";
        let tfld = trim(fld.value);

        // simple-ish email filter (demo purpose, not RFC complete)
        let emailFilter = /^[^@]+@[^@.]+\.[^@]*\w\w$/;
        let illegalChars = /[\(\)\<\>\,\;\:\\\"\[\]]/;

        if (tfld === "") {
          fld.style.background = 'Yellow';
          error = "<li>You didn't enter an email address.</li>";
        } else if (!emailFilter.test(tfld)) {
          fld.style.background = 'Yellow';
          error = "<li>Please enter a valid email address.</li>";
        } else if (illegalChars.test(tfld)) {
          fld.style.background = 'Yellow';
          error = "<li>The email address contains illegal characters.</li>";
        } else {
          fld.style.background = 'White';
        }
        return error;
      }

      /*
        Phone rules:
        - Not empty
        - Strip non-digits
        - Must be exactly 10 digits
      */
      function validatePhone(fld) {
        let error = "";
        let value = trim(fld.value);

        // keep digits only
        let digits = value.replace(/\D/g, '');

        if (value === "") {
          fld.style.background = 'Yellow';
          error = "<li>You didn't enter a phone number.</li>";
        } else if (digits.length !== 10) {
          fld.style.background = 'Yellow';
          error = "<li>The phone number is the wrong length. Make sure you included an area code.</li>";
        } else {
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

This document implements a simple HTML form with client-side validation. Validation is performed in two different ways: most fields are validated with custom JavaScript on form submission, while the “Alternate email” field is validated using built-in HTML5 constraints (`required` and `pattern`). If validation succeeds, the browser submits the form to `test.html`. If validation fails, JavaScript-generated errors are displayed inside an on-page error region, and invalid fields are highlighted.

### Page structure and layout

The document uses standard HTML5 structure with UTF-8 encoding and a responsive viewport configuration. The visible page content is wrapped in a container `<div id="theContent">`, which holds a heading, the form, and an empty `<div id="errorDiv"></div>` reserved for error output.

A table is used to align labels and inputs in rows. Each row contains a `<label>` associated to its corresponding `<input>` via the `for` and `id` attributes.

CSS styles define the layout and basic appearance:

- `#theContent` is a centered content panel with `width: 25%`, `margin: 100px auto`, background color `bisque`, padding, and black text.
- `#errorDiv` is styled with a `khaki` background and `navy` text to visually separate error messages from the form.

### Form submission and control flow

The form element specifies:

- `onsubmit="return validateFormOnSubmit(this)"`: before submission, JavaScript runs `validateFormOnSubmit`. Returning `false` cancels submission; returning `true` allows submission to continue.
- `action="test.html"`: if submission proceeds, the browser submits/navigates to `test.html`.

The validation model is “submit-time validation”: checks occur when the user submits the form, not continuously as they type.

### JavaScript validation design

JavaScript validation is organized as one validator function per field. Each validator returns:

- `""` (empty string) when valid, or
- an error message formatted as an HTML list item (`"<li>...</li>"`) when invalid.

Each validator also provides immediate visual feedback by setting the input’s background color: Yellow for invalid and White for valid.

A utility function, `trim(s)`, removes leading and trailing whitespace so that inputs containing only spaces are treated as empty.

### Submission validator: `validateFormOnSubmit(theForm)`

On every submit attempt, the script first clears any prior messages by setting `errorDiv.innerHTML = ""`. It then calls field validators and concatenates their returned error strings:

- `validateUsername(theForm.username)`
- `validatePassword(theForm.pwd)`
- `validateEmail(theForm.email)`
- `validatePhone(theForm.phone)`
- `validateEmpty(theForm.from)`

If any validator returns an error, the combined errors are wrapped in a heading and unordered list (`<h2>Errors</h2><ul>...</ul>`) and displayed in `errorDiv`, and the function returns `false` to block submission. If no errors exist, it returns `true`, allowing the browser to submit to `test.html`.

### Field rules enforced by JavaScript

**Required field check (`validateEmpty`)**
 After trimming whitespace, the field must contain at least one character.

**Username (`validateUsername`)**
 Rules:

- Required (must not be empty).
- Length must be 5–15 characters.
- Only letters, digits, and underscores are allowed.
  - Implemented by rejecting `\W` (any character not in `[A-Za-z0-9_]`).

**Password (`validatePassword`)**
 Rules:

- Required (must not be empty).
- Length must be 7–15 characters.
- Only letters and digits are allowed; underscores and symbols are rejected.
  - Implemented by rejecting `[\W_]` (non-word characters and underscore).
- Must contain at least one letter and at least one digit.

**Email (`validateEmail`)**
 Rules (demonstration-level, not RFC-complete):

- Required (must not be empty).
- Must match a basic email pattern (`emailFilter`).
- Must not contain certain punctuation characters: parentheses, angle brackets, commas, semicolons, colons, backslashes, quotes, or square brackets.

**Phone (`validatePhone`)**
 Rules:

- Required (must not be empty).
- All non-digit characters are removed.
- After stripping non-digits, the number must contain exactly 10 digits (assumes an area code).

### HTML5 validation on Alternate Email

The “Alternate email” field (`altemail`) uses HTML validation attributes:

- `required`: prevents submission if empty.
- `pattern="..."`: prevents submission if the value does not match the given regular expression.

This field is not validated by the JavaScript functions, so failures on `altemail` will be reported by the browser’s native validation UI rather than appearing in `errorDiv`, and the field will not receive the Yellow/White styling logic from the JavaScript validators.