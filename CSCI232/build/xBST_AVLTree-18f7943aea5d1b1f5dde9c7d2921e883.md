# AVL Tree



**AVL Tree Overview**

An **AVL (Adelson-Velsky and Landis) Tree** is a type of self-balancing binary search tree. It is named after its inventors, **Georgy Adelson-Velsky** and **Evgenii Landis**, who introduced it in 1962.

In a typical binary search tree, the key in each node is larger than all keys in its left subtree and smaller than all keys in its right subtree. While a standard binary search tree can degrade to a linked list in the worst case, an AVL tree enforces additional balance properties that prevent extreme imbalance.

------

## Key Properties and Balance Rules

1. **Balance Factor**:
    For each node, the AVL tree tracks a balance factor defined as:

   balance(node)=height(node.left)−height(node.right)\text{balance}(node) = \text{height}(node.left) - \text{height}(node.right)

   In an AVL tree, the balance factor for any node must always be **-1**, **0**, or **1**.

2. **Height Constraint**:
    The height of the left and right subtrees of any node differ by at most **1**. If the height difference exceeds 1, the tree performs rotations to restore balance.

3. **Rotations**:
    The four possible rotation cases occur after an insertion or deletion that breaks the balance:

   - **Left-Left (LL) rotation**: Performed when a node is inserted into the left subtree of the left child. Fixed by a single right rotation.
   - **Right-Right (RR) rotation**: Performed when a node is inserted into the right subtree of the right child. Fixed by a single left rotation.
   - **Left-Right (LR) rotation**: Performed when a node is inserted into the right subtree of the left child. Fixed by a left rotation on the left child, then a right rotation on the node.
   - **Right-Left (RL) rotation**: Performed when a node is inserted into the left subtree of the right child. Fixed by a right rotation on the right child, then a left rotation on the node.

### Single Rotations

- **Right Rotation** (for an unbalanced node leaning left):

  ```
      y                            x
     / \                          / \
    x   T3       ---->          T1   y
   / \                              / \
  T1  T2                           T2  T3
  ```

- **Left Rotation** (for an unbalanced node leaning right):

  ```
    y                                x
   / \                              / \
  T1  x          ---->            y   T3
     / \                          / \
    T2  T3                       T1  T2
  ```

### Double Rotations

When the subtree is not in a strictly left-left or right-right configuration but rather “zig-zag,” two rotations are performed in sequence. For instance, **Left-Right** rotation is effectively a left rotation on the left child, followed by a right rotation on the original node.

------

## Java Implementation of an AVL Tree

Below is a simple Java class that implements:

- **Insertion**
- **Deletion**
- **Search**
- **Traversals**: In-order, Pre-order, Post-order
- A **pretty print** method to display the tree structure

