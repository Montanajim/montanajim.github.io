# Red Black Tree





A **Red-Black Tree** is a type of **self-balancing binary search tree** in computer science. Let’s delve into its fascinating properties:

1. **Structure and Color**:

   - Each node in a Red-Black Tree has an extra bit that represents its color (either **red** or **black**).
   - These color bits are used to ensure that the tree remains approximately balanced during insertions and deletions.
   - The tree’s structure guarantees that operations like searching, insertion, and deletion complete within a known time.

1. **Properties of Red-Black Trees**:

   - **Root Property**: The root node is always black.
   - **External Property**: Every leaf (which is a NULL child of a node) is black.
   - **Internal Property**: The children of a red node are black. Thus, a red node’s possible parent is a black node.
   - **Depth Property**: All leaves have the same black depth.
   - **Path Property**: Every simple path from the root to a descendant leaf node contains the same number of black nodes.

1. **Why Red-Black Trees?**:

   - Most Binary Search Tree (BST) operations (e.g., search, max, min, insert, delete) take O(h) time, where h is the height of the BST.

   - If we ensure that the tree’s height remains O(log n) after every insertion and deletion, we guarantee an upper bound of O(log n) for all these operations.

   - The height of a Red-Black tree is always O(log n), where n is the number of nodes in the tree.

     

## Insertion Process

1. **Initial Setup**:
   - When inserting a new node, it is initially colored **red**.
   - If the tree is empty, the new node becomes the **root** (colored **black**).
   - Otherwise, we insert the node as a **leaf** (colored **red**).
1. **Insertion Algorithm**:
   - Perform a standard **BST insertion** (similar to a regular binary search tree).
   - Color the newly inserted nodes as **RED**.
   - If the newly inserted node is the **root**, change its color to **BLACK** (increasing the black height of the tree by 1).
1. **Balancing Steps**:
   - If the parent of the newly inserted node is not BLACK and the node is not the root :
     - Case 1: If the uncle of the node is RED :
       - Change the color of the parent and uncle to **BLACK**.
       - Change the color of the **grandparent** to **RED**.
       - Repeat steps 2 and 3 for the new **grandparent**.
     - Case 2: If the uncle is BLACK :
       - There are four possible configurations (similar to AVL Tree rotations):
         - **Left Left Case (LL rotation)**
         - **Left Right Case (LR rotation)**
         - **Right Right Case (RR rotation)**
         - **Right Left Case (RL rotation)**
       - After these rotations, re-color according to the rotation case.
1. **Re-coloring after Rotations**:
   - For **Left Left Case** and **Right Right Case**, swap colors of **grandparent** and **parent** after rotations.
   - For **Left Right Case** and **Right Left Case**, swap colors of **grandparent** and **inserted node** after rotations.



## Deletion Process

1. **Initial Setup**:
   - When deleting a node, it can fall into three cases:
     - The node has **no children**: Simply remove it and update the parent node.
     - The node has **one child**: Replace the node with its child.
     - The node has **two children**: Replace the node with its **in-order successor**, which is the leftmost node in the right subtree.
1. **Deletion Algorithm**:
   - Perform a standard **BST delete** operation (similar to regular binary search tree deletion).
   - Color the newly inserted nodes as **RED**.
   - If the deleted node was **BLACK**, we introduce the concept of **double black** (marking the replacement child as double black).
1. **Balancing Steps**:
   - After deletion, the Red-Black Tree properties might be violated.
   - To restore these properties, perform color changes and rotations similar to those during insertion, but with different conditions.
   - The main goal is to convert the **double black** node back to a **single black** node.
   - The cases for restructuring and recoloring are determined by the color of the **sibling** of the double black node.



## RED BLACK Class

