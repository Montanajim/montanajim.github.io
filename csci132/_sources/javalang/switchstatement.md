# Switch Statement



## Key Ideas

* Switch Statement



## Readings

[If / Switch](https://www.geeksforgeeks.org/decision-making-javaif-else-switch-break-continue-jump/?ref=lbp)

[Swtich Statement](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html)



## Lecture Code


```{admonition} Definition
A switch statement acts like an if statement, but there are definite choices. The switch statement will allow specific code to run pending the choice. Swtich statements are usually used in building menus, but can be used anywhere where there is a definite choice.
```

**Example**

```java

/* Switch / Menu Demo
This is a demo program to demonstrate a design pattern for creating
a menu system in the console environment.
:)---- Bob Ross Coding ---- :)
Jim Goudy
*/

package menu_demo;
import java.util.Scanner;
public class Menu_Demo {
    
    // Happy Function 1
    static void HappyFunction1() {
    	System.out.println("\n\nThis is happy function 1");
    }
    
    // Happy Function 2
    static void HappyFunction2() {
    	System.out.println("\n\nThis is happy function 2");
    }
    
    // Happy Function 3
    static void HappyFunction3() {
        System.out.println("\n\nThis is happy function 3");
    }
    
    // This function creates a menu system.
    static void menu() {
        
        // variables
        int choice = 0; // hold user choice
        
        // Scanner for user input
        Scanner myScan = new Scanner(System.in);
        
        // display the user choices
        System.out.println("\nMENU\n"
        + "\n1. Happy Function 1"
        + "\n2. Happy Function 2"
        + "\n3. Happy Function 3"
        + "\nPlease choose a function 1,2 or 3");
        choice = Integer.parseInt(myScan.nextLine());
        
        // take the choice stored in choice and use it in the switch
        // case values can be an int, char or enum
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
            // This is optional
            // default is used if the user entered any
            // number that was note 1,2 or 3
            System.out.println("\nThat wasn't a choice");
        }
    }

    public static void main(String[] args) {
        
        // variables
        String quit = "n";
        
        // Scanner for user input
        Scanner myScan = new Scanner(System.in);
        
        // quit has to be initialized with the value of n
        // so the loop will run at least once. Putting the menu
        // call in a while statement will allow the user to run
        // the program as many times as they wish.
        
        while (quit.equals("n")) {
            // call the menu
            menu();
     
            // prompt the user if they want to quit
            System.out.println("\nWould you like to quit - y or n");
            quit = myScan.nextLine().toLowerCase();
        }
        
        // Inform the user the program is done executing
        System.out.println("Good Bye");
    }
}
```



## More Menu Examples

```java
package switch_menuexamples;

import java.util.Scanner;


public class Switch_MenuExamples {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
            
            //create variables
            int UserChoice1 = 0;
            char UserChoice2 = 'A';
            String UserChoice3 = "";

            //create a scanner for input
            Scanner myScanner = new Scanner(System.in);

            //Example One
            //Menu using integer choices
            System.out.println("Example 1 using integer choices");
            System.out.println("Choose one of the following:" +
                               "\n1. Move the character to the left" +
                                "\n2. Move the character to the right" +
                                "\n3. Move the character straight ahead" +
                                "\n4. Quit" +
                                "\nPlease choose 1, 2, 3 or 4:"
                                  );
            UserChoice1 = Integer.parseInt(myScanner.nextLine());

            switch (UserChoice1)
            {
                case 1:
                    System.out.println("Character moves to the left");
                    break;
                case 2:
                    System.out.println("Character moves to the right");
                    break;
                case 3:
                    System.out.println("Character moves straight");
                    break;
                case 4:
                    System.out.println("Quit Program");
                    break;
                default:
                    //if user chooses a value that is not 1,2,3 or 4
                    System.out.println("That was not a choice");
                    break;
            }
        
		    //Example two
            //Menu using char choices
            System.out.println("\n\nExample 2 using char choices");
            System.out.println("Choose one of the following:" +
                   "\nL  Move the character to the left" +
                    "\nR  Move the character to the right" +
                    "\nS  Move the character straight ahead" +
                    "\nQ  Quit" +
                    "\nPlease choose L, R, S or Q:"
                      );
            //NOTE the "toUpperCase()" This will convert anything typed
            //from the keyboard into uppercase.
            UserChoice2 = myScanner.nextLine().toUpperCase().charAt(0);

            switch (UserChoice2)
            {
                case 'L':
                    System.out.println("Character moves to the left");
                    break;
                case 'R':
                    System.out.println("Character moves to the right");
                    break;
                case 'S':
                    System.out.println("Character moves straight");
                    break;
                case 'Q':
                    System.out.println("Quit Program");
                    break;
                default:
                    //if user chooses a value that is not L, R, S or Q
                    System.out.println("That was not a choice");
                    break;
            }

            //Example three
            //Menu using string choices
            System.out.println("\n\nExample 3 using string choices");
            System.out.println("Choose one of the following:" +
                    "\nLeft      Move the character to the left" +
                    "\nRight     Move the character to the right" +
                    "\nStraight  Move the character straight ahead" +
                    "\nQuit      Quit" +
                    "\nPlease choose Left, Right, Straight or Quit:"
                      );
            //NOTE the "toUpperCase()" This will convert anything typed
            //from the keyboard into uppercase. Converting all the strings
            //to uppercase ensures we are comparing uppercase to uppercase
            UserChoice3 = myScanner.nextLine().toUpperCase();
        
            switch (UserChoice3)
            {
                case "LEFT":
                    System.out.println("Character moves to the left");
                    break;
                case "RIGHT":
                    System.out.println("Character moves to the right");
                    break;
                case "STRAIGHT":
                    System.out.println("Character moves straight");
                    break;
                case "QUIT":
                    System.out.println("Quit Program");
                    break;
                default:
                    //if user chooses a value that 
                    //is not Left, Right, Straight or Quit
                    System.out.println("That was not a choice");
                    break;
            }


            //Inform the user the program is done executing
            System.out.println("\n\nGood Bye - Press enter to exit");
            myScanner.nextLine();
    }
    
}

```



---

