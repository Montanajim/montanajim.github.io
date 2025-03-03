# Skip List



## Introduction

Skip lists are a powerful data structure that offer efficient search and insertion operations on sorted data. They achieve this by combining the simplicity of linked lists with the efficiency of jump searches. Here's a deeper dive into their inner workings:

**Structure:**

- **Levels:** A skip list is made up of multiple levels, with Level 0 being the bottommost level and acting as a standard sorted linked list. Higher levels contain fewer elements and serve as shortcuts to navigate the data faster.

- Nodes:

   

  Each element in the skip list is stored in a node. A node typically contains the element's value and pointers:

  - **Forward Pointers:** These point to the next element in the same level, maintaining the sorted order within each level.
  - **Shortcut Pointers (Optional):** These pointers "jump" over some elements in the level below, allowing for faster traversal during search and insertion.

**Random Height Assignment:**

- A crucial aspect of skip lists is the random height assigned to each element. This randomness is what gives them their probabilistic nature.
- A coin-flipping approach (or any other random number generation) is used to determine the height. Higher levels have fewer elements because the chance of a successful coin flip (reaching a higher level) decreases with each level.

**Searching in a Skip List:**

1. Start at the highest level (Level 3 in the 4-level example).
1. Compare the search value with the current element's value.
1. If the search value is less, move to the previous element using the forward pointer in the current level.
1. If the search value is greater and there's a shortcut pointer available, use it to jump several elements ahead in the level below (Level 2).
1. Repeat steps 2-4 until you either find the element or reach the end of the level.
1. If you haven't found it yet, move down to Level 1 and repeat the process (compare, move, jump using shortcuts if available).
1. Finally, search the bottom level (Level 0) using the standard linked list traversal.

**Benefits:**

- **Average Search Time (O(log n)):** Due to the shortcut pointers, searching a skip list on average takes logarithmic time (O(log n)), where n is the number of elements. This is significantly faster than a linear search (O(n)) in a standard linked list.
- **Efficient Insertions:** Similar to searching, insertions also benefit from the layered structure. By efficiently navigating through the levels, the element can be inserted in its correct sorted position.
- **Simpler than Balanced Trees:** Compared to balanced search trees (e.g., AVL trees), skip lists are easier to implement and have lower memory overhead.

**Drawbacks:**

- **Probabilistic:** The random height assignment makes skip lists probabilistic. While the average performance is excellent, there's a small chance of the worst-case scenario (O(n)) happening in search or insertion.
- **Space Overhead:** The shortcut pointers add some extra space compared to a regular linked list.

**Overall, skip lists offer a compelling balance between simplicity and efficiency for maintaining sorted data. They are a powerful alternative to balanced search trees in situations where the slight possibility of a worst-case scenario is acceptable.**



## Skiplist Diagram

Here's a diagram of a skip list with 4 levels:

```
         Level 3  ->  80  ->  ...
                     ^
                     |
        Level 2  ->  40  ->  60  ->  ...
                     ^         ^         ^
                     |         |         |
        Level 1  ->  20  ->  30  ->  50  ->  ...
                     ^         ^         ^         ^
                     |         |         |         |  
Level 0 (Bottom) ->  5  ->  10  ->  15  ->  25  ->  35
```

Explanation:

- This diagram shows a skip list with four levels (Level 0, Level 1, Level 2, Level 3).

- Similar to the previous diagram, Level 0 is the bottommost sorted linked list.

- Elements have values and pointers. Solid arrows show pointers to the next element in the same level. Dashed arrows represent shortcut pointers that jump over elements in the lower level.

- In this example:
  - Elements 5, 10, 15, 25, and 35 only appear in Level 0.
  - Elements 20, 30, and 50 have a level of 1 (one shortcut pointer).
  - Elements 40 and 60 have a level of 2 (two shortcut pointers).
  - Element 80 has the highest level (3) with three shortcut pointers, skipping all elements in the lower levels.
  
  



## Lecture code explaination



Skip Lists are a probabilistic alternative to traditional sorted linked lists. They achieve faster search times by utilizing a linked list structure with multiple layers (levels).

Here's a breakdown of the code:

### Classes:

- `Node`: This class represents a single node in the SkipList. It has two properties:
  - `key`: An integer value representing the data stored in the node.
  - `forward`: An array of pointers to other nodes. The length of this array determines the level of the node in the SkipList.
  
