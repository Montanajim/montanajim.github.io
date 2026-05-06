# Chapter: Hash Maps, Open Addressing, and Chaining

## Introduction

Hash maps are one of the workhorses of computer science. They power symbol tables, caches, dictionaries, indexing structures, and lookup systems across almost every area of software. When they behave well, they are astonishingly fast. A key goes in, a value comes out, and the whole operation feels almost immediate.

That speed, however, is not free. A hash map works because it converts a key into a numeric form, uses that number to compute an array position, and then deals intelligently with the awkward fact that different keys may land in the same location. That last detail matters. Collisions are not a sign that something has gone wrong. They are an ordinary part of hashing. The real question is how the structure resolves them.

This chapter explains the foundations of hash maps and collision handling, with special attention to **chaining**, **linear probing**, **quadratic probing**, and **double hashing**. It also explains how indices are computed safely in Java, why deletion in open addressing is trickier than students first expect, and how design choices affect runtime and memory behavior. You will also study a complete Java demonstration program that includes all of the major topics discussed in this chapter.

------

## Chapter at a Glance

This chapter introduces the structure and purpose of hash maps, explains how hash functions map keys to array positions, and examines why collisions are unavoidable. It then studies the two major families of collision handling: **chaining** and **open addressing**. Within open addressing, it explores three probing strategies in detail: **linear probing**, **quadratic probing**, and **double hashing**. The chapter compares their behavior, tradeoffs, and typical use cases, and concludes with a complete Java program that demonstrates all of them in one place.

------

## Learning Goals

By the end of this chapter, you should be able to:

Explain what a hash map is and why it is useful.

Describe how a hash function helps compute a table position.

Explain why collisions occur and why they must be handled deliberately.

Distinguish between **chaining** and **open addressing**.

Explain in detail how **linear probing**, **quadratic probing**, and **double hashing** work.

Describe when each probing strategy is appropriate.

Explain why deletion in open addressing usually requires tombstones.

Interpret and explain the Java expression

```java
int index = (hash & 0x7fffffff) % table.length;
```

Trace insertion, search, and deletion behavior in hash-based structures.

Evaluate the performance tradeoffs among different collision strategies.

------

## Foundations

A **map** is an abstract data type that stores associations between keys and values. If you know the key, you can retrieve the value. A student ID may map to a student record. A course code may map to a course title. A username may map to an account object.

A **hash map** is a map implementation that uses a **hash function** to convert a key into an integer, then uses that integer to determine where the key-value pair should be stored in an array-like structure called a **hash table**.

The overall idea is straightforward:

Take a key.

Compute a hash code from that key.

Convert the hash code into a legal array index.

Store or search for the entry at that index.

The hope is that this process gives very fast access, often close to constant time on average.

A hash map is therefore an example of a data structure that uses computation to reduce search cost. Instead of scanning through all elements, it uses the key to jump to a likely location immediately.

------

## Why This Topic Matters

Hashing sits at the center of practical computing. If you write compilers, you use symbol tables. If you write web applications, you use caches and session maps. If you write search systems, databases, language runtimes, or operating systems, you will meet hash-based lookup again and again.

More importantly, hash maps are one of the first data structures that force students to face an uncomfortable but valuable truth: fast average performance depends on design assumptions. A hash map is not “always O(1).” That slogan is a half-truth repeated with the confidence of a bad witness. Hash maps are often extremely efficient, but only if the hash function distributes keys well, the collision policy is sensible, and the structure is resized before the table becomes overcrowded.

This topic matters because it teaches not only a useful data structure, but also a more mature habit of thought: performance claims depend on conditions.

------

## Core Concepts

### Keys and Values

A hash map stores pairs:

- key
- value

For example:

- `"CS101"` → `"Introduction to Programming"`
- `"apple"` → `17`
- `42` → `"student record"`

Each key identifies one associated value.

### Hash Code

A key is transformed into an integer called a **hash code**. In Java, this often comes from the `hashCode()` method.

```java
String s = "CS101";
int hash = s.hashCode();
```

The raw hash code is not automatically a valid array index. It may be negative, and it may be much larger than the table size. That means it must be converted.

### Index Computation

A common pattern in Java hash-table implementations is:

```java
int index = (hash & 0x7fffffff) % table.length;
```

This expression deserves careful attention because students often use it without understanding it.

Let us break it apart in detail.

Suppose `hash` is an `int`. In Java, an `int` is a 32-bit signed integer. That means the leftmost bit is the **sign bit**. If that bit is `1`, the number is negative.

The constant `0x7fffffff` is a hexadecimal number. In binary, it looks like this:

```text
01111111111111111111111111111111
```

Notice what that means:

The first bit is `0`.

The remaining 31 bits are `1`.

Now consider the bitwise AND operation:

```java
hash & 0x7fffffff
```

This clears the sign bit of `hash` and keeps the remaining 31 bits. The result is guaranteed to be nonnegative.

Then:

```java
(hash & 0x7fffffff) % table.length
```

takes that nonnegative number and reduces it into the range:

```text
0 to table.length - 1
```

So the full expression means:

Take the hash code.

Force it to be nonnegative by clearing its sign bit.

Reduce it modulo the table size so it becomes a valid array index.

### Why not just use `Math.abs(hash)`?

