# Tree Traversal




Pre-order, post-order, and in-order are not "order types" in the general sense, but rather **tree traversal methods** used to visit all nodes in a tree structure. They define the order in which we visit the root, left subtree, and right subtree of each node. Here's a breakdown of each:



**Pre-order:**

- Visit the **root** of the node.
- Recursively visit the **left subtree**.
- Recursively visit the **right subtree**.



Think of it as visiting the parent first, then the children, like inspecting a family photo by focusing on the parents before moving to their individual pictures.



**In-order:**

- Recursively visit the **left subtree**.
- Visit the **root** of the node.
- Recursively visit the **right subtree**.



Imagine reading a sentence word by word: you start at the leftmost word, move to the next, and so on, reaching the root (middle word) last.



**Post-order:**

- Recursively visit the **left subtree**.
- Recursively visit the **right subtree**.
- Visit the **root** of the node.



This is like cleaning up after a plant's growth: you prune the left and right branches before finally taking care of the main trunk.



Here are some examples of how these traversals are used in real life:



- **Pre-order:** Building a file system where folders are processed before their contents, or printing the document outline with headings first.

- **In-order:** Sorting a list of numbers in ascending order using a binary search tree, or printing the words in a sentence in the correct order.

- **Post-order:** Evaluating an arithmetic expression where leaves (operands) are processed before the operators, or calculating the size of a directory by first traversing all subdirectories.

  

---

