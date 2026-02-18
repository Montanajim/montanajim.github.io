# What is a Red-Black Tree?

A Red-Black Tree is a type of self-balancing binary search tree. That means it stores data in a way similar to a Binary Search Tree (BST), but it also keeps itself “balanced” to ensure operations (insertion, deletion, search) generally happen in **O(log n)** time.

## Key Properties

1. **Red or Black Color**: Each node is either red or black.
2. **Root is Black**: The root of the tree is always black.
3. **Leaves Are Black**: Often, the tree is represented with “NIL” leaves that are black. (In some implementations, we simply treat `null` as black leaves.)
4. **Red Node, Black Parent**: If a node is red, then its parent must be black. (This prevents two reds in a row.)
5. **Same Number of Black Nodes**: Every path from a given node down to any of its descendant null leaves has the same number of black nodes.

These rules ensure that no path in the tree is disproportionately longer than any other, thus balancing the tree height.

------

## High-Level Operations

### 1. Search (Find)

- Idea

  : Just like a regular Binary Search Tree.

  - Compare the key you’re searching for to the current node.
  - If it’s smaller, go left; if it’s larger, go right.
  - If it’s equal, you found it; otherwise, keep going until you hit a null (meaning the key is not in the tree).

### 2. Insert

1. **BST Insert**: Insert the new node like you would in a normal BST (ignoring color).
2. **Color the Node Red**: New nodes are typically inserted as **red**.
3. **Fix Violations**: If this creates any violation of red-black properties (for example, a red node having a red parent), perform rotations and/or color flips until the tree properties are restored.

### 3. Delete

1. **BST Delete**: Find the node, remove it in a BST-like fashion (replace with successor if it has two children, etc.).
2. **Fix Violations**: Removing a black node can disrupt the black-depth property. So, we fix the tree by performing rotations or color changes until the properties are restored.

------

## Sample Red-Black Tree Implementation in Java

Below is a **simplified** version of a Red-Black Tree implementation. This example demonstrates the main structure of the code and the core methods (`search`, `insert`, `delete`). In practice, you might have additional helper methods and thorough edge-case handling.

### Node Definition

