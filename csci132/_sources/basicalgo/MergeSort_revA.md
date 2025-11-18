# Merge Sort - Demo Code

### **How Merge Sort Works**

Merge sort is a **divide-and-conquer** sorting algorithm. It recursively divides the array into two halves until each subarray has only one element (which is trivially sorted). Then it **merges** these sorted halves back together, comparing elements and building a larger sorted array step by step. This merging process continues until the entire array is reassembled in sorted order.

The algorithm has a consistent time complexity of **O(n log n)** — it divides the array (log n times) and merges n elements at each level. Merge sort is stable and efficient but requires extra space proportional to the array size due to its temporary workspace array.

## Arrays

### Demo Code

```java
/*
Engineer: James Goduy
 */
package mergesort_rev;

import java.util.Random;


/*
 * The Sorter interface defines a contract that all sorting classes must follow.
 * Any class that implements Sorter must provide concrete versions of insert(),
 * sort(), and displayArray(). These are method signatures only—no code 
 * is written here.
 *
 * Using an interface allows us to treat different sorting algorithms (e.g.,
 * recursive and iterative merge sorts) as the same "type." This is an example
 * of polymorphism: we can write one block of code that works with any object
 * implementing Sorter, regardless of how it performs the sorting internally.
 *
 * In short, the interface provides a common structure (what must be done),
 * while each class defines its own behavior (how it is done).
 */

interface Sorter {
    void insert(int value);
    void sort();
    void displayArray();
}


class MergeSort implements Sorter {

    private int[] theArray;  // Main array to be sorted
    private int nElems;      // Current number of elements in the array
    private int max;         // Maximum capacity of the array

    // Constructor: initializes the array and tracking variables
    public MergeSort(int max) {
        theArray = new int[max];
        nElems = 0;
        this.max = max;
    }

    // Check if array is full
    private boolean isFull() {
        return nElems == max;
    }

    // Insert a value into the array (if space allows)
    public void insert(int value) {
        if (isFull()) {
            System.out.println("Array is full");
            return;
        }
        theArray[nElems++] = value; // Place value and increment element count
    }

    // Public method to start the merge sort process
    public void sort() {
        int[] workspace = new int[nElems]; // Temporary workspace for merging
        recMergeSort(workspace, 0, nElems - 1); // Begin recursive sorting
    }

    // Recursive function that splits and sorts subarrays
    private void recMergeSort(int[] workspace, int lowerBound, int upperBound) {
        if (lowerBound >= upperBound) return; // Base case: one element

        int mid = (lowerBound + upperBound) / 2; // Find midpoint

        // Recursively sort left and right halves
        recMergeSort(workspace, lowerBound, mid);
        recMergeSort(workspace, mid + 1, upperBound);

        // Merge the two sorted halves
        merge(workspace, lowerBound, mid + 1, upperBound);
    }

    // Merge two sorted halves into a single sorted run
    private void merge(int[] workspace, int lowPtr, int highPtr, int upperBound) {
        int j = 0;                   // Index for workspace
        int lowerBound = lowPtr;     // Start index of left half
        int mid = highPtr - 1;       // End index of left half
        int n = upperBound - lowerBound + 1; // Total elements to merge

        // Compare elements from both halves and copy the smaller one first
        while (lowPtr <= mid && highPtr <= upperBound) {
            workspace[j++] = (theArray[lowPtr] <= theArray[highPtr])
                    ? theArray[lowPtr++]
                    : theArray[highPtr++];
        }

        // Copy any remaining elements from the left half
        if (lowPtr <= mid) {
            System.arraycopy(theArray, lowPtr, workspace, j, mid - lowPtr + 1);
            j += (mid - lowPtr + 1);
        }

        // Copy any remaining elements from the right half
        if (highPtr <= upperBound) {
            System.arraycopy(theArray, highPtr, workspace, j, upperBound - highPtr + 1);
        }

        // Copy merged elements back into the original array
        System.arraycopy(workspace, 0, theArray, lowerBound, n);
    }

    // Utility method to display the array contents
    public void displayArray() {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < nElems; i++) sb.append(theArray[i]).append(' ');
        System.out.println(sb.toString());
    }
} // End Of Class

class MergeSort_Iterative implements Sorter {

    // Instance Variables
    private int[] theArray;  // The array to be sorted
    private int nElems;      // Current number of elements in the array
    private int max;         // Maximum array capacity (limit)

    // Constructor
    public MergeSort_Iterative (int max) {
        // Initialize the array and size counters
        theArray = new int[max];
        nElems = 0;
        this.max = max;
    }


    // Utility Method
    // Checks whether the array is already full
    private boolean isFull() {
        return nElems == max;
    }

    // Insert Method
    // Adds a value to the array if space is available
    public void insert(int value) {
        if (isFull()) {
            System.out.println("Array is full");
            return;
        }
        // Store value and increase the element count
        theArray[nElems++] = value;
    }


    // Iterative Merge Sort
    public void sort() {
        int[] workspace = new int[nElems]; // Temporary array used during merging
        
        // subSize represents the size of subarrays being merged each pass
        // Start with subarrays of size 1 and double the size each iteration
        for (int subSize = 1; subSize < nElems; subSize *= 2) {
            
            // Process and merge all pairs of subarrays of the current subSize
            for (int leftStart = 0; leftStart < nElems - subSize; leftStart += 2 * subSize) {
                
                // leftStart: beginning index of left subarray
                int mid = leftStart + subSize - 1; // Last index of left subarray
                
                // Ensure the right subarray does not exceed array bounds
                int rightEnd = Math.min(leftStart + 2 * subSize - 1, nElems - 1);
                
                // Merge the two adjacent sorted subarrays into one
                merge(workspace, leftStart, mid + 1, rightEnd);
            }
        }
    }


    // Merge Method
    // Merges two sorted halves into a single sorted section
    private void merge(int[] workspace, int lowPtr, int highPtr, int upperBound) {
        int j = 0;                    // Index for workspace array
        int lowerBound = lowPtr;      // Start index of the left half
        int mid = highPtr - 1;        // End index of the left half
        int n = upperBound - lowerBound + 1; // Total number of elements to merge

        // Compare elements from both halves and copy the smaller one first
        while (lowPtr <= mid && highPtr <= upperBound) {
            if (theArray[lowPtr] <= theArray[highPtr])
                workspace[j++] = theArray[lowPtr++]; // Copy from left half
            else
                workspace[j++] = theArray[highPtr++]; // Copy from right half
        }

        // Copy any remaining elements from the left half
        while (lowPtr <= mid) {
            workspace[j++] = theArray[lowPtr++];
        }

        // Copy any remaining elements from the right half
        while (highPtr <= upperBound) {
            workspace[j++] = theArray[highPtr++];
        }

        // Copy merged elements back into the original array
        for (int k = 0; k < n; k++) {
            theArray[lowerBound + k] = workspace[k];
        }
    }
    
    // Utility method to display the array contents
    public void displayArray() {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < nElems; i++) sb.append(theArray[i]).append(' ');
        System.out.println(sb.toString());
    }
}


public class MergeSort_Rev {


    public static void main(String[] args)
    {
        
        int maxSize = 15    ;
        int sampleSize =  (int)(maxSize * .9);
        int choice = 2;
        
        Sorter ms;
        
        // create the object
        if(choice == 1)
        {
            // recursive
        	ms = new MergeSort(maxSize);
        }
        else
        {
            // iterative - loops
            ms = new MergeSort_Iterative (maxSize);
        }

        // Create RNG
        Random RNG = new Random();

        // insert random numbers
        for(int c = 0 ; c < sampleSize; c++)
        {
            ms.insert(RNG.nextInt(0,maxSize));
        }
      
        // display the orignal array
        ms.displayArray();

        
        // sort the list
        ms.sort();
        
        // spacing
        System.out.println();

        // display the sorted list
        ms.displayArray();

        System.out.println("\nbye\n");
    }
    
}
```

