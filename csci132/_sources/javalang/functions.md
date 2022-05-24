# Functions 

## Key Ideas

* Definition
* Readings
* Examples



## Readings

https://books.trinket.io/thinkjava/chapter4.html

https://books.trinket.io/thinkjava/chapter6.html

https://www.geeksforgeeks.org/methods-in-java/?ref=gcse



## Definition

It is important to segment the code, break it into chunks.  This is done by creating **functions**. Using functions have the following advantages:

* **Reusability**  - a function will allow code to be reused when needed. 

```{admonition} Helpful Tip
  If you have coded the same thing more than once, that code should be turned into a function.
```

* **Organization** - It allows large complex programs to be broken down into smaller steps.
* **Testing** - Functions can be easily tested for errors.



```{Tip}
The term functions and methods are usually interchangeable. The do the same thing.  However, the term method is usually applied to a function in a class that has a public interface - meaning it can be called by the created object of that class.
```





## Concepts

- Function form that takes parameters and returns a variable / data
- Function form that takes parameters and returns nothing (displays answer in function)
- Function form that takes no parameters and returns a variable / data
- Function form that takes no parameters and returns nothing (does everything within the function)





**Structure Of A Function**

```{admonition} Function 
```java
static datatype functionName(arguments)
{
	// if the function does a calculation
	// the datatype will always match the 
	// answer of that calculation
	
	// datatypes are int, long, float, double
	// boolean,chr, String, Object
	// void is used when the function does
	// return anything to whatever other function called it
	
	// arguments are the values sent 
	// to the function - they are optional
	
	//code goes here


	// if there is a datatype define then 
	// then there will always be a return
	// with a variable of the same datatype
	return aVariable;
}

static void main()
{
	//call the function
	functionName(arguments)
}

```
Functions are always called by other functions, including main(). 

Suppose a programmer wants to write a function to convert inches to feet. There are four ways to write the function pending if the function is supplied arguments or not and whether the function or the main program displays the answer.

|Options|With Arguments(arguments)|Without Arguments () - empty|
|--------|--------------|-----------------|
|**Return answer**|<span style="font-size: 12px">static double inchesFeet(double inches)<br/>{<br/>    double ans = 0;<br/>    ans = inches / 12.0;<br/>    return ans;<br/>}</span>|<span style="font-size: 12px">static double inchesFeet()<br/>{<br/>    double ans = 0;<br/>    inches = 0;<br/>    <br/>    System.out.print("Enter inches: ");<br/>    inches = Double.parseDouble(myScanner.nextLine());<br/>    <br/> 	ans = inches / 12.0;<br/>    return ans;<br/>}</span>|
|**Display answer**|<span style="font-size: 12px">static void inchesFeet(double inches)<br/>{<br/>    double ans = 0;<br/>    ans = inches / 12;<br/>   System.out.print("Answer is "+ ans);<br/>}</span>|<span style="font-size: 12px">static double inchesFeet()<br/>{<br/>    double ans = 0;<br/>    inches = 0;<br/>    <br/>    System.out.print("Enter inches: ");<br/>    inches = Double.parseDouble(myScanner.nextLine());<br/>    <br/> 	ans = inches / 12.0;<br/>    System.out.print("Answer is "+ ans);<br/>}</span>||



**Example**

```java
static double inchesFeet()
{
    double ans = 0;
    inches = 0;
    
    System.out.print("Enter inches: ");
    inches = Double.parseDouble(myScanner.nextLine());
    
 	ans = inches / 12.0;
    System.out.print("Answer is "+ ans);
}
```



**Example**

```java
 /*
    Programmer: James Goudy
    Project: Function Lecture Code
 */
package function_demo_rev1;

import java.util.Scanner;

public class Function_Demo_Rev1
{

    //functions can here
    //Add two numbers - Functions requires 2 numbers
    //and returns the total
    static double add2nums_a(double num1, double num2)
    {
        //Note - double num1 and double num2 act as if
        //they are within the braces
        
        //declare variables
        double ans;

        ans = num1 + num2;

        return ans;
    }

    //add two numbers B
    //Add two numbers - Functions requires 2 numbers
    //returns nothing, and displays the answer
    static void add2nums_b(double num1, double num2)
    {
        double ans;

        ans = num1 + num2;

        System.out.println("\n\nB The answer for add2nums_b is " + ans);
    }