```java
public class AVLTree<T extends Comparable<T>> {

    private class Node {
        T key;
        Node left, right;
        int height;

        Node(T key) {
            this.key = key;
            height = 1;
        }
    }

    private Node root;

    // ------------------------
    // Utility Functions
    // ------------------------

    // Return the height of a node, or 0 if null
    private int height(Node node) {
        return (node == null) ? 0 : node.height;
    }

    // Calculate the balance factor of a node
    private int getBalance(Node node) {
        if (node == null) {
            return 0;
        }
        return height(node.left) - height(node.right);
    }

    // Update the node's height based on children's heights
    private void updateHeight(Node node) {
        node.height = 1 + Math.max(height(node.left), height(node.right));
    }

    // ------------------------
    // Rotations
    // ------------------------

    // Right rotate subtree rooted with y
    private Node rotateRight(Node y) {
        Node x = y.left;
        Node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        updateHeight(y);
        updateHeight(x);

        // x becomes new root
        return x;
    }

    // Left rotate subtree rooted with x
    private Node rotateLeft(Node x) {
        Node y = x.right;
        Node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        updateHeight(x);
        updateHeight(y);

        // y becomes new root
        return y;
    }

    // ------------------------
    // Insertion
    // ------------------------
    public void insert(T key) {
        root = insertRec(root, key);
    }

    private Node insertRec(Node node, T key) {
        // 1. Perform the normal BST insertion
        if (node == null) {
            return new Node(key);
        }

        int cmp = key.compareTo(node.key);
        if (cmp < 0) {
            node.left = insertRec(node.left, key);
        } else if (cmp > 0) {
            node.right = insertRec(node.right, key);
        } else {
            // Duplicate keys not allowed or handle as desired
            return node;
        }

        // 2. Update the height of the ancestor node
        updateHeight(node);

        // 3. Get the balance factor
        int balance = getBalance(node);

        // 4. If the node becomes unbalanced, then check the four cases

        // Left Left Case
        if (balance > 1 && key.compareTo(node.left.key) < 0) {
            return rotateRight(node);
        }

        // Right Right Case
        if (balance < -1 && key.compareTo(node.right.key) > 0) {
            return rotateLeft(node);
        }

        // Left Right Case
        if (balance > 1 && key.compareTo(node.left.key) > 0) {
            node.left = rotateLeft(node.left);
            return rotateRight(node);
        }

        // Right Left Case
        if (balance < -1 && key.compareTo(node.right.key) < 0) {
            node.right = rotateRight(node.right);
            return rotateLeft(node);
        }

        // return the (unchanged) node pointer
        return node;
    }

    // ------------------------
    // Deletion
    // ------------------------
    public void delete(T key) {
        root = deleteRec(root, key);
    }

    private Node deleteRec(Node node, T key) {
        // 1. Perform standard BST delete
        if (node == null) {
            return node;
        }

        int cmp = key.compareTo(node.key);
        if (cmp < 0) {
            node.left = deleteRec(node.left, key);
        } else if (cmp > 0) {
            node.right = deleteRec(node.right, key);
        } else {
            // Node with only one child or no child
            if (node.left == null || node.right == null) {
                Node temp = (node.left != null) ? node.left : node.right;
                // No child
                if (temp == null) {
                    node = null;
                } else {
                    // One child
                    node = temp;
                }
            } else {
                // Node with two children: get the inorder successor
                Node successor = getMinValueNode(node.right);
                // Copy successor's data to this node
                node.key = successor.key;
                // Delete the successor
                node.right = deleteRec(node.right, successor.key);
            }
        }

        // If the tree had only one node
        if (node == null) {
            return node;
        }

        // 2. Update height of the current node
        updateHeight(node);

        // 3. Get balance factor
        int balance = getBalance(node);

        // 4. Rebalance if needed

        // Left Left Case
        if (balance > 1 && getBalance(node.left) >= 0) {
            return rotateRight(node);
        }

        // Left Right Case
        if (balance > 1 && getBalance(node.left) < 0) {
            node.left = rotateLeft(node.left);
            return rotateRight(node);
        }

        // Right Right Case
        if (balance < -1 && getBalance(node.right) <= 0) {
            return rotateLeft(node);
        }

        // Right Left Case
        if (balance < -1 && getBalance(node.right) > 0) {
            node.right = rotateRight(node.right);
            return rotateLeft(node);
        }

        return node;
    }

    // Helper function to find the node with the minimum key value
    private Node getMinValueNode(Node node) {
        Node current = node;
        while (current.left != null) {
            current = current.left;
        }
        return current;
    }

    // ------------------------
    // Search
    // ------------------------
    public boolean search(T key) {
        return searchRec(root, key);
    }

    private boolean searchRec(Node node, T key) {
        if (node == null) {
            return false;
        }
        int cmp = key.compareTo(node.key);
        if (cmp < 0) {
            return searchRec(node.left, key);
        } else if (cmp > 0) {
            return searchRec(node.right, key);
        } else {
            // cmp == 0, key found
            return true;
        }
    }

    // ------------------------
    // Traversals
    // ------------------------
    public void inOrder() {
        System.out.print("InOrder: ");
        inOrderRec(root);
        System.out.println();
    }

    private void inOrderRec(Node node) {
        if (node == null) {
            return;
        }
        inOrderRec(node.left);
        System.out.print(node.key + " ");
        inOrderRec(node.right);
    }

    public void preOrder() {
        System.out.print("PreOrder: ");
        preOrderRec(root);
        System.out.println();
    }

    private void preOrderRec(Node node) {
        if (node == null) {
            return;
        }
        System.out.print(node.key + " ");
        preOrderRec(node.left);
        preOrderRec(node.right);
    }

    public void postOrder() {
        System.out.print("PostOrder: ");
        postOrderRec(root);
        System.out.println();
    }

    private void postOrderRec(Node node) {
        if (node == null) {
            return;
        }
        postOrderRec(node.left);
        postOrderRec(node.right);
        System.out.print(node.key + " ");
    }

    // ------------------------
    // Pretty Print (Tree Display)
    // ------------------------
    public void printTree() {
        printTreeRec(root, "", true);
    }

    /*
     * Traverses the tree in a rotated manner and prints branches to visualize
     * the structure. The approach is to go right, then print current, then go left.
     */
    private void printTreeRec(Node node, String indent, boolean isRight) {
        if (node == null) {
            return;
        }
        // Print right subtree
        printTreeRec(node.right, indent + (isRight ? "     " : " |   "), false);

        // Print current node
        System.out.print(indent);
        if (isRight) {
            System.out.print("└───");
        } else {
            System.out.print("┌───");
        }
        System.out.println(node.key);

        // Print left subtree
        printTreeRec(node.left, indent + (isRight ? " |   " : "     "), true);
    }

    // ------------------------
    // Main (for demonstration)
    // ------------------------
    public static void main(String[] args) {
        AVLTree<Integer> tree = new AVLTree<>();
        int[] values = { 10, 20, 30, 40, 50, 25 };
        for (int val : values) {
            tree.insert(val);
        }

        tree.printTree();
        tree.inOrder();
        tree.preOrder();
        tree.postOrder();

        System.out.println("Search 25: " + tree.search(25));
        System.out.println("Search 15: " + tree.search(15));

        System.out.println("\nDelete 20");
        tree.delete(20);
        tree.printTree();
    }
}
```