Because `Math.abs()` has a famous edge case:

```java
Math.abs(Integer.MIN_VALUE)
```

still returns a negative number. That happens because the negative range of two’s complement integers is slightly larger than the positive range. In other words, one value does not have a positive counterpart representable as an `int`.

That means this can fail:

```java
int index = Math.abs(hash) % table.length;
```

if `hash` is `Integer.MIN_VALUE`.

The bit-mask approach avoids that particular problem.

### Key Point

The expression

```java
int index = (hash & 0x7fffffff) % table.length;
```

is a practical way to convert a possibly negative Java hash code into a safe, nonnegative array index.

### Debugging Note

If your indexing logic sometimes produces a negative index, do not blame the compiler, the phase of the moon, or Java in general. Check your hash-to-index computation first.

------

## Terminology

A **hash function** transforms a key into an integer hash code.

A **hash table** is the array-like structure that stores entries.

A **bucket** is one location in that table.

A **collision** occurs when two different keys map to the same bucket.

A **load factor** measures how full the table is.

A **probe** is an attempt to examine a slot during open addressing.

A **probe sequence** is the order of slots examined during probing.

A **tombstone** is a deletion marker used in open addressing.

A **rehash** moves entries into a new table, usually after resizing.

------

## Hash Map Architecture

At a conceptual level, a hash map needs four things:

A way to represent entries.

A hash-to-index computation.

A collision-resolution strategy.

A resizing policy.

A simple entry representation in Java might be:

```java
static class Entry<K, V> {
    K key;
    V value;
    boolean deleted;

    Entry(K key, V value) {
        this.key = key;
        this.value = value;
        this.deleted = false;
    }
}
```

For chaining, the `deleted` flag is not usually needed. For open addressing, it is useful because deletion is more delicate.

------

# Chaining

## How Chaining Works

In **chaining**, each table position stores a collection of entries rather than only one entry. If multiple keys hash to the same index, all of them are stored in that bucket’s chain.

That chain is often implemented as a linked list in introductory treatments, though dynamic arrays or balanced trees may also be used in more advanced implementations.

If a collision occurs, chaining does not search for a different array position. It simply adds the new entry to the collection stored at that bucket.

### Example Idea

If keys `10`, `15`, and `20` all map to bucket `2`, then bucket `2` might hold a linked list containing:

```text
[10] -> [15] -> [20]
```

The array position remains the same. The chain grows.

## Why Chaining Is Attractive

Chaining is conceptually straightforward. Collisions are stored together. Deletion is simpler than in open addressing. The table can even handle a load factor greater than 1.0, because one bucket can store multiple entries.

## Chaining Runtime

Average-case behavior is often:

Insert: O(1)

Search: O(1)

Delete: O(1)

Worst-case behavior is O(n) if many keys pile into the same bucket.

### Performance Note

Chaining is often more forgiving than open addressing when the load factor rises. That does not mean overcrowding is fine. It means the collapse is usually less dramatic.

------

# Open Addressing

## How Open Addressing Works

In **open addressing**, every entry is stored directly in the table array itself. If a collision occurs, the algorithm probes other locations until it finds a suitable slot.

This means there are no external lists. Everything stays in the table.

That sounds elegant, and it is. It is also more fragile.

Search and insertion must follow the same probing rules. Deletion must preserve the integrity of those probe sequences. If you break the sequence, later searches can fail even when the desired key is still in the table.

The three probing strategies covered here are:

Linear probing

Quadratic probing

Double hashing

------

## Linear Probing

### What Linear Probing Is

**Linear probing** resolves a collision by checking the next slot, then the next, then the next, wrapping around the table if necessary.

If the original hash index is `h(k)`, then the probe sequence is:

```text
h(k), h(k)+1, h(k)+2, h(k)+3, ...
```

taken modulo the table size.

Mathematically:


$$
\text{index}_i = (h(k) + i) \bmod m
$$




where:

- `h(k)` is the starting index
- `i` is the probe number
- `m` is the table length

### Step-by-Step Example of Linear Probing

Suppose the table size is `7`, and keys `10`, `17`, and `24` all hash initially to index `3`.

Insert `10`:

- slot 3 is empty
- place `10` at slot 3

Insert `17`:

- slot 3 is occupied
- try slot 4
- slot 4 is empty
- place `17` at slot 4

Insert `24`:

- slot 3 occupied
- slot 4 occupied
- try slot 5
- place `24` at slot 5

So the cluster becomes:

```text
3: 10
4: 17
5: 24
```

### Strengths of Linear Probing

It is simple.

It is easy to implement.

It often has good cache performance because nearby locations are examined in sequence.

### Weaknesses of Linear Probing

Its major weakness is **primary clustering**. Once a block of occupied cells forms, new collisions tend to enlarge that block. Clusters become magnets for more collisions. As the load factor rises, probe lengths can increase sharply.

### When Should One Use Linear Probing?

Use linear probing when:

You want the simplest open-addressing implementation.

You want a compact table with good cache locality.

You expect the load factor to be kept relatively low.

You want a teaching implementation or a performance-oriented design where simplicity matters.

Do not choose linear probing casually if the table will become crowded. It performs well when managed properly and degrades badly when neglected.

------

## Quadratic Probing

### What Quadratic Probing Is

