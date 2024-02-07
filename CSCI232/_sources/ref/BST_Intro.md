# Binary Search Tree - Intro



## Background Information

A binary search tree (BST) is a special type of binary tree data structure used to efficiently store and access sorted data. It's like a regular tree, but with additional rules that keep everything neatly organized:



**Key features:**

- **Ordering:** Each node in the tree has a value (key), and the key of a node is **always greater than** all the keys in its **left subtree** and **less than** all the keys in its **right subtree**. This creates a sorted order throughout the tree.
- **Efficient searching:** Because of this ordering, you can very quickly search for specific values in the tree. Imagine searching a phone book - you wouldn't start at the very beginning or end, but somewhere in the middle based on the last name. Similarly, in a BST, you can efficiently move left or right depending on the value you're searching for, narrowing down the possibilities with each comparison.
- **Dynamic insertions and deletions:** You can easily add new values (insert) or remove existing ones (delete) from the tree while maintaining the sorted order. The process involves comparing the new value with existing nodes and finding its appropriate place based on the ordering rule.



**Benefits of using BSTs:**

- **Fast search:** Searching for elements in a balanced BST takes **logarithmic time** on average, which is significantly faster than searching an unsorted list.
- **Ordered access:** You can easily traverse the tree in sorted order (e.g., for printing all elements in ascending order).
- **Efficient insertions and deletions:** These operations can also be done in logarithmic time in balanced BSTs.



**However, BSTs also have some drawbacks:**

- **Performance depends on balance:** The efficiency of BST operations relies heavily on the tree's balance. An unbalanced tree can perform much worse than a balanced one.
- **Not self-balancing:** By default, BSTs are not self-balancing, meaning insertions and deletions can sometimes lead to imbalances. Special techniques are needed to maintain balance and ensure optimal performance.



Overall, binary search trees are a powerful and versatile data structure for storing and managing sorted data efficiently. They offer fast search, insertion, and deletion operations, making them suitable for various applications like symbol tables, priority queues, and sorting algorithms.