## Linked Lists

### Demo Code	

```java
/*
 * Example program demonstrating two implementations of Merge Sort
 * for a linked list of people (first name, last name, city).
 * 
 * Both recursive (top-down) and iterative (bottom-up) versions
 * implement a common interface (Sorter) for interchangeable use.
 *
 * Author: [Your Name]
 * Course: [Your Class Name or Section]
 */

package mergesortlinkedlist;

// ----------------------------------------------------------------------
// Interface Definition
// ----------------------------------------------------------------------

/**
 * The Sorter interface defines a simple contract for
 * inserting, sorting, and displaying a collection.
 * 
 * Both recursive and iterative merge sort classes
 * will implement this interface to ensure consistent usage.
 */
interface Sorter {
    void insert(String fn, String ln, String cty);
    void sort();
    void displayList();
}

// ----------------------------------------------------------------------
// Recursive Merge Sort Implementation
// ----------------------------------------------------------------------

/**
 * MergeSortLinkedList_Recursive
 * 
 * Uses a recursive (top-down) merge sort approach.
 * The list is divided into halves until single nodes remain,
 * then merged back together in sorted order by last name.
 */
class MergeSortLinkedList_Recursive implements Sorter {

    /**
     * Inner class Node — represents a single record in the linked list.
     * Each node stores a person's first name, last name, and city.
     */
    class Node {
        String firstName;
        String lastName;
        String city;
        Node next;

        Node(String firstName, String lastName, String city) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.city = city;
            this.next = null;
        }
    }

    private Node head;  // Head pointer for the linked list

    /**
     * Inserts a new node at the end of the list.
     */
    public void insert(String firstName, String lastName, String city) {
        Node newNode = new Node(firstName, lastName, city);
        if (head == null) {
            head = newNode;
            return;
        }

        Node current = head;
        while (current.next != null)
            current = current.next;
        current.next = newNode;
    }

    /**
     * Public sort method — initiates recursive merge sort.
     */
    public void sort() {
        head = mergeSort(head);
    }

    /**
     * Recursive merge sort: splits the list, sorts each half, and merges them.
     */
    private Node mergeSort(Node h) {
        // Base case: 0 or 1 element
        if (h == null || h.next == null) return h;

        // Split the list into two halves
        Node middle = getMiddle(h);
        Node nextOfMiddle = middle.next;
        middle.next = null; // Split into two sublists

        // Recursively sort both halves
        Node left = mergeSort(h);
        Node right = mergeSort(nextOfMiddle);

        // Merge the two sorted halves
        return sortedMerge(left, right);
    }

    /**
     * Merges two sorted linked lists into one (sorted by last name).
     */
    private Node sortedMerge(Node a, Node b) {
        if (a == null) return b;
        if (b == null) return a;

        Node result;

        // Compare by last name (case-insensitive)
        if (a.lastName.compareToIgnoreCase(b.lastName) <= 0) {
            result = a;
            result.next = sortedMerge(a.next, b);
        } else {
            result = b;
            result.next = sortedMerge(a, b.next);
        }

        return result;
    }

    /**
     * Finds the middle node of a linked list using the fast/slow pointer method.
     */
    private Node getMiddle(Node h) {
        if (h == null) return h;

        Node slow = h, fast = h;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    /**
     * Displays the contents of the linked list.
     */
    public void displayList() {
        Node current = head;
        while (current != null) {
            System.out.printf("%-10s %-10s %-10s%n",
                    current.firstName, current.lastName, current.city);
            current = current.next;
        }
        System.out.println();
    }
}

// ----------------------------------------------------------------------
// Iterative Merge Sort Implementation
// ----------------------------------------------------------------------

/**
 * MergeSortLinkedList_Iterative
 * 
 * Uses an iterative (bottom-up) merge sort approach.
 * Starts by merging small sorted sublists of size 1, then doubles
 * the size of the sublists (1, 2, 4, 8...) until the full list is sorted.
 */
class MergeSortLinkedList_Iterative implements Sorter {

    /**
     * Inner class Node — represents a single record in the linked list.
     */
    class Node {
        String firstName;
        String lastName;
        String city;
        Node next;

        Node(String firstName, String lastName, String city) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.city = city;
            this.next = null;
        }
    }

    private Node head; // Head of the linked list

    /**
     * Inserts a new node at the end of the list.
     */
    public void insert(String firstName, String lastName, String city) {
        Node newNode = new Node(firstName, lastName, city);
        if (head == null) {
            head = newNode;
            return;
        }
        Node current = head;
        while (current.next != null)
            current = current.next;
        current.next = newNode;
    }

    /**
     * Public method to start iterative merge sort.
     */
    public void sort() {
        head = mergeSortIterative(head);
    }

    /**
     * Iterative (loop-based) merge sort implementation.
     * Uses sublist merging of increasing size to avoid recursion.
     */
    private Node mergeSortIterative(Node head) {
        if (head == null || head.next == null) return head;

        int n = getSize(head);

        // Dummy node simplifies pointer management during merging
        Node dummy = new Node("", "", "");
        dummy.next = head;

        // Merge sublists of size 1, 2, 4, 8, etc.
        for (int step = 1; step < n; step *= 2) {
            Node prev = dummy;
            Node current = dummy.next;

            while (current != null) {
                Node left = current;
                Node right = split(left, step);
                current = split(right, step);

                Node merged = sortedMerge(left, right);
                prev.next = merged;

                // Move 'prev' to the end of the merged sublist
                while (prev.next != null)
                    prev = prev.next;
            }
        }

        return dummy.next;
    }

    /**
     * Splits the list after 'size' nodes and returns the next sublist.
     */
    private Node split(Node head, int size) {
        if (head == null) return null;
        for (int i = 1; head.next != null && i < size; i++)
            head = head.next;

        Node second = head.next;
        head.next = null;
        return second;
    }

    /**
     * Merges two sorted linked lists (by last name).
     */
    private Node sortedMerge(Node a, Node b) {
        Node dummy = new Node("", "", "");
        Node tail = dummy;

        while (a != null && b != null) {
            if (a.lastName.compareToIgnoreCase(b.lastName) <= 0) {
                tail.next = a;
                a = a.next;
            } else {
                tail.next = b;
                b = b.next;
            }
            tail = tail.next;
        }

        tail.next = (a != null) ? a : b;
        return dummy.next;
    }

    /**
     * Counts the number of nodes in the list.
     */
    private int getSize(Node head) {
        int count = 0;
        while (head != null) {
            count++;
            head = head.next;
        }
        return count;
    }

    /**
     * Displays the contents of the linked list.
     */
    public void displayList() {
        Node current = head;
        while (current != null) {
            System.out.printf("%-10s %-10s %-10s%n",
                    current.firstName, current.lastName, current.city);
            current = current.next;
        }
        System.out.println();
    }
}

// ----------------------------------------------------------------------
// Driver Class
// ----------------------------------------------------------------------

/**
 * Main driver class.
 * 
 * Demonstrates the use of both recursive and iterative
 * linked list merge sort implementations via the Sorter interface.
 */
public class MergeSortLinkedList {

    public static void main(String[] args) {

        Sorter list;

        int choice = 1;  // 1 = Recursive, 2 = Iterative

        if (choice == 1)
            list = new MergeSortLinkedList_Recursive();
        else
            list = new MergeSortLinkedList_Iterative();

        // Insert sample data
        list.insert("Alice", "Zimmer", "Chicago");
        list.insert("Bob", "Anderson", "Kalispell");
        list.insert("Cathy", "Johnson", "Seattle");
        list.insert("Daniel", "Brown", "Denver");

        // Display before sorting
        System.out.println("Before Sorting:");
        list.displayList();

        // Sort and display results
        list.sort();
        System.out.println("After Sorting by Last Name:");
        list.displayList();
    }
}

```