**Quadratic probing** resolves collisions by increasing the probe distance quadratically rather than linearly.

Instead of checking:

```text
h, h+1, h+2, h+3, ...
```

it checks something like:

```text
h, h+1^2, h+2^2, h+3^2, ...
```

modulo the table size.

A common form is:


$$
\text{index}_i = (h(k) + i^2) \bmod m
$$


Other variants use constants such as:


$$
\text{index}_i = (h(k) + c_1 i + c_2 i^2) \bmod m
$$


but the simpler square-based version is enough for learning the idea.

### Step-by-Step Example of Quadratic Probing

Suppose the table size is `11`, and a key hashes to index `5`.

If slot `5` is occupied, quadratic probing tries:

- `5 + 1^2 = 6`
- `5 + 2^2 = 9`
- `5 + 3^2 = 14 mod 11 = 3`
- `5 + 4^2 = 21 mod 11 = 10`

So the probe sequence is:

```text
5, 6, 9, 3, 10, ...
```

Notice that the probes spread out more than linear probing. That reduces contiguous clustering.

### Strengths of Quadratic Probing

It reduces primary clustering compared with linear probing.

It still remains fairly easy to implement.

It spreads collisions out more broadly.

### Weaknesses of Quadratic Probing

It can still suffer from **secondary clustering**, meaning keys that start at the same initial hash index follow the same probe pattern.

Also, depending on the table size and probing formula, the sequence may fail to visit every slot. That means insertion can fail to find an open slot even though one exists, unless the table size and formula are chosen carefully.

### Chapter Warning

Quadratic probing is not “linear probing but smarter” in some vague universal sense. It helps with clustering, but it introduces mathematical constraints. If the table size and formula are chosen badly, the probe sequence may not cover the whole table.

### When Should One Use Quadratic Probing?

Use quadratic probing when:

You want to reduce clustering compared with linear probing.

You still want an open-addressing method that is simpler than double hashing.

You can control the table size and probing design carefully.

Quadratic probing is often a reasonable middle ground: less clustering than linear probing, less conceptual overhead than double hashing.

------

## Double Hashing

### What Double Hashing Is

**Double hashing** is an open-addressing collision-resolution strategy that uses a second hash function to determine the step size between probes.

Instead of moving by `+1` each time, or by quadratic offsets, the algorithm computes a second value and uses that as the jump distance.

A common form is:


$$
\text{index}_i = (h_1(k) + i \cdot h_2(k)) \bmod m
$$


where:

- `h1(k)` is the primary hash and gives the starting position
- `h2(k)` is the secondary hash and gives the step size
- `i` is the probe number
- `m` is the table size

This means each key may follow its own probe path through the table rather than sharing the same fixed pattern used by linear or quadratic probing.

That is the central strength of double hashing. It reduces the tendency of colliding keys to travel together in the same sequence.

### Why Double Hashing Matters

The big weakness of linear probing is **primary clustering**. Once a run of occupied slots appears, new collisions tend to extend it.

Quadratic probing reduces that problem, but keys with the same starting index can still follow the same general probe pattern. That is **secondary clustering**.

Double hashing addresses both issues more effectively by making the probe increment depend on the key itself. Two keys that start at the same initial bucket may still move through the table differently if their second-hash values differ.

That usually produces better probe distribution, shorter average probe sequences, and more stable performance as collisions increase.

### Key Point

Double hashing works well not because it “uses two hashes” in some vague symbolic sense, but because the second hash gives each key a more individualized probe step.

### Step-by-Step Example of Double Hashing

Suppose:

```text
m = 11
h1(k) = k % 11
h2(k) = 7 - (k % 7)
```

Now consider key `22`.

Primary hash:

```text
h1(22) = 22 % 11 = 0
```

Secondary hash:

```text
h2(22) = 7 - (22 % 7)
       = 7 - 1
       = 6
```

So the probe sequence is:

- `(0 + 0*6) % 11 = 0`
- `(0 + 1*6) % 11 = 6`
- `(0 + 2*6) % 11 = 1`
- `(0 + 3*6) % 11 = 7`
- `(0 + 4*6) % 11 = 2`
- `(0 + 5*6) % 11 = 8`

and so on.

This sequence jumps around the table rather than walking in a fixed pattern. That is exactly what makes double hashing effective.

Now compare that with another key, say `33`.

Primary hash:

```text
h1(33) = 33 % 11 = 0
```

Secondary hash:

```text
h2(33) = 7 - (33 % 7)
       = 7 - 5
       = 2
```

Its probe sequence becomes:

- `(0 + 0*2) % 11 = 0`
- `(0 + 1*2) % 11 = 2`
- `(0 + 2*2) % 11 = 4`
- `(0 + 3*2) % 11 = 6`
- `(0 + 4*2) % 11 = 8`

So even though `22` and `33` begin at the same primary index, they move through the table differently. That is the point.

### The Real Design Question: How Should the Second Hash Be Chosen?

This is the part many short explanations skip, and they should not.

The second hash function must be chosen carefully. A bad second hash can sabotage the entire design.

A good secondary hash should satisfy three conditions:

It should never return `0`.

It should produce step sizes that allow the probe sequence to cover the table effectively.

It should vary across keys so different keys are likely to follow different probe paths.

If the second hash returns zero, the probe formula becomes:

[
(h_1(k) + i \cdot 0) \bmod m
]

which means the algorithm never moves beyond the original slot. That is not probing. That is being stuck with mathematical paperwork.

### Chapter Warning

In double hashing, a zero-valued second hash is a design failure. The probe sequence will never advance.

## Common Secondary Hash Functions

### 1. `1 + (hash % (m - 1))`

One of the most common textbook choices is:

```java
int step = 1 + ((hash & 0x7fffffff) % (table.length - 1));
```

This is a strong general-purpose teaching example.

Why it works:

- `hash % (table.length - 1)` produces a value from `0` to `table.length - 2`
- adding `1` shifts the range to `1` through `table.length - 1`
- therefore the step size is never zero

This choice works especially well when the table length is **prime**. If `m` is prime, then every value from `1` through `m - 1` is relatively prime to `m`, which helps the probe sequence visit the entire table.

This is the cleanest secondary hash to teach first.

### 2. `R - (hash % R)`

Another classic form is:

```java
int R = 7; // prime smaller than table length
int step = R - ((hash & 0x7fffffff) % R);
```

Here, `R` is usually chosen as a prime number smaller than the table size.

Why it works:

- the result is nonzero
- it often gives a good spread of step sizes
- it is a traditional and widely taught form

Example:

If `R = 7` and `hash % 7 = 3`, then:

```java
step = 7 - 3; // step = 4
```

This form is simple, memorable, and common in algorithm texts.

### 3. Odd-valued step for power-of-two table sizes

If the table size is a power of two, a common strategy is to force the step size to be odd.

For example:

```java
int step = ((hash & 0x7fffffff) % (table.length - 1)) | 1;
```

or more explicitly:

```java
int step = 1 + 2 * ((hash & 0x7fffffff) % ((table.length - 1) / 2));
```

Why this works:

If the table size is a power of two, then any odd step is relatively prime to that table size. That helps the probe sequence cover the table rather than cycling through a smaller subset of positions.

This is especially useful in implementations that deliberately use power-of-two capacities for performance reasons.

### 4. Simple classroom examples for integer keys

For classroom tracing, you may also see examples like:

```java
int step = 7 - (key % 7);
```

These are fine for hand computation and lecture demonstrations. They are easy to trace on a whiteboard.

But for a more general implementation, it is better to compute the step from the key’s hash code rather than the raw integer key value. That makes the design work more cleanly for arbitrary object keys.

## Choosing a Good Secondary Hash in Practice

The best advice is:

If the table size is prime, use a prime-friendly form such as:

```java
1 + (hash % (m - 1))
```

or:

```java
R - (hash % R)
```

where `R` is a smaller prime.

If the table size is a power of two, force the step size to be odd.



### Performance Note

Double hashing is often one of the strongest standard open-addressing strategies because it reduces both primary and secondary clustering more effectively than linear or quadratic probing.

### Strengths of Double Hashing

It greatly reduces clustering.

Keys with the same initial hash can still follow different probe sequences.

It often gives better probe distribution than linear probing.

It often gives better probe distribution than quadratic probing.

It usually performs well when the table is moderately full, provided the secondary hash and table size are chosen intelligently.

### Weaknesses of Double Hashing

It is more complicated to implement.

The second hash function must be chosen carefully.

The table size and step size must be compatible enough to let the probe sequence cover the table well.

It is harder to explain quickly than linear probing, which is probably why people explain it quickly and badly.

### When Should One Use Double Hashing?

Use double hashing when:

You want better probe distribution than linear or quadratic probing.

You want to reduce both primary and secondary clustering.

You are willing to accept a more careful implementation.

You want open addressing, but you do not want all colliding keys marching in lockstep through the table.

Double hashing is often the best open-addressing choice when collision quality matters enough to justify the extra complexity.

------

## Comparing Linear, Quadratic, and Double Hashing

### Comparison Box

**Linear probing**

- simplest implementation
- very cache-friendly
- suffers from primary clustering
- good when load factor stays low and simplicity matters

**Quadratic probing**

- reduces primary clustering
- still simpler than double hashing
- can suffer from secondary clustering
- requires careful table-size design

**Double hashing**

- usually best probe distribution of the three
- reduces both primary and secondary clustering effectively
- depends on a well-designed second hash function
- more complex to implement
- strong choice when collision behavior and probe quality matter

------

## Deletion in Open Addressing

Deletion in open addressing is more complicated than in chaining.

Suppose several keys collide and are placed later in the probe sequence. If you remove one entry by setting its slot to `null`, a later search may stop too early, incorrectly concluding that the desired key is not present.

For that reason, open addressing usually uses a **tombstone** marker. A tombstone means:

“There used to be something here. Keep probing.”

### Example

Suppose linear probing placed these entries:

```text
index 3 -> A
index 4 -> B
index 5 -> C
```

If `A` is deleted and slot `3` becomes `null`, then a search for `C` starting at `3` may incorrectly stop immediately.

If slot `3` becomes a tombstone instead, probing continues and `C` can still be found.

### Common Mistake

Students often write open-address deletion by assigning `null` to the slot and then wonder why later searches mysteriously fail. This is not mysterious. This is a broken probe chain.

------

## Behind-the-Scenes Behavior

Hash maps are shaped by more than their visible interface.

