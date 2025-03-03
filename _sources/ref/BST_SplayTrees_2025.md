# Splay Trees

### Splay Trees

A **splay tree** is a type of self-adjusting binary search tree (BST) where recently accessed elements are moved to the root of the tree using a process called *splaying*. This helps ensure that frequently accessed elements are quicker to access.

#### Who Invented It:

- Splay trees were invented by **Daniel Sleator** and **Robert Tarjan** in 1985. The invention was part of their research on self-adjusting data structures.

#### When Was It Invented:

- The splay tree was introduced in **1985**.

#### Major Uses:

- **Dynamic sets**: Splay trees are used to maintain a dynamic set of elements that can support a variety of search and update operations.
- **Memory-efficient**: Since splay trees do not require additional space for balancing data like AVL trees or Red-Black trees, they can be more memory-efficient.
- **Efficient in practice for certain workloads**: Splay trees perform well when there are repeated accesses to a small subset of elements (i.e., the access pattern exhibits locality).

#### Insert Function:

- **Insertion in a splay tree** is similar to that in a regular binary search tree. The node is inserted following the normal BST rules. However, after insertion, the tree is "splayed" to bring the newly inserted node to the root.

```java
public void insert(int value) {
    root = insertRec(root, value);
    splay(root, value);
}

private Node insertRec(Node root, int value) {
    if (root == null) {
        root = new Node(value);
        return root;
    }

    if (value < root.data) {
        root.left = insertRec(root.left, value);
    } else if (value > root.data) {
        root.right = insertRec(root.right, value);
    }

    return root;
}
```

#### Delete Function:

- **Deletion** is performed in the same way as in a normal binary search tree. After finding the node to delete, it is removed, and then the tree is splayed to restore the tree's structure.

```java
public void delete(int value) {
    root = deleteRec(root, value);
}

private Node deleteRec(Node root, int value) {
    if (root == null) return root;

    if (value < root.data) {
        root.left = deleteRec(root.left, value);
    } else if (value > root.data) {
        root.right = deleteRec(root.right, value);
    } else {
        // node with value found
        if (root.left == null) return root.right;
        else if (root.right == null) return root.left;
    }

    return root;
}
```

#### Find Function:

- The **find function** searches for a value in the tree, and if the value is found, it performs a splay operation to bring that value to the root. If the value is not found, the tree remains unchanged.

```java
public boolean find(int value) {
    root = splay(root, value);
    return (root != null && root.data == value);
}
```

#### Rules for Rotations:

- Splay trees use three types of rotations to adjust the tree during splaying:
  1. **Zig**: When the node is the child of the root.
  2. **Zig-Zig**: When the node is the left or right child of a left or right child (two-level deep).
  3. **Zig-Zag**: When the node is the left child of the right child or the right child of the left child.

#### Rotations:

- **Single Rotation (Zig)**: If the node is the child of the root, perform a single rotation (right or left depending on the situation).
- **Double Rotation (Zig-Zig or Zig-Zag)**: In these cases, two rotations are needed. They help in cases where the tree has more than one level to adjust.

```java
private Node splay(Node root, int value) {
    if (root == null || root.data == value) return root;

    if (value < root.data) {
        if (root.left == null) return root;
        if (value < root.left.data) {
            root.left.left = splay(root.left.left, value);
            root = rotateRight(root);
        } else if (value > root.left.data) {
            root.left.right = splay(root.left.right, value);
            if (root.left.right != null) {
                root.left = rotateLeft(root.left);
            }
        }
        return (root.left == null) ? root : rotateRight(root);
    } else {
        if (root.right == null) return root;
        if (value > root.right.data) {
            root.right.right = splay(root.right.right, value);
            root = rotateLeft(root);
        } else if (value < root.right.data) {
            root.right.left = splay(root.right.left, value);
            if (root.right.left != null) {
                root.right = rotateRight(root.right);
            }
        }
        return (root.right == null) ? root : rotateLeft(root);
    }
}
```

#### Java Program Demonstrating Insert, Find, Delete, and Pretty Print:

Sure! Here's the updated version of the Java program with comments and the inclusion of the rules for rotations:

```java
class SplayTree {
    private Node root;

    // Node class to represent each node in the tree
    class Node {
        int data;  // Data stored in the node
        Node left, right;  // Left and right child nodes

        // Constructor to create a new node with the given value
        public Node(int item) {
            data = item;
            left = right = null;
        }
    }

    // Insert function to add a new value into the splay tree
    public void insert(int value) {
        root = insertRec(root, value);  // Perform regular BST insertion
        root = splay(root, value);  // Splay the tree to bring the inserted value to the root
    }

    // Recursive helper function for insertion
    private Node insertRec(Node root, int value) {
        if (root == null) {
            root = new Node(value);  // Create a new node if the tree is empty
            return root;
        }

        // Follow the BST insertion rules
        if (value < root.data) {
            root.left = insertRec(root.left, value);  // Insert in the left subtree
        } else if (value > root.data) {
            root.right = insertRec(root.right, value);  // Insert in the right subtree
        }

        return root;
    }

    // Find function to search for a value in the splay tree
    public boolean find(int value) {
        root = splay(root, value);  // Splay the tree to bring the searched node to the root
        return (root != null && root.data == value);  // Return true if the node is found
    }

    // Delete function to remove a node from the splay tree
    public void delete(int value) {
        root = deleteRec(root, value);  // Perform regular BST deletion
    }

    // Recursive helper function for deletion
    private Node deleteRec(Node root, int value) {
        if (root == null) return root;  // If the root is null, return

        // Search for the node to delete
        if (value < root.data) {
            root.left = deleteRec(root.left, value);  // Recursively search in the left subtree
        } else if (value > root.data) {
            root.right = deleteRec(root.right, value);  // Recursively search in the right subtree
        } else {
            // Node with the value found
            if (root.left == null) return root.right;  // If the node has no left child, replace it with the right child
            else if (root.right == null) return root.left;  // If the node has no right child, replace it with the left child
        }

        return root;  // Return the updated root
    }

    // Function to perform a right rotation on the tree (used during splaying)
    private Node rotateRight(Node root) {
        Node newRoot = root.left;  // Make the left child the new root
        root.left = newRoot.right;  // Make the right child of the new root the left child of the old root
        newRoot.right = root;  // Make the old root the right child of the new root
        return newRoot;  // Return the new root
    }

    // Function to perform a left rotation on the tree (used during splaying)
    private Node rotateLeft(Node root) {
        Node newRoot = root.right;  // Make the right child the new root
        root.right = newRoot.left;  // Make the left child of the new root the right child of the old root
        newRoot.left = root;  // Make the old root the left child of the new root
        return newRoot;  // Return the new root
    }

    // Splay function to bring the node with the given value to the root
    private Node splay(Node root, int value) {
        if (root == null || root.data == value) return root;  // If the root is null or the value is found, return the root

        // The following part implements the three rules of rotation:

        // 1. Zig: If the node is the child of the root (one-level deep), perform a single rotation.
        if (value < root.data) {
            if (root.left == null) return root;  // If the left child is null, no rotation is possible
            if (value < root.left.data) {
                // Zig-Zig: Perform a right rotation (two-level deep)
                root.left.left = splay(root.left.left, value);
                root = rotateRight(root);  // Rotate the root to the right
            } else if (value > root.left.data) {
                // Zig-Zag: Perform a left rotation on the left child and then a right rotation
                root.left.right = splay(root.left.right, value);
                if (root.left.right != null) {
                    root.left = rotateLeft(root.left);  // Rotate the left child to the left
                }
            }
            return (root.left == null) ? root : rotateRight(root);  // Return the rotated root
        } else {
            if (root.right == null) return root;  // If the right child is null, no rotation is possible
            if (value > root.right.data) {
                // Zig-Zig: Perform a left rotation (two-level deep)
                root.right.right = splay(root.right.right, value);
                root = rotateLeft(root);  // Rotate the root to the left
            } else if (value < root.right.data) {
                // Zig-Zag: Perform a right rotation on the right child and then a left rotation
                root.right.left = splay(root.right.left, value);
                if (root.right.left != null) {
                    root.right = rotateRight(root.right);  // Rotate the right child to the right
                }
            }
            return (root.right == null) ? root : rotateLeft(root);  // Return the rotated root
        }
    }

    // Pretty print function to display the tree visually
    public void prettyPrint(Node root, String indent) {
        if (root == null) return;  // If the root is null, return

        // Print the right subtree first with increased indentation
        prettyPrint(root.right, indent + "   ");
        System.out.println(indent + root.data);  // Print the current node
        // Print the left subtree with increased indentation
        prettyPrint(root.left, indent + "   ");
    }

    // Wrapper function to print the tree
    public void printTree() {
        prettyPrint(root, "");  // Call the prettyPrint function starting from the root
    }
}

public class Inst_splay_2025 {
    
    public static void main(String[] args) {
        SplayTree tree = new SplayTree();

        // Inserting values into the tree
        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(15);

        // Pretty print the tree after insertion
        System.out.println("Tree after insertion:");
        tree.printTree();

        // Find a value in the tree and bring it to the root
        tree.find(20);
        System.out.println("\nTree after finding 20:");
        tree.printTree();

        // Delete a value from the tree
        tree.delete(10);
        System.out.println("\nTree after deleting 10:");
        tree.printTree();
    }
}
```