- `SkipList`: This class implements the SkipList data structure. It has several properties and methods:
  - `maxLevel`: An integer specifying the maximum level allowed in the SkipList.
  - `P`: A double value between 0 and 1 representing the probability of adding a new level when inserting a node.
  - `level`: An integer representing the current highest level in the SkipList.
  - `head`: A pointer to the head node of the SkipList. This node has a special key value (usually -1) and forward pointers for all possible levels.
  
  

### Methods:



#### Helper Methods

- `randomLevel()`: This function generates a random integer value between 1 and `maxLevel` that determines the level of a new node being inserted. It uses the `P` value to simulate a coin toss. With a higher `P`, there's a greater chance of getting a higher level.
- `createNode(int key, int level)`: This function creates a new `Node` object with the specified `key` and `level`.

---

### Insert Element

`insertElement(int key)`: This function inserts a new element with the provided `key` into the SkipList. Here's a simplified explanation of the process:

The provided function `insertElement(int key)` inserts a new element with the specified `key` into the SkipList data structure. Here's a breakdown of how it works:

**1. Initialization:**

- `Node current = head;`: This line sets a pointer `current` to the head node of the SkipList. This will be used to traverse the list during insertion.
- `Node update[] = new Node[maxLevel + 1];`: This line creates an array of `Node` pointers named `update`. This array will hold references to nodes at each level that will be used to update the forward pointers during insertion.

**2. Traversing Levels and Finding Insertion Point:**

- `for (int i = level; i >= 0; i--)`  : This loop iterates through each level of the SkipList, starting from the highest level (`level` ) down to level 0.

  - `while (current.forward[i] != null && current.forward[i].key < key)`: This inner loop iterates within a specific level, moving the `current` pointer forward until it reaches the end of the level (null) or finds a node with a key greater than the `key` being inserted. This ensures we find the last node before the insertion point for the new element.
  - `update[i] = current;`: After finding the appropriate position in the current level, the `update` array at index `i` is assigned the value of the `current` pointer. This essentially stores references to nodes at each level that will be used to link the new node into the SkipList.

**3. Checking for Existing Key:**

- `current = current.forward[0]`: This line moves the `current` pointer to the node pointed to by the head node's forward pointer at level 0 (the bottommost level). This effectively checks if a node with the same `key` already exists in the list.
- `if (current == null || current.key != key)`: This condition checks if the `current` pointer is null (meaning the key is not present) or if the key of the current node (if found) doesn't match the `key` being inserted. This indicates that we need to insert a new node.

**4. Determining Random Level for New Node:**

- `int rlevel = randomLevel();`: This line calls the `randomLevel()` function (assumed to be implemented elsewhere) to generate a random level for the new node. The `randomLevel()` function likely uses a probability `P` to determine the level with a higher chance of getting a higher level for the new node.

**5. Updating Head Pointers if Needed:**

- `if (rlevel > level)`  : This condition checks if the randomly generated level (`rlevel` ) for the new node is higher than the current highest level (`level` ) in the SkipList.

  - `for (int i = (level + 1); i < (rlevel + 1); i++)`  : This loop iterates from the current highest level (`level`+ 1) up to the randomly generated level (`rlevel` ).

    - `update[i] = head;`: Inside the loop, each element of the `update` array for these new levels is assigned the `head` node. This essentially updates the head node's forward pointers for these higher levels to point to the new node being inserted. This creates a new "tower" in the SkipList if the random level is higher.

  - `level = rlevel;`: This line updates the `level` variable to reflect the new highest level in the SkipList after potentially adding new head pointers.

**6. Creating the New Node:**

- `Node n = createNode(key, rlevel);`: This line calls the `createNode(key, rlevel)` function (assumed to be implemented elsewhere) to create a new `Node` object with the specified `key` and the randomly generated level (`rlevel`). This function likely allocates memory and sets the initial forward pointers of the new node to null.

**7. Updating Forward Pointers for Insertion:**

- `for (int i = 0; i <= rlevel; i++)`  : This loop iterates through all levels, including the new ones if applicable (up to `rlevel`).

  - `n.forward[i] = update[i].forward[i];`: This line updates the forward pointer of the new node (`n`) at level `i` to point to the node currently stored in the `update` array at the same level `i`. This essentially connects the new node to the previous nodes at each level.
  - `update[i].forward[i] = n;`: This line updates the forward pointer of the node stored in the `update` array at level `i`