A good implementation depends on:

a usable hash function

a safe index computation

a table size policy

a collision-resolution strategy

a resizing threshold

a deletion policy

In Java, custom key classes must also obey the relationship between `equals()` and `hashCode()`. If two objects are considered equal by `equals()`, they must produce compatible hash behavior. If they do not, a hash-based structure can fail to retrieve a key that is already in the table.

That is not a minor technicality. It is structural.

------

## Best Practices

Use a good hash function.

Keep the load factor under control.

Resize before performance collapses.

Use chaining if you want simpler deletion behavior and tolerance for fuller tables.

Use linear probing when simplicity and locality matter.

Use quadratic probing when you want to reduce clustering but keep the design moderately simple.

Use double hashing when you want better probe distribution and can manage the extra design complexity.

For Java keys, implement `equals()` and `hashCode()` correctly.

Do not treat hash maps as magical boxes. They are engineered compromises, and every compromise has consequences.

------

## Sample Program Covering All Topics

The following Java program demonstrates:

chaining

linear probing

quadratic probing

double hashing

safe index computation using

```java
(hash & 0x7fffffff) % table.length
```

tombstone-based deletion in open addressing

This is an educational demonstration, not a production replacement for `java.util.HashMap`.

```java
import java.util.LinkedList;
import java.util.Iterator;

public class HashingChapterDemo {

    // ---------------- Entry ----------------
    static class Entry<K, V> {
        K key;
        V value;
        boolean deleted;

        Entry(K key, V value) {
            this.key = key;
            this.value = value;
            this.deleted = false;
        }

        @Override
        public String toString() {
            return deleted ? "[DELETED]" : key + "=" + value;
        }
    }

    // ---------------- Base utility ----------------
    static abstract class BaseHashTable<K, V> {
        protected Entry<K, V>[] table;
        protected int size;

        @SuppressWarnings("unchecked")
        public BaseHashTable(int capacity) {
            table = new Entry[capacity];
            size = 0;
        }

        protected int primaryIndex(K key) {
            int hash = key.hashCode();
            return (hash & 0x7fffffff) % table.length;
        }

        public void printTable(String title) {
            System.out.println(title);
            for (int i = 0; i < table.length; i++) {
                System.out.println(i + ": " + (table[i] == null ? "empty" : table[i]));
            }
            System.out.println();
        }
    }

    // ---------------- Chaining ----------------
    static class ChainedHashMap<K, V> {
        private LinkedList<Entry<K, V>>[] table;
        private int size;

        @SuppressWarnings("unchecked")
        public ChainedHashMap(int capacity) {
            table = new LinkedList[capacity];
            size = 0;
        }

        private int indexFor(K key) {
            int hash = key.hashCode();
            return (hash & 0x7fffffff) % table.length;
        }

        public void put(K key, V value) {
            int index = indexFor(key);

            if (table[index] == null) {
                table[index] = new LinkedList<>();
            }

            for (Entry<K, V> e : table[index]) {
                if (e.key.equals(key)) {
                    e.value = value;
                    return;
                }
            }

            table[index].add(new Entry<>(key, value));
            size++;
        }

        public V get(K key) {
            int index = indexFor(key);

            if (table[index] == null) {
                return null;
            }

            for (Entry<K, V> e : table[index]) {
                if (e.key.equals(key)) {
                    return e.value;
                }
            }
            return null;
        }

        public boolean remove(K key) {
            int index = indexFor(key);

            if (table[index] == null) {
                return false;
            }

            Iterator<Entry<K, V>> it = table[index].iterator();
            while (it.hasNext()) {
                Entry<K, V> e = it.next();
                if (e.key.equals(key)) {
                    it.remove();
                    size--;
                    return true;
                }
            }
            return false;
        }

        public void printTable(String title) {
            System.out.println(title);
            for (int i = 0; i < table.length; i++) {
                System.out.print(i + ": ");
                if (table[i] == null || table[i].isEmpty()) {
                    System.out.println("empty");
                } else {
                    System.out.println(table[i]);
                }
            }
            System.out.println();
        }
    }

    // ---------------- Linear Probing ----------------
    static class LinearProbingMap<K, V> extends BaseHashTable<K, V> {

        public LinearProbingMap(int capacity) {
            super(capacity);
        }

        public void put(K key, V value) {
            int index = primaryIndex(key);
            int firstDeleted = -1;

            while (table[index] != null) {
                if (table[index].deleted) {
                    if (firstDeleted == -1) {
                        firstDeleted = index;
                    }
                } else if (table[index].key.equals(key)) {
                    table[index].value = value;
                    return;
                }

                index = (index + 1) % table.length;
            }

            if (firstDeleted != -1) {
                table[firstDeleted] = new Entry<>(key, value);
            } else {
                table[index] = new Entry<>(key, value);
            }
            size++;
        }

        public V get(K key) {
            int index = primaryIndex(key);
            int start = index;

            while (table[index] != null) {
                if (!table[index].deleted && table[index].key.equals(key)) {
                    return table[index].value;
                }
                index = (index + 1) % table.length;
                if (index == start) break;
            }
            return null;
        }

        public boolean remove(K key) {
            int index = primaryIndex(key);
            int start = index;

            while (table[index] != null) {
                if (!table[index].deleted && table[index].key.equals(key)) {
                    table[index].deleted = true;
                    size--;
                    return true;
                }
                index = (index + 1) % table.length;
                if (index == start) break;
            }
            return false;
        }
    }

    // ---------------- Quadratic Probing ----------------
    static class QuadraticProbingMap<K, V> extends BaseHashTable<K, V> {

        public QuadraticProbingMap(int capacity) {
            super(capacity);
        }

        public void put(K key, V value) {
            int base = primaryIndex(key);
            int firstDeleted = -1;

            for (int i = 0; i < table.length; i++) {
                int index = (base + i * i) % table.length;

                if (table[index] == null) {
                    if (firstDeleted != -1) {
                        table[firstDeleted] = new Entry<>(key, value);
                    } else {
                        table[index] = new Entry<>(key, value);
                    }
                    size++;
                    return;
                }

                if (table[index].deleted) {
                    if (firstDeleted == -1) {
                        firstDeleted = index;
                    }
                } else if (table[index].key.equals(key)) {
                    table[index].value = value;
                    return;
                }
            }

            System.out.println("Quadratic probing insert failed for key " + key + ". Table may be too full.");
        }

        public V get(K key) {
            int base = primaryIndex(key);

            for (int i = 0; i < table.length; i++) {
                int index = (base + i * i) % table.length;

                if (table[index] == null) {
                    return null;
                }

                if (!table[index].deleted && table[index].key.equals(key)) {
                    return table[index].value;
                }
            }
            return null;
        }

        public boolean remove(K key) {
            int base = primaryIndex(key);

            for (int i = 0; i < table.length; i++) {
                int index = (base + i * i) % table.length;

                if (table[index] == null) {
                    return false;
                }

                if (!table[index].deleted && table[index].key.equals(key)) {
                    table[index].deleted = true;
                    size--;
                    return true;
                }
            }
            return false;
        }
    }

    // ---------------- Double Hashing ----------------
    static class DoubleHashingMap<K, V> extends BaseHashTable<K, V> {

        public DoubleHashingMap(int capacity) {
            super(capacity);
        }

        // Option 1: common choice when table length is prime
        private int stepHashOption1(K key) {
            int hash = key.hashCode() & 0x7fffffff;
            return 1 + (hash % (table.length - 1));
        }

        // Option 2: classic textbook form using a smaller prime R
        private int stepHashOption2(K key) {
            int hash = key.hashCode() & 0x7fffffff;
            int R = 7; // should be prime and smaller than table length
            return R - (hash % R);
        }

        // Option 3: odd-valued step, useful for power-of-two style thinking
        private int stepHashOption3(K key) {
            int hash = key.hashCode() & 0x7fffffff;
            return ((hash % (table.length - 1)) | 1);
        }

        // Pick one strategy for actual use
        private int stepHash(K key) {
            return stepHashOption1(key);
            // return stepHashOption2(key);
            // return stepHashOption3(key);
        }

        public void put(K key, V value) {
            int base = primaryIndex(key);
            int step = stepHash(key);
            int firstDeleted = -1;

            for (int i = 0; i < table.length; i++) {
                int index = (base + i * step) % table.length;

                if (table[index] == null) {
                    if (firstDeleted != -1) {
                        table[firstDeleted] = new Entry<>(key, value);
                    } else {
                        table[index] = new Entry<>(key, value);
                    }
                    size++;
                    return;
                }

                if (table[index].deleted) {
                    if (firstDeleted == -1) {
                        firstDeleted = index;
                    }
                } else if (table[index].key.equals(key)) {
                    table[index].value = value;
                    return;
                }
            }

            System.out.println("Double hashing insert failed for key " + key + ". Table may be too full.");
        }

        public V get(K key) {
            int base = primaryIndex(key);
            int step = stepHash(key);

            for (int i = 0; i < table.length; i++) {
                int index = (base + i * step) % table.length;

                if (table[index] == null) {
                    return null;
                }

                if (!table[index].deleted && table[index].key.equals(key)) {
                    return table[index].value;
                }
            }
            return null;
        }

        public boolean remove(K key) {
            int base = primaryIndex(key);
            int step = stepHash(key);

            for (int i = 0; i < table.length; i++) {
                int index = (base + i * step) % table.length;

                if (table[index] == null) {
                    return false;
                }

                if (!table[index].deleted && table[index].key.equals(key)) {
                    table[index].deleted = true;
                    size--;
                    return true;
                }
            }
            return false;
        }
    }

    // ---------------- Helper to show hash/index computation ----------------
    public static void showIndexComputation(Integer key, int tableLength) {
        int hash = key.hashCode();
        int masked = hash & 0x7fffffff;
        int index = masked % tableLength;

        System.out.println("Key: " + key);
        System.out.println("hashCode(): " + hash);
        System.out.println("hash & 0x7fffffff: " + masked);
        System.out.println("index = (hash & 0x7fffffff) % " + tableLength + " = " + index);
        System.out.println();
    }

    // ---------------- Demo ----------------
    public static void main(String[] args) {

        System.out.println("=== Safe Index Computation Demo ===");
        showIndexComputation(10, 11);
        showIndexComputation(-25, 11);

        System.out.println("=== Chaining Demo ===");
        ChainedHashMap<Integer, String> chained = new ChainedHashMap<>(5);
        chained.put(10, "Ten");
        chained.put(15, "Fifteen");
        chained.put(20, "Twenty");
        chained.printTable("Chaining table after inserts:");
        System.out.println("Get 15: " + chained.get(15));
        chained.remove(15);
        chained.printTable("Chaining table after removing 15:");

        System.out.println("=== Linear Probing Demo ===");
        LinearProbingMap<Integer, String> linear = new LinearProbingMap<>(7);
        linear.put(10, "Ten");
        linear.put(17, "Seventeen");
        linear.put(24, "Twenty-Four");
        linear.printTable("Linear probing after inserts:");
        System.out.println("Get 24: " + linear.get(24));
        linear.remove(17);
        linear.printTable("Linear probing after removing 17:");
        linear.put(31, "Thirty-One");
        linear.printTable("Linear probing after inserting 31:");

        System.out.println("=== Quadratic Probing Demo ===");
        QuadraticProbingMap<Integer, String> quadratic = new QuadraticProbingMap<>(11);
        quadratic.put(10, "Ten");
        quadratic.put(21, "Twenty-One");
        quadratic.put(32, "Thirty-Two");
        quadratic.put(43, "Forty-Three");
        quadratic.printTable("Quadratic probing after inserts:");
        System.out.println("Get 32: " + quadratic.get(32));
        quadratic.remove(21);
        quadratic.printTable("Quadratic probing after removing 21:");
        quadratic.put(54, "Fifty-Four");
        quadratic.printTable("Quadratic probing after inserting 54:");

        System.out.println("=== Double Hashing Secondary Hash Demo ===");
        int sampleKey = 22;
        int hash = Integer.hashCode(sampleKey) & 0x7fffffff;

        System.out.println("Sample key: " + sampleKey);
        System.out.println("Primary index: " + (hash % 11));
        System.out.println("Option 1 step = 1 + (hash % (m - 1)) = " + (1 + (hash % (11 - 1))));
        System.out.println("Option 2 step = R - (hash % R), R = 7 => " + (7 - (hash % 7)));
        System.out.println("Option 3 odd-valued step = ((hash % (m - 1)) | 1) = " + ((hash % (11 - 1)) | 1));
        System.out.println();

        System.out.println("=== Double Hashing Demo ===");
        DoubleHashingMap<Integer, String> doubleHash = new DoubleHashingMap<>(11);
        doubleHash.put(22, "Twenty-Two");
        doubleHash.put(33, "Thirty-Three");
        doubleHash.put(44, "Forty-Four");
        doubleHash.put(55, "Fifty-Five");
        doubleHash.printTable("Double hashing after inserts:");
        System.out.println("Get 44: " + doubleHash.get(44));
        doubleHash.remove(33);
        doubleHash.printTable("Double hashing after removing 33:");
        doubleHash.put(66, "Sixty-Six");
        doubleHash.printTable("Double hashing after inserting 66:");
    }
}
```

