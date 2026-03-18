# Binary Search Tree

## Background Information

A binary search tree (BST) is a special type of binary tree data structure used to efficiently store and access sorted data. It's like a regular tree, but with additional rules that keep everything neatly organized:



**Key features:**

- **Ordering:** Each node in the tree has a value (key), and the key of a node is **always greater than** all the keys in its **left subtree** and **less than** all the keys in its **right subtree**. This creates a sorted order throughout the tree.
- **Efficient searching:** Because of this ordering, you can very quickly search for specific values in the tree. Imagine searching a phone book - you wouldn't start at the very beginning or end, but somewhere in the middle based on the last name. Similarly, in a BST, you can efficiently move left or right depending on the value you're searching for, narrowing down the possibilities with each comparison.
- **Dynamic insertions and deletions:** You can easily add new values (insert) or remove existing ones (delete) from the tree while maintaining the sorted order. The process involves comparing the new value with existing nodes and finding its appropriate place based on the ordering rule.
- **No Duplicates**: Typically, BSTs do **not** allow duplicate values, although variations exist that permit duplicates with specific rules (e.g., storing duplicates in the left or right subtree).



**Benefits of using BSTs:**

- **Fast search:** Searching for elements in a balanced BST takes **logarithmic time** on average, which is significantly faster than searching an unsorted list.
- **Ordered access:** You can easily traverse the tree in sorted order (e.g., for printing all elements in ascending order).
- **Efficient insertions and deletions:** These operations can also be done in logarithmic time in balanced BSTs.



**However, BSTs also have some drawbacks:**

- **Performance depends on balance:** The efficiency of BST operations relies heavily on the tree's balance. An unbalanced tree can perform much worse than a balanced one.
- **Not self-balancing:** By default, BSTs are not self-balancing, meaning insertions and deletions can sometimes lead to imbalances. Special techniques are needed to maintain balance and ensure optimal performance.



Overall, binary search trees are a powerful and versatile data structure for storing and managing sorted data efficiently. They offer fast search, insertion, and deletion operations, making them suitable for various applications like symbol tables, priority queues, and sorting algorithms.





## Lecture Code

