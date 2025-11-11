# First Program

## Key Ideas

* Declaring variables

* Creating a scanner

* Printing to the console

* Storing information from the keyboard to a variable

* Casting data from a String to a number

  

## Readings

https://books.trinket.io/thinkjava2/chapter3.html



Programs are written functions/methods. In the example below there is only one function called *main()*. 

```{admonition} Definition
**main()** is the function where the program starts and finishes.
```



**Print to the console, the following command is used:**

- ```java
  System.out.println("your text here or variable here");
  // Variable names do not get quotes around them.
  ```
  
- System.out.**println()** will move the cursor to the next line.

- System.out.**print()** will leave the cursor on the same line at the end of the text.

**Get Input From The Console**

- The library / class *java.util.Scanner* needs to be imported.

  ```java
  import java.util.Scanner;
  ```

- Create scanner

  ```java
  Scanner myScan = new Scanner(System.in);
  // NOTE: myScan is your name for the scanner
  // You can name it anything you want as long as it
  // follows the rules for variable names.
  ```

  

- Input from the scanner is stored in a variable

  - By default, all data from a scanner is a String datatype

  - To convert it into an Integer or Double use the parse command;

    ```java
    System.out.print("Please enter your first name: ");
    firstname = myScan.nextLine();
    
    System.out.print("Please enter your salary: ");
    firstname = Double.parseDouble(myScan.nextLine());
    ```

    ```{warning}
    Do not use .nextDouble(), nextInt() without using a .nextLine() to ensure the "return" is removed from the keyboard buffer.
    ```

    

**Programming Pattern**

Notice the programing pattern:

1. Asks for information from the user with a System.out.print().
2. Collect the information from the user using a scanner and store it in a variable.
3. Calculate the data
4. Return an answer using the System.out.print().




---

```{note}
The filename of the project is always the name of the public class. In the example below, the project name is J1_FirstProgrA
```





```java
/*
Names:  Jim Goudy
Program: First_Program

Note: When you are naming projects - do not use spaces.
 */

import java.util.Scanner;

public class J1_FirstProgrA {

    public static void main(String[] args) {

        //variables
        String xFirstName, xLastName;
        String xCity;
        String xNickName = "Ramone";

        double xInches = 0;
        double xAnswer = 0;
        double xCentimeterss = 0;
        double xNum1, xNum2, xNum3;

        //Create a scanner
        Scanner myScan = new Scanner(System.in);

        //Create a greeting
        System.out.print("Please enter"
                + " your name: ");
        xFirstName = myScan.nextLine();

        System.out.println("Enter your city");
        xCity = myScan.nextLine();

        System.out.println("\n\nGreetings " + xFirstName + " from " + xCity);

        //convert Inches To Centimeters
        System.out.print("\nPlease \nenter a \nmeasurment in inches : ");
        xInches = Double.parseDouble(myScan.nextLine());
        xAnswer = xInches * 2.54;
        System.out.println("The is answer is" + xAnswer);

        //Centers To Inches  - divide 2.54
        System.out.print("\n\nPleaseenter a measurment in centimeters : ");
        xCentimeterss = Double.parseDouble(myScan.nextLine());
        xAnswer = xCentimeterss / 2.54;
        System.out.println("The is answer is" + xAnswer);

        //Add three numbers
        System.out.println("Add three numbers\nEner the first number");
        xNum1 = Double.parseDouble(myScan.nextLine());

        System.out.println("Ener the second number");
        xNum2 = Double.parseDouble(myScan.nextLine());

        System.out.println("Ener the third number");
        xNum3 = Double.parseDouble(myScan.nextLine());

        xAnswer = xNum1 + xNum2 + xNum3;

        System.out.println("\nThe sum of three numbers is " + xAnswer);

        /*
        //DO NOT USE THIS IN JIM'S CLASS!!!!!!!!!!!!!!!!!!!!
        System.out.println("Enter a number");
        xInches = myScan.nextDouble();  
        System.out.println("Enter your FirstName xxxxx- ");
        xFirstName = myScan.nextLine();
        
        NOTE: Suppose the user enters the number 42.  They literally press the
        "4" key, the "2" key and the "enter" key. Because the 
        "myScan.nextDouble()" only takes the numbers, it does not 
        take the enter key - which is left in the keyboard buffer.  
        nextLine() excutes when it sees an enter key in the buffer.  Since the 
        nextDouble() does not clear the enter key, it is still left over for
        the nextLine(), which will excecute immediately and not allow the user
        to enter their name.
        */
   
        //Message to let the user know the program is finished.
        System.out.println("Thank you for using my software");

    }
}

```





---

End Of Topic