------

## Walkthrough of the Sample Program

The program begins with an `Entry` class used by all implementations. Each entry stores a key, a value, and a `deleted` flag. That flag matters for open addressing because tombstones preserve the probe sequence after deletion.

The `BaseHashTable` class provides a shared table and a shared `primaryIndex()` method. That method uses the expression:

```java
(hash & 0x7fffffff) % table.length
```

to convert a key’s hash code into a safe index.

The `ChainedHashMap` class uses an array of `LinkedList<Entry<K, V>>`. If several keys land in the same bucket, they are stored together in the linked list for that bucket.

The `LinearProbingMap` class places entries directly into the array and resolves collisions by moving one step at a time.

The `QuadraticProbingMap` class uses square offsets such as `i * i` to spread collisions out.

The `DoubleHashingMap` class computes both a primary hash index and a secondary hash step size. Unlike linear probing and quadratic probing, which follow fixed probe patterns, double hashing uses a second hash function so that different keys can follow different probe sequences. The sample code includes several common secondary-hash strategies, including `1 + (hash % (m - 1))`, `R - (hash % R)` for a smaller prime `R`, and an odd-valued step suitable for power-of-two table sizes. This makes the probe pattern more individualized and usually reduces clustering more effectively than the other two open-addressing methods.

The `showIndexComputation()` method prints the internal stages of the safe index formula so students can see the hash code, the masked nonnegative value, and the final modulo reduction.

