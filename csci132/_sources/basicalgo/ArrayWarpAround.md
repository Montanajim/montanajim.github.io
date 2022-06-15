# Array Warp Around

## Key Ideas

- Place data in an array.
  - If the data element is "full/occupied",  look to the right for the next empty element and wrap around to the beginning element if at the end.

## Lecture Code 

```java
/*
 * DS132SU_WrapAround
 *
 * Programmer: Jim Goudy
 * Project: Wrap Around Array
 This shows how to wrap around in an around.
 Meaning, the program looks to see if an array
 element is open. If it is not, then look to
 the right. Continue looking to the right,
 till the next available element is open.
 
 *
 */


import java.util.Random;
import java.util.Scanner;

public class DS_WrapAround {

    static int ArrayLength = 8;
    static String[] myArray = new String[ArrayLength];
    static int maxVal = ArrayLength;
	
    static Scanner myScan = new Scanner(System.in);
	static Random RNG = new Random();
    
    static int myRNG() {
        // Generate a random number 
        // within the number of array elements
        return RNG.nextInt(maxVal);
    }

    static void printArray() {
        // print the array
        
        for (int c = 0; c < myArray.length; c++) {
            if (myArray[c] == null) {
                System.out.print(" - |");
            } else {
                System.out.print(myArray[c] + " |");
            }
        }
    }

    public static void main(String[] args) {

        String run = "y";
        int aIndex = -1;
        boolean check = true;
        int boxCntr = 0;

        String quit = "y";
        
        // assign values to the array - go to right if occupied
        // this loops continues till the array is full
        while (run.equals("y")) {
            aIndex = myRNG();
            System.out.print("\nComputer chooses " + aIndex + "\n");

            // fill the array element
            while (check) {
                if (myArray[aIndex] == null) {
                    //array index(box) is empty
                    myArray[aIndex] = " X";
                    
                    // this variable keeps track of 
                    // the total number of elments that
                    // are occupied/filled
                    boxCntr++;
                    
                    // sets variable to exit 
                    // the inner while loop
                    check = false;
                    
                    // check if all the array elements are filled
                    if (boxCntr == myArray.length) {
                        run = "n";
                    }
                } else {
                    // array index (box) is not empty 
                    aIndex++;
                    System.out.println("move right " + aIndex);
                    
                    // if the index is at the end of the array
                    // wrap around to the first element 0
                    if (aIndex == myArray.length) {
                        aIndex = 0;
                        System.out.println("move right " + aIndex);
                    }
                }
            }
            
            check = true;
            printArray();
        }

    }
}
/*
Note: Since the computer use a random generator to pick numbers - individual results will vary
Example Output: 
Computer chooses 5
 - | - | - | - | - | X | - | - |
Computer chooses 6
 - | - | - | - | - | X | X | - |
Computer chooses 7
 - | - | - | - | - | X | X | X |
Computer chooses 7
move right 8
move right 0
 X | - | - | - | - | X | X | X |
Computer chooses 6
move right 7
move right 8
move right 0
move right 1
 X | X | - | - | - | X | X | X |
Computer chooses 3
 X | X | - | X | - | X | X | X |
Computer chooses 0
move right 1
move right 2
 X | X | X | X | - | X | X | X |
Computer chooses 5
move right 6
move right 7
move right 8
move right 0
move right 1
move right 2
move right 3
move right 4
 X | X | X | X | X | X | X | X |
------------------------------------------------------------------------
*/
```



------

End Of Topic



