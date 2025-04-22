# Examples of Java's HashMap, TreeMap, and LinkedHashMap

## 1. `HashMap`

**Characteristics:**

- Unordered collection (no guarantees on order).
- Fastest performance for basic operations (`get`, `put`) with O(1) average complexity.
- Allows `null` as key/value.

**Example:**

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();

        map.put("apple", 3);
        map.put("banana", 2);
        map.put("orange", 5);

        System.out.println("Value of apple: " + map.get("apple"));

        System.out.println("Iterating HashMap:");
        for (String key : map.keySet()) {
            System.out.println("Key: " + key + ", Value: " + map.get(key));
        }
    }
}
```

**Best Uses:**

- When you need fast lookup and insertion.
- Order doesn't matter.

------

## 2. `TreeMap`

**Characteristics:**

- Sorted according to natural ordering or a specified comparator.
- `O(log n)` complexity for `put`, `get`, `remove` operations.
- Cannot contain `null` keys (but can have null values).

**Example:**

```java
import java.util.Map;
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new TreeMap<>();

        map.put("apple", 3);
        map.put("banana", 2);
        map.put("orange", 5);

        System.out.println("Value of banana: " + map.get("banana"));

        System.out.println("Iterating TreeMap (sorted):");
        for (String key : map.keySet()) {
            System.out.println("Key: " + key + ", Value: " + map.get(key));
        }
    }
}
```

**Best Uses:**

- Maintaining sorted order (such as alphabetical order).
- Range queries (`subMap()`, `headMap()`, `tailMap()`).

------

## 3. `LinkedHashMap`

**Characteristics:**

- Maintains insertion order.
- Slightly slower than `HashMap`, with O(1) average complexity.
- Allows `null` key/value.

**Example:**

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new LinkedHashMap<>();

        map.put("apple", 3);
        map.put("banana", 2);
        map.put("orange", 5);

        System.out.println("Value of orange: " + map.get("orange"));

        System.out.println("Iterating LinkedHashMap (insertion order):");
        for (String key : map.keySet()) {
            System.out.println("Key: " + key + ", Value: " + map.get(key));
        }
    }
}
```

**Best Uses:**

- Caching implementations, where insertion/access order is important.
- Preserving the order of inserted keys (e.g., configurations, ordered tasks).

------

## **Summary (Quick Reference):**

| Feature                        | `HashMap`          | `TreeMap` | `LinkedHashMap` |
| ------------------------------ | ------------------ | --------- | --------------- |
| **Order**                      | No order guarantee | Sorted    | Insertion order |
| **Performance (`get`, `put`)** | O(1) avg.          | O(log n)  | O(1) avg.       |
| **Null Keys Allowed**          | Yes                | No        | Yes             |

------

**References:**

- [Oracle Documentation – HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
- [Oracle Documentation – TreeMap](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)
- [Oracle Documentation – LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)