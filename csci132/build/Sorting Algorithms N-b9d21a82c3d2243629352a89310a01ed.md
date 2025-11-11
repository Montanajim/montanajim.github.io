# Sorting Algorithms



[TOC]



---




Sure, here is a summary of the sorting algorithms mentioned in the text:

**Sorting Algorithms**

| Algorithm      | Time Complexity | Space Complexity | Notes                                                        |
| :------------- | :-------------- | :--------------- | :----------------------------------------------------------- |
| Bubble Sort    | O(n^2)          | O(1)             | Simple to implement but inefficient for large datasets       |
| Insertion Sort | O(n^2)          | O(1)             | Efficient for small datasets or when the input is nearly sorted |
| Selection Sort | O(n^2)          | O(1)             | Inefficient for large datasets                               |
| Merge Sort     | O(n log n)      | O(n)             | Stable and efficient for large datasets                      |
| Quick Sort     | O(n log n)      | O(log n)         | Efficient for large datasets but unstable                    |
| Heap Sort      | O(n log n)      | O(1)             | In-place and efficient for large datasets                    |
| Counting Sort  | O(n + k)        | O(k)             | Efficient when the range of input values is small            |
| Radix Sort     | O(nk)           | O(k)             | Efficient for sorting strings or numbers                     |
| Shell Sort     | O(n log n)      | O(1)             | Efficient for large datasets with a specific distribution    |
| Timesort       | O(n log n)      | O(1)             | Hybrid sorting algorithm that is efficient for a variety of input data |





## Popular Sorting Algorithms

Here are some of the most popular sorting algorithms:

1. **Bubble Sort**: This algorithm compares adjacent elements and swaps them if they are in the wrong order. It repeats this process until no more swaps are needed. [It has a time complexity of O(n^2) ](https://www.sitepoint.com/best-sorting-algorithms/)[1](https://www.sitepoint.com/best-sorting-algorithms/).
1. **Insertion Sort**: This algorithm iterates through an array and removes one element per iteration, finds the place the element belongs among the sorted elements, and inserts it there. [It has a time complexity of O(n^2) ](https://www.sitepoint.com/best-sorting-algorithms/)[1](https://www.sitepoint.com/best-sorting-algorithms/).
1. **Selection Sort**: This algorithm sorts an array by repeatedly finding the minimum element from the unsorted part of the array and putting it at the beginning. [It has a time complexity of O(n^2) ](https://www.freecodecamp.org/news/sorting-algorithms-explained-with-examples-in-python-java-and-c/)[2](https://www.freecodecamp.org/news/sorting-algorithms-explained-with-examples-in-python-java-and-c/).
1. **Merge Sort**: This algorithm divides the input array into two halves, calls itself for the two halves, and then merges the two sorted halves. [It has a time complexity of O(n log n) ](https://www.sitepoint.com/best-sorting-algorithms/)[1](https://www.sitepoint.com/best-sorting-algorithms/).
1. **Quick Sort**: This algorithm picks an element as a pivot and partitions the given array around the picked pivot. [It has a time complexity of O(n log n) ](https://www.sitepoint.com/best-sorting-algorithms/)[1](https://www.sitepoint.com/best-sorting-algorithms/).
1. **Heap Sort**: This algorithm sorts an array by first building a heap from the input data, then removing the largest element and placing it at the end of the sorted array. [It has a time complexity of O(n log n) ](https://builtin.com/machine-learning/fastest-sorting-algorithm)[3](https://builtin.com/machine-learning/fastest-sorting-algorithm).
1. **Counting Sort**: This algorithm sorts an array by counting the number of occurrences of each unique element in the array and sorting them according to their counts. [It has a time complexity of O(n + k), where k is the range of the non-negative key values ](https://www.freecodecamp.org/news/sorting-algorithms-explained-with-examples-in-python-java-and-c/)[2](https://www.freecodecamp.org/news/sorting-algorithms-explained-with-examples-in-python-java-and-c/).
1. **Radix Sort**: This algorithm sorts an array by grouping elements by the individual digits which share the same significant position and value. [It has a time complexity of O(nk), where k is the number of digits in the longest number ](https://www.freecodecamp.org/news/sorting-algorithms-explained-with-examples-in-python-java-and-c/)[2](https://www.freecodecamp.org/news/sorting-algorithms-explained-with-examples-in-python-java-and-c/).
1. **Shell Sort**: This algorithm sorts an array by comparing elements that are distant from each other. [It has a time complexity of O(n log n) ](https://betterprogramming.pub/5-basic-sorting-algorithms-you-must-know-9ef5b1f3949c)[4](https://betterprogramming.pub/5-basic-sorting-algorithms-you-must-know-9ef5b1f3949c).
1. **Timsort**: This algorithm is a hybrid sorting algorithm derived from merge sort and insertion sort. [It has a time complexity of O(n log n) ](https://www.geeksforgeeks.org/sorting-algorithms/)[5](https://www.geeksforgeeks.org/sorting-algorithms/).

I

---

## Fast Sorting Alogithms



There are several sorting algorithms, each with its own strengths and weaknesses. The efficiency of a sorting algorithm is usually measured by its **time complexity** and **space complexity**. Here are some of the most efficient sorting algorithms:

1. **Quick Sort**: This algorithm is one of the fastest sorting algorithms in practice. It picks an element as a pivot and partitions the given array around the picked pivot. [It has a time complexity of O(n log n) ](https://builtin.com/machine-learning/fastest-sorting-algorithm)[1](https://builtin.com/machine-learning/fastest-sorting-algorithm)[2](https://cs.stackexchange.com/questions/18536/what-is-a-the-fastest-sorting-algorithm-for-an-array-of-integers).
1. **Merge Sort**: This algorithm is also very fast and is often used as the standard algorithm for sorting large amounts of data. It divides the input array into two halves, calls itself for the two halves, and then merges the two sorted halves. [It has a time complexity of O(n log n) ](https://builtin.com/machine-learning/fastest-sorting-algorithm)[1](https://builtin.com/machine-learning/fastest-sorting-algorithm).
1. **Heap Sort**: This algorithm sorts an array by first building a heap from the input data, then removing the largest element and placing it at the end of the sorted array. [It has a time complexity of O(n log n) ](https://builtin.com/machine-learning/fastest-sorting-algorithm)[3](https://stackoverflow.com/questions/63979874/whats-the-most-efficient-way-to-construct-a-new-sorted-array).
1. **Counting Sort**: This algorithm sorts an array by counting the number of occurrences of each unique element in the array and sorting them according to their counts. [It has a time complexity of O(n + k), where k is the range of the non-negative key values ](https://builtin.com/machine-learning/fastest-sorting-algorithm)[2](https://cs.stackexchange.com/questions/18536/what-is-a-the-fastest-sorting-algorithm-for-an-array-of-integers).
1. **Radix Sort**: This algorithm sorts an array by grouping elements by the individual digits which share the same significant position and value. [It has a time complexity of O(nk), where k is the number of digits in the longest number ](https://builtin.com/machine-learning/fastest-sorting-algorithm)[2](https://cs.stackexchange.com/questions/18536/what-is-a-the-fastest-sorting-algorithm-for-an-array-of-integers).

Please note that the efficiency of a sorting algorithm depends on the size of the input data, the distribution of the data, and the available memory. Therefore, it is important to choose the right algorithm for the specific use case.



---

## Quick Sort Pros and Cons



Quick Sort is a popular and efficient sorting algorithm. Here are some of its pros and cons:

**Pros:**

- [Quick Sort is one of the fastest sorting algorithms in practice ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[2](https://www.ablison.com/pros-and-cons-of-quick-sort/).
- [It has a time complexity of O(n log n) ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[2](https://www.ablison.com/pros-and-cons-of-quick-sort/).
- [It is an in-place sorting algorithm, meaning it doesn’t require additional memory ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It is cache-friendly, which means it works well with modern computer architectures ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It is widely used in practice ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It adapts well to many data types ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).

**Cons:**

- [Quick Sort has a worst-case time complexity of O(n^2) ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It is unstable, meaning it does not maintain the relative order of equal elements ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It is dependent on pivot selection, which can affect its performance ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It is not suitable for small datasets ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It is not suitable for linked lists ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).
- [It requires a recursive implementation, which can lead to stack overflow ](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/)[1](https://www.techquintal.com/advantages-and-disadvantages-of-quick-sort/).

Please note that the efficiency of a sorting algorithm depends on the size of the input data, the distribution of the data, and the available memory. Therefore, it is important to choose the right algorithm for the specific use case.



---

## Merge Sort Pros and Cons



Merge Sort is a popular and efficient sorting algorithm. Here are some of its pros and cons:

**Pros:**

- [Merge Sort is stable, meaning it maintains the relative order of equal elements in the input array ](https://brilliant.org/wiki/merge/)[1](https://brilliant.org/wiki/merge/).
- [It has a time complexity of O(n log n) ](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages)[2](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages)[1](https://brilliant.org/wiki/merge/).
- [It is widely used in practice ](https://brilliant.org/wiki/merge/)[3](https://www.geeksforgeeks.org/merge-sort/).
- [It is suitable for sorting large datasets ](https://brilliant.org/wiki/merge/)[2](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages)[4](https://dev.to/ayabouchiha/merge-sort-algorithm-1l55).
- [It is suitable for parallel processing ](https://brilliant.org/wiki/merge/)[1](https://brilliant.org/wiki/merge/).
- [It is a good choice for sorting linked lists ](https://brilliant.org/wiki/merge/)[1](https://brilliant.org/wiki/merge/).

**Cons:**

- [Merge Sort requires additional memory to store the sub-arrays ](https://dev.to/ayabouchiha/merge-sort-algorithm-1l55)[4](https://dev.to/ayabouchiha/merge-sort-algorithm-1l55)[5](https://sage-answer.com/what-are-the-advantages-and-disadvantages-of-a-merge-sort/).
- [It is marginally slower than Quick Sort in practice ](https://brilliant.org/wiki/merge/)[1](https://brilliant.org/wiki/merge/).
- [It is not suitable for small datasets ](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages)[2](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages).
- [It is not an in-place sorting algorithm ](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages)[2](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages).
- [It is not cache-friendly, which means it does not work well with modern computer architectures ](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages)[2](https://getrevising.co.uk/grids/merge-sort-advantages-and-disadvantages).

Please note that the efficiency of a sorting algorithm depends on the size of the input data, the distribution of the data, and the available memory. Therefore, it is important to choose the right algorithm for the specific use case.

I hope this helps!

---

Heap Sort is a popular sorting algorithm with its own strengths and weaknesses. Here are some of its pros and cons:

**Pros:**

- [Heap Sort has a time complexity of O(n log n) ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[2](https://www.2braces.com/data-structures/heap-sort).
- [It is an in-place sorting algorithm, meaning it doesn’t require additional memory ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[2](https://www.2braces.com/data-structures/heap-sort).
- [It is cache-friendly, which means it works well with modern computer architectures ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It is widely used in practice ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It is suitable for sorting large datasets ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[2](https://www.2braces.com/data-structures/heap-sort).
- [It is suitable for parallel processing ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It is a good choice for sorting priority queues ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).

**Cons:**

- [Heap Sort has a slower average-case performance than Quick Sort and Merge Sort ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It is not stable, meaning it does not maintain the relative order of equal elements ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It is not suitable for small datasets ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It is not suitable for linked lists ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).
- [It requires additional memory to store the sub-arrays ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[2](https://www.2braces.com/data-structures/heap-sort).
- [It has a worst-case time complexity of O(n log n) ](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/)[1](https://www.geeksforgeeks.org/applications-advantages-and-disadvantages-of-heap/).

Please note that the efficiency of a sorting algorithm depends on the size of the input data, the distribution of the data, and the available memory. Therefore, it is important to choose the right algorithm for the specific use case.



---

## Small Data Sets



When dealing with **small data sets**, there are several sorting algorithms to consider. Let’s explore a few options:

1. **Insertion Sort**:
   - **Efficiency**: For small input data, insertion sort can work well.
   - **How it works**: It repeatedly finds the minimum  element (in ascending order) from the unsorted portion and places it at  the beginning. This process continues until all elements are sorted.
   - [**Time Complexity**: O(n) for almost sorted data](https://www.enjoyalgorithms.com/blog/comparison-of-sorting-algorithms/)[1](https://www.enjoyalgorithms.com/blog/comparison-of-sorting-algorithms/).
1. **Selection Sort**:
   - **Efficiency**: Also suitable for small datasets.
   - **How it works**: It repeatedly selects the smallest element from the remaining unsorted portion and places it in the correct position.
   - [**Time Complexity**: O(n2), which is less efficient than insertion sort for larger data](https://datatrained.com/post/sorting-in-data-structures/)[2](https://datatrained.com/post/sorting-in-data-structures/).
1. **QuickSelect**:
   - **Efficiency**: Useful for finding the median or N/2 smallest elements.
   - **How it works**: It’s a variation of quicksort that finds the kth smallest element (in this case, N/2).
   - **Time Complexity**: O(n) on average for finding the median.
1. **Hard-Coded Sorting Networks**:
   - **Efficiency**: Potentially fast, especially if there’s hardware support for sorting two memory cells.
   - **How it works**: Implement a specific sorting network (e.g., Batcher, bitonic, or pairwise) tailored to your needs.
   - **Time Complexity**: Depends on the specific network design.

Remember that the best choice depends on your specific requirements  and constraints. You might want to run micro-benchmarks to compare  different algorithms based on your actual data and usage patterns.  Experiment with these approaches to find the most efficient solution for your use case

---

## Quick Sort and Merge Sort

When choosing between **Quick Sort** and **Merge Sort**, consider the following factors:

1. **Stability**:
   - **Merge Sort** is a **stable sorting algorithm**, meaning that elements with equal values maintain their relative order in the sorted output as they were in the input.
   - **Quick Sort** is **unstable** in this regard.
1. **Data Structures**:
   - **Merge Sort** performs best on **linked lists** due to its divide-and-conquer approach.
   - **Quick Sort** excels when working with **arrays stored in RAM**.
1. **Worst-Case Complexity**:
   - **Quick Sort** has a worst-case complexity of **O(n^2)**, which occurs when there are many comparisons in unfavorable conditions.
   - **Merge Sort** maintains the same complexities of **O(n log n)** for both worst and average cases.
1. **Additional Storage**:
   - **Merge Sort** is **not in-place** because it requires extra memory for auxiliary arrays.
   - **Quick Sort** is **in-place**, avoiding the need for additional storage.
1. **Efficiency**:
   - For **larger array sizes or datasets**, **Merge Sort** tends to be more efficient and faster.
   - For **smaller array sizes or datasets**, **Quick Sort** often outperforms Merge Sort.
1. **Sorting Method**:
   - **Quick Sort** is an **internal sorting method**, operating directly in main memory.
   - **Merge Sort** is an **external sorting method**, suitable when data cannot fit entirely in memory.
1. **Locality of Reference**:
   - **Quick Sort** exhibits **good cache locality**, making it faster than Merge Sort in many scenarios (especially in virtual memory environments).

In summary:

- Use **Quick Sort** for **arrays**.
- Opt for **Merge Sort** when dealing with **linked lists**.

---

## Stable vs Unstable Sorting Algorithms



 Let’s explore the difference between **stable** and **unstable** sorting algorithms:

1. **Stable Sorting Algorithm**:
   - A stable sorting algorithm **maintains the relative order of items with equal sort keys**.
   - When you sort a collection using a stable algorithm, items with the **same sort keys preserve their order** after the collection is sorted.
   - In other words, equivalent elements retain their relative positions in the sorted output as they appeared in the input data set.
   - **Example**: If you sort a list of people’s names  alphabetically, a stable sort ensures that people with the same name  stay in the same order.
1. **Unstable Sorting Algorithm**:
   - An unstable sorting algorithm **does not guarantee the relative order of equal elements**.
   - After sorting, items with equal keys might change their positions.
   - **Example**: If you sort a list of integers using an unstable algorithm, the relative order of identical integers may not be preserved.
1. **Why Does Stability Matter?**:
   - **Key-Value Pairs**: Stability is crucial when dealing  with key-value pairs where duplicate keys are possible (e.g., names as  keys and details as values).
   - **Grouping Data**: Consider a dataset of student names  and their class sections. If you sort by name only, an unstable  algorithm might mix up the sections. A stable sort ensures that both  name and section order are maintained.
1. **Examples**:
   - **Stable Sorting Algorithms**: Bubble Sort, Insertion Sort, Merge Sort, Counting Sort, etc.
   - **Comparison-Based Stable Sorts**: Merge Sort and Insertion Sort maintain stability by preserving the relative order of equal elements.
   - **Unstable Sorting Algorithms**: Quick Sort, Heap Sort, etc. These can be made stable by considering element positions, but  they are inherently faster and easier to code.

Remember that the choice between stable and unstable sorting depends on your specific use case and requirements!



---

## Quick Sort, Merge Sort vs Heap Sort

Let’s explore the characteristics of **Quick Sort**, **Merge Sort**, and **Heap Sort** to help you decide when to use each algorithm:

1. **Quick Sort**:
   - **Divide-and-Conquer Approach**: Quick Sort partitions the unsorted array around a randomly chosen pivot element and recursively sorts the subarrays.
   - **Efficiency**: It has an average time complexity of **O(n log n)**, making it faster than Merge Sort.
   - **Space Complexity**: Quick Sort requires **O(log n)** space due to variables on the stack during recursion.
   - **In-Place Sorting**: Quick Sort is an in-place algorithm, meaning it doesn’t need additional memory.
   - **Cache Locality**: It exhibits good cache locality, which contributes to its speed.
   - **Worst Case**: While worst-case scenarios can occur, choosing a good pivot minimizes this risk.
1. **Merge Sort**:
   - **Divide-and-Conquer Approach**: Merge Sort breaks the  list into sublists until each sublist contains only one element, then  merges them to obtain a sorted list.
   - **Efficiency**: It also has an average time complexity of **O(n log n)**.
   - **Space Complexity**: Merge Sort is **not in-place** and requires additional **O(n)** space.
   - **Stability**: It maintains stability (equal elements retain their relative order).
   - **Memory Usage**: It uses twice the memory of Heap Sort due to the second array.
   - **Suitability**: Merge Sort is slightly faster than Heap Sort for larger sets.
1. **Heap Sort**:
   - **Max-Heap Structure**: Heap Sort treats the array as a Max-Heap and utilizes a heapify function to arrange elements correctly.
   - **Efficiency**: It also has an average time complexity of **O(n log n)**.
   - **Space Complexity**: Heap Sort is **not in-place** and requires **O(1)** extra space.
   - **Recursion**: Unlike Merge and Quick Sort, it doesn’t require massive recursion.
   - **Memory Usage**: It uses less memory than Merge Sort.
   - **Trade-offs**: Slower than Quick Sort but avoids excessive recursion.

**Choose Quick Sort** when:

- You need an efficient, in-place sorting algorithm.
- Cache locality is crucial.
- You can handle worst-case scenarios by selecting a good pivot.

**Choose Merge Sort** when:

- Stability matters.
- You have enough memory for the additional space.
- You want a reliable, predictable performance.

**Choose Heap Sort** when:

- You want a simple, space-efficient algorithm.
- You’re okay with slightly slower performance compared to Quick Sort or Merge Sort.

Remember that the choice depends on your specific requirements and constraints! 🚀

---

##  Java Quick Sort

**Quick Sort** is a popular sorting algorithm in Java. It follows the **divide-and-conquer** approach to efficiently sort an array of elements. Here’s how it works:

1. **Divide**: First, a **pivot element** is chosen from the array. The goal is to partition the array into two sub-arrays:
   - The left sub-array contains elements **less than or equal to** the pivot.
   - The right sub-array contains elements **greater than** the pivot.
1. **Conquer**: Recursively, the Quick Sort algorithm is applied to both sub-arrays.
1. **Combine**: Finally, the already sorted sub-arrays are combined to form the fully sorted array.

Here’s the Java implementation of Quick Sort:

```java
public class QuickSort {

    public static void quicksort(int[] arr, int start, int end) {
        if (start < end) {
            int pivot = partition(arr, start, end);
            quicksort(arr, start, pivot - 1);
            quicksort(arr, pivot + 1, end);
        }
    }

    private static int partition(int[] arr, int start, int end) {
        int pivot = arr[end]; // Choose the last element as the pivot
        int i = start - 1;

        for (int j = start; j < end; j++) {
            if (arr[j] < pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        swap(arr, i + 1, end);
        return i + 1;
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = { 24, 13, 27, 16, 10, 35 }; // Example unsorted array
        quicksort(arr, 0, arr.length - 1);

        System.out.println("Sorted array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}

```



In this example, the `quicksort` method recursively sorts the array by choosing a pivot and partitioning the sub-arrays. The `partition` method rearranges the elements in place.

Remember that choosing a good pivot is essential for efficient Quick  Sort. You can select the pivot randomly, use the leftmost or rightmost  element, or even find the median as the pivot.

Java’s built-in `Arrays.sort()` method also uses Quick Sort for sorting arrays of primitives.

---

## Java Merge Sort

Certainly! Let’s dive into the **Merge Sort** algorithm and its implementation in Java.

1. **Introduction**:

   - Merge Sort is an efficient sorting technique based on the “divide and conquer” paradigm.
   - It divides the problem into subproblems, sorts them, and then merges the sorted subarrays to obtain the final sorted array.

1. **The Algorithm**:

   - **Divide**: We divide the input array into two halves, with the pivot being the midpoint.
   - This division is carried out recursively until there are no more half arrays to divide.
   - **Conquer**: We sort and merge the divided arrays from bottom to top to get the final sorted array.

1. **Java Implementation**:

   - We’ll write a `mergeSort` function that takes the input array and its length as parameters.
   - The base condition checks if the array length is 1 (in which case, we return).
   - For the recursive case, we find the middle index and create two temporary arrays, `l[]` and `r[]`.
   - Then we call `mergeSort` recursively for both subarrays.
   - Finally, we call the `merge` function to combine the sorted subarrays.

   ```java
   public class MergeSort {
   
       public static void mergeSort(int[] a, int n) {
           if (n < 2) {
               return;
           }
           int mid = n / 2;
           int[] l = new int[mid];
           int[] r = new int[n - mid];
           for (int i = 0; i < mid; i++) {
               l[i] = a[i];
           }
           for (int i = mid; i < n; i++) {
               r[i - mid] = a[i];
           }
           mergeSort(l, mid);
           mergeSort(r, n - mid);
           merge(a, l, r, mid, n - mid);
       }
   
       public static void merge(int[] a, int[] l, int[] r, int left, int right) {
           int i = 0, j = 0, k = 0;
           while (i < left && j < right) {
               if (l[i] <= r[j]) {
                   a[k++] = l[i++];
               } else {
                   a[k++] = r[j++];
               }
           }
           while (i < left) {
               a[k++] = l[i++];
           }
           while (j < right) {
               a[k++] = r[j++];
           }
       }
   
       public static void main(String[] args) {
           int[] arr = { 10, 6, 8, 5, 7, 3, 4 }; // Example unsorted array
           mergeSort(arr, arr.length);
           System.out.println("Sorted array:");
           for (int num : arr) {
               System.out.print(num + " ");
           }
       }
   }
   
   ```

   

In this example, the `mergeSort` method recursively sorts the array by dividing it into subarrays and then merging them using the `merge` function. Remember that Merge Sort is stable and guarantees consistent performance.

---

## Java Merge Sort Linked List

Certainly! Let’s explore how to implement **Merge Sort** for a **linked list** in Java. Merge Sort is often preferred for sorting linked lists due to  its stable performance and suitability for this data structure.

Below is a Java program that demonstrates Merge Sort for a singly linked list:

```java
public class LinkedListMergeSort {

    static class Node {
        int val;
        Node next;

        public Node(int val) {
            this.val = val;
        }
    }

    public Node mergeSort(Node head) {
        if (head == null || head.next == null) {
            return head; // Base case: empty list or single element
        }

        Node middle = getMiddle(head);
        Node nextOfMiddle = middle.next;
        middle.next = null; // Split the list into two halves

        Node left = mergeSort(head);
        Node right = mergeSort(nextOfMiddle);

        return sortedMerge(left, right);
    }

    private Node sortedMerge(Node a, Node b) {
        if (a == null) return b;
        if (b == null) return a;

        Node result;
        if (a.val <= b.val) {
            result = a;
            result.next = sortedMerge(a.next, b);
        } else {
            result = b;
            result.next = sortedMerge(a, b.next);
        }
        return result;
    }

    private Node getMiddle(Node head) {
        if (head == null) return head;

        Node fastPtr = head.next;
        Node slowPtr = head;

        while (fastPtr != null) {
            fastPtr = fastPtr.next;
            if (fastPtr != null) {
                slowPtr = slowPtr.next;
                fastPtr = fastPtr.next;
            }
        }
        return slowPtr;
    }

    public void push(int newData) {
        Node newNode = new Node(newData);
        newNode.next = head;
        head = newNode;
    }

    public void printList(Node headRef) {
        while (headRef != null) {
            System.out.print(headRef.val + " ");
            headRef = headRef.next;
        }
    }

    public static void main(String[] args) {
        LinkedListMergeSort list = new LinkedListMergeSort();
        list.push(15);
        list.push(10);
        list.push(5);
        list.push(20);
        list.push(3);
        list.push(2);

        System.out.println("Linked List before sorting:");
        list.printList(list.head);

        list.head = list.mergeSort(list.head);

        System.out.println("\nSorted Linked List:");
        list.printList(list.head);
    }
}
```

**Output**:

```
Linked List before sorting:
2 3 20 5 10 15
Sorted Linked List:
2 3 5 10 15 20
```

**Time Complexity**: O(n*log n) **Auxiliary Space**: O(n*log n)

In this example, the `mergeSort` method recursively sorts the linked list by dividing it into sublists and then merging them using the `sortedMerge` function. Remember that Merge Sort is stable and guarantees consistent performance for linked lists