    //add two numbers C
    //Add two numbers - the asks for the numbers
    //and returns the answer
    static double add2nums_c()
    {
        //variabls
        double ans;
        double num1 = 0;
        double num2 = 0;

        //create a scanner
        Scanner myScan = new Scanner(System.in);

        System.out.println(" C Please enter first number");
        num1 = Double.parseDouble(myScan.nextLine());

        System.out.println("C Please enter second number");
        num2 = Double.parseDouble(myScan.nextLine());

        ans = num1 + num2;

        return ans;
    }

    //add two numbers d
    //Add two numbers - the function does everything
    //Function asks for the numbers and displays the answer
    static void add2nums_d()
    {
        double ans;
        double num1 = 0;
        double num2 = 0;

        //create a scanner
        Scanner myScan = new Scanner(System.in);

        System.out.println(" D Please enter first number");
        num1 = Double.parseDouble(myScan.nextLine());

        System.out.println("D Please enter second number");
        num2 = Double.parseDouble(myScan.nextLine());

        ans = num1 + num2;

        System.out.println("\n\nB The answer for add2nums_d is " + ans);
    }

    // -------------- InClass Dogyears ----------------
    static double dogYears_a(double humanYears)
    {
        double ans = 0;

        ans = humanYears * 7;

        return ans;
    }

    static void dogYears_d()
    {
        double ans = 0;
        double humanYears = 0;

        //create a scanner
        Scanner myScan = new Scanner(System.in);

        System.out.println(" Please enter human years");
        humanYears = Double.parseDouble(myScan.nextLine());

        ans = humanYears * 7;

        System.out.println("DogYears D - Dogs years is equal to " + ans);
    }

    
    // ------------- Greetings A --------------------------
    static String Greetings_A(String firstName, String lastName, int PlayerNum)
    {
        String ans = "";
        
        ans = "Welcome " + firstName + " " + lastName + " player " + PlayerNum;
               
        return ans;
    }
    
    
    
    public static void main(String[] args)
    {
         //variables
        double xNum1 = 0;
        double xNum2 = 0;
        double xAns = 0;

        double xhumanYears = 0;
        
        String xFirstName, xLastName, xAnsString;
        int xPlayerNumber = 0;
        
        

        //create a scanner
        Scanner myScan = new Scanner(System.in);

        //Base Code
        System.out.println("Add two numbers");
        System.out.println("Please enter first number");
        xNum1 = Double.parseDouble(myScan.nextLine());

        System.out.println("Please enter second number");
        xNum2 = Double.parseDouble(myScan.nextLine());

        xAns = xNum1 + xNum2;

        System.out.println("The answer is " + xAns);

        //Example A
        System.out.println("\n\n--------- Example A ---------\n\n");

        System.out.println(" A Please enter first number");
        xNum1 = Double.parseDouble(myScan.nextLine());

        System.out.println("A Please enter second number");
        xNum2 = Double.parseDouble(myScan.nextLine());

        xAns = add2nums_a(xNum1, xNum2);

        System.out.println("A The answer for add2nums_A is " + xAns);

        //Example B
        System.out.println("\n\n--------- Example B ---------\n\n");

        System.out.println(" B Please enter first number");
        xNum1 = Double.parseDouble(myScan.nextLine());

        System.out.println("B Please enter second number");
        xNum2 = Double.parseDouble(myScan.nextLine());

        add2nums_b(xNum1, xNum2);

        //EXample C
        System.out.println("\n\n--------- Example c ---------\n\n");

        xAns = add2nums_c();

        System.out.println("C The answer for add2nums_c is " + xAns);

        //Example D
        System.out.println("\n\n--------- Example d ---------\n\n");

        add2nums_d();

        // ************** Inclass *******************************
        // Inclass - Dog Years
  		// in the style of A - parenthesis are have arguments return answer
        // in the style of D - parenthesis are empty - function does everything
        
        // ----------------- Greeting_A ---------------------
        
        System.out.println("\n\nGreeting Please enter your first name");
        xFirstName= myScan.nextLine();
        
        System.out.println("Please enter your last name");
        xLastName = myScan.nextLine();
        
        System.out.println("Please enter your player number");
        xPlayerNumber = Integer.parseInt(myScan.nextLine());
        
        xAnsString = Greetings_A(xFirstName, xLastName, xPlayerNumber);
        
        System.out.println(xAnsString);
        
        // -------------- End Of Program ----------------------------
        
        System.out.println("Thank you for using Goudy Software - good bye");
    }

    //functions can also go here
}

```



---

