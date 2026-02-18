# Hash Table - Open Addressing

**Open addressing**, also known as **closed hashing**, is a method of collision resolution in hash tables. Unlike chaining, which stores elements in separate linked lists, open addressing stores all elements directly in the hash table itself. Here’s how it works:

1. **Collision Resolution**: When a hash collision occurs (i.e., two keys hash to the same index), open addressing aims to find an alternative location within the array to place the new key. It does this by probing or searching through different array slots until it either finds the target record or an unused slot.
1. **Probe Sequences**: Various probe sequences are used to find the next available slot:
   - **Linear Probing**: The interval between probes is fixed (often set to 1). If the initial slot is occupied, it checks the next slot, then the next, and so on.
   - **Quadratic Probing**: The interval between probes increases quadratically (indices described by a quadratic function).
   - **Double Hashing**: The interval between probes is fixed for each record but computed using another hash function.
1. **Trade-offs**:
   - **Linear probing** has good cache performance but is sensitive to clustering (when consecutive slots are filled).
   - **Double hashing** exhibits virtually no clustering but has poor cache performance.
   - **Quadratic probing** falls in-between in both areas.
1. **Load Factor**: The proportion of used slots in the array (load factor) significantly affects performance. As the load factor approaches 100%, the number of probes required rises dramatically. Load factors are typically limited to 80% to prevent performance degradation.

---



## Linear Probing

Linear probing is a collision resolution technique used in open addressing for hash tables. It's a simple approach that aims to find an empty slot in the hash table when a collision occurs due to two different keys mapping to the same index. Here's how it works:

**Scenario:**

Imagine you have a hash table with a size of 10 and a hash function that calculates the index for each key. You try to insert two keys: "apple" and "banana" with calculated indices of 5 and 5, respectively. Since both keys map to the same index, a collision occurs.

**Steps involved in linear probing:**

1. **Initial placement:** When a collision happens after calculating the index using the hash function (5 in this case), linear probing starts at the calculated index (position 5).
1. **Check for availability:** If the slot at the calculated index is already occupied (by "apple"), linear probing moves to the **next slot** in the table (position 6).
1. **Repeat check:** It keeps checking for an empty slot by moving linearly to the **next available slot** in the table until it finds one.
1. **Insertion:** Once an empty slot is found (position 6), the new key-value pair ("banana") is inserted there.

**Formula for next index:**

The formula for finding the next index during linear probing is:

```
next_index = (current_index + 1) % table_size
```

- `current_index` is the current index where a collision occurred.
- `table_size` is the total size of the hash table.

**Example:**

In the earlier scenario, after finding the initial index (5) occupied, linear probing would move to the next index (6) using the formula:

```
next_index = (5 + 1) % 10 = 6
```

As position 6 is empty, "banana" would be inserted at that index.

**Advantages:**

- **Simple to implement:** Linear probing is straightforward to understand and implement compared to other probing techniques.
- **Cache-friendly:** It can be faster for accessing elements due to better cache locality, as elements tend to be stored close to each other in the table.

**Disadvantages:**

- **Clustering:** As the load factor (number of elements compared to table size) increases, elements can bunch up in specific areas of the table, leading to longer probing sequences and slower performance.
- **Primary clustering:** In the worst case, all elements can become clustered in one section, resulting in very long probing sequences and degrading performance significantly.

**Overall, linear probing is a viable option for hash tables with low load factors. As the load factor increases, it's recommended to consider other probing techniques like double hashing or quadratic probing to minimize clustering and maintain good performance.**

---



## Double Hashing

Double hashing is a collision resolution technique used within the context of open addressing for hash tables.  It aims to minimize the clustering effect that can occur with linear or quadratic probing techniques. Here's how it works:

1. **Two hash functions:** In double hashing, we use two separate hash functions, let's call them h1(key) and h2(key).

1. **Initial placement:** When we want to insert a new key-value pair into the hash table, we first calculate the initial index using the first hash function h1(key).

1. **Collision:** If the calculated index is already occupied, we don't simply move to the next slot (linear probing) or in a quadratic pattern (quadratic probing). Instead...

1. **Step size calculation:** We calculate a step size by applying the second hash function h2(key). The most important requirement is that h2(key) should never result in a value of zero.

1. Probing sequence:

    

   The probing sequence then proceeds as follows:

   - If the initial index is occupied, we add the step size to it.
   - If the resulting index is still occupied, we add the step size to that index, and so on until we find an empty slot.

**Formula**

The formula for finding the next index during a probing sequence in double hashing is:

```
index = (index + i * h2(key)) % table_size
```

where:

- `index` is the current index.
- `i` is the iteration number (0 for the initial try, 1 for the second try, etc.)
- `h2(key)` is the second hash function, which calculates the step size.
- `table_size` is the size of the hash table.

**Advantages**

- **Less clustering:** Double hashing is highly effective in reducing clustering effects compared to linear and quadratic probing, leading to more uniform distribution of elements in the hash table.
- **Better performance:** This decreased clustering results in better overall hash table performance, as the chances of lengthy probing sequences are reduced.

---

## Quadratic  Probing



Quadratic probing/hashing is another collision resolution technique used in open addressing for hash tables.  It aims to reduce clustering compared to linear probing by using a quadratic formula to disperse elements and probe for empty slots. Here's how it works:

**Scenario**

Imagine you have a hash table, a hash function, and keys like in the linear probing example ("apple" and "banana" mapping to index 5). Quadratic hashing still encounters the collision, but how it finds empty positions is different.

**Steps involved in quadratic probing:**

1. **Initial placement:** The first step is the same as linear probing. Quadratic probing also starts at the calculated index based on the hash function (position 5).

1. **Check for availability:** If the desired position is occupied (by "apple"), quadratic probing examines the next slots based on the quadratic pattern.

1. Quadratic steps:

    

   Instead of a linear step size of 1, it calculates probes in the following quadratic sequence:

   - 1st probe: `(initial_index + 1^2) % table_size`
   - 2nd probe: `(initial_index + 2^2) % table_size`
   - 3rd probe: `(initial_index + 3^2) % table_size`
   - And so on...

**Example:**

1. **Initial Collision:** Suppose the hash value for "banana" is 5 and that slot is occupied.
1. **1st Probe:** The first probe would be: `(5 + 1^2) % table_size = 6 % table_size = 6`.
1. **Checking:** If position 6 is also occupied, the next probe would be: `(5 + 2^2) % table_size = 9 % table_size = 9`.
1. **Continuing:** This pattern continues with probes calculated as (5 + 3^2) % table_size, (5 + 4^2) % table_size, and so on until an available slot is found.

**Benefits of Quadratic Probing**

- **Reducing primary clustering:** Quadratic probing spreads out the probes more effectively than linear probing, reducing the tendency for elements to cluster very tightly in one area of the table. This can help mitigate performance degradation compared to linear probing in cases of moderate to high load factors.

**Drawbacks of Quadratic Probing:**

- **Secondary clustering:** While it may reduce primary clustering, quadratic probing can still lead to some clustering issues known as secondary clustering.
- **Not always guaranteed empty slot:** Quadratic probing doesn't guarantee that you'll always find an empty slot, even if they exist in the table. This depends on the size of the hash table and the hash functions used.

**Conclusion:**

Quadratic probing often provides better performance than linear probing, particularly with higher load factors, by decreasing primary clustering effects. Nonetheless, it's important to be aware of its limitations regarding secondary clustering and the potential for not always finding available slots. 