# HashSet, LinkedHashSet, and TreeSet Comparision

Comparison of `HashSet`, `LinkedHashSet`, and `TreeSet` in Java. These are all implementations of the `Set` interface, meaning they store unique elements. Their main differences lie in their internal implementation, element ordering, performance characteristics, and handling of null values.

**Core Similarity:**

- **Implement `Set` Interface:** All three classes implement the `java.util.Set` interface.
- **Store Unique Elements:** They do not allow duplicate elements. Adding an element that is already present (according to the `equals()` method) has no effect.

**Key Differences:**

Here's a table summarizing the main distinctions:

| **Feature**                | **HashSet**                                    | **LinkedHashSet**                                            | **TreeSet**                                                  |
| -------------------------- | ---------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Underlying Structure**   | `HashMap`                                      | `LinkedHashMap`                                              | `TreeMap` (Red-Black Tree)                                   |
| **Ordering**               | Unordered                                      | Insertion Order                                              | Sorted Order (Natural or Custom)                             |
| **Performance (Avg)**      | O(1) for `add`, `remove`, `contains`           | O(1) for `add`, `remove`, `contains` (slightly higher constant factor than HashSet) | O(logn) for `add`, `remove`, `contains`                      |
| **Iteration Performance**  | Proportional to capacity + size                | Proportional to size                                         | Proportional to size (O(n) total)                            |
| **Null Elements**          | Allows one `null` element                      | Allows one `null` element                                    | Does *not* allow `null` elements (by default)¹               |
| **Interfaces Implemented** | `Set`, `Cloneable`, `Serializable`             | `Set`, `Cloneable`, `Serializable`                           | `Set`, `NavigableSet`, `SortedSet`, `Cloneable`, `Serializable` |
| **Key Requirement**        | `hashCode()` and `equals()` must be consistent | `hashCode()` and `equals()` must be consistent               | Elements must be mutually comparable (implement `Comparable` or use a `Comparator`)² |

**Detailed Explanations:**

1. **`HashSet`**
   - **Implementation:** Uses a `HashMap` internally. The elements you add to the `HashSet` become the keys in the underlying `HashMap`, and a dummy `Object` is used as the value.
   - **Ordering:** It makes no guarantees about the iteration order of the elements. The order might even change over time as more elements are added and the internal hash table is resized.
   - **Performance:** Offers the best average-case performance (O(1)) for basic operations (`add`, `remove`, `contains`), assuming the hash function disperses elements properly among the buckets. However, iteration performance depends on both the number of elements (size) and the hash table's capacity.
   - **Nulls:** Allows one `null` element.
   - **Use Case:** Best choice when you need a general-purpose `Set`, don't care about the order of elements, and want the fastest performance for adding, removing, and checking for presence.
2. **`LinkedHashSet`**
   - **Implementation:** It's a subclass of `HashSet`. Internally, it uses a `LinkedHashMap` (which maintains both a hash table like `HashMap` and a doubly-linked list connecting the elements).
   - **Ordering:** Maintains the insertion order of elements. When you iterate over a `LinkedHashSet`, the elements appear in the order they were added.
   - **Performance:** Offers the same O(1) average-case performance for `add`, `remove`, and `contains` as `HashSet`, although with a slightly higher constant overhead due to maintaining the linked list. Iteration performance is better than `HashSet` in typical scenarios because it only depends on the number of elements (size), not the capacity.
   - **Nulls:** Allows one `null` element.
   - **Use Case:** Ideal when you need the uniqueness of a `Set` but also need to maintain the order in which elements were inserted. Useful for creating predictable sequences or caches where insertion order matters.
3. **`TreeSet`**
   - **Implementation:** Uses a `TreeMap` internally, which is based on a Red-Black Tree data structure.
   - **Ordering:** Keeps elements sorted according to their *natural ordering* (if the elements implement the `Comparable` interface) or according to a `Comparator` provided when the `TreeSet` is created.
   - **Performance:** Offers O(logn) performance for `add`, `remove`, and `contains` operations due to the balanced tree structure. Iteration is efficient (O(n) for the whole set).
   - **Nulls:** ¹ Does **not** allow `null` elements by default because `null` cannot be compared to other elements using natural ordering (it would cause a `NullPointerException`). If you use a `Comparator` that explicitly handles `null`, you *might* be able to store one, but it's generally not recommended.
   - **Interfaces:** Implements `NavigableSet` and `SortedSet`, providing additional methods for navigation (e.g., `first()`, `last()`, `headSet()`, `tailSet()`, `ceiling()`, `floor()`).
   - **Requirements:** ² Elements added must be *mutually comparable*. This usually means they must all implement the `Comparable` interface, or you must supply a suitable `Comparator`. Adding non-comparable elements (or elements of incompatible types) will result in a `ClassCastException`.
   - **Use Case:** The go-to choice when you need a `Set` that automatically keeps elements sorted, or when you need the navigational capabilities provided by the `SortedSet` and `NavigableSet` interfaces.