## When To Use

### Quick summary

- **Both** are `O(n log n)` time, **stable**, and `O(1)` extra space on the list (recursive adds `O(log n)` call-stack space).
- **Recursive** = simpler to read/teach; **Iterative** = no recursion, often better constants and safer for huge inputs.

### Strengths vs. weaknesses

#### Recursive (top-down)

**How it works:** repeatedly split with fast/slow pointers (`getMiddle`), then merge.

**Strengths**

- **Clarity & pedagogy:** mirrors the textbook definition; very readable for students.
- **Natural structure:** the “divide → conquer → combine” flow matches the mental model of merge sort.
- **Easy to parallelize:** left and right halves can be sorted concurrently if you go multi-threaded later.
- **Stable by construction:** merge step preserves order of equals.

**Weaknesses**

- **Call-stack use:** `O(log n)` stack frames. Usually fine, but it’s still extra memory and can matter on very tight stacks or unusual environments.
- **Function-call overhead:** many small recursive calls; minor but measurable on some JVMs.
- **Middle finding every level:** each split uses fast/slow pointers; total cost stays `O(n log n)` but the constant factor isn’t free.

#### Iterative (bottom-up)

**How it works:** repeatedly merge runs of size `1, 2, 4, 8, …` using loops; uses pointer “splicing” (`split`, `merge`) and a dummy head.

