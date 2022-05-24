# Variable Lecture Code



## Key Ideas

* Printing
* Getting Information From The Console



## Printing

To print to the console, the following command is used:

**System.out.println("your text here or variable here");**

System.out.**println()** will drop the cursor to the next line.

System.out.**print()** will leave the cursor on the same line at the end of the text.

## Getting Input From The Console
* The library / class *java.util.Scanner* needs to be imported.
* A scanner is created 
* Input from the scanner is stored in a variable
  * By default, all data from a scanner is a String datatype
  * To convert it into an Integer or Double use  the parse command;


**Example**

```java
import java.util.Scanner;

public class MyProgram
{
    public static void main()
    {
        double salary = 0.0;
        int age = 0;
        String name = "";
        
        //create the scanner
        Scanner myScan = new Scanner(System.in);
        
        System.out.print("Enter your name: ");
        salary = myScan.nextLine();
        
        System.out.print("Enter your salary: ");
        salary = Double.parseDouble(myScan.nextLine());
            
        System.out.print("Enter your age: ");
        age = Integer.parseDouble(myScan.nextLine());       
        
    }
    
    
}

```



**Example 2**


```java
/*
 Lecture Code Class 
 Topic: Variables
 */
package j1_20150902;

import java.util.Scanner;

public class J1_20150902 {

    public static void main(String[] args) {

        //put variables here
        //Integer datatypes
        int age = 20;
        int NumberOfDogs;
        short dogage = 7;
        long geologicalyears = 200000000;

        //Real Numbers
        float Salary = 50000;
        double SpaceMiles = 0;
        float dogYears;
        float humanYears;
        
        //Byte
        byte Codingblock = 64;

        //Boolean
        boolean IsItRaining = true;
        boolean AmIHungry = false;

        //Char
        char MiddleInitial = 'C';
        char Gender = 'M';

        //Strings
        String FirstName;
        String LastName = "Smith";
        String Fruit;

        //Constants - values that will not change
        //The practice is to put constants in 
        //ALL CAPS.
        final double PI = 3.14159265359;
        final String MYTITLE = "Code Guru";

        //----------------Scanner-------------------------
        /*
         Scanners are used to read information from the keyboard.
         Scanner is the key word.  "scan" is a name designated by the programmer.
         "scan" could be called anything the programmer wishes to name it. 
         "new Scanner(System.in)" is the command to create an object that will
         read keystrokes from the keyboard.
         */
        Scanner scan = new Scanner(System.in);

        
        //Ask a question or present information to user
        //"System.out.println("your text")" writes a message to the screen
        System.out.println("Please enter your first name");

        //"scan nextline will read kestrokes until enter key is depressed.
        //All keystrokes that are read from the keyboard using "nextline"
        //reads that data/keystrokes as the String datatype
        FirstName = scan.nextLine();
        System.out.println("Hello " + FirstName);

        //Get an age
        System.out.println("Please enter your age");
        age = Integer.parseInt(scan.nextLine());
        System.out.println("Your age is " + age);

        /*
         scan.nextDouble()
         scan.nextInteger()
         scan.nextFloat()
         scan.nextByte()
         Using these, the scanner will read in only the numbers but leave the
         "enter" keystroke in the buffer. If the next scanner command is 
         "nextLine()", it will immediately see the "enter" keystroke that was
         in the buffer and not allow the user to enter any data. This is 
         demonstrated by the following code.
         */
        //--------  using nextInteger example --------------------
        System.out.println("\n\n***** nextInteger Example ****");
        System.out.println("Please enter your age");
        age = scan.nextInt();
        System.out.println("Your age is " + age);

        System.out.println("Please enter your favorite fruit");
        Fruit = scan.nextLine();  //nextline sees the enter from nextInt and
                                  //executes the line immediately - not
                                  //allowing the user to enter a fruit.
        System.out.println("Your favorite fruit is" + Fruit); 
        
        
        //--------  Fixing the  nextInteger previous example ------------------
        System.out.println("\n\n***** nextInteger Example ****");
        System.out.println("***** The Fix ****");
        System.out.println("Please enter your age");
        age = scan.nextInt();
        scan.nextLine(); //This will clear the "enter" keystroke from the buffer
        System.out.println("Your age is " + age);
        
        System.out.println("Please enter your favorite fruit");
        Fruit = scan.nextLine();  //The user can now enter a fruit.
        System.out.println("Your favorite fruit is " + Fruit);

        /*
        It is better to use the following:
        yourVariableName = Double.parseDouble(scannerName.nextLine())
        yourVariableName = Integer.parseInt(scannerName.nextLine())
        yourVariableName = Float.parseFloat(scannerName.nextLine())
        */
        
        //Calculating dog years
        System.out.println("\n\nWe are going to calculate dog years");
        System.out.println("Enter your human age");
        humanYears = float.parseFloat(scan.nextLine());
        dogYears = humanYears / 7.0f;
        System.out.println("Your age in dogyears is " + dogYears);
        
        //Exit program
        System.out.println("\n\nBye Bye");
        
    }

}
```



---