```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */


import java.util.Random;

public class RedBlackTree
{

    //An inner nested class can be declared private and only accessed
    //within the class
    //A inner nested class can be declared static and can be accessed
    //from outside the class. 
    //Example in main or other function outside of class
    // RedBlackTree.Node tempNode = new RedBlackTree.Node(); 
    
    static class Node
    {

        int key; // holds the key
        Node parent; // pointer to the parent
        Node left; // pointer to left child
        Node right; // pointer to right child
        int color; // 1 . Red, 0 . Black

        //some data - in this case string
        String sdata;
    }

    private Node root;
    private Node TNULL;

    private void preOrderHelper(Node node)
    {
        if (node != TNULL)
        {
            System.out.print(node.key + " ");
            preOrderHelper(node.left);
            preOrderHelper(node.right);
        }
    }

    private void inOrderHelper(Node node)
    {
        if (node != TNULL)
        {
            inOrderHelper(node.left);
            System.out.print(node.key + " ");
            inOrderHelper(node.right);
        }
    }

    private void postOrderHelper(Node node)
    {
        if (node != TNULL)
        {
            postOrderHelper(node.left);
            postOrderHelper(node.right);
            System.out.print(node.key + " ");
        }
    }

    void preOrder()
    {
        System.out.println("\nPreOder");
        Node node = root;
        if (node != TNULL)
        {
            System.out.print(" **" + node.key + "** ");
            preOrderHelper(node.left);
            preOrderHelper(node.right);
        }
        System.out.println("\n------------------\n");
    }

    // In-Order traversal
    // Left Subtree . Node . Right Subtree
    public void inOrder()
    {
        System.out.println("\ninOder");
        Node node = root;
        if (node != TNULL)
        {
            inOrderHelper(node.left);
            System.out.print(" **" + node.key + "** ");
            inOrderHelper(node.right);
        }
        System.out.println("\n------------------\n");
    }

    // Post-Order traversal
    // Left Subtree . Right Subtree . Node
    public void postOrder()
    {
        System.out.println("\npostOder");
        Node node = root;
        if (node != TNULL)
        {
            postOrderHelper(node.left);
            postOrderHelper(node.right);
            System.out.print(" **" + node.key + "** ");
        }
        System.out.println("\n------------------\n");
    }

    // search the tree for the key k
    // and return the corresponding node
    public Node searchTree(int k)
    {
        return searchTreeHelper(this.root, k);
    }

    private Node searchTreeHelper(Node node, int key)
    {
        if (node == TNULL || key == node.key)
        {
            //if(node == null)

            return node;
        }

        if (key < node.key)
        {
            return searchTreeHelper(node.left, key);
        }
        return searchTreeHelper(node.right, key);
    }

    // fix the rb tree modified by the delete operation
    private void fixDelete(Node x)
    {
        Node s;
        while (x != root && x.color == 0)
        {
            if (x == x.parent.left)
            {
                s = x.parent.right;
                if (s.color == 1)
                {
                    // case 3.1
                    s.color = 0;
                    x.parent.color = 1;
                    leftRotate(x.parent);
                    s = x.parent.right;
                }

                if (s.left.color == 0 && s.right.color == 0)
                {
                    // case 3.2
                    s.color = 1;
                    x = x.parent;
                } else
                {
                    if (s.right.color == 0)
                    {
                        // case 3.3
                        s.left.color = 0;
                        s.color = 1;
                        rightRotate(s);
                        s = x.parent.right;
                    }

                    // case 3.4
                    s.color = x.parent.color;
                    x.parent.color = 0;
                    s.right.color = 0;
                    leftRotate(x.parent);
                    x = root;
                }
            } else
            {
                s = x.parent.left;
                if (s.color == 1)
                {
                    // case 3.1
                    s.color = 0;
                    x.parent.color = 1;
                    rightRotate(x.parent);
                    s = x.parent.left;
                }

                if (s.right.color == 0 && s.right.color == 0)
                {
                    // case 3.2
                    s.color = 1;
                    x = x.parent;
                } else
                {
                    if (s.left.color == 0)
                    {
                        // case 3.3
                        s.right.color = 0;
                        s.color = 1;
                        leftRotate(s);
                        s = x.parent.left;
                    }

                    // case 3.4
                    s.color = x.parent.color;
                    x.parent.color = 0;
                    s.left.color = 0;
                    rightRotate(x.parent);
                    x = root;
                }
            }
        }
        x.color = 0;
    }

    private void rbTransplant(Node u, Node v)
    {
        if (u.parent == null)
        {
            root = v;
        } else if (u == u.parent.left)
        {
            u.parent.left = v;
        } else
        {
            u.parent.right = v;
        }
        v.parent = u.parent;
    }

    private void deleteNodeHelper(Node node, int key)
    {
        // find the node containing key
        Node z = TNULL;
        Node x, y;
        while (node != TNULL)
        {
            if (node.key == key)
            {
                z = node;
            }

            if (node.key <= key)
            {
                node = node.right;
            } else
            {
                node = node.left;
            }
        }

        if (z == TNULL)
        {
            System.out.println("Couldn't find key in the tree");
            return;
        }

        y = z;
        int yOriginalColor = y.color;
        if (z.left == TNULL)
        {
            x = z.right;
            rbTransplant(z, z.right);
        } else if (z.right == TNULL)
        {
            x = z.left;
            rbTransplant(z, z.left);
        } else
        {
            y = minimum(z.right);
            yOriginalColor = y.color;
            x = y.right;
            if (y.parent == z)
            {
                x.parent = y;
            } else
            {
                rbTransplant(y, y.right);
                y.right = z.right;
                y.right.parent = y;
            }

            rbTransplant(z, y);
            y.left = z.left;
            y.left.parent = y;
            y.color = z.color;
        }
        if (yOriginalColor == 0)
        {
            fixDelete(x);
        }
    }

    // fix the red-black tree
    private void fixInsert(Node k)
    {
        Node u;
        while (k.parent.color == 1)
        {
            if (k.parent == k.parent.parent.right)
            {
                u = k.parent.parent.left; // uncle
                if (u.color == 1)
                {
                    // case 3.1
                    u.color = 0;
                    k.parent.color = 0;
                    k.parent.parent.color = 1;
                    k = k.parent.parent;
                } else
                {
                    if (k == k.parent.left)
                    {
                        // case 3.2.2
                        k = k.parent;
                        rightRotate(k);
                    }
                    // case 3.2.1
                    k.parent.color = 0;
                    k.parent.parent.color = 1;
                    leftRotate(k.parent.parent);
                }
            } else
            {
                u = k.parent.parent.right; // uncle

                if (u.color == 1)
                {
                    // mirror case 3.1
                    u.color = 0;
                    k.parent.color = 0;
                    k.parent.parent.color = 1;
                    k = k.parent.parent;
                } else
                {
                    if (k == k.parent.right)
                    {
                        // mirror case 3.2.2
                        k = k.parent;
                        leftRotate(k);
                    }
                    // mirror case 3.2.1
                    k.parent.color = 0;
                    k.parent.parent.color = 1;
                    rightRotate(k.parent.parent);
                }
            }
            if (k == root)
            {
                break;
            }
        }
        root.color = 0;
    }

    private void printHelper(Node root, String indent, boolean last)
    {
        // print the tree structure on the screen
        if (root != TNULL)
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

            String sColor = root.color == 1 ? "RED" : "BLACK";
            System.out.println(root.key + "-" + root.sdata
                    + "(" + sColor + ")");
            printHelper(root.left, indent, false);
            printHelper(root.right, indent, true);
        }
    }

    public RedBlackTree()
    {
        TNULL = new Node();
        TNULL.color = 0;
        TNULL.left = null;
        TNULL.right = null;
        root = TNULL;
    }

    // find the node with the minimum key
    public Node minimum(Node node)
    {
        while (node.left != TNULL)
        {
            node = node.left;
        }
        return node;
    }

    // find the node with the maximum key
    public Node maximum(Node node)
    {
        while (node.right != TNULL)
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
        if (x.right != TNULL)
        {
            return minimum(x.right);
        }

        // else it is the lowest ancestor of x whose
        // left child is also an ancestor of x.
        Node y = x.parent;
        while (y != TNULL && x == y.right)
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
        if (x.left != TNULL)
        {
            return maximum(x.left);
        }

        Node y = x.parent;
        while (y != TNULL && x == y.left)
        {
            x = y;
            y = y.parent;
        }

        return y;
    }

    // rotate left at node x
    public void leftRotate(Node x)
    {
        Node y = x.right;
        x.right = y.left;
        if (y.left != TNULL)
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
    }

    // rotate right at node x
    public void rightRotate(Node x)
    {
        Node y = x.left;
        x.left = y.right;
        if (y.right != TNULL)
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
    }

    // insert the key to the tree in its appropriate position
    // and fix the tree
    public void insert(int key, String sdata)
    {
        // Ordinary Binary Search Insertion
        Node node = new Node();
        node.parent = null;
        node.key = key;

        node.sdata = sdata;

        node.left = TNULL;
        node.right = TNULL;
        node.color = 1; // new node must be red

        Node y = null;
        Node x = this.root;

        while (x != TNULL)
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

        // if new node is a root node, simply return
        if (node.parent == null)
        {
            node.color = 0;
            return;
        }

        // if the grandparent is null, simply return
        if (node.parent.parent == null)
        {
            return;
        }

        // Fix the tree
        fixInsert(node);
    }

    public Node getRoot()
    {
        return this.root;
    }

    // delete the node from the tree
    public void deleteNode(int key)
    {
        deleteNodeHelper(this.root, key);
    }

    // print the tree structure on the screen
    public void prettyPrint()
    {
        printHelper(this.root, "", true);
    }

   // static RedBlackTree bst = new RedBlackTree();

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

