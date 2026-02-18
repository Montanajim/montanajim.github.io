# Java code for double hashing in a hash table:



```java
public class DoubleHashingHashTable {

    private final int tableSize;
    private final Entry[] table;

    public DoubleHashingHashTable(int tableSize) {
        this.tableSize = tableSize;
        this.table = new Entry[tableSize];
    }

    private int hash1(String key) {
        return key.hashCode() % tableSize; // Replace with a better hash function
    }

    private int hash2(String key) {
        int prime = 5; // Choose a prime number less than tableSize
        return prime - (key.hashCode() % prime);
    }

    public void put(String key, String value) {
        int index = insert(key, value);
        if (index == -1) {
            System.out.println("Hash table full!");
        }
    }

    private int insert(String key, String value) {
        int index = hash1(key);
        int stepSize = hash2(key);
        int i = 0;

        while (table[index] != null && table[index].key != key) {
            index = (index + i * stepSize) % tableSize;
            i++;
            if (i == tableSize) {
                return -1; // Table full
            }
        }

        table[index] = new Entry(key, value);
        return index;
    }

    public String get(String key) {
        int index = find(key);
        if (index == -1) {
            return null;
        }
        return table[index].value;
    }

    private int find(String key) {
        int index = hash1(key);
        int stepSize = hash2(key);
        int i = 0;

        while (table[index] != null) {
            if (table[index].key.equals(key)) {
                return index;
            }
            index = (index + i * stepSize) % tableSize;
            i++;
            if (i == tableSize) {
                return -1; // Key not found
            }
        }

        return -1; // Key not found
    }

    private static class Entry {
        String key;
        String value;

        public Entry(String key, String value) {
            this.key = key;
            this.value = value;
        }
    }

    public static void main(String[] args) {
        DoubleHashingHashTable table = new DoubleHashingHashTable(10);
        table.put("apple", "red");
        table.put("banana", "yellow");
        table.put("cherry", "red");
        table.put("grape", "purple");

        System.out.println(table.get("apple")); // Output: red
        System.out.println(table.get("cherry")); // Output: red
    }
}
```

**Explanation:**

1. This code defines a `DoubleHashingHashTable` class that implements a hash table with double hashing.
1. It uses two separate hash functions: `hash1` and `hash2`.
1. The `put` method inserts a key-value pair into the table. If the table is full, it returns -1.
1. The `insert` method uses the first hash function to find the initial index and then employs the second hash function to calculate the step size for probing.
1. The `get` method searches for a key in the table using a similar probing strategy.
1. The `Entry` class represents a key-value pair within the table.
1. The `main` method demonstrates how to use the `DoubleHashingHashTable` by inserting some key-value pairs and then retrieving them.

**Note:** This is a basic implementation and can be further improved by considering:

- Using a better hash function for `hash1`.
- Implementing deletion functionality.
- Rehashing the table when the load factor becomes too high.

---

Here's a code sample demonstrating quadratic hashing in a Java hash table:

Java

```java
public class QuadraticHashTable {

    private final int tableSize;
    private final Entry[] table;

    public QuadraticHashTable(int tableSize) {
        this.tableSize = tableSize;
        this.table = new Entry[tableSize];
    }

    private int hash(String key) {
        return key.hashCode() % tableSize; // Replace with a better hash function
    }

    public void put(String key, String value) {
        int index = insert(key, value);
        if (index == -1) {
            System.out.println("Hash table full!");
        }
    }

    private int insert(String key, String value) {
        int index = hash(key);
        int i = 0;
        int stepSize = 1;

        while (table[index] != null && table[index].key != key) {
            index = (index + stepSize * stepSize) % tableSize;
            stepSize++;
            if (i == tableSize) {
                return -1; // Table full
            }
        }

        table[index] = new Entry(key, value);
        return index;
    }

    public String get(String key) {
        int index = find(key);
        if (index == -1) {
            return null;
        }
        return table[index].value;
    }

    private int find(String key) {
        int index = hash(key);
        int i = 0;
        int stepSize = 1;

        while (table[index] != null) {
            if (table[index].key.equals(key)) {
                return index;
            }
            index = (index + stepSize * stepSize) % tableSize;
            stepSize++;
            if (i == tableSize) {
                return -1; // Key not found
            }
        }

        return -1; // Key not found
    }

    private static class Entry {
        String key;
        String value;

        public Entry(String key, String value) {
            this.key = key;
            this.value = value;
        }
    }

    public static void main(String[] args) {
        QuadraticHashTable table = new QuadraticHashTable(10);
        table.put("apple", "red");
        table.put("banana", "yellow");
        table.put("cherry", "red");

        System.out.println(table.get("apple")); // Output: red
        System.out.println(table.get("cherry")); // Output: red
    }
}
```

**Explanation:**

1. The code defines a `QuadraticHashTable` class with methods for inserting (`put`), retrieving (`get`), and searching for (`find`) key-value pairs.
1. The `hash` function calculates the initial index for a key.
1. The `insert` method implements the core logic of quadratic probing. It calculates the initial index and then uses a quadratic sequence to probe for an empty slot until it finds one or reaches the table size limit.
1. The `get` and `find` methods follow a similar approach to search for an existing key in the table.
1. The `Entry` class represents a key-value pair within the table.
1. The `main` method demonstrates inserting and retrieving elements from the table.

**Note:** This is a basic implementation and can be further improved by:

- Implementing a better hash function for `hash`.
- Implementing deletion functionality.
- Rehashing the table when the load factor becomes too high.