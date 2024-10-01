# Lambda Functions

## Key Ideas

* Lambda functions



```{admonition} Definition
**Lambda Function** is an anonymous function that can take arguments, but only has one expression / only one formula.
```



**Key Points:**

- **Lambda Functions:** The code demonstrates the use of lambda functions, which are concise anonymous functions often used for inline expressions.
- **List/Array:** It creates a list of numbers and performs various operations on it.
- **Function Calls:** Functions are called to print the numbers and calculate their sum.
- **Output:** The program prints the numbers, their sum using both traditional and lambda functions, and a final "Bye bye" message.

**Code Breakdown:**

1. **Lambda Function Definition:**
   - `num Sum3Lambda(num xx, yy, zz) => (xx + yy + zz);` defines a lambda function that takes three numbers as input and returns their sum. The arrow (`=>`) syntax is used to concisely define the function body.
1. **Traditional Function Definition:**
   - `void printNums(var alist) { ... }` defines a traditional function that takes a list as input and prints its elements using a `for` loop.
1. **Main Function:**
   - The `main` function is the entry point of the program.
   - It creates a list of numbers.
   - Calls the `printNums` function to print the numbers using a traditional function.
   - Uses the `forEach` method with a lambda function to print the numbers concisely.
   - Calculates and prints the sum of the first three numbers using both `Sum3` and `Sum3Lambda` functions.
   - Prints a final "Bye bye" message.





```dart
import 'dart:io';

//in Dart, if you can write a function in one line
//then it can be written as a lambda function.

//traditional form of a function
void printNums(var alist) {
  for (var item in alist) {
    stdout.write(item.toString() + " ");
  }
}

//Sum 3 numbers
num Sum3(num xx, num yy, num zz) {
  num ans = 0;

  ans = xx + yy + zz;

  return ans;
}

//Sum 3 numbers written as a Lambda Function
num Sum3Lambda(num xx, yy, zz) => (xx + yy + zz);

main(List<String> arguments) {

  //List / array
  var someNums = [10, 20, 80, 77, 26, 79, 37, 58, 8, 98, 2, 23, 54, 81, 3];

  //print numbers
  print("Print Numbers using function");

  //call function and pass the array
  printNums(someNums);

  //print numbers
  print("\n\nPrint Numbers using a lambda function");
  someNums.forEach((var item) => stdout.write(item.toString() + " "));

  print("\n\Sum 3 numbers ");
  stdout.writeln(Sum3(someNums[0], someNums[1], someNums[2]));

  print("\n\Sum 3 numbers using a lambda function");
  stdout.writeln(Sum3Lambda(someNums[0], someNums[1], someNums[2]));

  print("\nBye bye");
}

```

---

End Of Topic



