# Doubly Linked List



## Key Ideas

* The doubly linked list allows the list to be traversed in both directions; forwards and backwards



A **doubly linked list** is a type of linked list in which each node contains three parts:

1. **Data**: The value stored in the node.
1. **Pointer to the next node**: A reference to the next node in the list.
1. **Pointer to the previous node**: A reference to the previous node in the list.

### Structure:

- In a doubly linked list, each node is connected to both its next and previous nodes, creating a two-way linkage.
- The first node (head) has its previous pointer set to `null`, and the last node (tail) has its next pointer set to `null`.

### Benefits of a Doubly Linked List:

- **Bidirectional Traversal**: You can easily traverse the list in both forward and backward directions.
- **Efficient Deletion**: Insertion and deletion of nodes can be more efficient since you can easily access the previous node.



## Lecture Code

```java
/*
 * Programmer: James Goudy
 * Project: Doubly Linked List 
 */

// Define a class representing each link/node in the doubly linked list
class Link {

    // Pointers for the first and last nodes in the list
    Link first = null;
    Link last = null;

    // Data stored in the node
    String city = null;

    // Pointers for the next and previous nodes
    Link next = null;
    Link prev = null;

    // Constructor to initialize a node with the city name
    Link(String city) {
        this.city = city;
        this.next = null;
        this.prev = null;
    }

    // Display the data of the current node
    public void displayNode() {
        System.out.print(city + " ");
    }
} // End of Link class

// Define a class representing the doubly linked list itself
class Doubly {

    // References to the first and last nodes in the list
    Link first = null;
    Link last = null;

    // Constructor to initialize an empty doubly linked list
    public Doubly() {
        first = null;
        last = null;
    }

    // Method to add a node at the beginning of the list
    public boolean addFirst(String city) {
        Link newLink = new Link(city);

        // If list is empty, set first and last to the new node
        if (first == null) {
            first = newLink;
            last = newLink;
        } else {
            // Otherwise, update pointers for the new node and the current first node
            newLink.next = first;
            first.prev = newLink;
            first = newLink;
        }

        return true;
    }

    // Method to add a node at the end of the list
    public boolean addLast(String city) {
        Link newLink = new Link(city);

        // If list is empty, set first and last to the new node
        if (first == null) {
            first = newLink;
            last = newLink;
        } else {
            // Otherwise, update pointers for the new node and the current last node
            newLink.prev = last;
            last.next = newLink;
            last = newLink;
        }

        return true;
    }

    // Method to find a city in the list
    public boolean findCity(String citySearch) {

        // If list is empty, return false
        if (first == null) {
            return false;
        } else {
            Link current = first;

            // Traverse the list to search for the city
            while (current != null) {
                if (current.city.equals(citySearch)) {
                    return true; // City found
                }
                current = current.next;
            }

            return false; // City not found
        }
    }

    // Method to insert a new node after a given city
    public boolean insertAfter(String citySearch, String insertCity) {
        Link newLink = new Link(insertCity);

        // If list is empty, add the new node as the only node
        if (first == null) {
            first = newLink;
            last = newLink;
        } else {
            Link current = first;

            // Traverse the list to find the specified city
            while (current != null) {
                if (current.city.equals(citySearch)) {

                    // If the city is the last node, update last
                    if (current.next == null) {
                        current.next = newLink;
                        newLink.prev = current;
                        last = newLink;
                    } else {
                        // Update pointers for inserting in the middle
                        newLink.next = current.next;
                        newLink.prev = current;
                        current.next.prev = newLink;
                        current.next = newLink;
                    }

                    return true; // City inserted
                }
                current = current.next;
            }
        }

        return false; // City not found
    }

    // Method to insert a new node before a given city
    public boolean insertBefore(String citySearch, String insertCity) {
        Link newLink = new Link(insertCity);

        // If list is empty, add the new node as the only node
        if (first == null) {
            first = newLink;
            last = newLink;
        } else {
            Link current = first;

            // Traverse the list to find the specified city
            while (current != null) {
                if (current.city.equals(citySearch)) {

                    // If the city is the first node, update first
                    if (current.prev == null) {
                        current.prev = newLink;
                        newLink.next = current;
                        first = newLink;
                    } else {
                        // Update pointers for inserting in the middle
                        newLink.next = current;
                        newLink.prev = current.prev;
                        current.prev.next = newLink;
                        current.prev = newLink;
                    }

                    return true; // City inserted
                }
                current = current.next;
            }
        }

        return false; // City not found
    }

    // Method to delete a node with a specified city
    public boolean deleteCity(String citySearch) {

        // If list is empty, return false
        if (first == null) {
            return false;
        } else {
            Link current = first;

            // Traverse the list to find the specified city
            while (current != null) {
                if (current.city.equals(citySearch)) {

                    // If the city is the first node
                    if (current.prev == null) {
                        current.next.prev = null;
                        first = current.next;
                        current = null;
                        return true; // City deleted
                    } else if (current.next == null) {
                        // If the city is the last node
                        current.prev.next = null;
                        last = current.prev;
                        current = null;
                        return true; // City deleted
                    } else {
                        // If the city is in the middle
                        current.prev.next = current.next;
                        current.next.prev = current.prev;
                        current = null;
                        return true; // City deleted
                    }
                }
                current = current.next;
            }

            return false; // City not found
        }
    }

    // Method to display the entire list
    public void displayList() {
        Link current = first;

        System.out.println("");
        while (current != null) {
            current.displayNode(); // Display each node
            current = current.next; // Move to next node
        }
        System.out.println("");
    }
}

// Main class to demonstrate doubly linked list functionality
public class DS_DoublyLinkedList {

    // Create an instance of the Doubly linked list
    static Doubly dl = new Doubly();

    // Method to search for a city
    public static void citySearch(String searchCity) {
        if (dl.findCity(searchCity)) {
            System.out.println("\n" + searchCity + " is in the list");
        } else {
            System.out.println("\n" + searchCity + " not found");
        }
    }

    // Method to delete a city
    public static void deleteCity(String searchCity) {
        if (dl.deleteCity(searchCity)) {
            System.out.println(searchCity + " was deleted");
        } else {
            System.out.println(searchCity + " was NOT deleted");
        }
    }

    // Main method to execute the program
    public static void main(String[] args) {

        String searchCity = "";
        String insertCity = "";

        // Insert data at the front of the list
        dl.addFirst("Kali");
        dl.addFirst("Polson");
        dl.addFirst("Missoula");
        dl.addFirst("Whitefish");

        // Insert data at the end of the list
        dl.addLast("Chicago");
        dl.addLast("Denver");
        dl.addLast("Sandiego");

        dl.displayList(); // Display the list

        System.out.println("\n----- Find Examples------\n");

        searchCity = "Chicago";
        citySearch(searchCity);

        searchCity = "Bozeman";
        citySearch(searchCity);

        System.out.println("\n----- Delete Examples------\n");

        searchCity = "Polson";
        deleteCity(searchCity);

        searchCity = "Bozeman";
        deleteCity(searchCity);

        searchCity = "Sandiego";
        deleteCity(searchCity);

        searchCity = "Whitefish";
        deleteCity(searchCity);

        dl.displayList(); // Display the list

        System.out.println("\n----- Insert Examples------\n");

        searchCity = "Missoula";
        insertCity = "Dayton";
        dl.insertAfter(searchCity, insertCity);

        searchCity = "Denver";
        insertCity = "Boulder";
        dl.insertAfter(searchCity, insertCity);

        dl.displayList(); // Display the list

        searchCity = "Chicago";
        insertCity = "Springfield";
        dl.insertBefore(searchCity, insertCity);

        searchCity = "Missoula";
        insertCity = "Libby";
        dl.insertBefore(searchCity, insertCity);

        dl.displayList(); // Display the list

        System.out.println("\nbye");
    }
}

/*
 * OUTPUT  *
 * Whitefish Missoula Polson Kali Chicago Denver Sandiego  *
 * ----- Find Examples------
 *
 *
 * Chicago is in list
 *
 * Bozeman not found
 *
 * ----- Delete Examples------
 *
 * Polson was deleted
 * Bozeman was NOT deleted
 * Sandiego was deleted
 * Whitefish was deleted
 *
 * Missoula Kali Chicago Denver  *
 * ----- Insert Examples------
 *
 *
 * Missoula Dayton Kali Chicago Denver Boulder  *
 * Libby Missoula Dayton Kali Springfield Chicago Denver Boulder  *
 * bye
 *
 */


```



---

End Of Topic