**When to Use Which:**

- Use `HashSet` if: You need maximum speed and don't care about element order.
- Use `LinkedHashSet` if: You need the performance benefits of hashing but also need to maintain the order of insertion.
- Use `TreeSet` if: You need elements to be kept in a sorted order (either natural or custom) or require navigational methods.

By understanding these differences, you can choose the most appropriate `Set` implementation for your specific needs in Java.



```java

/**
Developer: James Goudy 
Project HashSet, LinkedHashSet, TreeSet - Demo 

Sets - can only contain unique values 


 */
package java_sets; // Declares the package name for this Java file

/**
 *
 * @author jgoudy 
 */
// Import statements for necessary Java utility classes


// Imports the HashSet class, which implements the Set interface 
// using a hash table (no guaranteed order)
import java.util.HashSet;

// Imports the LinkedHashSet class, which maintains insertion order
import java.util.LinkedHashSet;

// Imports the Set interface, the base interface for all set collections
import java.util.Set;

// Imports the TreeSet class, which stores elements 
// in a sorted order (natural ordering or by Comparator)
import java.util.TreeSet;

// Public class definition named Java_Sets
public class Java_Sets {


    /*
    Notice how easy it is to switch between the different sets. 
    Difference being is how order is being stored/not stored pending 
    the algorithm 
    
    */
    
    
    // The main method, the entry point of the Java application
    public static void main(String[] args) 
    {

        // Declare a variable 'mySet' of type Set that can hold String objects. 
        // This uses the interface type, allowing different 
        // implementations to be assigned later.
        Set<String> mySet; 
        

        // Initialize a String array 'myData' with some sample data, 
        // including duplicate values.
        String[] myData = {"AA","AA.","BB", "CC", "DD", "BB", "EE.", 
                           "CC", "AA", "FF", "AA","BB", "GG","EE"};
        
        // --------------- HashSet Demonstration -----------------------------------      
        
        // Instantiate 'mySet' as a new HashSet. 
        // HashSet does not guarantee any specific order of elements.
        mySet = new HashSet<>(); 
        
        // Loop through each 'value' in the 'myData' array
        for (String value : myData) {
            
            // Add the 'value' to the HashSet. If the value is already present,
            // add() returns false and 
            // the set remains unchanged (ensuring uniqueness).
            
            mySet.add(value); 
        }

        // Print a header indicating the output is from the HashSet
        System.out.println("\nHashset - no guarantee of order");
        
        // Loop through each 'value' currently in the HashSet
        for (String value : mySet) {
            // Print the value followed by a space. The order is unpredictable.
            System.out.print(value + " "); 
        }
        
        // Print newlines for better formatting in the console output
        System.out.println("\n"); 
        

        // --------------- LinkedHashSet Demonstration -----------------------
        // Re-instantiate 'mySet' as a new LinkedHashSet. 
        // LinkedHashSet maintains the order in which elements were inserted.
        mySet = new LinkedHashSet<>(); 

        // Loop through each 'value' in the 'myData' array again
        for (String value : myData) {
            // Add the 'value' to the LinkedHashSet. 
            // Duplicates are ignored. Insertion order is preserved.
            mySet.add(value); 
        }

        // Print a header indicating the output is from the LinkedHashSet and 
        // its characteristic (Insertion Order)
        System.out.println("\nLinkedSet - Insertion Order"); 
        
        
        // Loop through each 'value' currently in the LinkedHashSet
        for (String value : mySet) {
            
            // Print the value followed by a space. 
            // The order will match the insertion sequence 
            // of unique elements from myData.
            System.out.print(value + " "); 
        }
        // Print newlines for formatting
        System.out.println("\n"); 
        

        // ------------------ TreeSet Demonstration --------------------------
        // Re-instantiate 'mySet' as a new TreeSet. 
        // TreeSet stores elements in a sorted order 
        // (natural alphabetical order for Strings).
        mySet = new TreeSet<>(); 

        // Loop through each 'value' in the 'myData' array once more
        for (String value : myData) {
            
            // Add the 'value' to the TreeSet. 
            // Duplicates are ignored. 
            //Elements are automatically sorted upon insertion.
            mySet.add(value); 
        }

        // Print a header indicating the output is from the TreeSet and 
        // its sorting mechanism (based on Red-Black Tree, 
        // resulting in sorted order)
        System.out.println("\nTreeSet - Items put in order based "
                           + "on Red Black Tree");
        
        
        // Loop through each 'value' currently in the TreeSet
        for (String value : mySet) {
            // Print the value followed by a space. 
            // The order will be alphabetical.
            System.out.print(value + " "); 
        }
        
        
        // Print newlines for formatting
        System.out.println("\n"); 

    } // End of the main method

} // End of the Java_Sets class

```

