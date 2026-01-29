# Objects By Function

Create objects by use of a function.



## Lecture Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>Objects By Function</title>
  <style>
    .theContent {
      width: 25%;
      margin: 100px auto; /* Combines margin properties for top/bottom and left/right centering */
      background-color: bisque;
      padding: 40px;
      color: black;
    }

    #numppl {
      width: 50px;
    }
  </style>
  <script>
    function Person(fname, lname, city) {
      this.fname = fname;
      this.lname = lname;
      this.city = city;
      this.fullname = () => {
        return this.fname + " " + this.lname + ", " + this.city;
      }
    }

    // Lists containing names and cities for random generation
    let firstList = ["John", "Mary", "Abe", "Jim", "Stanley", "Salley", "Ann"];
    let lastList = ["Rodes", "Smith", "Miller", "Jones", "Stucci", "Kindreck", "Patton"];
    let cityList = ["Kali", "Polson", "Libby", "Whitefish", "Dayton", "Noxon", "Bozeman"];

    let people = new Array(); // Array to store Person objects

    // Function to generate a random integer between 0 (inclusive) and max (inclusive)
    function RandomIntMax(max) {
      // + 1 to make the max inclusive
      return Math.floor(Math.random() * (max + 1));
    }

    function createPeople() {

      people.length = 0;

      let numPeople = Number(document.getElementById("numppl").value);

      if (numPeople > 25) {
        numPeople = 25;
      }

      for (let i = 0; i < numPeople; i++) {
        const rfname = firstList[RandomIntMax(firstList.length - 1)];
        const rlname = lastList[RandomIntMax(lastList.length - 1)];
        const rcity = cityList[RandomIntMax(cityList.length - 1)];

        const xperson = new Person(rfname, rlname, rcity); // Use `new` keyword to create a new Person object
        people[i] = xperson;
      }

      document.getElementById("numppl").value = '';
      displayPeople();
    }


    // Function to display the full names and cities of all Person objects in the people array
    function displayPeople() {
      let strpeople = "";

      for (let i = 0; i < people.length; i++) {
        strpeople += people[i].fullname() + "\n<br>"; // Use the fullname method of each Person object
      }
      console.log(strpeople);
      document.getElementById("ppl").innerHTML = strpeople;
    }
  </script>
</head>

<body>
  <div class="theContent">
    <h1>Objects By Function</h1>

    <br><hr><br>

    <label for="numppl">Enter the number of people:</label>
    <input type="number" name="numppl" id="numppl" min="0" max="25" value="0" placeholder="1-25">
    <button onclick="createPeople()">Enter</button>

    <p id="ppl"></p>

    <p><a href="index.html">Objects By Class</a></p>
  </div>
</body>

</html>

```



## Explaination

This code creates a webpage that allows users to generate a random list of people with full names and cities. Here's a breakdown of the different parts:

**HTML (Structure and Appearance):**

- The code starts with the standard HTML structure (`DOCTYPE`, `<html>`, `<head>`, `<body>`).

- Inside the `<head>` section, it defines the character encoding (`<meta charset="utf-8">`), sets the viewport for mobile devices (`<meta name="viewport"...`), and sets the page title (`<title>`).

- There's also a `<style>` section that defines styles for a class named `.theContent` (likely for a content area). This style applies width, margins, background color, padding, and text color. Another style targets the element with the id `#numppl` and sets its width.

- The `<body>` section contains the main content displayed on the webpage wrapped in a `<div>` with the class `.theContent`.

- Inside the content area (

  ```
  <div>
  ```

  ):

  - There's a heading (`<h1>`) for the page title ("Objects By Function").
  - A horizontal line (`<hr>`) for separation.
  - A label (`<label>`) for the number of people input field with the `for` attribute linking it to the input element's id.
  - An input field (`<input>`) with type "number", id "numppl", minimum value (0), maximum value (25), initial value (0), and a placeholder ("1-25").
  - A button (`<button>`) with text "Enter" that triggers the `createPeople()` function when clicked (using the `onclick` attribute).
  - A paragraph element (`<p>`) with the id "ppl" where the generated list of people will be displayed.
  - Another paragraph with a link (`<a>`) to "Objects By Class" (likely another webpage).

**JavaScript (Functionality):**

- Inside the `<head>` section, there's a `<script>` section containing the JavaScript code that makes the page interactive.

- The code defines a function called `Person(fname, lname, city)`. This function is a constructor for creating Person objects. It takes three arguments: first name (`fname`), last name (`lname`), and city (`city`). Inside the function, it uses the `this` keyword to assign these arguments as properties of the newly created object. It also defines another property called `fullname` using an arrow function. This `fullname` function returns a string by concatenating the first name, last name, comma, space, and city.

- Three lists of names and cities (`firstList`, `lastName`, `cityList`) are defined as arrays to be used for random generation. There's a typo in the code (`lastName` should be `lastIndex`).

- An empty array called `people` is created to store the Person objects.

- Another function called `RandomIntMax(max)` is defined. This function takes a maximum value (`max`) and uses `Math.random()` to generate a random floating-point number between 0 (inclusive) and the provided `max` (inclusive). It then uses `Math.floor()` to round down the number to the nearest integer, effectively making the maximum value inclusive.

- The 

  ```
  createPeople()
  ```

   function is responsible for generating the random list of people. This function first clears the 

  ```
  people
  ```

   array by setting its length to 0. Then, it retrieves the user input for the number of people using 

  ```
  document.getElementById("numppl").value
  ```

   and converts it to a number using 

  ```
  Number()
  ```

  . It checks if the user entered a value greater than 25 and limits it to 25 if so. A loop iterates for the desired number of people. Inside the loop:

  - Three random indexes are generated using the `RandomIntMax()` function for each list (first name, last name, city). These indexes are used to access and retrieve random names and a city from the respective lists.
  - A new Person object is created using the `new` keyword and the `Person` constructor, passing the retrieved random names and city.
  - The newly created Person object is then stored in the `people` array at the current loop index.

- Finally, the function clears the input field for the number of people and calls the `displayPeople()` function.

- The `displayPeople()` function is responsible for displaying the generated list of people. It initializes an empty string variable (`strpeople`). It loops through the `people` array. Inside the loop, it calls the `fullname()` method of each Person object in the array to get the full name and city information. This information is then appended to the `strpeople` string along with a newline character (`\n`) and a line break tag (`<br>`).