```java
/*
 * binary tree
 *
 */
package btreedemoone;

import java.util.Scanner;
import java.util.Stack;

class Node {

    // key
    public int key;

    // data - that's a double	
    public int data;

    // node characteristics
    public Node leftChild;
    public Node rightChild;

    public Node(int key, int data) {
        this.key = key;
        this.data = data;
    }

    // display node
    public void displayNode() {
        System.out.print("{" + key + "," + data + "}");
    }

}// end of node

class Tree {

    private Node root;
    static Scanner myScan = new Scanner(System.in);

    public Tree() {
        root = null;
    }

    public void insert(int key, int data) {
        // newNode
        Node newNode = new Node(key, data);
        boolean run = true;

        if (root == null) {
            root = newNode;
        } else {
            Node current = root;
            Node parent;

            while (run) {
                parent = current;

                if (key < current.key) //go left
                {
                    current = current.leftChild;

                    if (current == null) {
                        parent.leftChild = newNode;
                        run = false;
                    }
                } else // go right
                {
                    current = current.rightChild;

                    if (current == null) {
                        parent.rightChild = newNode;
                        run = false;
                    }
                }
            }

        }

    }// end of insert

    public Node find(int key) {

        Node current = root;

        // check if empty
        if (root == null) {
            System.out.println("** Tree is empty **");
            return null;
        }

        while (current.key != key) {

            if (key < current.key) // go left?
            {
                current = current.leftChild;
            } else // go right
            {
                current = current.rightChild;
            }

            if (current == null) {
                System.out.println("*** key not found ***");
                return null;
            }
        }

        System.out.println("Key was FOUND");
        return current;
    }

    public boolean delete(int key) {
        Node current = root;
        Node parent = root;
        boolean isLeftChild = true;

        //check if empty
        if (root == null) {
            System.out.println("*** Tree is empty ***");
            return false;
        }

        // look for the key
        while (current.key != key) {
            parent = current;

            if (key < current.key) // go left?
            {
                isLeftChild = true;
                current = current.leftChild;
            } else // go right
            {
                isLeftChild = false;
                current = current.rightChild;
            }

            if (current == null) {
                System.out.println("*** key not found ***");
                return false;
            }

        }// end while

        // found we are on the node to delete
        // if there is no children - simply delete the node
        if (current.leftChild == null && current.rightChild == null) {
            //check if node is the root (there is only one node in tree)
            if (current == root) {
                root = null;
            } else if (isLeftChild) {
                parent.leftChild = null;
            } else {
                parent.rightChild = null;
            }
        } // if no right child, rplace with left subtree
        else if (current.rightChild == null) {
            if (current == root) {
                root = current.leftChild;
            } else if (isLeftChild) {
                parent.leftChild = current.leftChild;
            } else {
                parent.rightChild = current.leftChild;
            }
        } //if no left child, replace with right subtree
        else if (current.leftChild == null) {
            if (current == root) {
                root = current.rightChild;
            } else if (isLeftChild) {
                parent.leftChild = current.rightChild;
            } else {
                parent.rightChild = current.rightChild;
            }
        } // if there are two children, replace with inorder successor
        else {
            //get successor of node to delete of current
            Node successor = getSuccessor(current);

            // connect parent of current to successor instead
            if (current == root) {
                root = successor;
            } else if (isLeftChild) {
                parent.leftChild = successor;
            } else {
                parent.rightChild = successor;
            }

            // connect successor to current's left child
            successor.leftChild = current.leftChild;

            // NOTE: successor cannot have a left child
        }

        return true;

    }

    // return node with the next highest value after the delete node
    // goes to right child, then right child's lef descendent's
    private Node getSuccessor(Node deleteNode) {
        Node successorParent = deleteNode;
        Node successor = deleteNode;
        Node current = deleteNode.rightChild;

        while (current != null) {
            successorParent = successor;
            successor = current;
            current = current.leftChild;
        }

        // if successor not successful
        if (successor != deleteNode.rightChild) {
            successorParent.leftChild = successor.rightChild;
            successor.rightChild = deleteNode.rightChild;
        }

        return successor;
    }

    public void traverse2() {

        System.out.print("\nPreorder Traversal: ");
        preorder(root);

        System.out.print("\nInorder Traversal: ");
        inorder(root);

        System.out.print("\nPostorder Traversal: ");
        postorder(root);

    }

    private void preorder(Node nodeStart) {
        if (nodeStart != null) {
            System.out.print(nodeStart.key + " ");
            preorder(nodeStart.leftChild);
            preorder(nodeStart.rightChild);
        }
    }

    private void inorder(Node nodeStart) {
        if (nodeStart != null) {
            inorder(nodeStart.leftChild);
            System.out.print(nodeStart.key + " ");
            inorder(nodeStart.rightChild);
        }
    }

    private void postorder(Node nodeStart) {
        if (nodeStart != null) {
            postorder(nodeStart.leftChild);
            postorder(nodeStart.rightChild);
            System.out.print(nodeStart.key + " ");
        }
    }

    public void displayTree() {
        Stack globalStack = new Stack();
        globalStack.push(root);

        int nBlanks = 32;

        boolean isRowEmpty = false;

        System.out.println(
                "\n..........         Display Tree     ..........................");

        while (!isRowEmpty) {
            Stack localStack = new Stack();
            isRowEmpty = true;

            for (int j = 0; j < nBlanks; j++) {
                System.out.print(" ");
            }

            while (globalStack.isEmpty() == false) {
                Node temp = (Node) globalStack.pop();
                if (temp != null) {
                    System.out.print(temp.data);
                    localStack.push(temp.leftChild);
                    localStack.push(temp.rightChild);

                    if (temp.leftChild != null || temp.rightChild != null) {
                        isRowEmpty = false;
                    }
                } else {
                    System.out.print("--");
                    localStack.push(null);
                    localStack.push(null);
                }

                for (int j = 0; j < nBlanks * 2 - 2; j++) {
                    System.out.print(' ');
                }
            }//while

            System.out.println();
            nBlanks /= 2;
            while (localStack.isEmpty() == false) {
                globalStack.push(localStack.pop());
            }
        }
        // for separation
        System.out.println("---------------------------");
    } // display tree

}

public class BTreeDemoOne {

    static Scanner myScan = new Scanner(System.in);

    public static void main(String[] args) {

        String quit = "n";

        int findValue = 0;
        int deleteValue = 0;
        int insertValue = 0;
        
        boolean result = false;

        Tree theTree = new Tree();

        while (!quit.equals("y")) {
            theTree.insert(50, 50);
            theTree.insert(25, 25);
            theTree.insert(75, 75);
            theTree.insert(12, 12);
            theTree.insert(37, 37);
            theTree.insert(43, 43);
            theTree.insert(30, 30);
            theTree.insert(33, 33);
            theTree.insert(87, 87);
            theTree.insert(93, 93);
            theTree.insert(97, 97);
            theTree.insert(70, 70);
            theTree.insert(60, 60);

            theTree.displayTree();

            theTree.insert(85, 85);
            theTree.insert(47, 47);
            

            theTree.displayTree();

            try {
                System.out.print("Enter an integer to insert "
                        + "or letter to skip: ");
                insertValue = Integer.parseInt(myScan.nextLine());
                theTree.insert(insertValue, insertValue);
                theTree.displayTree();
                
            } catch (Exception e) {
            }
            
            
            theTree.traverse2();
            try {
                
                System.out.print("\nEnter Value To Find or letter to skip: ");
                findValue = Integer.parseInt(myScan.nextLine());
                theTree.find(findValue);

            
                System.out.println("\nEnter value to delete: ");
                deleteValue = Integer.parseInt(myScan.nextLine());

                if (theTree.delete(deleteValue)) {
                    theTree.displayTree();
                } else {
                    System.out.println("NOT FOUND");
                }
            } catch (Exception e) {
            }

            System.out.print("Would you like to quit y/n: ");
            quit = myScan.nextLine().toLowerCase();

        }

        System.out.println("\nbye\n");
    }

}

```



BST as Class