### Explanation of Rotation Rules:

1. **Zig (Single Rotation)**: If the node to be accessed is the left or right child of the root, perform a single rotation (either left or right).
2. **Zig-Zig (Double Rotation)**: If the node is the left or right child of a left or right child (two levels deep), perform two rotations. This optimizes the tree by rotating both the node and its parent.
3. **Zig-Zag (Double Rotation)**: If the node is the left child of the right child, or the right child of the left child (mixed child directions), perform a rotation on the child followed by a rotation on the node itself.

This program demonstrates how to use splay tree operations and includes helpful comments and explanations of the rotation rules. Each rotation helps ensure the tree remains balanced by moving frequently accessed nodes towards the root.



---

## Splay using for loops

Sure! Here's the modified version of the Splay Tree program, using **loops** instead of recursion for the insert, delete, and splay operations.

This version avoids the recursive calls and uses loops to handle the tree traversal and adjustments.

```java
class SplayTree {
    private Node root;

    // Node class to represent each node in the tree
    class Node {
        int data;  // Data stored in the node
        Node left, right;  // Left and right child nodes

        // Constructor to create a new node with the given value
        public Node(int item) {
            data = item;
            left = right = null;
        }
    }

    // Insert function to add a new value into the splay tree
    public void insert(int value) {
        if (root == null) {
            root = new Node(value);  // If tree is empty, create a new node as root
            return;
        }

        Node node = root;
        Node parent = null;

        // Loop to find the correct position for insertion
        while (node != null) {
            parent = node;
            if (value < node.data) {
                node = node.left;
            } else if (value > node.data) {
                node = node.right;
            } else {
                return;  // If the value is already present, do nothing
            }
        }

        // Create a new node and attach it to the parent
        node = new Node(value);
        if (value < parent.data) {
            parent.left = node;
        } else {
            parent.right = node;
        }

        // After insertion, splay the tree to bring the inserted node to the root
        root = splay(root, value);
    }

    // Delete function to remove a node from the splay tree
    public void delete(int value) {
        if (root == null) return;

        // Splay the tree to bring the node to be deleted to the root
        root = splay(root, value);

        if (root == null || root.data != value) return;  // Node not found

        // Node to be deleted is at the root
        if (root.left == null) {
            root = root.right;  // If left child is null, replace root with right child
        } else {
            Node rightSubtree = root.right;
            root = root.left;
            root = splay(root, value);  // Splay the left subtree to bring the max element to the root
            root.right = rightSubtree;  // Attach the right subtree to the new root
        }
    }

    // Find function to search for a value in the splay tree
    public boolean find(int value) {
        if (root == null) return false;

        // Splay the tree to bring the searched node to the root
        root = splay(root, value);

        return (root != null && root.data == value);
    }

    // Function to perform a right rotation on the tree (used during splaying)
    private Node rotateRight(Node root) {
        Node newRoot = root.left;  // Make the left child the new root
        root.left = newRoot.right;  // Make the right child of the new root the left child of the old root
        newRoot.right = root;  // Make the old root the right child of the new root
        return newRoot;  // Return the new root
    }

    // Function to perform a left rotation on the tree (used during splaying)
    private Node rotateLeft(Node root) {
        Node newRoot = root.right;  // Make the right child the new root
        root.right = newRoot.left;  // Make the left child of the new root the right child of the old root
        newRoot.left = root;  // Make the old root the left child of the new root
        return newRoot;  // Return the new root
    }

    // Splay function to bring the node with the given value to the root
    private Node splay(Node root, int value) {
        while (root != null) {
            // Base case: if the node is found or we reach the leaf, break out of the loop
            if (root.data == value) return root;

            // Zig (single rotation): If the node is the left child or right child of the root
            if (value < root.data) {
                if (root.left == null) break;  // If there's no left child, stop

                // Zig-Zig (double rotation): If node's value is in the left subtree of left child
                if (value < root.left.data) {
                    root = rotateRight(root);
                } else if (value > root.left.data) {
                    // Zig-Zag (double rotation): If node's value is in the right subtree of left child
                    root.left = rotateLeft(root.left);
                    root = rotateRight(root);
                }
            } else {
                if (root.right == null) break;  // If there's no right child, stop

                // Zig-Zig (double rotation): If node's value is in the right subtree of right child
                if (value > root.right.data) {
                    root = rotateLeft(root);
                } else if (value < root.right.data) {
                    // Zig-Zag (double rotation): If node's value is in the left subtree of right child
                    root.right = rotateRight(root.right);
                    root = rotateLeft(root);
                }
            }
        }
        return root;
    }

    // Pretty print function to display the tree visually
    public void prettyPrint(Node root, String indent) {
        if (root == null) return;  // If the root is null, return

        // Print the right subtree first with increased indentation
        prettyPrint(root.right, indent + "   ");
        System.out.println(indent + root.data);  // Print the current node
        // Print the left subtree with increased indentation
        prettyPrint(root.left, indent + "   ");
    }

    // Wrapper function to print the tree
    public void printTree() {
        prettyPrint(root, "");  // Call the prettyPrint function starting from the root
    }

    public static void main(String[] args) {
        SplayTree tree = new SplayTree();

        // Inserting values into the tree
        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(15);

        // Pretty print the tree after insertion
        System.out.println("Tree after insertion:");
        tree.printTree();

        // Find a value in the tree and bring it to the root
        tree.find(20);
        System.out.println("\nTree after finding 20:");
        tree.printTree();

        // Delete a value from the tree
        tree.delete(10);
        System.out.println("\nTree after deleting 10:");
        tree.printTree();
    }
}
```

### Explanation of Changes:

1. **Insert Method**: The insertion now uses a loop to traverse the tree and find the correct position to insert the new node. The insertion process is followed by a splay operation to move the newly inserted node to the root.
2. **Delete Method**: Similar to insertion, the delete method now uses a loop to traverse the tree and delete the node. It also includes a splay operation to move the necessary nodes after deletion.
3. **Splay Method**: The splay function has been rewritten to use a loop instead of recursion. It continuously adjusts the tree until the target node is either found or no further adjustments are necessary.
4. **Rotation Methods**: The left and right rotations remain the same, as these are simple tree manipulations that don't depend on recursion.

This approach eliminates recursion in favor of iterative methods using loops, which may help avoid potential stack overflow issues with deep trees, though it may still be less efficient compared to a more balanced tree like an AVL or Red-Black tree. However, the splay tree performs well with specific access patterns, especially when there is locality of reference.

