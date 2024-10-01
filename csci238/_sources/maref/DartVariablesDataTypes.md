# Dart Variables and Datatypes

## Key Ideas

* Variables
* Data Types
  * double
  * int
  * String
  * bool
  * lists
  * collections
  * unicode
  * dynamic



``` {admonition}Variables
  *Ifinitial values are not declared
  then the intial value is null*

  **ALL VARIABLES ARE OBJECTS**
```



## Lecture Code

```dart
//variables and datatypes
//Programmer: James Goudy

//import this if you want to use stdout and stdin
import 'dart:io';

void variableReview() {
  /*
  variables
  note if initial values are not declared
  then the intial value is null

  ALL VARIABLES ARE OBJECTS
  */

  print('Variable Review\n');
  //numbers
  double salary = 0.0;
  int anum = 42;

  //Note that salary is an object so the .toString() function is called
  print('double  = ' + salary.toString() + "\n");
  print('int = ' + anum.toString() + '\n');

  //String and booleans
  //note you can use both single or double quotes
  String someWord = 'This is a string';
  String someWord2 = "Yada Yada";
  bool isBreathing = true;

  print("\n Print string variable someWord:  " + someWord);

  //note a dollar sign in front of variable name
  //the dollar sign makes it a place holder in a string 
  //when attached to a variable.
  print('\n Print string variable someWord2: $someWord2');
  print("\n Print boolean variable isBreathing: " + isBreathing.toString());

  //lists / arrays - orderd list
  var nums = [10, 20, 30, 40, 50];
  var names = ["Larry", "Curly", "Moe", "Shemp"];

  print("\nPrint nums list using a for statement");
  for (int c = 0; c < nums.length; c++) {
    //import dart.io
    stdout.write(nums[c].toString() + " ");
  }

  //using a string
  String theString = " ";

  print("\n\nPrint nums list by concatenating a variable");
  for (int c = 0; c < nums.length; c++) {
    theString = theString + nums[c].toString() + " ";
  }
  print(theString);

  print("\nPrint nums list by using an anonymous function");
  nums.forEach((numsIndex) {
    stdout.write(nums.indexOf(numsIndex).toString() + " ");
  } //end of anonymous function
      ); //end of forEach function

  print("\nPrint String List of Names");
  names.forEach((stooge) => stdout.write(stooge + " "));

  //sets -  unordered collection of ** UNIQUE ** items
  var us_states = {'MT', 'OH', 'NV', 'WY', 'CO'};

  //print set
  print("\n\n Print set");
  for (var value in us_states) {
    stdout.write(value + " ");
  }
  int cs = 1;
  print('\nIndividual element at position 1 = ' + us_states.elementAt(cs));

  //maps - key : value
  var vehicles = {
    'car': 'mustang',
    'airplane': 'cessna',
    'boat': 'wellcraft',
    'truck': 'f150',
    'scooter': 'lime',
    'personal': 'segway'
  };

  print('\nPrint keys in Maps');
  for (var valueKey in vehicles.keys) {
    stdout.write(valueKey + " ");
  }

  print('\n\nPrint keys in Maps');
  for (var value in vehicles.values) {
    stdout.write(value + " ");
  }

  print("\n\nKey Value Pairs in Maps");
  vehicles.forEach((k, v) => stdout.writeln('Key=$k, Value=$v'));

  print('\n print value for the specific key of "truck"');
  print(vehicles['truck']);

  //Runes - emoji
  var personalComputer = '\u{1F4BB}';
  var camera = '\u{1F4F7}';

  print('\nPrint Runes');
  print(personalComputer + " " + camera);

  //generic var datatype - Dart will interpret the data type
  var num1 = 80;
  var num2 = 20;
  var unit = "miles";
  print("\nVar example");
  print("var add num1 + num2 = " + (num1 + num2).toString() + " $unit");

  //dynamic dataype the data type can change
  dynamic xx = "Some text"; //string
  xx = 42.0; //double
  xx = true; //boolean
  xx = '\u{1F603}'; //rune
  print("\nxx is equal to $xx\n");
}

main(List<String> arguments) {
  variableReview();

  print("\n\nGoody Bye");
}

```



---

