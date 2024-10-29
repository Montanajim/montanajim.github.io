# C# Linked List Class

Here's the revised version, adding information about `ArrayList` in Section 3:

## 1. **What is a Linked List?**

A linked list is a data structure used to store a sequence of elements, where each element is called a node. In the case of a doubly linked list:
- **Data**: Each node contains the data or value.
- **Pointers**: Each node has two pointers—one pointing to the next node and one pointing to the previous node.

C# has a built-in generic `LinkedList<T>` class that represents a doubly linked list, supporting dynamic memory allocation and efficient insertions and deletions.

## 2. **Real-Life Applications of Linked Lists**

- **Music Playlists**: Linked lists can manage playlists, where songs can be accessed or rearranged using the next and previous pointers.
- **Undo Functionality in Applications**: Applications like text editors can use linked lists to maintain a history of changes.
- **Web Browser History**: Browsers can use linked lists to manage navigation history, allowing forward and backward traversal.
- **Dynamic Memory Allocation**: Operating systems can use linked lists to manage memory blocks, making memory allocation and deallocation efficient.
- **Adjacency Lists in Graphs**: In graphs, adjacency lists are often implemented using linked lists for efficient traversal of vertices and edges.

## 3. **ArrayList vs. LinkedList**

C# provides two main collections that can be used to manage dynamic sequences of elements: `ArrayList` and `LinkedList<T>`. Here's a comparison:

| Feature                       | ArrayList                          | LinkedList (C#)                         |
| ----------------------------- | ---------------------------------- | --------------------------------------- |
| **Underlying Data Structure** | Resizable array                    | Doubly linked list                      |
| **Memory Allocation**         | Contiguous (requires resizing)     | Non-contiguous (nodes can be scattered) |
| **Access Time**               | O(1) for index-based access        | O(n) (must traverse nodes)              |
| **Insertion/Deletion**        | O(n) for shifting elements         | O(1) at ends; O(n) for middle           |
| **Memory Overhead**           | Less (just array)                  | More (extra pointers for each node)     |
| **Search Complexity**         | O(n) (linear search)               | O(n) (linear search)                    |
| **Thread Safety**             | Not synchronized (not thread-safe) | Not synchronized (not thread-safe)      |

### Key Differences:

- **Access Speed**: 
  - `ArrayList` provides faster access due to contiguous memory allocation, allowing elements to be accessed directly via index.
  - `LinkedList<T>` requires traversal from the head to access an element by index, making it slower for random access.
- **Insertion and Deletion**:
  - `ArrayList` has slower insertion and deletion times (O(n) in the worst case) because elements need to be shifted.
  - `LinkedList<T>` excels in insertions and deletions at both ends (O(1)), making it ideal for scenarios where these operations are frequent.
- **Memory Usage**: 
  - `ArrayList` typically uses less memory since it only stores the elements.
  - `LinkedList<T>` uses more memory due to the extra pointers needed for each node.

### Use Cases:

- **ArrayList**: Better suited for scenarios where fast access to elements is needed and the size of the data structure is stable or grows infrequently.
- **LinkedList<T>**: Ideal for applications that require frequent insertions and deletions, such as queues, stacks, and dynamic data management.

## 4. **Use Cases**

- **ArrayList**: Best for fast access and stable size.
- **LinkedList**: Ideal for scenarios involving frequent insertions and deletions, particularly at the ends.

## 5. **C# Linked List Methods**

Here's a breakdown of common methods in the C# `LinkedList<T>` class:

| C# Method           | Description                                            |
| ------------------- | ------------------------------------------------------ |
| `AddLast(T value)`  | Adds an element to the end of the list.                |
| `AddFirst(T value)` | Adds an element at the start of the list.              |
| `Remove(T value)`   | Removes the first occurrence of the specified element. |
| `RemoveFirst()`     | Removes and returns the first element.                 |
| `RemoveLast()`      | Removes and returns the last element.                  |
| `Count`             | Returns the number of elements in the list.            |

## 6. **Demo Code**

Here’s a C# code example that performs basic operations with `LinkedList<T>`:

```csharp
using System;
using System.Collections.Generic;

public class LinkedListDemo
{
    public static void Main(string[] args)
    {
        // Create a LinkedList
        LinkedList<string> list = new LinkedList<string>();

        // Add elements to the LinkedList
        list.AddLast("Apple");
        list.AddLast("Banana");
        list.AddLast("Cherry");
        list.AddFirst("Mango");
        list.AddLast("Orange");

        // Display the LinkedList
        Console.WriteLine("Initial LinkedList: " + string.Join(", ", list));

        // Access elements in the LinkedList
        Console.WriteLine("First element: " + list.First.Value);
        Console.WriteLine("Last element: " + list.Last.Value);

        // Check the size of the LinkedList
        Console.WriteLine("Size of LinkedList: " + list.Count);

        // Remove elements from the LinkedList
        list.RemoveFirst();
        list.RemoveLast();
        list.Remove("Banana");

        // Display the LinkedList after removals
        Console.WriteLine("LinkedList after removals: " + string.Join(", ", list));

        // Check if LinkedList contains a specific element
        if (list.Contains("Cherry"))
        {
            Console.WriteLine("LinkedList contains Cherry");
        }
        else
        {
            Console.WriteLine("LinkedList does not contain Cherry");
        }

        // Clear the LinkedList
        list.Clear();
        Console.WriteLine("LinkedList after clearing: " + (list.Count == 0 ? "Empty" : string.Join(", ", list)));
    }
}
```

## 7. **Iterator with LinkedList in C#**

Iterators allow sequential traversal through a linked list in C#, facilitating the processing of each element.

#### Example Code Using Iterator with LinkedList:

```csharp
using System;
using System.Collections.Generic;

public class LinkedListIteratorDemo
{
    public static void Main(string[] args)
    {
        LinkedList<string> list = new LinkedList<string>(new[] { "Apple", "Banana", "Cherry", "Mango" });

        // Get an enumerator for the LinkedList
        var enumerator = list.GetEnumerator();

        Console.WriteLine("Traversing the LinkedList:");
        while (enumerator.MoveNext())
        {
            string element = enumerator.Current;
            Console.WriteLine(element);

            // Remove "Banana" during iteration
            if (element == "Banana")
            {
                list.Remove(element);
                Console.WriteLine("\"Banana\" has been removed");
            }
        }

        // Display the LinkedList after iteration
        Console.WriteLine("\nLinkedList after iteration: " + string.Join(", ", list));
    }
}
```

### 8. **Why Use an Iterator with LinkedList in C#?**
- **Efficient Traversal**: Iterators (or enumerators) provide an efficient way to traverse through linked list nodes.
- **Modification During Traversal**: Enumerators allow safe modification of elements during traversal, making them useful for dynamic data handling.

