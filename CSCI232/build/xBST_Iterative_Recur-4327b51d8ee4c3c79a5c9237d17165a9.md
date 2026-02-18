# Demonstrate BST using iterative looping and recursion



This Java program implements a **Binary Search Tree (BST)** that supports insertion, searching, and in-order traversal. It generates unique random numbers, inserts them into the BST, and allows the user to search for a specific number using both recursive and iterative approaches.

The **`Node` class** defines a BST node with an integer value and left and right child references. The **`BST` class** manages the BST operations, including inserting new values, searching for values recursively and iteratively, and performing an in-order traversal to display elements in sorted order.

In the **main method (`BST_Recursion_Loops`)**, the program first generates an array of 50 unique random numbers using a `HashSet`, ensuring all values are distinct. These numbers are inserted into the BST, and an in-order traversal is performed to display the sorted tree contents. The program then prompts the user to enter a search key and performs both iterative and recursive searches to check for its presence, displaying whether the key was found or not.

This implementation highlights key BST operations and provides a practical demonstration of recursion, loops, and tree traversal techniques in Java.

---

## HashSet

A HashSet in Java is a part of the java.util package and implements 
the Set interface. It is used to store a collection of unique elements, 
meaning it does not allow duplicate values. It is backed by a HashMap, 
which makes its operations fast, typically running in O(1) time complexity 
for basic operations like add, remove, and contains.
Key Features of HashSet

    No Duplicates –         It does not allow duplicate elements.
    Unordered Collection –  It does not maintain the order of elements.
    Allows Null Values –    It permits a single null value.
    Fast Operations –       Add, remove, and search operations are 
                            generally O(1) due to hashing.
    No Indexing –           Unlike lists,you cannot access elements by an index.



## Demo Code

```java
/*

Demonstrate iterative and recursive searching
Developer: James Goudy
 */
package bst_recursion_loops;

import java.util.HashSet;
import java.util.Random;
import java.util.Scanner;
import org.w3c.dom.css.Counter;

// Class for a Binary Search Tree Node
class Node {

    int value;
    Node left, right;

    public Node(int item) {
        value = item;
        left = right = null;
    }
}

class BST {

    int cntr = 1;
    Node root;

    // Constructor
    public BST() {
        root = null;
    }

    // Recursive Search Function
    public boolean searchRecursive(Node root, int key) {
        // Base case: root is null or key is found
        if (root == null) {
            return false;
        }
        if (root.value == key) {
            return true;
        }

        // If the key is smaller, search in the left subtree
        if (key < root.value) {
            return searchRecursive(root.left, key);
        } else {
            // If the key is larger, search in the right subtree
            return searchRecursive(root.right, key);
        }
    }

    // Iterative Search Function
    public boolean searchIterative(Node root, int key) {
        while (root != null) {
            if (root.value == key) {
                return true;
            } else if (key < root.value) {
                root = root.left;  // Move to left subtree
            } else {
                root = root.right; // Move to right subtree
            }
        }
        return false; // Key not found
    }

    // Insert function to add nodes to the BST
    public void insert(int key) {
        root = insertData(root, key);
    }

    private Node insertData(Node root, int key) {
        if (root == null) {
            root = new Node(key);
            return root;
        }

        if (key < root.value) {
            root.left = insertData(root.left, key);
        } else if (key > root.value) {
            root.right = insertData(root.right, key);
        }

        return root;
    }

    // Helper function to start recursive search from the root
    public boolean searchRecursive(int key) {
        return searchRecursive(root, key);
    }

    // Helper function to start iterative search from the root
    public boolean searchIterative(int key) {
        return searchIterative(root, key);
    }

    // Inorder Traversal to print the BST
    public void inorder() {
        cntr = 1;
        inorderData(root);
        System.out.println();
    }

    private void inorderData(Node root) {

        if (root != null) {
            cntr++;

            if (cntr % 10 == 0 && cntr > 1) {
                System.out.println("");
            }

            

            inorderData(root.left);
            System.out.print(root.value + " ");
            inorderData(root.right);

        }

    }

}

public class BST_Recursion_Loops {

    public static int[] generateUniqueArray(int size) {

        // create new HashSet
        HashSet<Integer> uniqueNumbers = new HashSet<>();

        Random rng = new Random();

        // Fill the set with unique random numbers
        while (uniqueNumbers.size() < size) {
            // Generates numbers from 0 to 999
            uniqueNumbers.add(rng.nextInt(1000));
        }

        // Convert HashSet to an array
        int[] result = new int[size];
        int index = 0;
        for (int num : uniqueNumbers) {
            result[index++] = num;
        }

        return result;
    }

    public static void main(String[] args) {

        // create sample data
        int[] sampleKeys;
        int numOfKeys = 50;
        int searchKey = 0;
        String status;
        
        
        
        Scanner myScan = new Scanner(System.in);
        BST myBST = new BST();

        sampleKeys = generateUniqueArray(numOfKeys);

        System.out.println("\nInput Data\n");
        for (int i = 0; i < sampleKeys.length; i++) {
            myBST.insert(sampleKeys[i]);
            System.out.print(sampleKeys[i] + " ");

            if (i % 10 == 0 && i > 0) {
                System.out.println("");
            }
        }

        System.out.println("\n-----------------------------\n");

        myBST.inorder();
        
        System.out.print(" Enter Search Key: ");
        searchKey = Integer.parseInt(myScan.nextLine());
        
        System.out.println("\nSearch Iteratively");
        status = myBST.searchIterative(searchKey)? "Found" : "Not Found";
        System.out.println("The items was - " + status);
        
        System.out.println("\nSearch Recursively");
        status = myBST.searchRecursive(searchKey)? "Found" : "Not Found";
        System.out.println("The items was - " + status);
        

    }

}
```

