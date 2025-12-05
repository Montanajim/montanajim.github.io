

# Big O Notation - Explained





> [!NOTE]
>
> Big O notation is the language we use for talking about how long an algorithm takes to run (time complexity) or how much memory is used by an algorithm (space complexity). 
>





> [!NOTE]
>
> Big O notation is generally referencing *worst case scenario* for the algorithm
>




## O(1) -  Constant Time



O(1) means that it takes a constant time to run an algorithm, regardless of the size of the input. In programming, a lot of operations are constant. 

Here are some examples:

* math operations
* accessing an array via the index
* accessing a hash via the key
* pushing and popping on a stack
* insertion and removal from a queue
* returning a value from a function



```java
int theArray = new int[Integer.MAX_VALUE]

for(int c = 0; c < Integer.MAX_VALUE; c++)
{
    // This step is O(1)
    theArray[c] = c;
}
```



## O(n) - Linear Time

`O(n)` means that the run-time increases at the rate/size as the input.



```java
// n is some integer

// The for statement is 0(n)
// if n is small, it will take less time
// if n is very large number, it will take more time

for(int c = 0; c < n; c++)
{
    // This step is O(1)
    System.out.println(c)
}
```



## O(n²) -  Quadratic Time

 O(n^2^) means that the calculation runs in quadratic time.

Examples of algorithms having worst-case run times of  O(n^2^):

- Bubble Sort
- Insertion Sort
- Selection Sort

```{tip}
The general pattern is a for statement within a for statement
```



```java
// Bubble Sort

/*
 * Programmer: James Goudy
 * Project: Bubble Sort
 */
package com.mycompany.bubblesort_lecturecode;

import java.util.Random;

class BubbleSort {

    // arrInt is an array of integers
    // numDataElements is the actual count 
    // of elements of data in the array
    // algorithm assumes the data is contiguous
    int arrInt[];
    int numDataElments;

    public BubbleSort(int[] arrInt, int numDataElments) {
        this.arrInt = arrInt;
        this.numDataElments = numDataElments;
    }

    public void Sort() {
        // 
        int n = numDataElments;

        for (int c = 0; c < n; c++) {
            for (int j = 1; j < (n); j++) {
                
                // check if the left element is 
                // greater to the one on the right
                // "Bubble" the lowest to the left

                if (arrInt[j - 1] > arrInt[j]) {
                    // swap left element arr[j-1]
                    // with the one on the right and arr[j]
                    
                    // store left one in temp
                    int temp = arrInt[j - 1];
                    //copy the right into the left
                    arrInt[j - 1] = arrInt[j];
                    //copy the left into the right
                    arrInt[j] = temp;
                }
            }
        }
    }

}

public class BubbleSort_LectureCode {

    static int arrSize = 8;
    //static int theArray[] = new int[arrSize];
    static int theArray[] ={3,60,35,2,45,320,5,1}; 
    
    static void fillTheArray()
    {
        Random RNG  = new Random();
        for(int c = 0; c < arrSize; c++)
        {
            theArray[c] = RNG.nextInt(0,(arrSize*10));
        }
    }
    
    static void printArray(int anArray[], int numOfDataElements)
    {
        System.out.println("");
        for (int i = 0; i < numOfDataElements; i++) {
            System.out.print(anArray[i] + " ");
        }
        System.out.println("\n--------------\n");
        
    }
    
    public static void main(String[] args) {
       
        // option to randomly fill the array
        //fillTheArray();
        
        printArray(theArray, arrSize);
        
        BubbleSort bs = new BubbleSort(theArray, arrSize);
        bs.Sort();
        
        printArray(theArray, arrSize);
    
    }
}

/*
3 60 35 2 45 320 5 1 
--------------


1 2 3 5 35 45 60 320 
--------------
*/
```



https://betterprogramming.pub/big-o-notation-a-simple-explanation-with-examples-a56347d1daca



---

End Of Topic



