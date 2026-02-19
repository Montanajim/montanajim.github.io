# Objects By Class



JavaScript classes are a relatively new way to structure code using object-oriented programming (OOP) principles. While JavaScript itself is prototype-based, classes act like syntactic sugar on top of that foundation, making it easier for programmers coming from other OOP languages like Java or C++ to adapt.

Here's a breakdown of key concepts in JavaScript classes:

- **Structure:** Classes are defined using the `class` keyword. Inside the class, you can define properties (like variables) and methods (like functions) that act on the data.
- **Constructors:** A constructor is a special method called with the `new` keyword when creating a new object (called an instance) from the class. It's typically used to initialize the object's properties.
- **Inheritance:** Classes can inherit properties and methods from other classes, promoting code reuse.
- **Encapsulation (sort of):** While JavaScript doesn't have strict public/private access modifiers like some languages, you can simulate encapsulation using conventions like starting property names with underscores to discourage direct modification outside the class.

JavaScript introduced private members with the introduction of classes in ES6 (ECMAScript 2015).

Here's a breakdown of private members in JavaScript:

**Declaring Private Members:**

- Private members are denoted using a hash (#) symbol before the property name.
- This creates a special kind of property that cannot be accessed directly outside of the class.

**Benefits of Private Members:**

- **Encapsulation:** Protects internal state of the object from unintentional modification.
- **Abstraction:** Exposes only necessary functionalities through public methods.
- **Reduced naming conflicts:** Protects private members from clashes with public names.

**Limitations:**

- **Accessibility:** While private members are enforced by JavaScript, a determined developer can still access them through trickery. However, it's generally not recommended practice.
- **Constructors:** Constructors themselves cannot be private in JavaScript.



Overall, JavaScript classes provide a familiar way to structure object-oriented code, making it easier to reason about complex applications and maintain larger codebases.

Here are some resources to learn more about JavaScript classes:

- JavaScript Classes - MDN Web Docs: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/class
- JavaScript Classes – How They Work with Use Case Example: https://www.freecodecamp.org/news/javascript-classes-tutorial/

---

For the example below: 

The `Person` class has the following constructor parameters:

- `fname`: The first name of the person.
- `lname`: The last name of the person.
- `city`: The city where the person lives.

The `Person` class also has the following methods:

- `getfname`: A getter method that returns the value of the `fname` property.
- `setfname`: A setter method that sets the value of the `fname` property.
- `getlname`: A getter method that returns the value of the `lname` property.
- `setlname`: A setter method that sets the value of the `lname` property.
- `getcity`: A getter method that returns the value of the `city` property.
- `setcity`: A setter method that sets the value of the `city` property.
- `fullNameCity`: A method that returns the full name of the person and the city where they live.

## Lecture Code

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Classes Objectes</title>

  <script>
    // Define a Person class to represent a person with first name, last name, and city
    class Person {

      // Constructor to initialize a Person object with given name and city
      constructor(fname, lname, city) {
        this.fname = fname;
        this.lname = lname;
        this.city = city;
      }

      // Getters and Setters for accessing and modifying properties
      get getfname() {
        return this.fname;
      }

      set setfname(fname) {
        this.fname = fname;
      }

      get getlname() {
        return this.lname;
      }

      set setlname(lname) {
        this.lname = lname;
      }

      get getcity() {
        return this.city;
      }

      set setcity(city) {
        this.city = city;
      }

      // Method to return the full name of the person along with their city
      fullNameCity() {
        let fullName = this.fname + " " + this.lname + ", " + this.city;
        return fullName;
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

    // Function to generate a random integer between min (inclusive) and max (inclusive)
    function RandomIntMinMax(min, max) {
      // + 1 to make the max inclusive
      return Math.floor(Math.random() * ((max + 1) - min) ) + min;
    }

    // Function to create a specified number of Person objects with random names and cities
    function createPeople(numPeople) {

      let test = ""; // Temporary string for building output (not used in final version)

      for (let i = 0; i < numPeople; i++) {
        let rfname = firstList[RandomIntMax(firstList.length - 1)]; 
        let rlname = lastList[RandomIntMax(lastList.length - 1)]; 
        let rcity = cityList[RandomIntMax(cityList.length - 1)]; 

        // Uncomment these lines to display temporary output during person creation (for debugging purposes)
        //test = test + (rfname + " " + rlname + ", " + rcity +"\n<br>");

        xperson = new Person(rfname, rlname, rcity);
        people[i] = xperson;
      }

      // Uncomment this line to display temporary output after person creation (for debugging purposes)
      //document.getElementById("test").innerHTML = test;
    }

    // Function to display the full names and cities of all Person objects in the people array
    function displayPeople() {
      let strpeople = "";

      for (let i = 0; i < people.length; i++) {
        strpeople = strpeople + people[i].fname + " " + people[i].lname + 
          " " + ", " + people[i].city + "\n<br>";
      }

      document.getElementById("test2").innerHTML = strpeople;
    }
  </script>

</head>
<body>

  <p id="test"></p>
  <br><hr><br>
  <p id="test2"></p>
  
  <script>
    createPeople(5);
    displayPeople();
  </script>
</body>
</html>

```



## Explaination

This code creates a webpage that allows users to generate a random list of people with names and city locations. Here's a breakdown of the different sections:

**HTML Structure (head and body):**

- Defines the document type (`<!DOCTYPE html>`)

- Sets the language to English (`<html lang="en">`)

- Creates the 

  ```
  <head>
  ```

   section containing document metadata:

  - Character encoding (`<meta charset="utf-8">`)
  - Viewport configuration for responsive design (`<meta name="viewport" content="width=device-width">`)
  - Page title (`<title>Objects By Class</title>`)
  - Styles for the content area (`<style>...</style>`)

- Creates the 

  ```
  <body>
  ```

   section containing the visible content:

  - A styled content area (

    ```
    <div class="theContent">...</div>
    ```

    )

    - Page heading (`<h1>Objects By Class</h1>`)

    - Line break, horizontal rule, and another line break for separation

    - User input for number of people (

      ```
      <label>...<input>...<button>...
      ```

      )

      - Label (`<label>`) explains the input field
      - Input field (`<input>`) allows users to enter a number between 0 and 25
      - Button (`<button>`) triggers the `createPeople()` function on click

    - Paragraph element with an empty ID (`<p id="ppl"></p>`) to display the generated list

    - Link to another webpage (`<a href="personObject.html">Objects By Function</a>`)

**JavaScript Code (script):**

- Defines a 

  ```
  Person
  ```

   class to represent a person:

  - Constructor (`constructor(fname, lname, city)`) initializes a new `Person` object with first name, last name, and city properties.
  - Getter and setter methods for each property:
    - `getfname`, `setfname` for first name
    - `getlname`, `setlname` for last name
    - `getcity`, `setcity` for city
  - `fullNameCity()` method that returns the full name of the person with their city (e.g., John Smith, Kali)

- Creates three lists containing names and locations for random generation:

  - `firstList`: Array of first names
  - `lastName`: Array of last names
  - `cityList`: Array of city names

- Creates an empty array called `people` to store `Person` objects.

- Defines two helper functions for generating random integers:

  - `RandomIntMax(max)` generates a random integer between 0 (inclusive) and `max` (inclusive).
  - `RandomIntMinMax(min, max)` generates a random integer between `min` (inclusive) and `max` (inclusive).

- Defines the 

  ```
  createPeople()
  ```

   function:

  - Clears the `people` array (`people.length = 0`).

  - Gets the number of people entered by the user (`numPeople`).

  - Limits the number of people to 25 if the user enters a higher value.

  - Loops to create the specified number of 

    ```
    Person
    ```

     objects:

    - Randomly selects first name, last name, and city from the respective lists.
    - Creates a new `Person` object with the random names and city.
    - Adds the new `Person` object to the `people` array.

  - Clears the user input field (`document.getElementById("numppl").value = ""`).

  - Calls the `displayPeople()` function to show the generated list.

- Defines the 

  ```
  displayPeople()
  ```

   function:

  - Initializes an empty string (`strpeople`) to store the list.

  - Loops through the 

    ```
    people
    ```

     array:

    - For each `Person` object, retrieves their full name and city using the `fullNameCity()` method.
    - Appends the full name and city information to the `strpeople` string with line breaks for formatting.

  - Sets the content of the paragraph element with ID "ppl" to the generated list (`document.getElementById("ppl").innerHTML = strpeople`).

**Overall Functionality:**

1. When the webpage loads, the user sees a heading, input field for number of people, a button labeled "Enter", and an empty paragraph area.
1. The user enters a number between 0 and 25 (or keeps the default 0) and clicks the "Enter" button.
1. The `createPeople()` function is triggered.
1. The function generates the specified number of `Person` objects with random names and cities.
1. It then displays the full name and city information of each person in the paragraph area with line breaks for better readability.
