# Arrays, ArrayLists, Lists, Sets, and Maps

1. **Arrays**:
    - **Fixed Size**: Arrays have a fixed size determined during initialization.
    - **Indexed Access**: Elements can be accessed by their index.
    - **Primitive Types and Objects**: Arrays can hold both primitive types and objects.
    - **Use Cases**:
        - When you know the exact size of the collection in advance.
        - For efficient memory usage and direct access to elements.
2. **ArrayList**:
    - **Dynamic Size**: ArrayLists can grow or shrink dynamically.
    - **Ordered Collection**: Elements are ordered by their insertion order.
    - **Allows Duplicates**: ArrayLists allow duplicate elements.
    - **Use Cases**:
        - When you need a resizable list.
        - For maintaining a collection of related data.
3. **Lists (Interface)**:
    - **Ordered Collection**: Lists maintain order and allow positional access.
    - **Allows Duplicates**: Lists can contain duplicate elements.
    - **Common Implementations**: ArrayList, LinkedList, Vector, Stack.
    - **Use Cases**:
        - To-do lists, history tracking, playlist management.
4. **Sets (Interface)**:
    - **Distinct Elements**: Sets ensure uniqueness; no duplicates allowed.
    - **Unordered Collection**: Sets don’t guarantee any specific order.
    - **Common Implementations**: HashSet, LinkedHashSet.
    - **Use Cases**:
        - User authentication (unique usernames or IDs).
        - Removing duplicates from data.
        - Tagging systems.
5. **Key-Value Lists (Map Interface)**:
    - **Associative Data Structure**: Maps store key-value pairs.
    - **Fast Lookup**: Efficient retrieval of values using keys.
    - **Common Implementations**: HashMap, TreeMap, LinkedHashMap.
    - **Use Cases**:
        - Storing configuration settings.
        - Building dictionaries or caches.
        - Counting occurrences of elements.
        
        ```java
        import java.util.*;
        
        public class DataStructureComparison {
            public static void main(String[] args) {
                // Example usage of ArrayList, HashSet, and HashMap
                ArrayList<String> myList = new ArrayList<>();
                myList.add("apple");
                myList.add("banana");
                myList.add("cherry");
        
                Set<Integer> mySet = new HashSet<>();
                mySet.add(10);
                mySet.add(20);
                mySet.add(10); // Duplicate value won't be added
        
                Map<String, Integer> myMap = new HashMap<>();
                myMap.put("one", 1);
                myMap.put("two", 2);
                myMap.put("three", 3);
        
                System.out.println("ArrayList: " + myList);
                System.out.println("HashSet: " + mySet);
                System.out.println("HashMap: " + myMap);
            }
        }
        
        /*
        Output
        ArrayList: [apple, banana, cherry]
        HashSet: [10, 20]
        HashMap: {one=1, two=2, three=3}
        */
        ```
        
        ---
        
        ## **Comparison of Java Data Structures**
        
        | Feature | Arrays | ArrayLists (implements List) | Lists (Interface) | Sets | Key-Value Lists (Maps) |
        | --- | --- | --- | --- | --- | --- |
        | Underlying Structure | Fixed-size contiguous memory block | Dynamically resizable array | Interface, can have various implementations | Hash table for fast lookups | Key-value pairs |
        | Ordering | Ordered | Ordered | Ordered (depends on implementation) | Unordered | Not applicable |
        | Duplicates | Allowed | Allowed | Allowed (depends on implementation) | Not allowed | Keys must be unique |
        | Resizing | Not possible | Dynamically grows/shrinks | Depends on implementation | Dynamically grows | Dynamically grows |
        | Accessing Elements | Efficient random access by index | Efficient random access by index | Depends on implementation (may/may not support random access) | No random access, uses contains(element) | Access by unique key (e.g., map.get("key")) |
        | Use Cases | Fixed-size data with fast random access | Ordered, resizable collections with duplicates | General concept for ordered collections | Unique elements, fast membership checks | Associating unique keys with values |