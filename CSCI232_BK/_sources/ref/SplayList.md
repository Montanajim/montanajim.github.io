# Splay List

## Definition

A **splay list** is a self-adjusting data structure that rearranges its elements each time an element is accessed. It is based on the idea of **splaying**, which means moving the accessed item to the front (or root, in tree-based structures) to make future accesses to that item faster.

While the concept originates from **splay trees** (a type of binary search tree), a **splay list** is a simplified linear version using a singly or doubly linked list.

#### **How a Splay List Works**

When you access (search for) an element in a splay list:

1. The list is **sequentially searched** from the beginning.
2. When the item is found, it is **moved to the front** of the list by re-linking the nodes.
3. The result is that frequently accessed elements move closer to the front, reducing future access time.

This is called the **"move-to-front" heuristic**, a specific case of self-organizing lists.

**Example**:
 Suppose you have a list:
 `[D, B, C, A]`
 Searching for `A` results in:
 `[A, D, B, C]` — now `A` is at the front.

## **Why It Works (Intuition)**

- If some items are used more frequently than others, moving them to the front **improves average access time**.
- Over time, the structure optimizes itself for the **actual usage pattern**, without prior knowledge of that pattern.

## Use Cases

Splay lists are useful when:

- You **don't know ahead of time** which items will be accessed most often.
- The access pattern has **locality of reference** (i.e., recently or frequently accessed items are likely to be accessed again soon).
- Memory usage should remain simple—no need for complex tree structures.

**Typical Applications**:

- **Cache systems**: Frequently accessed items bubble to the front.
- **Text editors**: Recently opened files or commands can be organized in a splay list.
- **Autocomplete lists**: Recently or frequently used search terms are moved to the front.

```java
package inst_splay_2025;

class SplayTree {

    private Node root;

    // Inner class representing a node in the splay tree
    class Node {

        int data;
        Node left, right;

        public Node(int item)
        {
            data = item;
            left = right = null;
        }
    }

    // Inserts a value into the tree
    public void insert(int value)
    {
        if (root == null) {
            root = new Node(value);
            return;
        }

        // Splay the tree to bring the value (or closest) to the root
        root = splay(root, value);

        // If the value already exists, no need to insert
        if (root.data == value) {
            return;
        }

        Node newNode = new Node(value);

        // If the new value is smaller, make the new node root and adjust pointers
        if (value < root.data) {
            newNode.right = root;
            newNode.left = root.left;
            root.left = null;
        } else { // If the new value is greater
            newNode.left = root;
            newNode.right = root.right;
            root.right = null;
        }

        root = newNode; // Update root
    }

    // Searches for a value in the tree
    public boolean find(int value)
    {
        root = splay(root, value);
        return (root != null && root.data == value);
    }

    // Deletes a node with the given value
    public void delete(int value)
    {
        if (root == null) {
            return;
        }

        // Splay the tree so that the value (or closest) is at the root
        root = splay(root, value);

        if (root.data != value) {
            return; // If not found, do nothing
        }
        if (root.left == null) {
            root = root.right;
        } else {
            Node temp = root;
            // Splay the largest node in the left subtree to make it new root
            root = splay(root.left, value);
            root.right = temp.right;
        }
    }

    // Right rotation (Zig rotation)
    private Node rotateRight(Node root)
    {
        if (root == null || root.left == null) {
            return root;
        }
        Node newRoot = root.left;
        root.left = newRoot.right;
        newRoot.right = root;
        return newRoot;
    }

    // Left rotation (Zag rotation)
    private Node rotateLeft(Node root)
    {
        if (root == null || root.right == null) {
            return root;
        }
        Node newRoot = root.right;
        root.right = newRoot.left;
        newRoot.left = root;
        return newRoot;
    }

    /*
     * Splay Operation: Moves the given value to the root if present, or the closest value.
     * 
     * Splay tree follows these rules for rotations:
     * 
     * - Zig Rotation (Single Right): When the value is in the left child of the root.
     * - Zag Rotation (Single Left): When the value is in the right child of the root.
     * - Zig-Zig (Double Right Rotation): When the value is in the left child of the left child.
     * - Zag-Zag (Double Left Rotation): When the value is in the right child of the right child.
     * - Zig-Zag (Left-Right Rotation): When the value is in the right child of the left child.
     * - Zag-Zig (Right-Left Rotation): When the value is in the left child of the right child.
     */
    private Node splay(Node root, int value)
    {
        if (root == null || root.data == value) {
            return root;
        }

        if (value < root.data) {
            if (root.left == null) {
                return root;
            }

            // Zig-Zig case (left-left)
            if (value < root.left.data) {
                root.left.left = splay(root.left.left, value);
                root = rotateRight(root);
            } // Zig-Zag case (left-right)
            else if (value > root.left.data) {
                root.left.right = splay(root.left.right, value);
                if (root.left.right != null) {
                    root.left = rotateLeft(root.left);
                }
            }

            // Perform a final Zig rotation
            return (root.left == null) ? root : rotateRight(root);
        } else {
            if (root.right == null) {
                return root;
            }

            // Zag-Zag case (right-right)
            if (value > root.right.data) {
                root.right.right = splay(root.right.right, value);
                root = rotateLeft(root);
            } // Zag-Zig case (right-left)
            else if (value < root.right.data) {
                root.right.left = splay(root.right.left, value);
                if (root.right.left != null) {
                    root.right = rotateRight(root.right);
                }
            }

            // Perform a final Zag rotation
            return (root.right == null) ? root : rotateLeft(root);
        }
    }

    // Prints the tree structure
    public void prettyPrint(Node root, String indent)
    {
        if (root == null) {
            return;
        }
        prettyPrint(root.right, indent + "   ");
        System.out.println(indent + root.data);
        prettyPrint(root.left, indent + "   ");
    }

    // Initiates tree printing
    public void printTree()
    {
        prettyPrint(root, "");
    }
}

// Driver class to test the Splay Tree implementation
public class Inst_splay_2025 {

    public static void main(String[] args)
    {
        SplayTree tree = new SplayTree();

        tree.insert(10);
        tree.insert(20);
        tree.insert(5);
        tree.insert(55);
        tree.insert(60);
        tree.insert(65);
        tree.insert(70);
        tree.insert(75);
        tree.insert(30);
        tree.insert(15);
        tree.insert(25);

        tree.printTree();
        System.out.println("\n----------------\n");

        tree.find(20);
        tree.printTree();
        System.out.println("\n----------------\n");

        tree.find(5);
        tree.printTree();
        System.out.println("\n----------------\n");

        tree.find(65);
        tree.printTree();
        System.out.println("\n----------------\n");

        tree.delete(10);
        tree.printTree();
        System.out.println("\n----------------\n");

        tree.delete(30);
        tree.printTree();
        System.out.println("\n----------------\n");

        tree.delete(15);
        tree.printTree();
        System.out.println("\n----------------\n");

        tree.delete(5);
        tree.printTree();
    }
}

```

