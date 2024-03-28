# Onblur Form Validation



The `onblur` attribute in HTML is used to attach an event listener to an element. This event listener fires whenever the element loses focus. In simpler terms, the function specified in the `onblur` attribute gets executed when the user clicks away from the element.

Here's a breakdown of how it works:

1. **Attaching the Event Listener:**  The `onblur` attribute is assigned to an HTML element (like `<input>`, `<textarea>`, etc.).  It takes a JavaScript expression (usually a function call) as its value.
1. **Triggering the Event:** When the user interacts with the element (clicks on it, types text, etc.) and then clicks outside the element (clicks on another element or the background), the element loses focus.
1. **Executing the Function:**  As soon as the element loses focus, the JavaScript expression specified in the `onblur` attribute gets executed. This function can perform various actions depending on the element and the desired functionality.

Here are some common use cases for the `onblur` event:

- **Validation:** You can use `onblur` to validate user input in form fields. For example, you could check if a field is empty, has the correct format (email, phone number, etc.), or meets specific criteria.
- **Dynamic Updates:** When the user leaves a field, you might use `onblur` to update other parts of the form or the webpage dynamically based on the entered value.
- **Hiding Elements:** You could use `onblur` to hide instructional text or error messages that appear when the user focuses on a field.



## Lecture Code

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Form 2b</title>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width">
  <!- By James Goudy -->
    
  <style>
    .error { /* Combined error styling for reusability */
      display: none;
      position: absolute;
      width: 200px;
      left: 160px;
      bottom: 2px;
      color: red;
      padding: 2px;
    }
    .input-container { /* Descriptive class name */
      position: relative;
    }
    #areaA {
      width: 50%;
      margin: 100px auto; /* Combined margin properties */
      background-color: navy;
      padding: 10px;
      color: white;
    }
  </style>
</head>
<body>
  <div id="areaA">
    <h1>Onblur Example</h1>
    <div class="input-container">
      <div class="error" id="nameError">Enter Your Name</div> 
      Name <input id="textboxName" type="text" style="width: 100px" 
                  onfocus="hideError(this)" onblur="validateName(this)">
    </div>
    <br>
    <div class="input-container">
      <div class="error" id="zipError"></div> 
      Zip <input id="textboxZip" type="text" style="width: 100px" 
                 onfocus="hideError(this)" onblur="validateZip(this)">
    </div>

    <form onsubmit="return validateForm()" action="test.html">
      <br>
      <input type="submit" value="Enter">
    </form>
  </div>
  <script>
    let nameValid = false;
    let zipValid = false;

    function hideError(element) {
      element.parentNode.querySelector('.error').style.display = 'none';
    }

    function validateName(element) {
      const nameInput = document.getElementById("textboxName");
      const nameError = document.getElementById("nameError");

      if (nameInput.value === "") {
        nameError.style.display = 'block';
        nameValid = false;
        return;
      }

      nameValid = true;
    }

    function validateZip(element) {
      const zipInput = document.getElementById("textboxZip");
      const zipError = document.getElementById("zipError");


      if (zipInput.value === "") {
        zipError.innerHTML = "Zip - is empty";
        zipError.style.display = 'block';
        zipValid = false;
        return;
      } else if (zipInput.value.length != 5) {
        console.log("Length arrrg")
        zipError.innerHTML = "Zip - wrong length";
        zipError.style.display = 'block';
        zipValid = false;
        return;
      } else if (isNaN(zipInput.value)) {
        console.log("nNan arrrg")
        zipError.innerHTML = "Zip - numbers only";
        zipError.style.display = 'block';
        zipValid = false;
        return;
      }

      zipValid = true;
    }

    function validateForm() {
      return nameValid && zipValid;
    }
  </script>
</body>
</html>

```



**page2.html - if there was successful form validation**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<title>test success</title>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width">
	<!-- By James Goudy -->
	
	<style>
	.areaA {
      width: 50%;
      margin: 100px auto; /* Combined margin properties */
      background-color: navy;
      padding: 10px;
      color: white;
    }
	</style>
</head>
<body>
	<div class="areaA">
	<h1>Good test<br>Form 2<br>On Blurr</h1>
	</div>
</body>
</html>
```



## Explanation

The provided code implements a simple form with two input fields and a submit button. Here's a breakdown of its functionality:

**HTML Structure:**

- The code defines a basic HTML document with a title ("Form 2b").

- It sets the character encoding to UTF-8 and ensures proper responsiveness on various devices using the viewport meta tag.

- Styles are defined within a `<style>` tag.

- The body contains a container element with the ID "areaA".

  - Inside "areaA", there's a heading (`<h1>`) displaying "Onblur Example".

  - Two input fields are created using  `<div>`  elements with the class "input-container".

    - Each input container holds:
      - An error message element (`<div>`) with the class "error" and a unique ID (initially hidden).
      - A label ("Name" or "Zip") followed by a text input field (`<input>`) with an ID and event listeners.

  - A form element (`<form>` ) is placed after the input fields.

    - The form has an "onsubmit" event listener that calls the `validateForm` function and sets the form action to "test.html" (where the form data might be submitted).
    - Inside the form, a submit button (`<input type="submit">`) is displayed with the value "Enter".

**JavaScript Functionality:**

- Two variables, `nameValid` and `zipValid`, are declared with initial values of `false`, indicating that neither field is validated by default.

- Three functions are defined:

  - `hideError(element)`: This function takes an element as input (presumably an input field). It finds the closest error element (using `querySelector`) within the same container (`parentNode`) and hides it (sets `display` to "none").

  - `validateName(element)` : This function validates the name input field.

    - It retrieves the name input element and its corresponding error element using their IDs.
    - It checks if the name input value is empty. If so, it displays the error message ("Enter Your Name"), sets the error element to visible (`display: block`), and sets `nameValid` to `false`.
    - If the name is not empty, it sets `nameValid` to `true`.

  - `validateZip(element)`  : This function validates the zip code input field. It follows a similar logic to the `validateName`  function:
  - 
    - It retrieves the zip code input element and its corresponding error element.
    - It checks if the zip code value is empty. If so, it displays an error message ("Zip - is empty"), sets the error visibility, and sets `zipValid` to `false`.
    - If the zip code is not empty, it further validates the length (must be 5 characters) and if it contains only numbers (using `isNaN`). If either validation fails, it displays an appropriate error message, sets error visibility, and sets `zipValid` to `false`. Otherwise, it sets `zipValid` to `true`.

- The `validateForm` function checks if both `nameValid` and `zipValid` are true. It returns `true` if both fields are valid, allowing form submission; otherwise, it returns `false`, preventing form submission until errors are corrected.

**Event Listeners:**

- The name and zip code input fields have two event listeners each:
  - `onfocus`: When the user focuses on an input field (clicks on it), the `hideError` function is called, presumably to hide any previous error messages for that field.
  - `onblur`: When the user leaves an input field (clicks elsewhere), the corresponding validation function (`validateName` or `validateZip`) is called to check the field's value and display any errors if necessary.

In summary, this code implements a simple form with error handling for name and zip code input fields. It ensures that the user enters a name and a valid zip code (5 digits, numbers only) before allowing form submission.