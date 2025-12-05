

### Bucket Sort

1. **BucketSort Method**: This method performs the bucket sort algorithm.
   - First, it finds the maximum value in the input array to determine how many buckets are needed.
   - It then creates an array of buckets (a frequency count array) to track how many times each integer appears in the input.
   - After filling the buckets, it reconstructs the sorted array by placing each element in the correct order.
2. **printArray Method**: A helper function to print the array in a formatted way. This is useful for displaying the array both before and after sorting.
3. **Main Method**:
   - It initializes an array of a given size (`arrSize`), then populates it with random numbers. The size of the array and the number of elements to sort (`nelems`) are specified.
   - It prints the array before and after sorting using the `BucketSort` method and then ends the program with a "Bye" message.

### Key Concepts:

- **Bucket Sort**: It is an efficient sorting algorithm used for uniformly distributed data. The array elements are distributed into several "buckets" (frequency array in this case), sorted within those buckets (implicitly through frequency counts), and then combined back into a sorted array.
- **Random Number Generation**: The random number generator (`RNG.nextInt(maxInt)`) is used to fill the array with random integers between `0` and `maxInt`.

```java
/*
Bucket Sort Algorithm
*/
package fa25_bucket;

import java.util.Arrays;
import java.util.Random;

/**
 * Author: jgoudy
 */
public class Fa25_bucket {

    // Bucket Sort function
    public static void BucketSort(int[] array, int nelems){
        
        // Step 1: Find the maximum value in the array to determine the range of buckets
        int max = Arrays.stream(array).max().getAsInt();
        
        // Step 2: Create an array of buckets to 
        // store frequency counts (size max+1 to accommodate the largest element)
        int[] bucket = new int[max + 1];
        
        // Step 3: Initialize all bucket values to 0 (since we're counting frequencies)
        for (int i = 0; i <= max; i++) {
            bucket[i] = 0;            
        }
        
        // Step 4: Populate the buckets with the frequencies 
        // of elements in the input array
        // For each element in the array, increment the count 
        // at the corresponding bucket index
        for (int i = 0; i < nelems; i++) {
            bucket[array[i]]++;  // Increase frequency for each element
        }
        
        // Step 5: Reconstruct the sorted array from the bucket counts
        // Iterate through the buckets, placing each element back into the array
        // based on its frequency in the bucket array
        for(int i = 0, j=0; i <= max; i++){
            // While the current bucket contains elements (frequency > 0)
            while(bucket[i] > 0) {
                // Place the element in the array at the current position
                array[j++] = i;
                // Decrease the bucket's count (one element placed)
                bucket[i]--;
            }
        }
    } // End of BucketSort function
    
    // Utility function to print the array
    static void printArray(int[] arr, int nelemns){
        for (int i = 0; i < nelemns; i++) {
            // Print each element with spacing for neatness
            System.out.printf(String.format("%4s", arr[i]));
        }
    }
    
    /**
     * Main method for running the program
     */
    public static void main(String[] args)
    {
        // Define size of the array, maximum random integer, 
        // and number of elements to sort
        int arrSize = 25;
        int maxInt = arrSize - 5;   // Maximum value for random number generation
        int nelems = arrSize - 10;  // Number of elements to actually sort
        
        // Create an array with a specified size
        int[] arr = new int[arrSize];
        
        // Initialize random number generator (RNG)
        Random RNG = new Random();
        
        // Step 1: Populate the array with random values between 0 and maxInt
        for(int c = 0; c < nelems; c++) {
            arr[c] = RNG.nextInt(maxInt);
        }
        
        // Print the array before sorting
        System.out.print("Before ");
        printArray(arr, nelems);
        System.out.println("");
        
        // Step 2: Sort the array using BucketSort
        BucketSort(arr, nelems);
        
        // Print the array after sorting
        System.out.print("After  ");
        printArray(arr, nelems);
        System.out.println("");
        
        // Print a message indicating the end of the program
        System.out.println("Bye");
    }
}

```

