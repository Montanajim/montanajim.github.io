# String Functions

## Key Ideas

* Convert To Uppercase
* Covert To Lowercase
* Length of a string
* Substring - get parts of a string
* CharAt  - retreive a character out of a string
* Replace a character





```java
/*
String Functions
This program demonstrates some of the common 
string functions

Jim Goudy
 */
package string_functions;

public class String_Functions {

    public static void main(String[] args) {

        // Variables
        String xInputString;
        String xInputString2;
        String xTemp;
        int xLength = 0;
        char xChar;

        // Data for input strings
        xInputString = "Codingjava";
        xInputString2 = "Feed";

        // Original Word
        System.out.println("\nConvert To Uppercase");
        System.out.println(xInputString);


        // Get the length of a string
        System.out.println("\nGet lenght of a string");
        xLength = xInputString.length();
        System.out.println(xInputString + " is " + xLength + " characters long.");

        // Convert To Uppercase
        System.out.println("\nConvert To Uppercase");
        xInputString = xInputString.toUpperCase();
        System.out.println(xInputString);

        // Convert To Lowercase
        System.out.println("\nConvert To Lowercase");
        xInputString = xInputString.toLowerCase();
        System.out.println(xInputString);

        // Replace a character
        System.out.println("\nReplace a character");
        xInputString = xInputString.replace('g', 'b');
        System.out.println(xInputString);

        // Replace a charater - notices how it
        // turns Feed into Food
        System.out.println("\nReplace a character");
        xInputString2 = xInputString2.replace('e', 'o');
        System.out.println(xInputString2);

        
        
        // Returns a string starting at the position
        // NOTE: positions for this command start at 0
        // Bumpoint --> this command will return point
        System.out.println("\nRetreive part of a string");
        xTemp = xInputString.substring(3);
        System.out.println(xTemp);

        // Returns a string starting at the position
        // NOTE: positions for this command start at 0
        // Orignial word is bumpoint
        System.out.println("\nRetrieve Partical Strings");
        xTemp = xInputString.substring(0, 3);  // pulls out bum
        System.out.println(xTemp);
        xTemp = xInputString.substring(3, 8); // points
        System.out.println(xTemp);
        // note how you can use length in the following expression
        xTemp = xInputString.substring(3, xInputString.length());
        System.out.println(xTemp);

        // Retrieve a char from a string
        // NOTE  scanners only retrive strings. There are no methods
        // for chars
        System.out.println("\nRetrieve a char");
        xChar = xInputString.charAt(0);  // retreives the B as a char
        System.out.println(xChar);
        xChar = xInputString.charAt(3); // retreive the P as a char
        System.out.println(xChar);

        // check the equalality of a string
        // Note that String is an object and not a native datatype
        // Hence - we cannot use == for String
        // we must use the .equal() 
        System.out.println("\nCheck For Equality");
        if (xInputString.equals(xInputString2)) {
            System.out.println("It matches");
        } else {
            System.out.println("NO match");
        }

        // Another example
        if (xInputString.equals("Montana")) {
            System.out.println("It matches");
        } else {
            System.out.println("NO match");
        }

        // Another example
        xTemp = "Montana";
        if (xTemp.equals("Montana")) {
            System.out.println("It matches");
        } else {
            System.out.println("NO match");
        }

    }

    
}

```



---



---