---

### Search Element

`searchElement(int key)`: This function searches for an element with the provided `key` in the SkipList. It follows a similar process as `insertElement` to traverse down each level until it finds the key or reaches the end of the list. It then prints whether the key was found or not.



The provided function `searchElement(int key)` searches for a node with the specified `key` in the SkipList data structure. Here's a breakdown of how it works:

**1. Initialization:**

- `Node current = head;`: This line sets a pointer `current` to the head node of the SkipList. This will be used to traverse the list during the search.
- `System.out.println("\n---------------------\n");`: This line prints a line separator.

**2. Traversing Levels:**

- `for (int i = level; i >= 0; i--)`: This loop iterates through each level of the SkipList, starting from the highest level (`level`) down to level 0.

**3. Searching Within Each Level:**

- `while (current.forward[i] != null && current.forward[i].key < key)`: This loop iterates within a specific level, moving the `current` pointer forward until it reaches the end of the level (null) or finds a node with a key greater than or equal to the `key` being searched for. This ensures we find the last node before (or the node itself) that has a key less than the target `key`.

**4. Search Result:**

- `if (current.forward[0] == null)`  : This condition checks if the loop in step 3 completed without finding a node with a key greater than or equal to the target `key`  at level 0 (the bottommost level). This essentially means the target `key` is not present in the SkipList.

  - `System.out.println("Not Found"); return;`: If the key is not found, the function prints a message indicating "Not Found" and exits by returning from the function.

**5. Checking the Found Node (if any):**

- `current = current.forward[0]`: This line assumes we didn't exit in the previous step (i.e., the key might have been found). Here, the `current` pointer is moved to the node pointed to by the head node's forward pointer at level 0. This effectively moves to the first node in the list (remember, level 0 represents the bottommost level with all actual data).

- `if (current.key == key)`  : This condition checks if the key of the current node (potentially the found node)  matches the target `key` .

  - `System.out.println("Found key: " + key);`: If the keys match, the function prints a message indicating "Found key: " followed by the actual key value.

- `else` : If the keys don't match (i.e., we moved to a node with a higher key but not the exact target key), it implies the target key is not present in the list.

  - `System.out.println("Not Found");`: The function prints a message indicating "Not Found".

**Overall, the `searchElement` function efficiently searches for a node with a specific `key` in the SkipList by utilizing the multi-level structure. It traverses down each level, stopping at the last node before the target key (or the node itself if the key exists). Finally, it checks if the key matches and prints the appropriate message.**

---

###  Delete Element

`deleteElement(int key)`: This function searches for a node with the provided `key` and removes it from the SkipList. It adjusts the forward pointers of the surrounding nodes to skip over the deleted node. It also checks if the highest level can be reduced after a deletion.

The provided function `deleteElement(int key)` removes a node with the specified `key` from the SkipList data structure. Here's a breakdown of how it works:

**1. Debugging Message (Commented Out):**

Java

```
// Print a message indicating the key to be deleted (for debugging purposes)
System.out.println("\n" + key + " is to be deleted\n");
```

This line is commented out but serves a debugging purpose. It would print a message indicating the key being deleted.

**2. Initialization:**

- `Node current = head;`: This line sets a pointer `current` to the head node of the SkipList. This will be used to traverse the list during deletion.

**3. Traversing Levels:**

- `for (int i = level; i >= 0; i--)`: This loop iterates through each level of the SkipList, starting from the highest level (`level`) down to level 0.

**4. Searching Within Each Level:**

- `while (current.forward[i] != null && current.forward[i].key <= key)`: This loop iterates within a specific level, moving the `current` pointer forward until it reaches the end of the level (null) or finds a node with a key greater than the `key` being deleted. This ensures we find the node before or the node itself that has the `key` we want to delete.

**5. Deletion Logic:**

- `if (current.forward[i].key == key)`  : This condition checks if the current node's forward pointer at the current level points to the node with the  `key`  to be deleted.

  - `System.out.println("delete found");`: This line (for debugging) prints a message indicating the deletion target is found.

  - `current.forward[i] = current.forward[i].forward[i]`: This is the core deletion step. It updates the forward pointer of the `current` node at the current level to skip over the node being deleted. It essentially points to the node that comes after the deleted node in that level.

  - `if (current.key == -1 && current.forward[i] == null)` :  This condition checks if the deletion happened at level 0 (i.e., the head node) and the head node's forward pointer became null after the deletion. This means the list is now empty.

    - `level--;`: If the list is empty, the level is reduced to reflect that there are no elements anymore.
    - `System.out.println("level deleted");`: This line (for debugging) prints a message indicating the level has been reduced.

