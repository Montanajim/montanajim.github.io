# *Understanding Hash Tables and Hash Functions**

A **hash table** (or **hash map**) is a data structure that efficiently stores and retrieves key-value pairs using a **hash function**. The function converts a key into an index used to store and locate values quickly.

------

## **Real-World Use Cases of Hash Tables**

Hash tables are widely used in software development, databases, and networking due to their fast access times. Here are some key applications:

1. **Databases and Caching**
   - **Indexing**: Hash tables help optimize database search operations.
   - **Caching**: Used in applications like Redis and Memcached to store frequently accessed data.
2. **Compilers and Interpreters**
   - **Symbol Tables**: Stores variable names, function names, and their corresponding memory addresses.
3. **Networking**
   - **Routing Tables**: Hash tables map IP addresses to network devices for efficient packet routing.
   - **DNS Resolution**: Maps domain names to IP addresses.
4. **Cybersecurity**
   - **Cryptographic Hashing**: Used to store passwords securely (e.g., **SHA-256**, **bcrypt**).
   - **Data Integrity Verification**: Hash functions check if files have been altered.
5. **Operating Systems**
   - **Process Scheduling**: Hash tables store process states efficiently.
   - **File Systems**: Used in file indexing systems.
6. **Machine Learning & AI**
   - **Feature Hashing**: Converts large input spaces into a fixed-size representation.
   - **Nearest Neighbor Search**: Accelerates similarity searches.
7. **Blockchain and Cryptography**
   - **Bitcoin and Ethereum** use **Merkle Trees**, which rely on hash functions for data integrity.
8. **Web Development**
   - **Session Management**: Hash maps store user sessions efficiently.
   - **Auto-Complete Features**: Maps user input to predicted results.

Because of their efficiency and versatility, hash tables are a foundational data structure across various computing fields.

------

## **How Hash Tables Work**

1. **Hashing Function**: A function converts a key (e.g., a string or number) into an integer.
2. **Indexing**: The computed hash determines the storage location in an array.
3. **Collision Handling**: Since multiple keys can hash to the same index (collision), hash tables use methods like **chaining** or **open addressing**.

------

## **Understanding Hash Functions**

A **hash function** maps input data (keys) to an integer index in a hash table.

Example of a simple hash function in Java:

```java
private int hash(String key) {
    return Math.abs(key.hashCode()) % SIZE;  // Uses Java's built-in hashCode()
}
```

- The `hash()` method uses Java’s `hashCode()` function.
- The modulus operation ensures the index falls within the valid range of the array.

### **Key Properties of a Good Hash Function**

1. **Deterministic**: The same input always produces the same output.
2. **Uniform Distribution**: Keys should be distributed evenly across the table.
3. **Efficient Computation**: Fast calculation of hash values.
4. **Minimal Collisions**: Different keys should ideally generate unique outputs.

------

## **Collision Handling Methods**

Since different keys may hash to the same index, hash tables use **collision resolution strategies**.

### **1. Chaining (Separate Chaining)**

- Each index in the table holds a linked list (or another data structure) to store multiple key-value pairs.
- If a collision occurs, new elements are simply appended to the linked list at the index.

### **Chaining Implementation in Java**

```java
import java.util.LinkedList;

class HashTableChaining {
    private static final int SIZE = 10;
    private LinkedList<Entry>[] table;

    public HashTableChaining() {
        table = new LinkedList[SIZE];
        for (int i = 0; i < SIZE; i++) {
            table[i] = new LinkedList<>();
        }
    }

    private int hash(String key) {
        return Math.abs(key.hashCode()) % SIZE;
    }

    public void insert(String key, String value) {
        int index = hash(key);
        for (Entry entry : table[index]) {
            if (entry.key.equals(key)) {
                entry.value = value;
                return;
            }
        }
        table[index].add(new Entry(key, value));
    }

    public String search(String key) {
        int index = hash(key);
        for (Entry entry : table[index]) {
            if (entry.key.equals(key)) {
                return entry.value;
            }
        }
        return null;
    }

    public void delete(String key) {
        int index = hash(key);
        table[index].removeIf(entry -> entry.key.equals(key));
    }

    private static class Entry {
        String key, value;
        public Entry(String key, String value) { this.key = key; this.value = value; }
    }

    public static void main(String[] args) {
        HashTableChaining ht = new HashTableChaining();
        ht.insert("name", "Alice");
        ht.insert("age", "25");
        System.out.println(ht.search("name")); // Output: Alice
        ht.delete("name");
        System.out.println(ht.search("name")); // Output: null
    }
}
```

------

### **2. Open Addressing**

Instead of using separate lists, open addressing stores all entries directly in the table. If a collision occurs, the algorithm searches for an available slot using a **probing technique**.

#### **Types of Open Addressing**

1. **Linear Probing**: Check the next available slot sequentially.
2. **Quadratic Probing**: Check slots at increasing intervals (e.g., 1², 2², 3²…).
3. **Double Hashing**: Use a secondary hash function to find new slots.

### **Open Addressing Implementation in Java (Linear Probing)**

```java
class HashTableOpenAddressing {
    private static final int SIZE = 10;
    private Entry[] table;
    private static final Entry DELETED = new Entry(null, null); // Marker for deleted entries

    public HashTableOpenAddressing() {
        table = new Entry[SIZE];
    }

    private int hash(String key) {
        return Math.abs(key.hashCode()) % SIZE;
    }

    public void insert(String key, String value) {
        int index = hash(key);
        while (table[index] != null && table[index] != DELETED) {
            index = (index + 1) % SIZE; // Linear probing
        }
        table[index] = new Entry(key, value);
    }

    public String search(String key) {
        int index = hash(key);
        while (table[index] != null) {
            if (table[index] != DELETED && table[index].key.equals(key)) {
                return table[index].value;
            }
            index = (index + 1) % SIZE;
        }
        return null;
    }

    public void delete(String key) {
        int index = hash(key);
        while (table[index] != null) {
            if (table[index].key.equals(key)) {
                table[index] = DELETED; // Mark as deleted
                return;
            }
            index = (index + 1) % SIZE;
        }
    }

    private static class Entry {
        String key, value;
        public Entry(String key, String value) { this.key = key; this.value = value; }
    }

    public static void main(String[] args) {
        HashTableOpenAddressing ht = new HashTableOpenAddressing();
        ht.insert("name", "Alice");
        ht.insert("age", "25");
        System.out.println(ht.search("name")); // Output: Alice
        ht.delete("name");
        System.out.println(ht.search("name")); // Output: null
    }
}
```

------

### **Choosing the Right Hashing Method**

- **For general hash tables**: `MurmurHash` or `FNV-1a`

- **For security**: `SHA-256`

- **For simplicity**: `DJB2` or `Remainder`

- For handling collisions:

  - Use **chaining** when working with dynamic-sized tables.
- Use **open addressing** when memory efficiency is critical.

