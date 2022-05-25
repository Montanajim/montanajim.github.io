# Iteration / Loops

## Key Ideas

* Do Loop
* While Loop
* For Loop
* For Each Loop
* Loop Pattern for Menus / Programming Structure
* Loops for grids



## Readings

https://books.trinket.io/thinkjava/chapter7.html

https://docs.oracle.com/javase/tutorial/java/nutsandbolts/while.html

https://docs.oracle.com/javase/tutorial/java/nutsandbolts/while.html



## Lecture



```{admonition} Definition
**Iteration / Loops**: the repetition of a sequence of computer instructions a specified number of times or until a condition is met. [Merriam Webster](https://www.merriam-webster.com/dictionary/iteration) 
```



### Java Loops

Iteration has several purposes:

* **Reusability** - loops allow us to repeat code as often as we wish in the form that we can write it once and run it many times.
* Loops allow us to traverse the items in a list, array, or data structure.  



## Types Of Loops

Java has four main types of loops

* **Do Loop** - This loop will *always* run once
* **While Loop** - This loop runs while a condition is true
* **For Loop** - This loop runs a specific amount of times
* **For Each Loop** - This loop is a form of the **for-loop**. It is set up to easily iteration of each item in an array, list, or data structure.



## Example Basic Loops

```java
/*
Loop Lecture Code
Programmer: James Goudy
 */
package loops;


public class Loops {

    public static void main(String[] args) {
      
        int cntr = 0;
        
        //Do Loop This loop will always run once       
        do
        {
            System.out.println(cntr + " do loop");
            
            //We have to increment a counter 
            //otherwise our while statement will never
            //go to false and we will be in a endless loop.
            cntr++;
        }while(cntr < 2000);
        
        
        //while loop - This loop will always check for true before running
        cntr = 0;
        
        while (cntr < 2000)
        {
            System.out.println(cntr + " while loop");
            cntr++;
            //We have to increment a counter 
            //otherwise our while statement will never
            //go to false and we will be in a endless loop.
        }
        
        //for statments are excellent if we have 
        //a known number of cycles to loop.
        //Also we create a cntr, check for true and increment
        //the counter all on one line.
        for(int cntr2 = 0; cntr2 < 2000; cntr2++)
        {
            System.out.println(cntr2 + " for loop");        
        }
             
    }
    
}

```



## Loop To Control Menu

* Note this is using a **while-loop** and a **switch statement**.

* This is a programming style that fits 90% of your programs.  Note that the functions are *not* calling the *menu() function*.

```java
/* Switch / 
Program: Menu Lecture
Programmer: Jim Goudy
This is a demo program to demonstrate a design pattern for creating a menu system in the console environment. 
:)----  Bob Ross Coding ---- :)

 */
package menu_lecture;

import java.util.Scanner;

public class Menu_Lecture {

    //Happy Function 1
    static void HappyFunction1() {
        System.out.println("\n\nThis is happy function 1");
    }
    
    //Happy Function 2
    static void HappyFunction2() {
        System.out.println("\n\nThis is happy function 2");
    }
    
    //Happy Function 3
    static void HappyFunction3() {
        System.out.println("\n\nThis is happy function 3");
    }

    //This function creates a menu system.
    static void menu() {     
        //variables
        int choice = 0;     //hold user choice

        //Scanner for user input
        Scanner myScan = new Scanner(System.in);

        //display the user choices
        System.out.println("\nMENU\n"
                + "\n1. Happy Function 1"
                + "\n2. Happy Function 2"
                + "\n3. Happy Function 3"
                + "\nPlease choose a function 1,2 or 3");
        choice = Integer.parseInt(myScan.nextLine());

        //take the choice stored in choice and use it in the switch
        switch (choice) {
            case 1:
                HappyFunction1();
                break;
            case 2:
                HappyFunction2();
                break;
            case 3:
                HappyFunction3();
                break;
            default:
                //default is used if the user entered any 
                //number that was note 1,2 or 3
                System.out.println("\nThat wasn't a choice");
        }
    }

    public static void main(String[] args) {

        //variables
        String quit = "n";      

        //Scanner for user input
        Scanner myScan = new Scanner(System.in);

        //quit has to be initialized with the value of n
        //so the loop will run at least once. Putting the menu
        //call in a while statement will allow the user to run
        //the program as many times as they wish.
        while (quit.equals("n")) {
            
            //call the menu
            menu();
            //prompt the user if they want to quit
            System.out.println("\nWould you like to quit -  y or n");
            quit = myScan.nextLine().toLowerCase();
        }

        //Inform the user the program is done executing
        System.out.println("Good Bye");
    }
}

```



## Loops For Printing A Grid

```java
/*
Program: Loop Lecture Grid
Programmer: James Goudy
This program demonstrates how to write a grid
using loops.  The important note is that the 
counters in the loops act as coordinate to the row and columns
of the x's that are being printed out.

 */
package loops_lecture_grid;

public class Loops_Lecture_Grid {

    public static void main(String[] args) {

        //Variables
        String xx = "x";

        int Colcntr = 0;    //This is our column counter
        int ColStop = 5;    //This is the actual number of 
        //columns for the grid

        int Rowcntr = 0;    //This is our row counter
        int RowStop = 5;    //This is the actual number of 
        //rows for the grid  

        //loop to control the number of rows
        while (Rowcntr < RowStop) {
            //loopt to control the number of columns
            while (Colcntr < ColStop) {
                //Note the print. If a println is used
                //all of the starts will print down / "vertical"
                System.out.print("x");

                //Increment the column counter to the next column
                Colcntr++;
            }

            //this represents the end of the row
            //the cursor needs to be put on the next row
            //so a println will be used.
            System.out.println("");

            //Next the Colcntr needs to be reset to zero
            Colcntr = 0;

            //Advance the rowcnter to the next row
            Rowcntr++;
        }

    }

}
```