**6. Moving to the Next Node (if not deleted):**

- `else`  : If the `key`  is not found at the current level (i.e., the loop condition `current.forward[i].key <= key` is not met), the `else` block executes.

  - `current = current.forward[i]`: This line simply moves the `current` pointer to the next node in the current level, continuing the search for the target `key`.

**Overall, the `deleteElement` function efficiently removes a node with the specified `key` from the SkipList by adjusting the forward pointers of surrounding nodes to skip over the deleted node. It also handles the case where the deletion empties the list, reducing the highest level (effectively making the list empty).**

---

- `displayList()`: This function prints the contents of the SkipList. It iterates through each level, starting from the highest, and prints the keys of the nodes in that level.

**Overall, Skip Lists provide a good balance between insertion, search, and deletion operations. They are well-suited for scenarios where search operations are frequent.**



## Lecture Code

```java
/*
Project: 	Skiplist
Programmer:	James Goudy
 */
package skiplists_rev24;

class Node {

    // A single node in the SkipList
    public int key;
    public Node[] forward;

    public Node(int key, int level) {
        // Initializes a new Node with a key and an array of forward pointers
        this.key = key;
        forward = new Node[level + 1];

        for (int c = 0; c < level + 1; c++) {
            forward[c] = null;
        }
    }
}

class SkipList {

    // A SkipList data structure
    private int maxLevel;
    private double P;
    private int level = 0;
    private Node head;

    public SkipList(int maxLevel, double P) {
        // Constructor for SkipList, initializes head node with special key
        this.maxLevel = maxLevel;
        this.P = P;
        level = 0;
        head = new Node(-1, maxLevel);
    }

    int randomLevel() {
        // Generates a random level for a new node
        double r = Math.random();
        int lvl = 0;
        while (r < P && lvl < maxLevel) {
            lvl++;
            r = Math.random();
        }
        return lvl;
    }

    static Node createNode(int key, int level) {
        // Creates a new node with a key and specified level
        Node n = new Node(key, level);
        return n;
    }

    public void insertElement(int key) {
        // Inserts a new element with the provided key into the SkipList
        Node current = head;
        Node update[] = new Node[maxLevel + 1];

        for (int i = level; i >= 0; i--) {
            // Traverse each level, find the last node before the key
            while (current.forward[i] != null 
                    && current.forward[i].key < key) {
                current = current.forward[i];
            }
            update[i] = current;
        }

        current = current.forward[0];

        if (current == null || current.key != key) {
            // If key not found, insert a new node
            int rlevel = randomLevel();

            if (rlevel > level) {
                // If random level is higher than current level, 
                // update head pointers
                for (int i = (level + 1); i < (rlevel + 1); i++) {
                    update[i] = head;
                }
                level = rlevel;
            }

            Node n = createNode(key, rlevel);

            for (int i = 0; i <= rlevel; i++) {
                // Update forward pointers of new node 
                // and previous nodes at each level
                n.forward[i] = update[i].forward[i];
                update[i].forward[i] = n;
            }
            System.out.println("Successfully Inserted key " + key + "\n");
        }
    }

    void searchElement(int key) {
        // Searches for an element with the provided key in the SkipList
        Node current = head;
        System.out.println("\n---------------------\n");
        for (int i = level; i >= 0; i--) {
            // Traverse each level, find the last node before the key
            while (current.forward[i] != null 
                    && current.forward[i].key < key) {
                current = current.forward[i];
            }
        }

        if (current.forward[0] == null) {
            // Key not found
            System.out.println("Not Found");
            return;
        }

        current = current.forward[0];

        if (current.key == key) {
            // Key found
            System.out.println("Found key: " + key);
        } else {
            // Key not found
            System.out.println("Not Found");
        }
    }

    //---------------------------------------
    void deleteElement(int key) {
        // Print a message indicating the key 
        // to be deleted (for debugging purposes)
        System.out.println("\n" + key + " is to be deleted\n");

        Node current = head;

        // Traverse down each level of the SkipList
        for (int i = level; i >= 0; i--) {
            // Search for the node with the key or 
            // the last node before the key at the current level
            while (current.forward[i] != null 
                    && current.forward[i].key <= key) {
                // If the key is found in the current level
                if (current.forward[i].key == key) {
                    System.out.println("delete found");

                    // Update the forward pointer 
                    // of the current node to skip the deleted node
                    current.forward[i] = current.forward[i].forward[i];

                    // If the head node's forward pointer 
                    // becomes null after deletion 
                    // and the current level is 0, 
                    // it means the list is empty, 
                    // so reduce the level
                    if (current.key == -1 && current.forward[i] == null) {
                        level--;
                        System.out.println("level deleted");
                    }
                } else {
                    // If the key is not found at the current level, 
                    // move to the next node
                    current = current.forward[i];
                }
            }
        }
    }

    void displayList() {
        // Prints the contents of the SkipList
        System.out.println("\n*****Skip List*****\n");
        for (int i = 0; i <= level; i++) {
            Node node = head.forward[i];
            System.out.print("Level " + i + ": ");
            // Traverse each level and print the keys of the nodes
            while (node != null) {
                System.out.print(node.key + " ");
                node = node.forward[i];
            }
            System.out.println("");
        }
    }
}

public class Skiplists_rev24 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // create SkipList object with MAXLVL and P > 0 and P < 1 
        int MAXLVL = 4;

        // the higer the probability number,
        // the greaterchance of more levels.
        double prob = .75;

        SkipList lst = new SkipList(MAXLVL, prob);

        //lst.insertElement(35);
        lst.insertElement(3);
        lst.insertElement(6);
        lst.insertElement(7);
        lst.insertElement(9);
        lst.insertElement(12);
        lst.insertElement(19);

        lst.insertElement(17);

        lst.insertElement(26);
        lst.insertElement(21);
        lst.insertElement(25);
        lst.displayList();

        lst.searchElement(19);
        lst.searchElement(25);
        lst.searchElement(9);
        lst.searchElement(5);
        lst.searchElement(55);

        lst.deleteElement(25);
        lst.displayList();

        lst.deleteElement(7);
        lst.displayList();

        lst.deleteElement(3);
        lst.displayList();

        lst.deleteElement(17);
        lst.displayList();

        System.out.println("\nbye\n");
    }

}


```



