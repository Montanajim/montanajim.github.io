# Second Program

## Observations

Note the following:

* The programmer name and project title are in the comments.

* We can put the project requirements in the comments as well. In bigger projects this would be a separate document.

* Variables are declared at the top of the function  - **main()** . When we have more functions the variables will always go at the top, with the exception of **var**.

* Note the programming pattern

  * Ask a question 

    ```java
    System.out.print("Question?");
    ```

  * Store the response in a variable using a scanner

  * Make a calculation

  * Show the answer using another 

    ```java
    System.out.print("Answer is " + x);
    ```
	
	* Note the commenting. 



## Lecture Code

```java
/*
Name: James Goudy
Project: Example 2

Program requirements
Greeting: Name and major

Problem 1 : Calculate the circumference of a circle
Formula:    C = πRD    
            C - circumference
            π - pi 3.14
            R - Radius
            D - Diameter

Problem 2 : Calculate the volume of a prism
Formula:    V = lwd
            V - Volume
            l - length
            w - width
            d - depth

Exit Message

 */


import java.util.Scanner;

public class JavaIntro_ExampleProgram2 {

    public static void main(String[] args) {

        //Greeting Variables
        String xName;       //variable to hold name
        String xMajor;      //variable to hold major

        //Problem 1 varialbes
        double xCircumference = 0;
        final double xPI = 3.14;
        double xRadius = 0;
        double xDiameter = 0;

        //Problem 2 variables
        double xVolume = 0;
        double xLength = 0;
        double xWidth = 0;
        double xDepth = 0;

        //Create a scanner to collect keyboard information
        Scanner myScanner = new Scanner(System.in);

        // -------------------------------------------------------------
        //Greeting
        System.out.println("Please Enter your name: ");     //ask the question
        xName = myScanner.nextLine();                       //collect the answer

        System.out.println("Please enter your major: ");    //ask the question
        xMajor = myScanner.nextLine();                      //collect the answer

        //Display the greeting
        System.out.println("Hello " + xName + " from " + xMajor);

        // ------------------------- Problem 1----------------------------
        System.out.println("\nProblem 1 - Circumference");

        System.out.print("\nPlease enter the radius: ");      //ask the question
        xRadius = Double.parseDouble(myScanner.nextLine()); //collect the answer

        System.out.print("\nPlease enter the diameter: ");      //ask the question
        xDiameter = Double.parseDouble(myScanner.nextLine()); //collect the answer

        //calculate the answer
        xCircumference = xPI * xRadius * xDiameter;

        //Display the answer
        System.out.println("\nThe circumerence is " + xCircumference);

        // ------------------------- Problem 2----------------------------
        System.out.println("\nProblem 2 - Volume of a prism");

        System.out.print("\nPlease enter the length: ");      //ask the question
        xLength = Double.parseDouble(myScanner.nextLine()); //collect the answer

        System.out.print("\nPlease enter the width: ");      //ask the question
        xWidth = Double.parseDouble(myScanner.nextLine()); //collect the answer

        System.out.print("\nPlease enter the depth: ");      //ask the question
        xDepth = Double.parseDouble(myScanner.nextLine()); //collect the answer
        
        
        //calculate the answer
        xVolume = xLength * xWidth * xDepth;

        //Display the answer
        System.out.println("\nThe volume is " + xVolume);
        
        //------------------------- Exit Messasge
        System.out.println("\nThank you for using Goudy Software");

    }

}

```

---



End Of Topic