**Strengths**

- **No recursion:** avoids stack growth entirely; safer for **very large lists** or constrained runtimes.
- **Good constants:** one linear pass per run size; practical throughput often edges out recursive on linked lists.
- **Predictable control flow:** all in loops; easy to bound and instrument.
- **Still stable:** merge loop preserves order of equals.

**Weaknesses**

- **More pointer surgery:** more places to make off-by-one / null-next mistakes; trickier to get right first time.
- **Slightly less intuitive to newcomers:** bottom-up run doubling is less obvious than “split in half”.
- **Needs size or tail walking:** typical pattern computes `n` up front or advances pointers carefully; again, more book-keeping.

#### Performance & resource notes

- **Time complexity:** both `O(n log n)` on singly linked lists.
- **Space:** both in-place on nodes; **recursive adds `O(log n)` call stack**, iterative doesn’t.
- **Cache locality:** neither is great (linked lists aren’t cache-friendly), but iterative’s fewer function calls can help a bit.
- **Stability:** both remain stable as long as your merge uses `<=` (or equivalent) and never reorders equals.

#### When to pick which

- **Teaching / readability / quick correctness:** **Recursive**.
- **Production on huge lists / tight memory / maximum robustness:** **Iterative**.
- **Parallel sort of very large lists:** **Recursive** lends itself to parallelizing the two halves.

#### Practical checklist

- Need simple code? → **Recursive**.
- Worried about stack or sorting millions of nodes? → **Iterative**.