```java
public class RedBlackTree {

    private enum Color {
        RED,
        BLACK
    }

    private class Node {
        int key;
        Node left, right, parent;
        Color color;

        Node(int key) {
            this.key = key;
            this.color = Color.RED; // New nodes start as RED
        }
    }

    private Node root;

    public RedBlackTree() {
        root = null;
    }
    
    // Utility method to check if a node is null or black
    private boolean isBlack(Node node) {
        return node == null || node.color == Color.BLACK;
    }

    // Utility method to get the parent of a node
    private Node parentOf(Node node) {
        return (node == null) ? null : node.parent;
    }

    // Utility method to get the grandparent of a node
    private Node grandparentOf(Node node) {
        return parentOf(parentOf(node));
    }

    // Utility method to get the sibling of a node
    private Node siblingOf(Node node) {
        Node parent = parentOf(node);
        if (parent == null) return null;
        return (node == parent.left) ? parent.right : parent.left;
    }

    // Utility method to get the uncle of a node
    private Node uncleOf(Node node) {
        Node parent = parentOf(node);
        return siblingOf(parent);
    }

    // Left rotate around a given node x
    private void rotateLeft(Node x) {
        Node y = x.right;
        x.right = y.left;
        if (y.left != null) {
            y.left.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null) {
            // x was the root
            root = y;
        } else if (x == x.parent.left) {
            x.parent.left = y;
        } else {
            x.parent.right = y;
        }
        y.left = x;
        x.parent = y;
    }

    // Right rotate around a given node x
    private void rotateRight(Node x) {
        Node y = x.left;
        x.left = y.right;
        if (y.right != null) {
            y.right.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null) {
            // x was the root
            root = y;
        } else if (x == x.parent.right) {
            x.parent.right = y;
        } else {
            x.parent.left = y;
        }
        y.right = x;
        x.parent = y;
    }

    // ---------------------------------------------------------
    // SEARCH
    // ---------------------------------------------------------
    public Node search(int key) {
        Node current = root;
        while (current != null) {
            if (key < current.key) {
                current = current.left;
            } else if (key > current.key) {
                current = current.right;
            } else {
                // Found the key
                return current;
            }
        }
        return null; // Not found
    }

    // ---------------------------------------------------------
    // INSERT
    // ---------------------------------------------------------
    public void insert(int key) {
        Node newNode = new Node(key);
        root = bstInsert(root, newNode);
        fixInsert(newNode);
    }

    // Standard BST insertion
    private Node bstInsert(Node root, Node node) {
        if (root == null) {
            return node;
        }

        if (node.key < root.key) {
            root.left = bstInsert(root.left, node);
            root.left.parent = root;
        } else if (node.key > root.key) {
            root.right = bstInsert(root.right, node);
            root.right.parent = root;
        } else {
            // Duplicate keys are typically not allowed; handle if desired
        }
        return root;
    }

    // Fix the red-black tree after insertion
    private void fixInsert(Node node) {
        // While the parent is RED, we have a violation
        while (node != root && parentOf(node).color == Color.RED) {
            Node uncle = uncleOf(node);
            Node parent = parentOf(node);
            Node grandparent = grandparentOf(node);

            if (parent == grandparent.left) {
                // If uncle is RED, just recolor
                if (uncle != null && uncle.color == Color.RED) {
                    parent.color = Color.BLACK;
                    uncle.color = Color.BLACK;
                    grandparent.color = Color.RED;
                    node = grandparent; // Move up the tree
                } else {
                    // If node is right child, rotate left
                    if (node == parent.right) {
                        node = parent;
                        rotateLeft(node);
                    }
                    // Recolor and rotate
                    parentOf(node).color = Color.BLACK;
                    grandparentOf(node).color = Color.RED;
                    rotateRight(grandparentOf(node));
                }
            } else {
                // Parent is right child
                if (uncle != null && uncle.color == Color.RED) {
                    parent.color = Color.BLACK;
                    uncle.color = Color.BLACK;
                    grandparent.color = Color.RED;
                    node = grandparent; 
                } else {
                    // If node is left child, rotate right
                    if (node == parent.left) {
                        node = parent;
                        rotateRight(node);
                    }
                    // Recolor and rotate
                    parentOf(node).color = Color.BLACK;
                    grandparentOf(node).color = Color.RED;
                    rotateLeft(grandparentOf(node));
                }
            }
        }
        // Root must always be BLACK
        root.color = Color.BLACK;
    }

    // ---------------------------------------------------------
    // DELETE
    // ---------------------------------------------------------
    public void delete(int key) {
        Node node = search(key);
        if (node == null) {
            return; // Key not found, no action
        }
        deleteNode(node);
    }

    private void deleteNode(Node node) {
        Node y = node; 
        Node x;  
        Color originalColor = y.color; 

        // Case 1: Node has 0 or 1 child
        if (node.left == null) {
            x = node.right;
            transplant(node, node.right);
        } else if (node.right == null) {
            x = node.left;
            transplant(node, node.left);
        } else {
            // Case 2: Node has 2 children
            // Replace with successor
            y = minimum(node.right);
            originalColor = y.color;
            x = y.right;
            if (y.parent == node) {
                if (x != null) {
                    x.parent = y;
                }
            } else {
                transplant(y, y.right);
                y.right = node.right;
                if (y.right != null) {
                    y.right.parent = y;
                }
            }
            transplant(node, y);
            y.left = node.left;
            if (y.left != null) {
                y.left.parent = y;
            }
            y.color = node.color;
        }

        // If the deleted node was black, fix double black issue
        if (originalColor == Color.BLACK) {
            fixDelete(x);
        }
    }

    // Replace the subtree rooted at u with the subtree rooted at v
    private void transplant(Node u, Node v) {
        if (u.parent == null) {
            root = v;
        } else if (u == u.parent.left) {
            u.parent.left = v;
        } else {
            u.parent.right = v;
        }
        if (v != null) {
            v.parent = u.parent;
        }
    }

    // Find the minimum node of a subtree
    private Node minimum(Node node) {
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }

    private void fixDelete(Node x) {
        while (x != root && isBlack(x)) {
            if (x == parentOf(x).left) {
                Node sibling = siblingOf(x);
                // Case 1: Sibling is RED
                if (sibling.color == Color.RED) {
                    sibling.color = Color.BLACK;
                    parentOf(x).color = Color.RED;
                    rotateLeft(parentOf(x));
                    sibling = siblingOf(x);
                }
                // Case 2: Sibling’s children are both BLACK
                if (isBlack(sibling.left) && isBlack(sibling.right)) {
                    sibling.color = Color.RED;
                    x = parentOf(x);
                } else {
                    // Case 3: Sibling’s left child is RED, right child is BLACK
                    if (isBlack(sibling.right)) {
                        sibling.left.color = Color.BLACK;
                        sibling.color = Color.RED;
                        rotateRight(sibling);
                        sibling = siblingOf(x);
                    }
                    // Case 4: Sibling’s right child is RED
                    sibling.color = parentOf(x).color;
                    parentOf(x).color = Color.BLACK;
                    if (sibling.right != null) sibling.right.color = Color.BLACK;
                    rotateLeft(parentOf(x));
                    x = root;
                }
            } else {
                // Symmetric cases if x is the right child
                Node sibling = siblingOf(x);
                if (sibling.color == Color.RED) {
                    sibling.color = Color.BLACK;
                    parentOf(x).color = Color.RED;
                    rotateRight(parentOf(x));
                    sibling = siblingOf(x);
                }
                if (isBlack(sibling.left) && isBlack(sibling.right)) {
                    sibling.color = Color.RED;
                    x = parentOf(x);
                } else {
                    if (isBlack(sibling.left)) {
                        if (sibling.right != null) sibling.right.color = Color.BLACK;
                        sibling.color = Color.RED;
                        rotateLeft(sibling);
                        sibling = siblingOf(x);
                    }
                    sibling.color = parentOf(x).color;
                    parentOf(x).color = Color.BLACK;
                    if (sibling.left != null) sibling.left.color = Color.BLACK;
                    rotateRight(parentOf(x));
                    x = root;
                }
            }
        }
        if (x != null) x.color = Color.BLACK;
    }

    // ---------------------------------------------------------
    // HELPER: IN-ORDER TRAVERSAL (OPTIONAL)
    // ---------------------------------------------------------
    public void inOrderTraversal() {
        inOrderHelper(root);
        System.out.println();
    }

    private void inOrderHelper(Node node) {
        if (node != null) {
            inOrderHelper(node.left);
            System.out.print("(" + node.key + "," + node.color + ") ");
            inOrderHelper(node.right);
        }
    }

    // ---------------------------------------------------------
    // MAIN METHOD EXAMPLE USAGE (TESTING)
    // ---------------------------------------------------------
    public static void main(String[] args) {
        RedBlackTree tree = new RedBlackTree();
        int[] valuesToInsert = {20, 15, 25, 10, 5, 1, 30};

        for (int val : valuesToInsert) {
            tree.insert(val);
        }

        System.out.println("In-order after insertions:");
        tree.inOrderTraversal();

        // Searching
        int searchKey = 25;
        Node foundNode = tree.search(searchKey);
        if (foundNode != null) {
            System.out.println("Found key: " + foundNode.key);
        } else {
            System.out.println("Key " + searchKey + " not found.");
        }

        // Deleting a key
        int deleteKey = 15;
        System.out.println("Deleting key: " + deleteKey);
        tree.delete(deleteKey);

        System.out.println("In-order after deletion:");
        tree.inOrderTraversal();
    }
}
```

