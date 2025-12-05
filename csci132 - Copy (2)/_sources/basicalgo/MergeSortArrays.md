# Merge Sort - Arrays



## Notable Code


The `System.arraycopy()` method in Java is used to copy a specified portion of an array to another array. It is a versatile method that can be used to copy arrays of primitive data types, as well as arrays of objects.



**Syntax:**



Java

```
System.arraycopy(src, srcPos, dest, destPos, length);
```

Use code with caution. [Learn more](https://bard.google.com/faq#coding)

content_copy



**Parameters:**





- `src`: The source array from which to copy data.

  

- `srcPos`: The starting position in the source array from which to copy data.

  

- `dest`: The destination array to which to copy data.

  

- `destPos`: The starting position in the destination array to which to copy data.

  

- `length`: The number of elements to copy.

  



**Return Value:**



The method does not return any value.



**Example:**



Java

```
int[] src = {1, 2, 3, 4, 5};
int[] dest = new int[10];

System.arraycopy(src, 2, dest, 0, 3); // Copy elements 3, 4, and 5 from src to dest

for (int i = 0; i < dest.length; i++) {
    System.out.print(dest[i] + " ");
}
```

Use code with caution. [Learn more](https://bard.google.com/faq#coding)

content_copy



**Output:**



```
3 4 5 0 0 0 0 0 0 0 0
```



As you can see, the `System.arraycopy()` method is a powerful tool for copying arrays in Java. It is a simple and efficient method that can be used to copy arrays of any size.





```java


package ds132fa_mergesortarray;

import java.util.Random;

class MSArr {

    // This array holds the elements to be sorted
    private int[] theArray;

    // This variable stores the number of elements in the array
    private int nElems;

    /**
     * Constructor for the MSArr class. Initializes the array with the given maximum size
     *
     * @param max The maximum size of the array
     */
    public MSArr(int max) {
        // Create an array with the given maximum size
        theArray = new int[max];

        // Initialize the number of elements to 0
        nElems = 0;
    }

    /**
     * Inserts an element into the array
     *
     * @param value The value to be inserted
     */
    public void insert(int value) {
        // Add the value to the array at the next available index
        theArray[nElems] = value;

        // Increment the number of elements in the array
        nElems++;
    }

    /**
     * Displays the elements of the array
     */
    public void displayArray() {
        // Create a StringBuilder object to efficiently concatenate strings
        StringBuilder sb = new StringBuilder();

        // Iterate through the array and append each element to the StringBuilder
        for (int i = 0; i < nElems; i++) {
            sb.append(theArray[i]).append(" "); // Use append method instead of + operator
        }

        // Convert the StringBuilder to a String and print it
        System.out.println(sb.toString());
    }
    
    public void mergeSort() {
        // Create a temporary workspace array with the same size as the original array
        int[] workspace = new int[nElems];

        // Initiate the recursive merge sort process
        inMergeSort(workspace, 0, nElems - 1);
    }

    private void inMergeSort(int[] workspace, int lowerbound, int upperbound) {
        // Check if the subarray has only one element, which is already sorted
        if (lowerbound == upperbound) {
            return;
        } else {
            // Find the midpoint of the subarray
            int mid = (lowerbound + upperbound) / 2;

            // Recursively sort the lower half of the subarray
            inMergeSort(workspace, lowerbound, mid);

            // Recursively sort the upper half of the subarray
            inMergeSort(workspace, mid + 1, upperbound);

            // Merge the sorted lower and upper halves into the workspace array
            merge(workspace, lowerbound, mid + 1, upperbound);
        }
    }

    private void merge(int[] workspace, int lowptr, int highptr, int upperbound) {
        // Initialize index variables
        int j = 0; // Index for the workspace array
        int lowerbound = lowptr; // Index for the first subarray
        int mid = highptr - 1; // Index for the second subarray

        // Calculate the number of elements to merge
        int n = upperbound - lowerbound + 1;

        // Compare elements from each subarray and copy them to the workspace array in sorted order
        while (lowptr <= mid && highptr <= upperbound) {
            // Use a ternary operator for concise comparison and assignment
            workspace[j++] = (theArray[lowptr] < theArray[highptr]) ? 
                theArray[lowptr++] : theArray[highptr++];
        }

        // Copy any remaining elements from the first subarray, if any
        System.arraycopy(theArray, lowptr, workspace, j, mid - lowptr + 1);

        // Copy any remaining elements from the second subarray, if any
        System.arraycopy(theArray, highptr, workspace, j, upperbound - highptr + 1);

        // Copy the sorted elements from the workspace array back to the original array
        System.arraycopy(workspace, 0, theArray, lowerbound, n);
    }

}

public class DS132FA_MergeSortArray {

    /**
     * The main method of the program
     *
     * @param args The command-line arguments
     */
    public static void main(String[] args) {
        // Set the maximum size of the array
        int maxSize = 100;

        // Create an instance of the MSArr class
        MSArr arr = new MSArr(maxSize);

        // Create a Random object for generating random numbers
        Random RNG = new Random();

        // Insert 20 random integers into the array
        for (int c = 0; c < 20; c++) {
            arr.insert(RNG.nextInt(300));
        }

        // Display the original unsorted array
        System.out.println("Unsorted Array:");
        arr.displayArray();

        // Perform the merge sort algorithm to sort the array
        arr.mergeSort();

        // Display the sorted array
        System.out.println("\nSorted Array:");
        arr.displayArray();

        // Print a final message
        System.out.println("\n\n\nbye\n");
    }
}


```

