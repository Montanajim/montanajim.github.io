# Quicksort Demo



## **How QuickSort Works (Recursive Version)**

QuickSort is a *divide-and-conquer* sorting algorithm. The recursive version works like a rhythm of splitting and sorting:

1. **Pick a pivot** — usually the last element.
2. **Partition the array** — move all smaller values to the left side, larger values to the right.
3. **Recursively sort the two halves** — QuickSort calls itself on the left subarray, then on the right.
4. **Base case** — when a segment has 0 or 1 elements, it’s already sorted.

The recursion naturally creates a call stack, breaking the array into smaller problems until each tiny piece is sorted. When the calls unwind, the entire array emerges in order.

------

## **How QuickSort Works (Iterative Version)**

The iterative version works the same way conceptually, but *no recursion* is used.
 Instead of letting the call stack manage sub-problems, we manage it ourselves:

1. **Use an explicit stack (an array)** to store the index ranges that still need sorting.
2. **Push the initial full array range** onto the stack.
3. **Loop** while the stack isn't empty:
   - Pop a range off the stack.
   - Partition that section around a pivot.
   - Push the left and right sub-ranges back onto the stack (if they exist).
4. Continue until no unsorted sections remain.

This version exposes what recursion does behind the scenes. It sorts the same way—just with loops and a manually managed stack.



```java
/*
Developer James Goudy
 */
package quicksort_demo;


interface SortingAlgorithm {

    // Method to sort the array in-place
    void sort(int[] arr);

}


// -------------------------------------------------------------
// QuickSort.java
// A simple, teaching-friendly implementation of QuickSort.
// This class contains ONLY the QuickSort logic.
//
// How it works
// - QuickSort is a "divide and conquer" sorting algorithm.
// - We pick a pivot, split the array into smaller/larger parts,
//   then recursively sort each part.
// - This version is NOT optimized. It's intentionally simple.
// -------------------------------------------------------------

class QuickSort implements SortingAlgorithm {

    @Override
    public void sort(int[] arr) {
        quickSort(arr, 0, arr.length - 1);
    }
    // Internal recursive method that performs the sorting
    private static void quickSort(int[] arr, int low, int high)
    {
        if (low < high) {
            // Partition the array and get the pivot index
            int pivotIndex = partition(arr, low, high);

            // Recursively sort the left side
            quickSort(arr, low, pivotIndex - 1);

            // Recursively sort the right side
            quickSort(arr, pivotIndex + 1, high);
        }
    }

    // ---------------------------------------------------------
    // partition()
    // This function:
    //   • chooses a pivot (here we use the last element)
    //   • rearranges elements so smaller values go left,
    //     larger values go right
    //   • returns the final position of the pivot
    // ---------------------------------------------------------
    private static int partition(int[] arr, int low, int high)
    {
        int pivot = arr[high]; // choose pivot
        int i = low - 1;       // index of smaller element

        // Move through the array and swap values as needed
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // Move pivot to the correct location
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1; // return pivot position
    }
}
// --------------------------------------------------------------

// -------------------------------------------------------------
// QuickSortIterative.java
// A simple, teaching-friendly **iterative** QuickSort.
// This version uses loops instead of recursion by manually
// managing our own "stack" of sub-array ranges.
//
// -------------------------------------------------------------

class QuickSortIterative implements SortingAlgorithm {

    @Override
    public void sort(int[] arr) {
        quickSort(arr);
    }

    // Iterative quicksort using manual stack
    private static void quickSort(int[] arr) {
        int low = 0;
        int high = arr.length - 1;

        // -----------------------------------------------------
        // Our manual stack will hold pairs of (low, high) index
        // ranges that still need to be processed.
        // -----------------------------------------------------
        int[] stack = new int[high - low + 1];

        int top = -1;

        // Push initial range onto stack
        stack[++top] = low;
        stack[++top] = high;

        // -----------------------------------------------------
        // Keep looping while we have ranges to process
        // -----------------------------------------------------
        while (top >= 0) {

            // Pop the high and low indexes for the next segment
            high = stack[top--];
            low = stack[top--];

            // Partition this segment
            int pivotIndex = partition(arr, low, high);

            // -------------------------------------------------
            // PUSH RIGHT SIDE (if it exists)
            // -------------------------------------------------
            if (pivotIndex + 1 < high) {
                stack[++top] = pivotIndex + 1;
                stack[++top] = high;
            }

            // -------------------------------------------------
            // PUSH LEFT SIDE (if it exists)
            // -------------------------------------------------
            if (pivotIndex - 1 > low) {
                stack[++top] = low;
                stack[++top] = pivotIndex - 1;
            }
        }
    }

    // ---------------------------------------------------------
    // partition()
    // Same idea as recursive QuickSort:
    //   - Pick last element as pivot
    //   - Move all smaller elements to the left
    //   - Move pivot to its correct position
    // ---------------------------------------------------------
    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;

        // Scan through and swap as necessary
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;

                // Swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // Move pivot into correct place
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }
}


// --------------------------------------------------------------

public class QuickSort_Demo {
    
    static SortingAlgorithm sa;
    
    
  

    // Utility method to print an array
    public static void printArray(int[] arr)
    {
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void main(String[] args)
    {
        
          int choice = 2;
    
        if (choice == 1) {
            sa = new QuickSort();
        } else {
            sa = new QuickSortIterative();
        }
        
        int[] data = {34, 7, 23, 32, 5, 62};

        System.out.println("Original Array:");
        printArray(data);

        // Call the QuickSort class
        sa.sort(data);

        System.out.println("\nSorted Array:");
        printArray(data);
    }

}

```