### Explanation of the Key Methods

1. **Node Class**
    Each node stores:
   - The key (generic type `T`).
   - References to the left and right children.
   - An integer `height` to aid in maintaining balance.
2. **Height and Balance Factor**
   - `height(node)`: returns the height of the node (with `null` as height 0).
   - `getBalance(node)`: computes the difference in heights of the left and right subtrees.
3. **Insertion**
   - Insert the new key as in a regular BST.
   - Update the height of the ancestor nodes.
   - Check the balance factor.
   - Perform appropriate rotations if unbalanced.
4. **Deletion**
   - Perform the usual BST deletion (case of no child, one child, or two children).
   - Update the height and balance for nodes on the path back up.
   - Fix any imbalance with the correct rotations.
5. **Search**
    Standard BST search logic:
   - Compare, traverse left or right, or return true if the key is found.
6. **Traversals**
   - **In-order**: left, node, right
   - **Pre-order**: node, left, right
   - **Post-order**: left, right, node
7. **Pretty Print**
    A simple, recursive approach that prints the tree horizontally, showing child branches with ASCII symbols.

------

**Time Complexity**

- **Insertion**, **Deletion**, and **Search** each take **O(log n)** time on average because the AVL tree remains balanced (height is O(log⁡n)\mathcal{O}(\log n)).

With this, you have a complete Java class demonstrating the core features of an AVL tree, along with helpful utility methods and a main routine for testing.



---

## Supplemental Note

Let's break down the line of code in detail:

```java
public class AVLTree<T extends Comparable<T>>
```

This declaration defines a generic class named `AVLTree` which has a single type parameter, `T`. The part that might look complex at first glance is:

```java
T extends Comparable<T>
```

### What does `T extends Comparable<T>` mean?

1. **Generic Type Parameter**
    When you write `class AVLTree<T>`, `T` is a generic type parameter. This allows the class `AVLTree` to work with **any** type without being tied to a specific class or interface.

2. **Type Bound (`extends Comparable<T>`)**
    By saying `T extends Comparable<T>`, we’re adding a **constraint** on what `T` can be:

   - It must be a type that implements the `Comparable<T>` interface.
   - In other words, `T` must be able to compare itself to another object of the same type `T`.

   In Java, `extends` in a generic type context can mean either “extends (a superclass)” **or** “implements (an interface).” Since `Comparable` is an interface, this part actually means “implements `Comparable<T>`.”

3. **Why do we need `Comparable<T>` in an AVL Tree?**
    An AVL tree is a **self-balancing binary search tree**. For a binary search tree, we need to **compare** elements to decide:

   - Where to insert a new node (go left if the new value is smaller, go right if it’s larger).
   - How to traverse or search in the tree.

   Because we need to compare elements, the type `T` used in this tree must be **comparable**. That’s why the code requires `T extends Comparable<T>`—so that each node’s value can be compared to another node’s value.

### What does the `Comparable` interface do?

`Comparable<T>` is a built-in Java interface (from the `java.lang` package) that has a single method:

```java
public interface Comparable<T> {
    int compareTo(T o);
}
```

Any class that implements `Comparable<T>` is expected to provide its own definition of the `compareTo(T o)` method. The `compareTo` method returns:

- A **negative integer** if the current object is “less than” the argument.
- **Zero** if they are “equal.”
- A **positive integer** if the current object is “greater than” the argument.

This enables sorting and ordering. In a data structure like an AVL tree, you rely on the `compareTo` method to decide how to place or find items.

### Example

For instance, Java’s built-in `String` class implements `Comparable<String>`:

```java
public final class String implements Comparable<String>, CharSequence, ...
{
    // Implementation details

    @Override
    public int compareTo(String anotherString) {
        // returns negative, 0, or positive
        // based on lexicographical comparison
    }
}
```

So if you create an `AVLTree<String>`, you know that you can compare `String` objects to decide their order in the tree.

Similarly, Java’s built-in numeric types like `Integer` implement `Comparable<Integer>`, so `AVLTree<Integer>` would also work.

### Summary of `T extends Comparable<T>`

- It **constrains** the generic parameter `T` to types that implement `Comparable` of themselves.
- It **ensures** that any instance of `AVLTree<T>` can compare its elements (`T` objects) with each other.
- It’s essential for data structures or algorithms that rely on comparing objects (e.g., sorting, searching, or balancing a tree).

------

By using `T extends Comparable<T>`, the `AVLTree` class is guaranteed that `T` has a `compareTo` method, making it possible to implement comparison-based logic correctly and safely within the tree’s operations.