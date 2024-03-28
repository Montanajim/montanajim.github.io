# JavaScript Classes



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
        var fullName = this.fname + " " + this.lname + ", " + this.city;
        return fullName;
      }
    }

    // Lists containing names and cities for random generation
    var firstList = ["John", "Mary", "Abe", "Jim", "Stanley", "Salley", "Ann"];
    var lastList = ["Rodes", "Smith", "Miller", "Jones", "Stucci", "Kindreck", "Patton"];
    var cityList = ["Kali", "Polson", "Libby", "Whitefish", "Dayton", "Noxon", "Bozeman"];

    var people = new Array(); // Array to store Person objects

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

      var test = ""; // Temporary string for building output (not used in final version)

      for (var i = 0; i < numPeople; i++) {
        var rfname = firstList[RandomIntMax(firstList.length - 1)]; 
        var rlname = lastList[RandomIntMax(lastList.length - 1)]; 
        var rcity = cityList[RandomIntMax(cityList.length - 1)]; 

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
      var strpeople = "";

      for (var i = 0; i < people.length; i++) {
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