Finally, the `main()` method demonstrates all of the structures and probing styles in action.

------

## Common Mistakes and Misconceptions

A hash map is not automatically O(1) in all cases. That is average-case behavior under good conditions.

A good hash function does not eliminate collisions. It reduces harmful clustering.

Linear probing is not always the best choice simply because it is easy.

Quadratic probing is not automatically safe under all table sizes and formulas.

Double hashing is not “too advanced to matter.” It is often the most effective probing strategy among the three.

Deletion in open addressing is not ordinary deletion. Probe sequences must be preserved.

Using a raw hash code as an array index is wrong unless it has been converted safely into the valid table range.

### Checkpoint

Can you explain, in your own words, why the bit mask `0x7fffffff` is used before taking modulo table length?

If not, revisit that section. It matters.

------

## Key Terms

hash map

hash table

hash function

hash code

bucket

collision

load factor

chaining

open addressing

linear probing

quadratic probing

double hashing

secondary hash function

probe

probe sequence

tombstone

rehash

primary clustering

secondary clustering

------

## Chapter Summary

A hash map stores key-value pairs by transforming keys into numeric hash codes and then converting those hash codes into table indices. Because different keys can map to the same index, collisions are unavoidable and must be handled carefully.

Two major strategies exist for collision handling. **Chaining** stores multiple entries in the same bucket, usually using a linked structure. It is conceptually simple and handles deletion gracefully. **Open addressing** keeps all entries inside the table itself and uses probing to find alternate positions.

