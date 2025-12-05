# Heap Sort

## Introduction

Merge Sort works by taking the chaotic mess of an array and breaking it down into smaller and smaller pieces until each piece is trivially simple to sort. It follows a **divide-and-conquer** rhythm: first divide the array into two halves, then divide those halves again, and keep going until each sub-array contains just one element. A single element is, by definition, already sorted. Once everything is split into these tiny, manageable chunks, Merge Sort begins the **conquer** phase—carefully merging pairs of sorted sub-arrays back together. During each merge, it compares the fronts of both lists and chooses the smaller element, building a new, larger sorted list one element at a time.

The brilliance of Merge Sort lies in this merging step: it guarantees that every combination of two sorted lists becomes one sorted list, and it repeats this until the entire array is reconstructed in perfect order. Its performance is reliably **O(n log n)**, regardless of the data’s original state, making it one of the most stable and predictable sorting algorithms in computer science. It does require extra memory—space to hold the temporary merged lists—but in exchange, it delivers elegant consistency and stability. Merge Sort doesn’t try to be clever; it just applies patient, mathematical discipline to tame disorder.

## **What Is a Heap? (With Diagrams)**

A **heap** is a special kind of binary tree stored inside an array.
 It follows two rules:

1. **Complete tree** (filled left to right)
2. **Heap property** (max-heap = parent ≥ children)

### **How a max-heap is stored in an array**

If an element is at index `i`:

- **Left child:** `2*i + 1`
- **Right child:** `2*i + 2`
- **Parent:** `(i-1) // 2`

### **Example Array**

```
Index: 0  1  2  3  4
Value: 4 10  3  5  1
```

### **As a Heap (Tree Form)**

```
          4 (0)
       /        \
   10 (1)       3 (2)
    /   \
  5(3)  1(4)
```

Right now this is **not** a proper max heap.
 Heap Sort’s first job is to fix that.

------

## **Phase 1: Building the Max Heap**

We “heapify” from the bottom up.

