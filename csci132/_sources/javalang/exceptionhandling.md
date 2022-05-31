# Exception Handling

## Key Ideas
* Try / Catch

## Readings

https://books.trinket.io/thinkjava2/chapter15.html#sec187

```{admonition} Definition
**Try and Catch** - This statement allows to so encapsultate a part of code that has the possibility to error or crash.  The try / catch will prevent the program from crashing.
```


```java
/*
Try and Catch Demo
by James Goudy
 */
package j1_try_catch;

import java.util.Scanner;

public class J1_Try_Catch {

    public static void main(String[] args) {

        //Variables
        char xquit = 'n';
        String zz;
        String xinput;
        char ww;
        double xx;

        
        //create a scanner
        Scanner scan = new Scanner(System.in);

        zz = "Top";
        
        // try and catch statments allow us to try code that could
        // possibly fail.  We put the code that could fail in the "try" part.
        // If it fails, we then catch the error in the "catch"
        // Exception e is the actual error message.
        try {
            //the word only has 3 letters and we are looking for the 10 letter
            // which it doesn not have.
            ww = zz.charAt(9);  
            System.out.println("The char is " + ww);

        } catch (Exception e) {
            //if there is an error, then this code will rund
            System.out.println(e);
            System.out.println("You had an error - cant you count - try again");
        } finally {
            //finally is optional and it will always run
            System.out.println(" any code in the finally section  "
                    + " will always run.");
        }

        //Example 2
        //This also demonstrates how we can use a char 
        //and use it in a while statement.
        while (xquit != 'y') {
            //this try and catch will catch any errors if anything
            //but a number is entered.  
            try {
                System.out.println("Enter a number");
                xx = Double.parseDouble(scan.nextLine());
                System.out.println("You entered " + xx);

            } catch (Exception e) {
                System.out.println("You  did not enter a number");
            }

            System.out.println("\nWould you like to quit y / n ");
            xinput = scan.nextLine().toLowerCase();
            //notice how we are taking one letter out and making it a char
            //remember that positions that at the number 0
            xquit = xinput.charAt(0);
        }

       System.out.println("\n\nGoodbye");
    }

}

```





---

End Of Topic