Three important probing strategies are **linear probing**, **quadratic probing**, and **double hashing**. Linear probing is simple and cache-friendly but suffers from primary clustering. Quadratic probing reduces primary clustering but can still suffer from secondary clustering and requires careful design. Double hashing typically provides the best probe distribution of the three strategies because it uses a second hash function to determine the probe step size. Common second-hash choices include `1 + (hash % (m - 1))`, `R - (hash % R)` for a smaller prime `R`, and odd-valued step functions for power-of-two table sizes. It is more complex to implement, but it often reduces clustering more effectively than linear or quadratic probing.

The expression

```java
int index = (hash & 0x7fffffff) % table.length;
```

is a practical way in Java to convert a possibly negative hash code into a safe, nonnegative array index.

The real lesson of hash maps is not merely that they are fast. It is that they are fast when their assumptions are respected.

### Final Takeaway

Hashing is where elegant theory meets rude reality. The array is finite, collisions are inevitable, and performance is conditional. The art is in how you recover from the collision without losing the speed that made hashing attractive in the first place.

------

## Multiple-Choice Review Questions

### 1. What is the purpose of a hash function in a hash map?

A. To sort keys
B. To convert a key into an integer useful for locating a table position
C. To remove collisions
D. To compress values only

### 2. What does the expression below mainly accomplish?

```java
(hash & 0x7fffffff) % table.length
```

A. It sorts the table
B. It forces the hash to be odd
C. It converts a possibly negative hash into a valid nonnegative index
D. It doubles the table length

### 3. In chaining, a collision is handled by:

A. jumping to the next empty slot
B. storing multiple entries in the same bucket structure
C. deleting the older entry
D. using two hash tables at once

### 4. Linear probing resolves collisions by:

A. using linked lists
B. using the next slot, then the next, and so on
C. squaring the hash code
D. reversing the key

### 5. Quadratic probing typically uses which kind of offset pattern?

A. powers of two only
B. consecutive negative offsets
C. square-based offsets such as `i * i`
D. a second table

### 6. Double hashing differs from linear and quadratic probing because it:

A. stores collisions in chains
B. uses a second hash function to determine step size
C. never has collisions
D. avoids modular arithmetic

### 7. Which probing method is most likely to suffer from primary clustering?

A. chaining
B. linear probing
C. double hashing
D. separate trees

### 8. Why are tombstones often needed in open addressing?

A. to increase table size
B. to make hash codes positive
C. to preserve probe sequences after deletion
D. to sort the entries

### 9. When might double hashing be a strong choice?

A. when you want good probe distribution and can accept extra implementation complexity
B. when you need the simplest code possible
C. when collisions never happen
D. when deletion does not matter

### 10. Which statement is most accurate?

A. Hash maps are always O(1)
B. A good hash function prevents all collisions
C. Open addressing and chaining are identical except for syntax
D. Hash-map performance depends on hashing quality, load factor, and collision strategy

------

## Answer Key

1. B
2. C
3. B
4. B
5. C
6. B
7. B
8. C
9. A
10. D

------

## End-of-Chapter Glossary

**Bucket**
A location in the table array. In chaining, one bucket may hold multiple entries.

**Chaining**
A collision-resolution method in which each bucket stores a collection of entries.

**Collision**
The event in which two different keys map to the same hash-table location.

**Double Hashing**
An open-addressing strategy that uses a second hash function to determine the probe step size, allowing different keys to follow different probe sequences.

**Entry**
A key-value pair stored in a hash-based structure.

**Hash Code**
An integer derived from a key and used to compute a table position.

**Hash Function**
A function that transforms a key into an integer hash code.

**Hash Map**
A map implementation based on hashing for fast average-case lookup, insertion, and deletion.

**Hash Table**
The underlying array-based storage structure used in a hash map.

**Linear Probing**
An open-addressing method that checks the next slot, then the next, in sequence.

**Load Factor**
A measure of how full the table is, usually the number of stored entries divided by table size.

**Open Addressing**
A collision-resolution strategy in which all entries remain inside the table array and alternate locations are found through probing.

**Primary Clustering**
A phenomenon in linear probing in which contiguous blocks of occupied cells grow and attract more collisions.

**Probe**
One attempt to inspect a slot during insertion or search in open addressing.

**Probe Sequence**
The sequence of positions examined during probing.

**Quadratic Probing**
An open-addressing strategy that uses square-based offsets to resolve collisions.

**Rehashing**
Reinserting entries into a new table after resizing.

**Secondary Clustering**
A collision pattern in which keys with the same initial hash follow the same probe sequence.

**Secondary Hash Function**
In double hashing, the second function used to compute the step size between probes.

**Tombstone**
A marker indicating that a slot once held an entry and must still be treated as part of a valid probe path.

