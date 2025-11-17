# Arrays Core Functionality





## `sort(int[] SampleData, boolean printData)`



This method implements an **Insertion Sort** algorithm. Unlike a traditional in-place Insertion Sort, this version copies elements from the input `SampleData` array into a *new* array, `SortedData`, inserting each element into its correct, sorted position within the `SortedData` array as it iterates. The sorted array is returned. If the `printData` flag is true, it prints the partially sorted array after each insertion.



## `reverse(int[] arr)`



This function reverses the order of elements in the given array **in-place**. It uses a two-pointer approach, with one pointer starting at the beginning (`start`) and the other at the end (`end`) of the array, iteratively swapping the elements they point to until the pointers meet or cross. The array itself is modified, and nothing is returned.



## `deleteByValue(int[] arr, int valueToDelete)`



This method finds the **first occurrence** of a specified `valueToDelete` in the array. If found, it delegates the actual deletion to the `deleteByPosition` function. If the value is not found, it prints a message and returns the original array unchanged. Because Java arrays have a fixed size, this function (via `deleteByPosition`) returns a **new array** that is one element shorter than the original.



## `deleteByPosition(int[] theArray, int pos)`



This is a utility function for deleting an element at a specific index (`pos`). It creates a **new array** that is one element smaller and copies all elements from the original array into the new one, skipping the element at the specified position and shifting subsequent elements left to fill the gap. The new, smaller array is returned.



## `printArray(int[] theArray, int dataLength)`



A simple **utility function** used to print the elements of an array from the beginning up to the specified `dataLength`.

------



## Program Execution in `main`



The `main` method orchestrates a demonstration of these functions using an initial data array: {9,1,8,2,7,3,6,5,3}.

1. **Insertion Sort:** It first sorts the initial data, printing the array after each insertion, resulting in a sorted array: {1,2,3,3,5,6,7,8,9}.
2. **Reverse:** It then reverses the resulting sorted array **in-place**, yielding: {9,8,7,6,5,3,3,2,1}.
3. **Delete by Value:** It deletes the first occurrence of the value **3** from the reversed array, returning a new array: {9,8,7,6,5,3,2,1}.
4. **Delete by Position:** Finally, it deletes the element at **index 2** (which is the value 7) from the array resulting from the previous step, producing the final array: {9,8,6,5,3,2,1}.



```java
package instinsertinorder;

public class InstInsertInOrder {

    // Insertion-sort into a NEW array; optionally print after each insert.
    static int[] sort(int[] SampleData, boolean printData) {
        int[] SortedData = new int[SampleData.length];
        int elementsSorted = 0; // size of the sorted prefix

        // For each element in SampleData
        for (int i = 0; i < SampleData.length; i++) {
            int key = SampleData[i];
            int j = elementsSorted - 1;

            // While items > key, shift them right
            while (j >= 0 && SortedData[j] > key) {
                SortedData[j + 1] = SortedData[j];
                j--;
            }

            // Insert key at correct position
            SortedData[j + 1] = key;
            elementsSorted++;

            if (printData) // If enabled, show current sorted portion
                printArray(SortedData, elementsSorted);
        }
        return SortedData;
    }

    /** Reverse array in place using two pointers. */
    static void reverse(int[] arr) {
        int start = 0, end = arr.length - 1;
        while (start < end) { // While pointers haven't crossed
            int tmp = arr[start];
            arr[start] = arr[end];
            arr[end] = tmp;
            start++; end--;
        }
    }

    /**
     * Delete first occurrence of value; returns NEW array (length-1).
     * If not found, return original.
     */
    static int[] deleteByValue(int[] arr, int valueToDelete) {
        int indexToDelete = -1;

        // For each element, check for match
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == valueToDelete) { // Found target
                indexToDelete = i;
                break;
            }
        }

        if (indexToDelete == -1) { // If value not found
            System.out.println("Value " + valueToDelete + " not found.");
            return arr;
        }

        return deleteByPosition(arr, indexToDelete);
    }

    /**
     * Delete element at index 'pos'; returns NEW array (length-1).
     */
    static int[] deleteByPosition(int[] theArray, int pos) {
        int[] temp = new int[theArray.length - 1];

        // Copy elements, skipping the deleted position
        for (int i = 0; i < temp.length; i++) {
            if (i >= pos) // If past delete index, shift left
                temp[i] = theArray[i + 1];
            else          // Otherwise copy directly
                temp[i] = theArray[i];
        }
        return temp;
    }

    // Print first dataLength elements on one line.
    static void printArray(int[] theArray, int dataLength) {
        System.out.print("Array: ");
        for (int i = 0; i < dataLength; i++) // Print up to given length
            System.out.print(theArray[i] + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        int[] SampleData = {9, 1, 8, 2, 7, 3, 6, 5, 3};

        System.out.println("--- 1. Insertion Sort  ---");
        int[] sortedArray = sort(SampleData, true);

        System.out.println("\n--- 2. Reverse Function  ---");
        printArray(sortedArray, sortedArray.length);
        reverse(sortedArray);
        System.out.print("Array after reverse: ");
        printArray(sortedArray, sortedArray.length);

        System.out.println("\n--- 3. Delete by Value  (Value 3) ---");
        int[] arrayAfterValueDelete = deleteByValue(sortedArray, 3);
        System.out.print("Array after deleting first '3': ");
        printArray(arrayAfterValueDelete, arrayAfterValueDelete.length);

        System.out.println("\n--- 4. Delete by Position  (Index 2) ---");
        int[] finalArray = deleteByPosition(arrayAfterValueDelete, 2);
        System.out.print("Array after deleting element \nat index 2 (Value 7): ");
        printArray(finalArray, finalArray.length);

        System.out.println("\nbye\n");
    }
}

```

10/2025