### Output

Note: Output will be different for the levels each time due to the randomness factor

```
Successfully Inserted key 3

Successfully Inserted key 6

Successfully Inserted key 7

Successfully Inserted key 9

Successfully Inserted key 12

Successfully Inserted key 19

Successfully Inserted key 17

Successfully Inserted key 26

Successfully Inserted key 21

Successfully Inserted key 25


*****Skip List*****

Level 0: 3 6 7 9 12 17 19 21 25 26 
Level 1: 3 6 7 9 12 17 19 21 25 26 
Level 2: 3 6 7 9 17 19 25 26 
Level 3: 3 6 9 17 19 25 
Level 4: 3 6 9 17 19 

---------------------

Found key: 19

---------------------

Found key: 25

---------------------

Found key: 9

---------------------

Not Found

---------------------

Not Found

25 is to be deleted

delete found
delete found
delete found
delete found

*****Skip List*****

Level 0: 3 6 7 9 12 17 19 21 26 
Level 1: 3 6 7 9 12 17 19 21 26 
Level 2: 3 6 7 9 17 19 26 
Level 3: 3 6 9 17 19 
Level 4: 3 6 9 17 19 

7 is to be deleted

delete found
delete found
delete found

*****Skip List*****

Level 0: 3 6 9 12 17 19 21 26 
Level 1: 3 6 9 12 17 19 21 26 
Level 2: 3 6 9 17 19 26 
Level 3: 3 6 9 17 19 
Level 4: 3 6 9 17 19 

3 is to be deleted

delete found
delete found
delete found
delete found
delete found

*****Skip List*****

Level 0: 6 9 12 17 19 21 26 
Level 1: 6 9 12 17 19 21 26 
Level 2: 6 9 17 19 26 
Level 3: 6 9 17 19 
Level 4: 6 9 17 19 

17 is to be deleted

delete found
delete found
delete found
delete found
delete found

*****Skip List*****

Level 0: 6 9 12 19 21 26 
Level 1: 6 9 12 19 21 26 
Level 2: 6 9 19 26 
Level 3: 6 9 19 
Level 4: 6 9 19 

bye

```

