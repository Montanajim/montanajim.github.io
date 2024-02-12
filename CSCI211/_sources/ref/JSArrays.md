# Arrays



A **JavaScript array** is a **special variable** that can hold more than one value. Here are the key points about arrays:

1. **Definition**:

   - An array is an **ordered list of values**.
   - Each value in an array is called an **element**.
   - [Elements within an array can be of **mixed types**, including numbers, strings, objects, and even other arrays ](https://www.w3schools.com/js/js_arrays.asp)[1](https://www.w3schools.com/js/js_arrays.asp)[2](https://www.javascript.com/learn/arrays).

1. **Dynamic Nature**:

   - JavaScript arrays are **dynamic**, meaning they can **grow or shrink** as needed.
   - [You can add or remove elements dynamically during runtime ](https://www.w3schools.com/js/js_arrays.asp)[3](https://www.javascripttutorial.net/javascript-array/).

1. **Zero-Indexed**:

   - Array elements are accessed using **indexes**.
   - The **first element** has an index of **0**, the second has an index of **1**, and so on.
   - The **last element** is at the value of the array’s **length property minus 1** [1](https://www.w3schools.com/js/js_arrays.asp).

1. **Creating Arrays**:

   - You can create an array using an array literal :

     ```javascript
     const cars = ["Saab", "Volvo", "BMW"];
     ```

     

   - Alternatively, you can use the `new Array()` constructor:

     ```javascript
     const cars = new Array("Saab", "Volvo", "BMW");
     ```

     

   - [However, the **literal method** is preferred for simplicity and execution speed ](https://www.w3schools.com/js/js_arrays.asp)[1](https://www.w3schools.com/js/js_arrays.asp).

1. **Accessing Elements**:

   - Array elements are accessed by index :

     ```javascript
     const cars = ["Saab", "Volvo", "BMW"];
     let car = cars[0]; // Accesses the first element ("Saab")
     ```

   - Remember that array indexes start with **0**.

1. **Changing Elements**:

   - You can modify an array element by assigning a new value:

     ```javascript
     const cars = ["Saab", "Volvo", "BMW"];
     cars[0] = "Opel"; // Changes the first element to "Opel"
     ```

1. **Converting to a String**:

   - The `toString()` method converts an array to a comma-separated string:

     ```javascript
     const fruits = ["Banana", "Orange", "Apple", "Mango"];
     const result = fruits.toString(); // Result: "Banana,Orange,Apple,Mango"
     ```

     

1. **Arrays as Objects**:

   - Arrays are a special type of objects.
   - They use **numbers as keys** to access elements.
   - Unlike regular objects, which use **names as keys**, arrays are best described as arrays.



## Properties

1. **Resizable and Mixed Data Types**:

   - JavaScript arrays are **resizable**, meaning you can add or remove elements dynamically.
   - They can contain a **mix of different data types** (e.g., numbers, strings, objects) within the same array.
   - If these characteristics are undesirable, consider using **typed arrays** instead [1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

1. **Zero-Indexed**:

   - JavaScript arrays are zero-indexed

     . This means:

     - The **first element** of an array is at index **0**.
     - The **second element** is at index **1**, and so on.
     - The **last element** is at the value of the array’s **length property minus 1**.

   - You access array elements using **nonnegative integers** (or their respective string form) as indexes 1.

1. **Not Associative Arrays**:

   - Unlike associative arrays, where elements can be accessed using arbitrary strings as indexes, JavaScript arrays use **nonnegative integers**.
   - You cannot access array elements using arbitrary strings directly.
   - Instead, you must use valid integer indexes [1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

1. **Shallow Copies**:

   - When you perform array-copy operations, JavaScript creates **shallow copies**.
   - This means that the copied array shares references to the same objects (rather than creating new copies of the objects).
   - Keep this in mind when working with arrays [1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

1. **Length and Numerical Properties**:

   - An array’s **length property** and **numerical properties** are connected.
   - Built-in array methods (e.g., `join()`, `slice()`, `indexOf()`) consider the array’s length when called.
   - Other methods (e.g., `push()`, `splice()`) also update the array’s length property [1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).



## Lecture Code

```javascript
<!DOCTYPE html>

<html>
    <head>
        <title>Arrays</title>

        <script>

            function printArray(array, tagId, heading)
            {
                var arrayItem = "";

                for (var cntr = 0; cntr < array.length; cntr++)
                {
                    arrayItem = arrayItem + array[cntr] + "<br>";
                }

                document.getElementById(tagId).innerHTML =
                        "<font color = 'blue' > " +
                        heading +
                        "</font><br>" +
                        arrayItem +
                        "<hr>";
            }


            function arrayFindItem(array, value)
            {
                var found = array.indexOf(value);

                return found;
            }

        </script>

    </head>
    <body>

        <p id="p0"></p>
        <p id="p1"></p>
        <p id="p2"></p>
        <p id="p3"></p>
        <p id="p4"></p>
        <p id="p5"></p>
        <p id="p6"></p>
        <p id="p7"></p>
        <p id="p8"></p>
        <p id="p9"></p>
        <p id="p10"></p>
        <p id="p11"></p>
        <p id="p12"></p>
        <p id="p13"></p>
        <p id="p14"></p>
        <p id="p15"></p>
        <p id="p16"></p>
        <p id="p17"></p>

        <script>
            //create an array
            var cities = ["New York", "Los Angles", "Chicago", "Houston",
                "Phoenix", "San Diego", "Dallas", "Kalispell"];

            //print the array            
            printArray(cities, "p0", "Array Contents");


            //get individual elements of the array.   
            //arrayName[element number]

            document.getElementById("p1").innerHTML =
                    cities[0] + "<br>" +
                    cities[2] + "<br>" +
                    cities[4] + "<br><hr>";

            //Remove an array time from the back of the array
            var x = cities.pop();

            printArray(cities, "p2", ".pop() - remove from the end");

            console.log(x);

            //Add item to the end of the array using push
            cities.push("Toledo", "Big Fork");

            printArray(cities, "p3", ".push() - add an item to the end");

            //Sort the array
            cities.sort();

            printArray(cities, "p4", ".sort() - sort the array");

            //Reverse the array order
            cities.reverse();

            printArray(cities, "p5", ".reverse() - reverse the array");

            //Shift  - remove the element - shift items to the left
            cities.shift();

            printArray(cities, "p6",
                    ".shift()- remove first and shift to the left");

            //Unshift - put a new element in the first position
            cities.unshift("Las Vegas");

            printArray(cities, "p7",
                    ".unshift()- insert new item in the first position");

            //Create a string using the join command
            //Note whatever is between the '' is the delimiter
            //you designate

            var cityString = cities.join('*');

            document.getElementById("p8").innerHTML =
                    "<font color='blue'>Join Example</font><br>" +
                    cityString +
                    "<br><hr>";

            //Create an array from a string

            var myNames = "Jim,Bob,George,Harry,Daryl,Daryl";

            //split the string on the delimiter "what's in the quotes"
            //and put it into an array

            var arrNames = myNames.split(',');


            printArray(arrNames, "p9",
                    ".split()- split a string into an array");


            //Splice - delete an element by index
            cities.splice(1, 1);

            printArray(cities, "p10",
                    ".splice()- delete one item by index");

            //Splice command - insert items starting at a specific index
            cities.splice(1, 0, "Dixon", "Whooville", "Helena");

            printArray(cities, "p11",
                    ".splice()- Insert Items at a specific index");

            //Splice command - delete and replace items
            cities.splice(1, 2, "Billings", "Missoula");

            printArray(cities, "p12",
                    ".splice()- Replace 2 items");

            //Slice copy of a port of the array as a string
            var yy = cities.slice(2, 5);

            document.getElementById("p13").innerHTML =
                    "<font color='blue'>Slice Example</font><br> " +
                    yy +
                    "<br><hr>";

            //show the array
            printArray(cities, "p14", "Show Array");

            //find an item - found
            var searchItem = "Chicago";

            var foundStatus = arrayFindItem(cities, searchItem);

            document.getElementById("p15").innerHTML =
                    '<font color="blue">Search Example - found returns ' +
                    'index</font><br>' +
                    foundStatus + '&nbsp;&nbsp;' + cities[foundStatus] +
                    '<br><hr>';

            //find item - not found
            var searchItem = "HooBoo";

            var foundStatus = arrayFindItem(cities, searchItem);

            document.getElementById("p16").innerHTML =
                    '<font color="blue">Search Example - not found returns ' +
                    'a negative number</font><br>' +
                    foundStatus +
                    '<br><hr>';

            //shorten the array
            cities.length = 2;

            printArray(cities, "p17", "Length - Shorten The Array");

        </script>
    </body>
</html>

```

---

