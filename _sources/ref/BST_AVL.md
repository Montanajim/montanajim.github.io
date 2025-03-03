# AVL Binary Search Tree



The AVL binary search tree is named after its inventors, *Georgy Adelson-Velsky* and *Evgenii Landis*. Their names are combined to form the acronym "AVL". They introduced the data structure in their 1962 paper "An algorithm for the organization of information".



**Key Concepts:**

- **Self-balancing Binary Search Tree (BST):** A specialized BST that maintains a height difference of at most 1 between its left and right subtrees for every node. This ensures efficient search, insertion, and deletion operations with a time complexity of O(log n).

- **Balance Factor:** The difference between the heights of a node's left and right subtrees (left height - right height). It's used to determine if a node is imbalanced and requires rebalancing.

- **Tree Rotations:**

   Operations used to restore balance in an AVL tree after insertions or deletions.

   There are four types:

  - **Left Rotation:** Pivots a node to the left, making its right child the new root.
  - **Right Rotation:** Pivots a node to the right, making its left child the new root.
  - **Left-Right Rotation:** A left rotation followed by a right rotation.
  - **Right-Left Rotation:** A right rotation followed by a left rotation.



**Key Properties:**

- **Height Balance:** The height difference between subtrees is always -1, 0, or 1.
- **Average Case Time Complexity:** O(log n) for search, insertion, and deletion.
- **Worst Case Time Complexity:** O(log n) for search, insertion, and deletion (due to rebalancing).



**Advantages:**

- **Fast operations:** Efficient for search, insertion, and deletion due to the balanced structure.
- **Guaranteed logarithmic time complexity:** Ensures predictable performance even in worst-case scenarios.



**Disadvantages:**

- **Rebalancing overhead:** Rotations can add some overhead to insertions and deletions, making them slightly slower than simple BSTs in some cases.
- **Implementation complexity:** More complex to implement than simple BSTs due to the rebalancing logic.



**Common Use Cases:**

- Database applications
- File systems
- Network routing
- Memory management
- Caching algorithms



**Additional Notes:**

- AVL trees are often compared to Red-Black trees, another self-balancing BST. While AVL trees maintain stricter balance, Red-Black trees have slightly faster insertion and deletion in some cases.



**Left Tree Rotations**

- To restore balance in an AVL tree when a node's **balance factor** becomes **-2** (meaning its right subtree is two levels taller than its left subtree).
- This imbalance usually occurs after an insertion in the right subtree of the right child.

**Steps:**

1. **Identify Imbalance:** Find the imbalanced node (balance factor -2).
1. **Pivot Node:** The imbalanced node becomes the pivot point for the rotation.
1. **New Subtree:** The pivot node's right child becomes the new root of the subtree.
1. Link Adjustments:
   - The pivot node's right child's left subtree becomes the pivot node's new right subtree.
   - The parent of the pivot node (if any) is updated to point to the new root.



**Right Tree Rotations**

- To restore balance in an AVL tree when a node's **balance factor** becomes **+2** (meaning its left subtree is two levels taller than its right subtree).
- This imbalance usually occurs after an insertion in the left subtree of the left child.



**Steps:**

1. **Identify Imbalance:** Find the imbalanced node (balance factor +2).
1. **Pivot Node:** The imbalanced node becomes the pivot point for the rotation.
1. **New Subtree:** The pivot node's left child becomes the new root of the subtree.
1. Link Adjustments:
   - The pivot node's left child's right subtree becomes the pivot node's new left subtree.
   - The parent of the pivot node (if any) is updated to point to the new root.



**Algorithm Code**