```java
/*
    Change the package to your specific package
 */
package ds_redblacktree_rev2_separateclass;

import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

/**
 *
 * @author jgoudy
 */
public class BinaryTreeSearch
{

    class Node
    {

        int key;
        Node left;
        Node right;
        
        

        Node(int key)
        {
            this.key = key;
            right = null;
            left = null;
        }
    }

    Node root;
    public int trip = 0;

    public void add(int key)
    {
        root = addRecursive(root, key);
    }

    private Node addRecursive(Node current, int key)
    {

        if (current == null)
        {
            return new Node(key);
        }

        if (key < current.key)
        {
            current.left = addRecursive(current.left, key);
        } else if (key > current.key)
        {
            current.right = addRecursive(current.right, key);
        }

        return current;
    }

    public boolean isEmpty()
    {
        return root == null;
    }

    public int getSize()
    {
        return getSizeRecursive(root);
    }

    private int getSizeRecursive(Node current)
    {
        return current == null ? 0 : getSizeRecursive(current.left)
                + 1 + getSizeRecursive(current.right);
    }

    public boolean containsNode(int key)
    {
        trip = 0;
        return containsNodeRecursive(root, key);
    }

    private boolean containsNodeRecursive(Node current, int key)
    {
        if (current == null)
        {
            return false;
        }
        trip++;
        if (key == current.key)
        {
            return true;
        }

        return key < current.key
                ? containsNodeRecursive(current.left, key)
                : containsNodeRecursive(current.right, key);
    }

    public void delete(int key)
    {
        root = deleteRecursive(root, key);
    }

    private Node deleteRecursive(Node current, int key)
    {
        if (current == null)
        {
            return null;
        }

        if (key == current.key)
        {
            // Case 1: no children
            if (current.left == null && current.right == null)
            {
                return null;
            }

            // Case 2: only 1 child
            if (current.right == null)
            {
                return current.left;
            }

            if (current.left == null)
            {
                return current.right;
            }

            // Case 3: 2 children
            int smallestValue = findSmallestValue(current.right);
            current.key = smallestValue;
            current.right = deleteRecursive(current.right, smallestValue);
            return current;
        }
        if (key < current.key)
        {
            current.left = deleteRecursive(current.left, key);
            return current;
        }

        current.right = deleteRecursive(current.right, key);
        return current;
    }

    public int findSmallestValue(Node root)
    {
        return root.left == null ? root.key : findSmallestValue(root.left);
    }

    public int findLargestValue(Node root)
    {
        return root.left == null ? root.key : findLargestValue(root.right);
    }

    public void traverseInOrder(Node node)
    {
        if (node != null)
        {
            traverseInOrder(node.left);
            visit(node.key);
            traverseInOrder(node.right);
        }
    }

    public void traversePreOrder(Node node)
    {
        if (node != null)
        {
            visit(node.key);
            traversePreOrder(node.left);
            traversePreOrder(node.right);
        }
    }

    public void traversePostOrder(Node node)
    {
        if (node != null)
        {
            traversePostOrder(node.left);
            traversePostOrder(node.right);
            visit(node.key);
        }
    }

    public void traverseLevelOrder()
    {
        if (root == null)
        {
            return;
        }

        Queue<Node> nodes = new LinkedList<>();
        nodes.add(root);

        while (!nodes.isEmpty())
        {

            Node node = nodes.remove();

            System.out.print(" " + node.key);

            if (node.left != null)
            {
                nodes.add(node.left);
            }

            if (node.left != null)
            {
                nodes.add(node.right);
            }
        }
    }

    public void traverseInOrderWithoutRecursion()
    {
        Stack<Node> stack = new Stack<Node>();
        Node current = root;
        stack.push(root);
        while (!stack.isEmpty())
        {
            while (current.left != null)
            {
                current = current.left;
                stack.push(current);
            }
            current = stack.pop();
            visit(current.key);
            if (current.right != null)
            {
                current = current.right;
                stack.push(current);
            }
        }
    }

    public void traversePreOrderWithoutRecursion()
    {
        Stack<Node> stack = new Stack<Node>();
        Node current = root;
        stack.push(root);
        while (!stack.isEmpty())
        {
            current = stack.pop();
            visit(current.key);

            if (current.right != null)
            {
                stack.push(current.right);
            }

            if (current.left != null)
            {
                stack.push(current.left);
            }
        }
    }

    public void traversePostOrderWithoutRecursion()
    {
        Stack<Node> stack = new Stack<Node>();
        Node prev = root;
        Node current = root;
        stack.push(root);

        while (!stack.isEmpty())
        {
            current = stack.peek();
            boolean hasChild = (current.left != null || current.right != null);
            boolean isPrevLastChild = (prev == current.right
                    || (prev == current.left && current.right == null));

            if (!hasChild || isPrevLastChild)
            {
                current = stack.pop();
                visit(current.key);
                prev = current;
            } else
            {
                if (current.right != null)
                {
                    stack.push(current.right);
                }
                if (current.left != null)
                {
                    stack.push(current.left);
                }
            }
        }
    }

    private void visit(int key)
    {
        System.out.print(" " + key);
    }

}

```

