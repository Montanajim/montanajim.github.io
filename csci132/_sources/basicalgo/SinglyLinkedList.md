# Singly Linked List



```{admonition} Definition
**singly linked list** is a type of linked list that is *unidirectional*. It can be traversed in only one direction from the head to the last node (tail). The last node always points to null
```



## Lecture Code

```java
/*
 *
 * Project: Singly LinkedList
 * Programmer: J Goudy
 */

class Node {

    // Data goes here
    public String city = "";
    public int population = 0;

    // link to the next node
    // Next is a reference - think of it as a location to the next link.
    public Node next;

    //constructor
    public Node(String city, int population) {
        this.city = city;
        this.population = population;
    }

    //display node
    public void displayNode() {
        System.out.print("{" + city + ", " + population + "} ");
    }

}

class LinkList {

    //keep track of the head / first
    private Node head;

    //constructor
    public LinkList() {
        this.head = null;
    }

    // check to see if the list is empty
    public boolean isEmpty() {
        
        // alternative code
        /* 
         * boolean status;
         * if(head == null)
         * {
         * status = true;
         * }
         *
         * return true;
         */

        return (head == null);
    }

    public void insertFirst(String city, int population) {


        // create a new node
        Node newNode = new Node(city, population);

        newNode.next = head;

        head = newNode;
    }

    public void displayList() {
        
        System.out.println("\nList (first/head ---> last)");

        // set the current node to the head
        // current will be the node/"variable" moving
        // through the list
        
        Node current = head;

        while (current != null) {
            current.displayNode();
            current = current.next;
        }

        System.out.println("\n");

    }

    public Node deleteFirst() {
        
        // Instantiate temp node
        Node temp = null;

        // check if empty
        if (isEmpty()) {
            return temp;
        }
        
        temp = head;
        
        head = head.next;
        
        return temp;

    }

    public boolean deleteCity(String city) {
        
        //flag to see if we found the city
        boolean found = false;

        Node current = head;
        Node prev = head;
        Node temp;

        //check to see if the first node is the city
        if (head.city.equals(city)) {
            head = head.next;
            return true;
        }

        while (current != null) {
            if (current.city.equals(city)) {
                found = true;
                break;
            }
            prev = current;
            current = current.next;
        }

        if (found == false) {
            System.out.println("City not found");
            return false;
        }

        // jump the one that needs to be deleted
        prev.next = current.next;

        // this destroys the node
        current = null;

        System.out.println("City was successfully deleted");
        return true;

    }

    public void insertAfter(String searchCity, String newCity, 
                            int newPopulation) {

        //flag to see if we found the city
        boolean found = false;

        Node current = head;
        Node temp;
        
        // create the new node
        Node newNode = new Node(newCity, newPopulation);

        
        while (current != null) {
            if (current.city.equals(searchCity)) {
                newNode.next = current.next;
                current.next = newNode;
                found = true;
                break;
            }
            current = current.next;
        }

        if (found == false) {
            System.out.println("Warning: City not inserted");
            return;
        }

        displayList();

    }

}

public class DS132SU_SinglyLinkkedList {

    public static void main(String[] args) {

        Node temp = new Node("", 0);
        LinkList theList = new LinkList();

        theList.insertFirst("Kali", 32000);
        theList.insertFirst("Whitefish", 33000);
        theList.insertFirst("Polson", 28000);
        theList.insertFirst("Chicago", 1320000);
        theList.insertFirst("Convoy", 500);

        theList.displayList();

        //delete first
        System.out.println("\nDelete First");
        temp = theList.deleteFirst();
        temp.displayNode();
        theList.displayList();

        System.out.println("Delete Polson");
        theList.deleteCity("Polson");
        theList.displayList();

        System.out.println("\nInsert New York after Whitefish");
        theList.insertAfter("Whitefish", "New York", 6000000);
        
        System.out.println("\nInsert Buffalo after Noxon - FAIL-NO NOXON");
        theList.insertAfter("Noxon", "Buffalo", 300000);
        
        System.out.println("\nInsert Billings after Kali");
        theList.insertAfter("Kali", "Billings", 400000);

    }
}

```



---

End Of Topic