### Explanation of Important Methods

1. **`search(int key)`**: Standard BST search. Repeatedly compares the `key` to the current node’s `key` and travels left or right.
2. **`insert(int key)`**:
   - We first call `bstInsert` to insert the node like a regular BST.
   - Then we call `fixInsert` to recolor and/or rotate nodes if the Red-Black properties are violated.
   - Common fix steps involve checking if the new node’s parent is red and if so, making sure we handle the “uncle” node colors and perform rotations as necessary.
3. **`delete(int key)`**:
   - We find the node using `search`. If it doesn’t exist, we do nothing.
   - Otherwise, we remove it in a BST fashion (if it has two children, replace with its successor).
   - If the node removed (or the node that actually gets transplanted) was black, we need to call `fixDelete` to restore red-black properties.
4. **Rotations (`rotateLeft` and `rotateRight`)**:
   - Rotations are used to rebalance the tree.
   - In a left rotation around node `x`, `x.right` becomes the parent of `x`, and in a right rotation, `x.left` becomes the parent of `x`.

------

## Summary

- **Red-Black Tree** keeps insertion, deletion, and search efficient by maintaining additional color and balancing rules.
- **Color and Rotations**: By assigning red/black colors and performing rotations, the tree ensures that no path is more than twice as long as any other path, giving us good performance.
- **Implementation**: The sample code covers the basic steps. In practice, detailed edge-case handling is crucial, but the patterns of “insert → fixInsert” and “delete → fixDelete” are the core of maintaining Red-Black properties.

This should give you a strong introductory understanding of how Red-Black Trees function, how they maintain balance, and how their primary operations can be implemented in Java.