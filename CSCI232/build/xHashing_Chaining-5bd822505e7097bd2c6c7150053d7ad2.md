# Hash Tables - Chaining

In hash tables, **chaining** is a **collision resolution technique** used to address the issue of collisions. A collision occurs when two different keys map to the same index in the hash table's internal array. Chaining provides a way to store these colliding elements efficiently.

Here's how chaining works:

1. **Hash Function:** Like other collision resolution techniques, chaining starts with a **hash function**. This function takes a key as input and generates a **hash value**, which is used as an index to access a specific location (bucket) in the hash table's array.
1. **Collision:** If two different keys happen to have the same hash value, a collision occurs.
1. **Linked List:** Instead of overwriting the existing element at the collided index, chaining uses a **linked list**. This linked list is attached to the bucket in the hash table array.
1. **Storing the Colliding Element:** The colliding element is then added as a new node to the linked list attached to the collided bucket.
1. **Searching and Accessing:** When searching for a specific key, the hash function is used again to generate the index. Then, the linked list at that index is traversed to find the node containing the key-value pair you're looking for. The process compares keys until the desired one is found.

**Benefits of Chaining:**

- **Efficient for Handling Collisions:** Chaining allows efficient handling of collisions, especially when the number of collisions is relatively low. Each bucket can hold multiple elements, preventing the need to re-hash and find a new location for the colliding element, which can be a costly operation.
- **Flexible:** Chaining can dynamically adapt to varying numbers of collisions. As the data grows and more collisions occur, the linked lists attached to buckets simply grow longer.

**Drawbacks of Chaining:**

- **Space Overhead:** Chaining uses additional memory to store the linked lists, which can be a slight overhead compared to other techniques like separate chaining (using a separate array for each bucket).
- **Potential for Longer Lookup Times:** In the worst case scenario, if too many elements collide and form very long linked lists, searching for a specific key can become slower as the entire list needs to be traversed.

**Overall, chaining is a common and effective collision resolution technique used in hash tables. It provides a flexible and efficient way to handle collisions while keeping lookup times relatively fast in most cases.**



```
+--------------------+
| Hash Table Array   |
+--------------------+
| [0] -> Node1(K1, V1) | --> Linked List 1
|                    | --> Node2(K2, V2)
+--------------------+
| [1] -> None        |
+--------------------+
| [2] -> Node3(K3, V3) | --> Linked List 2
|                    | --> Node4(K4, V4)
+--------------------+
| [3] -> Node5(K5, V5) |
+--------------------+
| [4] -> None        |
+--------------------+
| [5] -> Node6(K6, V6) | --> Linked List 3
|                    | --> Node7(K7, V7)
+--------------------+
| [6] -> None        |
+--------------------+
| [7] -> Node8(K8, V8) |
+--------------------+
| [8] -> None        |
+--------------------+
| [9] -> None        |
+--------------------+

K: Key      V: Value
```

This diagram represents a hash table with 10 buckets (index 0 to 9) and uses chaining for collision resolution. Here's a breakdown of the elements:

- **Hash Table Array:** This is the main array that stores the hash table entries. Each element in the array, called a bucket, can potentially hold a linked list of key-value pairs.
- **Linked Lists:** Each bucket that experiences a collision has an attached linked list. This list stores the key-value pairs that collided at that index.
- **Nodes:** Each node in the linked list represents a key-value pair (K1, V1) in the hash table.
- **Empty Buckets:** Buckets without collisions have a value of `None` to indicate they are empty.

For example:

- Key K1 and Key K2 collided and are stored in a linked list attached to bucket 0.
- Key K3 and Key K4 collided and are stored in a linked list attached to bucket 2.
- Keys K5, K6, K7, and K8 do not have collisions and are stored directly in their respective buckets (3, 5, and 7).

This is a simplified example, and in practice, hash tables may use different data structures for linked lists and have more complex logic for handling collisions and ensuring efficient retrieval of key-value pairs.