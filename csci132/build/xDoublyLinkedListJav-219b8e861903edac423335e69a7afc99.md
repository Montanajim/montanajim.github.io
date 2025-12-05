# Java Linked List Class



## What is a Linked List?

A **linked list** is a data structure used to store a collection of elements (nodes). Each node contains two parts:

1. **Data**: The actual value or information.
2. **Pointer (or Reference)**: A link to the next node in the sequence (and optionally, a link to the previous node in the case of doubly linked lists).

Linked lists allow for dynamic memory allocation and efficient insertions and deletions since nodes can be added or removed without reorganizing the entire structure. Unlike arrays, linked lists do not require a contiguous block of memory, making them more flexible.

## Real-Life Applications of Linked Lists

1. **Music Playlists**:
   - A music player can use a linked list to manage a playlist. Each song can be a node, and the player can easily move forward or backward through the playlist (using next and previous pointers), allowing for easy manipulation of the song order.

2. **Undo Functionality in Applications**:
   - Many applications, like text editors, implement an undo feature using a linked list. Each action can be stored as a node in the list, allowing users to navigate backward through their actions and revert to previous states.

3. **Web Browser History**:
   - Browsers use linked lists to maintain the history of visited pages. Each page can be a node, and users can navigate forward and backward through their browsing history easily.

4. **Dynamic Memory Allocation**:
   - Operating systems often use linked lists for managing memory. For instance, free memory blocks can be stored as nodes, allowing the OS to allocate and deallocate memory efficiently as processes start and finish.

5. **Adjacency Lists in Graphs**:
   - In graph data structures, linked lists are often used to represent adjacency lists. Each node in the list represents a vertex, and its linked nodes represent the edges connecting to other vertices, allowing for efficient traversal of graph data.

These applications highlight the versatility and efficiency of linked lists in various scenarios, particularly where dynamic data management is essential.



---



## ArrayList vs. LinkedList

| Feature                        | ArrayList                                                 | LinkedList                                                   |
| ------------------------------ | --------------------------------------------------------- | ------------------------------------------------------------ |
| **Underlying Data Structure**  | Resizable array                                           | Doubly linked list                                           |
| **Memory Allocation**          | Contiguous memory (requires resizing when full)           | Non-contiguous memory (nodes can be scattered)               |
| **Access Time**                | O(1) for index-based access                               | O(n) for index-based access (must traverse nodes)            |
| **Insertion/Deletion**         | O(n) in the worst case (shifting elements needed)         | O(1) for adding/removing at ends; O(n) for middle (traversal needed) |
| **Memory Overhead**            | Less overhead (just the array)                            | More overhead (extra pointers for each node)                 |
| **Performance for Large Data** | Better for large datasets with frequent access            | Better for large datasets with frequent insertions/deletions |
| **Search Complexity**          | O(n) (linear search)                                      | O(n) (linear search)                                         |
| **Thread Safety**              | Not synchronized (not thread-safe by default)             | Not synchronized (not thread-safe by default)                |
| **Use Cases**                  | Best for frequent access, fewer insertions/deletions      | Best for frequent insertions/deletions, less access          |
| **Iteration**                  | Faster for sequential access due to locality of reference | Slower for sequential access (due to pointers)               |

### Summary of Key Differences

1. **Access Speed**: 
   - **ArrayList** allows for faster access due to its contiguous memory allocation. You can directly access any element via its index.
   - **LinkedList** requires traversal from the head to access an element by index, making it slower for random access.

2. **Insertion and Deletion**:
   - **ArrayList** has slower insertion and deletion times (O(n) in the worst case) because elements may need to be shifted.
   - **LinkedList** excels in insertions and deletions at both ends (O(1)), making it ideal for scenarios where these operations are frequent.

3. **Memory Usage**:
   - **ArrayList** typically uses less memory per element since it only stores the elements.
   - **LinkedList** uses more memory due to the extra pointers needed for each node.

### Use Cases

- **ArrayList**: Ideal for scenarios where you need fast access to elements and the size of the data structure is stable or grows infrequently.
- **LinkedList**: Better suited for applications that involve frequent insertions and deletions, such as queues or stacks.

### Conclusion

Choosing between an `ArrayList` and a `LinkedList` depends on the specific use case and performance needs. If you need frequent access and stable size, go for `ArrayList`. If your application requires a lot of insertions and deletions, opt for `LinkedList`. 



---

## Java Linked List Methods

| Method                                         | Description                                                  |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `add(E e)`                                     | Appends the specified element to the end of the list.        |
| `add(int index, E element)`                    | Inserts the specified element at the specified position.     |
| `addFirst(E e)`                                | Inserts the specified element at the beginning of the list.  |
| `addLast(E e)`                                 | Appends the specified element to the end of the list.        |
| `remove(Object o)`                             | Removes the first occurrence of the specified element.       |
| `remove(int index)`                            | Removes the element at the specified position.               |
| `removeFirst()`                                | Removes and returns the first element of the list.           |
| `removeLast()`                                 | Removes and returns the last element of the list.            |
| `get(int index)`                               | Returns the element at the specified position.               |
| `set(int index, E element)`                    | Replaces the element at the specified position with the given element. |
| `size()`                                       | Returns the number of elements in the list.                  |
| `isEmpty()`                                    | Returns `true` if the list is empty, `false` otherwise.      |
| `clear()`                                      | Removes all elements from the list.                          |
| `contains(Object o)`                           | Returns `true` if the list contains the specified element.   |
| `indexOf(Object o)`                            | Returns the index of the first occurrence of the specified element, or -1 if not found. |
| `lastIndexOf(Object o)`                        | Returns the index of the last occurrence of the specified element, or -1 if not found. |
| `listIterator()`                               | Returns a list iterator over the elements in the list.       |
| `iterator()`                                   | Returns an iterator over the elements in the list.           |
| `toArray()`                                    | Returns an array containing all elements in the list.        |
| `toArray(T[] a)`                               | Returns an array containing all elements in the list; the runtime type of the returned array is that of the specified array. |
| `addAll(Collection<? extends E> c)`            | Appends all elements in the specified collection to the end of the list. |
| `addAll(int index, Collection<? extends E> c)` | Inserts all elements in the specified collection at the specified position. |
| `removeAll(Collection<?> c)`                   | Removes all elements in this list that are contained in the specified collection. |
| `retainAll(Collection<?> c)`                   | Retains only the elements in this list that are contained in the specified collection. |
| `clone()`                                      | Returns a shallow copy of the list.                          |