Starting at the last parent node: index **(n//2 − 1)**

For our array of 5 elements:

- Last parent = `5//2 - 1 = 1`

So we heapify indices: **1**, then **0**

------

### **Heapify index 1**

Node = 10
 Children = 5 and 1
 Already a valid max-heap section.

```
          4
       /     \
    10        3
   /   \
  5     1
```

No changes.

------

### **Heapify index 0**

Node 0 = 4
 Children = 10 and 3
 Largest is **10**, so swap 4 ↔ 10

```
          10
       /        \
     4           3
   /   \
  5     1
```

Now heapify the subtree rooted at index 1 (value 4):

Compare 4 to its children (5 and 1):

Largest is **5**, so swap 4 ↔ 5:

```
          10
       /        \
     5           3
   /   \
  4     1
```

We’re done—this is a proper **max heap**.

------

## **Phase 2: Extracting the Maximum (Sorting)**

Now we repeatedly:

1. Swap root ↔ last element
2. Shrink heap size
3. Heapify again

Each diagram below shows the transformation.

------

### **Step 1: Swap Root With Last Element**

Swap 10 ↔ 1

```
Array: [1, 5, 3, 4, 10]
Heap Size: 4
```

Tree:

```
           1
       /        \
     5           3
   /   
  4    
```

Now heapify index 0.

### **Heapify →**

Largest child = 5 → swap 1 ↔ 5

```
           5
       /        \
     1           3
   /
  4
```

Heapify index 1:

1 < 4 → swap 1 ↔ 4

```
           5
       /        \
     4           3
   /
  1
```

Array now:

```
[5, 4, 3, 1, 10]
```

------

## **Step 2: Swap Root With Element at Index 3**

Swap 5 ↔ 1:

```
[1, 4, 3, 5, 10]
Heap Size: 3
```

Tree:

```
         1
       /   \
     4       3
```

Heapify index 0 → swap 1 ↔ 4:

```
         4
       /   \
     1       3
```

Array becomes:

```
[4, 1, 3, 5, 10]
```

------

## **Step 3: Swap Root With Element at Index 2**

Swap 4 ↔ 3:

```
[3, 1, 4, 5, 10]
Heap Size: 2
```

Heapify index 0:

Compare 3 and 1 → already valid.

Array:

```
[3, 1, 4, 5, 10]
```

------

## **Step 4: Swap Root With Element at Index 1**

Swap 3 ↔ 1:

```
[1, 3, 4, 5, 10]
Heap Size: 1
```

Sorting complete.

------

## **Final Sorted Array**

```
[1, 3, 4, 5, 10]
```

The mountain of numbers has been carved into a perfect, ascending ridge.

------

## **Complete Visual Summary**

```
Start:          Build Max Heap:      Extract 1:         Extract 2:

[4 10 3 5 1] →  [10 5 3 4 1] →       [5 4 3 1 10] →     [4 1 3 5 10]

Extract 3:      Extract 4:           Sorted:

[3 1 4 5 10] →  [1 3 4 5 10] →       [1 3 4 5 10]
```

------

## **Python Code**

```python
# heap_sort()
# Performs Heap Sort on the provided array.
# The process has two phases:
#   1. Build a max-heap from the entire array.
#   2. Repeatedly swap the root (largest value) with the last
#      element in the heap and shrink the heap size.

def heap_sort(arr):

    n = len(arr)    # Number of elements in the list


    # Build the max heap (bottom-up)
    # We start heapifying at the last parent node and move
    # backwards toward the root. This ensures the entire array
    # becomes a valid max-heap.

    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)


    # Extract elements from the heap one by one
    # Each extraction moves the current maximum (index 0)
    # to the end of the array. Then we reduce the heap size
    # and restore the heap property.

    for i in range(n-1, 0, -1):

        # Move current largest value (arr[0]) to the end
        arr[i], arr[0] = arr[0], arr[i]

        # Restore heap property on the reduced heap (size i)
        heapify(arr, i, 0)




# heapify()
# Ensures that the subtree rooted at index i follows the
# max-heap property. If the parent is smaller than one of its
# children, we swap it with the larger child and continue
# heapifying downward.
#
# arr : the list we are treating as a heap
# n   : the size of the heap section we're working with
# i   : the index of the current parent node

def heapify(arr, n, i):

    largest = i             # Assume the parent is the largest
    left = 2*i + 1          # Index of the left child
    right = 2*i + 2         # Index of the right child

    # If the left child exists and is larger than the parent,
    # mark it as the new largest.
    if left < n and arr[left] > arr[largest]:
        largest = left

    # If the right child exists and is larger than the current
    # largest value, update the largest.
    if right < n and arr[right] > arr[largest]:
        largest = right

    # If the largest element is NOT the parent (i),
    # swap parent with the largest child.
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]

        # After the swap, the subtree rooted at 'largest'
        # may now violate the heap property, so we fix it
        # by heapifying again.
        heapify(arr, n, largest)




```

------

## **Java Code**

```java
// HeapSort class
public class HeapSort {


    public void sort(int[] arr) {

        int n = arr.length;   // Total number of elements

		/*
		Build Heap
        We start from the last parent node and move backward.
        (n/2 - 1) is the index of the last non-leaf node.
        Each heapify call ensures the subtree rooted at i
        follows the max-heap property.
        */
        
        
        for (int i = n/2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

       	/* Extract elements from heap
        We repeatedly swap the max element (index 0)
        with the last element in the heap.
        After each swap, we shrink the heap size by 1
        and restore heap order.
        */
        for (int i = n - 1; i >= 0; i--) {

            // Move current root (largest value) to end
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // Restore heap property on the reduced heap
            heapify(arr, i, 0);
        }
    }

    /* Heapify
    heapify(): Ensures the subtree rooted at index i
    obeys the max-heap rule.
    
    arr   = array representing the heap
    n     = size of the heap section we're working with
    i     = index of the current root node
    */
    
    void heapify(int[] arr, int n, int i) {

        int largest = i;        // Assume the parent is the largest
        int left = 2*i + 1;     // Index of left child
        int right = 2*i + 2;    // Index of right child

        // If the left child exists and is greater than the parent,
        // mark it as the new largest.
        if (left < n && arr[left] > arr[largest])
            largest = left;

        // If the right child exists and is greater than the current largest,
        // update the largest value.
        if (right < n && arr[right] > arr[largest])
            largest = right;

        // If the largest element is NOT the parent,
        // swap them and continue heapifying downward.
        if (largest != i) {

            // Swap parent with the larger child
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Recursively heapify the affected subtree
            heapify(arr, n, largest);
        }
    }
}

```


----

## **Best Use Cases for Heap Sort**

Heap Sort shines when you want **predictable performance** and **tight memory discipline**. Because it runs in a guaranteed **O(n log n)**—regardless of how ugly the input is—it’s a strong choice when you absolutely must avoid the worst-case meltdowns that plague something like QuickSort. It also sorts **in place**, which means it needs only constant extra space; this makes it ideal for memory-constrained environments such as embedded systems, older hardware, or large data sets that can’t afford the luxury of extra arrays. And since the algorithm is tightly aligned with the behavior of **priority queues**, it’s a natural fit whenever you are already working with heaps—like scheduling tasks, selecting the top-k elements, or managing simulations. When memory counts and guaranteed performance matters, Heap Sort is the reliable, strong-backed workhorse of the sorting world.



## **Worst Use Cases for Heap Sort**

But Heap Sort also has its rough edges. It is **not stable**, meaning equal elements can be reordered—a deal breaker in situations where order matters (such as sorting records by one field while preserving their sequence by another). It’s also **cache-unfriendly**; its constant jumping around in memory makes it slower in practice than algorithms like QuickSort or Merge Sort on modern hardware, even though they share the same theoretical time complexity. If you need blazing performance on real-world data, or if you're sorting structures where preserving relative order matters, Heap Sort isn’t the hero—there are faster, smoother tools. And if your environment allows recursion, extra memory, or stable sorting, then Merge Sort or TimSort will leave Heap Sort sitting in the dust.