```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

import java.util.Random;

/**
 *
 * @author jgoudy
 */
// AVL Binary search tree implementation in Java
// Author: AlgorithmTutor 
// Modifed by James Goudy
//https://algorithmtutor.com/Data-Structures/Tree/AVL-Trees/
// key structure that represents a node in the tree
public class AVL
{

    private Node root;

    //An inner nested class can be declared private and only accessed
    //within the class
    //A inner nested class can be declared static and can be accessed
    //from outside the class. 
    //Example in main or other function outside of class
    // RedBlackTree.Node tempNode = new RedBlackTree.Node(); 
    //inner nested class
    static class Node
    {

        int key; // holds the key
        Node parent; // pointer to the parent
        Node left; // pointer to left child
        Node right; // pointer to right child
        int bf; // balance factor of the node

        //some data - in this case string
        String sdata;

        //public Node(int key, String sdata)
        public Node()
        {
            this.key = 0;
            this.parent = null;
            this.left = null;
            this.right = null;
            this.bf = 0;
            this.sdata = "";
        }

        public Node(int key, String sdata)

        {
            this.key = key;
            this.parent = null;
            this.left = null;
            this.right = null;
            this.bf = 0;
            this.sdata = sdata;
        }

    }

    //constructor
    public AVL()
    {
        root = null;

    }

    private void printHelper(Node currPtr, String indent, boolean last)
    {
        // print the tree structure on the screen
        if (currPtr != null)
        {
            System.out.print(indent);
            if (last)
            {
                System.out.print("R----");
                indent += "     ";
            } else
            {
                System.out.print("L----");
                indent += "|    ";
            }

            System.out.println(currPtr.key + "-" + currPtr.sdata
                    + "(BF = " + currPtr.bf + ")");

            printHelper(currPtr.left, indent, false);
            printHelper(currPtr.right, indent, true);
        }
    }

    // search the tree for the key k
    // and return the corresponding node
    public Node searchTree(int k)
    {
        return searchTreeHelper(this.root, k);
    }

    private Node searchTreeHelper(Node node, int key)
    {
        if (node == null || key == node.key)
        {
            return node;
        }

        if (key < node.key)
        {
            return searchTreeHelper(node.left, key);
        }
        return searchTreeHelper(node.right, key);
    }

    private Node deleteNodeHelper(Node node, int key)
    {
        // search the key
        if (node == null)
        {
            return node;
        } else if (key < node.key)
        {
            node.left = deleteNodeHelper(node.left, key);
        } else if (key > node.key)
        {
            node.right = deleteNodeHelper(node.right, key);
        } else
        {
            // the key has been found, now delete it

            // case 1: node is a leaf node
            if (node.left == null && node.right == null)
            {
                node = null;
            } // case 2: node has only one child
            else if (node.left == null)
            {
                Node temp = node;
                node = node.right;
            } else if (node.right == null)
            {
                Node temp = node;
                node = node.left;
            } // case 3: has both children
            else
            {
                Node temp = minimum(node.right);
                node.key = temp.key;
                node.right = deleteNodeHelper(node.right, temp.key);
            }

        }

        // Write the update balance logic here 
        // YOUR CODE HERE
        return node;
    }

    // update the balance factor the node
    private void updateBalance(Node node)
    {
        if (node.bf < -1 || node.bf > 1)
        {
            rebalance(node);
            return;
        }

        if (node.parent != null)
        {
            if (node == node.parent.left)
            {
                node.parent.bf -= 1;
            }

            if (node == node.parent.right)
            {
                node.parent.bf += 1;
            }

            if (node.parent.bf != 0)
            {
                updateBalance(node.parent);
            }
        }
    }

    // rebalance the tree
    void rebalance(Node node)
    {
        if (node.bf > 0)
        {
            if (node.right.bf < 0)
            {
                rightRotate(node.right);
                leftRotate(node);
            } else
            {
                leftRotate(node);
            }
        } else if (node.bf < 0)
        {
            if (node.left.bf > 0)
            {
                leftRotate(node.left);
                rightRotate(node);
            } else
            {
                rightRotate(node);
            }
        }
    }

    private void preOrderHelper(Node node)
    {
        if (node != null)
        {
            System.out.print(node.key + " ");
            preOrderHelper(node.left);
            preOrderHelper(node.right);
        }
    }

    private void inOrderHelper(Node node)
    {
        if (node != null)
        {
            inOrderHelper(node.left);
            System.out.print(node.key + " ");
            inOrderHelper(node.right);
        }
    }

    private void postOrderHelper(Node node)
    {
        if (node != null)
        {
            postOrderHelper(node.left);
            postOrderHelper(node.right);
            System.out.print(node.key + " ");
        }
    }

    // Pre-Order traversal
    // Node.Left Subtree.Right Subtree
    public void preOrder()
    {
        preOrderHelper(this.root);
    }

    // In-Order traversal
    // Left Subtree . Node . Right Subtree
    public void inOrder()
    {
        inOrderHelper(this.root);
    }

    // Post-Order traversal
    // Left Subtree . Right Subtree . Node
    public void postOrder()
    {
        postOrderHelper(this.root);
    }

    // find the node with the minimum key
    public Node minimum(Node node)
    {
        while (node.left != null)
        {
            node = node.left;
        }
        return node;
    }

    // find the node with the maximum key
    public Node maximum(Node node)
    {
        while (node.right != null)
        {
            node = node.right;
        }
        return node;
    }

    // find the successor of a given node
    public Node successor(Node x)
    {
        // if the right subtree is not null,
        // the successor is the leftmost node in the
        // right subtree
        if (x.right != null)
        {
            return minimum(x.right);
        }

        // else it is the lowest ancestor of x whose
        // left child is also an ancestor of x.
        Node y = x.parent;
        while (y != null && x == y.right)
        {
            x = y;
            y = y.parent;
        }
        return y;
    }

    // find the predecessor of a given node
    public Node predecessor(Node x)
    {
        // if the left subtree is not null,
        // the predecessor is the rightmost node in the 
        // left subtree
        if (x.left != null)
        {
            return maximum(x.left);
        }

        Node y = x.parent;
        while (y != null && x == y.left)
        {
            x = y;
            y = y.parent;
        }

        return y;
    }

    // rotate left at node x
    void leftRotate(Node x)
    {
        Node y = x.right;
        x.right = y.left;
        if (y.left != null)
        {
            y.left.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null)
        {
            this.root = y;
        } else if (x == x.parent.left)
        {
            x.parent.left = y;
        } else
        {
            x.parent.right = y;
        }
        y.left = x;
        x.parent = y;

        // update the balance factor
        x.bf = x.bf - 1 - Math.max(0, y.bf);
        y.bf = y.bf - 1 + Math.min(0, x.bf);
    }

    // rotate right at node x
    void rightRotate(Node x)
    {
        Node y = x.left;
        x.left = y.right;
        if (y.right != null)
        {
            y.right.parent = x;
        }
        y.parent = x.parent;
        if (x.parent == null)
        {
            this.root = y;
        } else if (x == x.parent.right)
        {
            x.parent.right = y;
        } else
        {
            x.parent.left = y;
        }
        y.right = x;
        x.parent = y;

        // update the balance factor
        x.bf = x.bf + 1 - Math.min(0, y.bf);
        y.bf = y.bf + 1 + Math.max(0, x.bf);
    }

    // insert the key to the tree in its appropriate position
    public void insert(int key, String sdata)
    {
        // PART 1: Ordinary BST insert
        Node node = new Node(key, sdata);
        Node y = null;
        Node x = this.root;

        while (x != null)
        {
            y = x;
            if (node.key < x.key)
            {
                x = x.left;
            } else
            {
                x = x.right;
            }
        }

        // y is parent of x
        node.parent = y;
        if (y == null)
        {
            root = node;
        } else if (node.key < y.key)
        {
            y.left = node;
        } else
        {
            y.right = node;
        }

        // PART 2: re-balance the node if necessary
        updateBalance(node);
    }

    // delete the node from the tree
    Node deleteNode(int key)
    {
        return deleteNodeHelper(this.root, key);
    }

    // print the tree structure on the screen
    public void prettyPrint()
    {
        printHelper(this.root, "", true);
    }

    void insertRandom()
    {
        int amt = 12;
        int amts = 5;
        int amtNodes, amtLetters;
        int[] keys;

        int selectKey = -1;
        int selectIndex = -1;
        boolean run = true;

        String numberOrder = "";
        int numberOrderCount = 0;

        Random RNG = new Random();
        amtNodes = RNG.nextInt(amt);
        //amtNodes = 15; //hard code the amount 
        amtLetters = 3;

        System.out.println(amtNodes);
        keys = new int[amtNodes];

        //load keys
        for (int i = 0; i < keys.length; i++)
        {
            keys[i] = i;
        }

        for (int i = 0; i < amtNodes; i++)
        {
            //create random letter patterns
            String ld = "";
            for (int j = 0; j < amtLetters; j++)
            {
                ld = ld + (char) (RNG.nextInt(25) + 65);
            }

            //pick random key
            int cntr = 0;
            selectIndex = RNG.nextInt(amtNodes);

            selectKey = keys[selectIndex];
            run = true;
            while (run)
            {

                if (selectKey > -1)
                {
                    run = false;
                } else
                {
                    selectIndex = selectIndex + 1;
                    if (selectIndex >= amtNodes)
                    {
                        selectIndex = 0;
                    }

                }
                selectKey = keys[selectIndex];

            }
            //System.out.print(selectKey + " ");

            numberOrder = numberOrder + selectKey + " ";
            numberOrderCount++;
            if (numberOrderCount > 20)
            {
                numberOrder = numberOrder + "\n";
                numberOrderCount = 0;

            }

            insert(selectKey, ld);
            keys[selectKey] = -1;
        }
        System.out.println("\n" + numberOrder + "\n");
        System.out.println("");

    }

}

```





