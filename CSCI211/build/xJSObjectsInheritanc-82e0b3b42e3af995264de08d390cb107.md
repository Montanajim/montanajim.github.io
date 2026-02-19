# Objects Inheritance



JavaScript inheritance allows you to create new classes (subclasses) that inherit properties and methods from existing classes (parent classes). This promotes code reusability and helps you organize your code in a hierarchical way.

Here's a breakdown of key concepts in JavaScript inheritance:

**Classes and Inheritance:**

- **Classes:** JavaScript uses the `class` keyword to define classes. A class acts as a blueprint for creating objects that share the same properties and methods.
- **Inheritance:** The `extends` keyword is used to create a subclass that inherits from a parent class. The subclass can access and use the properties and methods defined in the parent class.
- **Super Class (Parent Class):** The class from which properties and methods are inherited.
- **Sub Class (Child Class):** The class that inherits properties and methods from the super class.

**Benefits of Inheritance:**

- **Code Reusability:** By inheriting properties and methods from a parent class, you avoid duplicating code for common functionality.
- **Code Maintainability:** Changes made to the parent class are automatically reflected in all subclasses that inherit from it, making maintenance easier.
- **Polymorphism:** Inheritance allows for polymorphic behavior, where subclasses can override methods inherited from the parent class to provide their own implementation.

**How Inheritance Works in JavaScript:**

1. **Define the Parent Class:** You start by defining the parent class using the `class` keyword. This class will contain the properties and methods that you want subclasses to inherit.
1. **Create the Subclass:** To create a subclass that inherits from the parent class, you use the `extends` keyword after the class name. This establishes a connection between the subclass and the parent class.
1. **Accessing Inherited Properties and Methods:**

- A subclass automatically inherits all the properties and methods defined in the parent class.
- You can access these inherited properties and methods directly within the subclass using the `this` keyword.

1. **Overriding Inherited Methods:** Subclasses can override inherited methods from the parent class to provide their own implementation. This allows for customization of behavior specific to the subclass.



## Lecture Code

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>Objects By Class</title>
  <style>
    .theContent {
      width: 40%;
      margin: 100px auto;
      background-color: bisque;
      padding: 40px;
      color: black;
    }
  </style>
  <script>
    class Person {
      constructor(fname, lname) {
        this.fname = fname;
        this.lname = lname;
      }

      getFullName() {
        return `${this.fname} ${this.lname}`;
      }
    }

    // ------- End Of Class --------------

    class Student extends Person {
      constructor(fname, lname, college, major) {
        super(fname, lname); // Call the parent class constructor
        this.college = college;
        this.major = major;
      }

      allinfo() {
        return `${this.fname} ${this.lname} - ${this.college}, ${this.major}`;
      }

      nameinfo() {
        return `${this.fname} ${this.lname}`;
      }
    }

    // ------- End Of Class --------------

    // Lists containing names and cities for random generation
    let firstList = ["John", "Mary", "Abe", "Jim", "Stanley", "Salley", "Ann"];
    let lastList = ["Rodes", "Smith", "Miller", "Jones", "Stucci", "Kindreck", "Patton"];
    let collegeList = ["MSU", "UM", "Montana Tech", "Ohio State", "Stanford", "FVCC", "MIT"];
    let majorList = ["Comp Sci", "Engineering", "Theater", "Math", "Geology", "AI", "Pre Med", "Pre Law"];
    let people = new Array(); // Array to store Person objects

    // Function to generate a random integer between 0 (inclusive) and max (inclusive)
    function RandomIntMax(max) {
      // + 1 to make the max inclusive
      return Math.floor(Math.random() * (max + 1));
    }

    // Function to create a specified number of Person objects with random names and cities
    function createPeople() {
      people.length = 0;
      let numPeople = Number(document.getElementById("numppl").value);
      if (numPeople > 25) {
        numPeople = 25;
      }
      for (let i = 0; i < numPeople; i++) {
        let rfname = firstList[RandomIntMax(firstList.length - 1)];
        let rlname = lastList[RandomIntMax(lastList.length - 1)];
        let rcollege = collegeList[RandomIntMax(collegeList.length - 1)];
        let rmajor = majorList[RandomIntMax(majorList.length - 1)];
        let xperson = new Student(rfname, rlname, rcollege, rmajor);
        people[i] = xperson;
      }
      document.getElementById("numppl").value = "";
      displayPeople();
    }

    // Function to display the full names and cities of all Person objects in the people array
    function displayPeople() {
      let strpeople = "";
      strpeople += " <ol>";
      for (let i = 0; i < people.length; i++) {
        strpeople +=
          ` <li> ${people[i].getFullName()} <br> ${people[i].allinfo()} <br> <br> </li>`;
      }
      strpeople += " </ol>";
      document.getElementById("ppl").innerHTML = strpeople;
    }
  </script>