## Demo Code



Here is a Java program that demonstrates the most frequently used methods in the `LinkedList` class. This program showcases common operations such as adding, removing, accessing elements, and checking the size of the list:

```java
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        // Create a LinkedList
        LinkedList<String> list = new LinkedList<>();
        
        // Add elements to the LinkedList
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        list.addFirst("Mango"); // Adds element at the start
        list.addLast("Orange"); // Adds element at the end
        
        // Display the LinkedList
        System.out.println("Initial LinkedList: " + list);

        // Access elements in the LinkedList
        System.out.println("First element: " + list.getFirst());
        System.out.println("Last element: " + list.getLast());
        System.out.println("Element at index 2: " + list.get(2));

        // Check the size of the LinkedList
        System.out.println("Size of LinkedList: " + list.size());

        // Remove elements from the LinkedList
        list.removeFirst(); // Removes the first element
        list.removeLast();  // Removes the last element
        list.remove(1);     // Removes element at index 1
        
        // Display the LinkedList after removals
        System.out.println("LinkedList after removals: " + list);

        // Check if LinkedList contains a specific element
        if (list.contains("Banana")) {
            System.out.println("LinkedList contains Banana");
        } else {
            System.out.println("LinkedList does not contain Banana");
        }

        // Clear the LinkedList
        list.clear();
        System.out.println("LinkedList after clearing: " + list);
    }
}
```

### Explanation of the Methods Used:
1. **`add(element)`** - Adds an element to the end of the list.
2. **`addFirst(element)`** - Adds an element at the beginning of the list.
3. **`addLast(element)`** - Adds an element at the end of the list.
4. **`get(index)`** - Returns the element at the specified position.
5. **`getFirst()` / `getLast()`** - Returns the first or last element, respectively.
6. **`size()`** - Returns the number of elements in the list.
7. **`remove(index)`** - Removes the element at the specified position.
8. **`removeFirst()` / `removeLast()`** - Removes the first or last element, respectively.
9. **`contains(element)`** - Checks if the list contains the specified element.
10. **`clear()`** - Removes all the elements from the list.

---

## LinkedList Iterator

The **LinkedList Iterator** in Java is an object that allows you to traverse the elements of a `LinkedList` sequentially. The `Iterator` is part of the Java Collections Framework and provides methods to iterate through the list, remove elements during iteration, and check for more elements.

### Key Methods of the Iterator:

1. **`hasNext()`**: Returns `true` if there are more elements to iterate.
2. **`next()`**: Returns the next element in the iteration.
3. **`remove()`**: Removes the last element returned by the iterator (optional operation).

### Example Code Using `Iterator` with `LinkedList`:
Here's a sample Java program that demonstrates how to use the `Iterator` to traverse a `LinkedList`:

```java
import java.util.LinkedList;
import java.util.Iterator;

public class LinkedListIteratorDemo {
    public static void main(String[] args) {
        // Create a LinkedList
        LinkedList<String> list = new LinkedList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");
        list.add("Mango");

        // Get the iterator from the LinkedList
        Iterator<String> iterator = list.iterator();

        // Iterate through the LinkedList
        System.out.println("Traversing the LinkedList:");
        while (iterator.hasNext()) {
            String element = iterator.next();
            System.out.println(element);
            
            // Remove "Banana" during iteration
            if (element.equals("Banana")) {
                iterator.remove();
                System.out.println("\"Banana\" has been removed");
            }
        }

        // Display the LinkedList after iteration
        System.out.println("\nLinkedList after iteration: " + list);
    }
}
```

### Output:
```
Traversing the LinkedList:
Apple
Banana
"Banana" has been removed
Cherry
Mango

LinkedList after iteration: [Apple, Cherry, Mango]
```

### Explanation:
1. **Create a `LinkedList`**:
   - We create a `LinkedList` of strings and add elements to it.
   
2. **Get an iterator**:
   - The `iterator()` method of `LinkedList` is used to obtain an `Iterator` for the list.
   
3. **Use the iterator to traverse**:
   - We loop through the list using `hasNext()` and `next()`, which ensure that each element is processed one by one.
   
4. **Remove an element during iteration**:
   - The `remove()` method removes the last element returned by the iterator.
   - In this case, if the current element is `"Banana"`, it is removed from the list.

### Why Use an Iterator with LinkedList?
- **Efficient Traversal**: Iterators are efficient for traversing and manipulating lists because they maintain the state of traversal.
- **Modification During Traversal**: Unlike using a `for` loop or enhanced `for` loop, an `Iterator` allows safe removal of elements during traversal, avoiding `ConcurrentModificationException`.

The iterator is a flexible and powerful way to navigate through and manipulate `LinkedList` elements in Java.