</head>

<body>
  <div class="theContent">
    <h1>Inheritance</h1>
    <br><hr><br>
    <label for="numppl">Enter the number of people:</label>
    <input type="number" id="numppl" min="0" max="25" value="0" placeholder="1-25">
    <button onclick="createPeople()">Enter</button>
    <p id="ppl"></p>
  </div>
</body>

</html>

```



## Explanation

This code creates a simple web page that allows you to generate a list of random student objects. Here's a breakdown of the different sections:

**HTML (Structure and Styling):**

- The HTML portion of the code defines the structure of the webpage using elements like `<html>`, `<head>`, `<body>`, etc.
- It sets the character encoding (`<meta charset="utf-8">`) and viewport size (`<meta name="viewport" content="width=device-width">`) for proper display.
- The `<title>` tag sets the title of the page to "Objects By Class".
- The `<style>` section defines styles for the content area using the class `.theContent`. This class sets the width, margin, background color, padding, and text color for the content.

**JavaScript (Creating Classes and Functionality):**

- The `<script>` section contains the JavaScript code responsible for creating the functionality of the page.

**1. Defining Classes:**

- `Person` Class:

   This class represents a generic person with two properties: 

  ```
  fname
  ```

   (first name) and 

  ```
  lname
  ```

   (last name).

  - The constructor (`constructor(fname, lname)`) takes the first and last names as arguments and assigns them to the corresponding properties.
  - The `getFullName()` method returns the full name of the person by concatenating the first and last names.

- `Student` Class:

   This class extends the 

  ```
  Person
  ```

   class, inheriting its properties and methods. It adds an additional property, 

  ```
  college
  ```

   and 

  ```
  major
  ```

  , to represent a student.

  - The constructor (`constructor(fname, lname, college, major)`) takes the first name, last name, college, and major as arguments and assigns them to the corresponding properties. It also calls the `super(fname, lname)` constructor to initialize the inherited properties from the `Person` class.
  - The `allinfo()` method returns a formatted string containing the student's full name, college, and major.
  - The `nameinfo()` method is the same as the `getFullName()` method from the `Person` class, just with a different name.

**2. Data and Functions:**

- Several lists (`firstList`, `lastName`, etc.) contain pre-defined names and colleges for random generation.

- The `people` array is used to store the created `Student` objects.

- The `RandomIntMax(max)` function generates a random integer between 0 (inclusive) and the specified `max` value (inclusive).

- The 

  ```
  createPeople()
  ```

   function:

  - Clears the `people` array.
  - Retrieves the number of people entered in the input field (`numppl`).
  - Limits the number of people to 25 if the entered value is greater.
  - Loops for the specified number of people:
    - Randomly selects a first name, last name, college, and major from the respective lists.
    - Creates a new `Student` object with the selected information.
    - Adds the created `Student` object to the `people` array.
  - Clears the input field and calls the `displayPeople()` function.

- The 

  ```
  displayPeople()
  ```

   function:

  - Initializes an empty string `strpeople`.

  - Starts an ordered list (`<ol>` tag).

  - Loops through the 

    ```
    people
    ```

     array:

    - For each student object, it uses template literals (`backticks ```) to create a formatted list item (`<li>`) containing the student's full name (from `getFullName()`), all information (from `allinfo()`), and line breaks.

  - Closes the ordered list and sets the inner HTML content of the element with the id "ppl" to the formatted string `strpeople`. This displays the list of students on the webpage.

**Overall Functionality:**

When you load the page, you'll see a heading "Inheritance", a label for entering the number of people (with a limit of 25), an input field, and a button labeled "Enter".

- Entering a number (between 0 and 25) and clicking the "Enter" button will trigger the `createPeople()` function.
- This function will generate the specified number of random student objects and store them in the `people` array.
- The `displayPeople()` function will then format and display these student objects on the page as a list.