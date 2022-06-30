# Singly Linked List



```{admonition} Definition
**singly linked list** is a type of linked list that is *unidirectional*. It can be traversed in only one direction from the head to the last node (tail). The last node always points to null
```



## Lecture Code

```java
/*
 * Single Link List
 *
 * SingleLinkList_Rev2
 * Programmer: James Goudy
 *
 */


class Link {

    //Data goes here
    public String city = "";
    public int population = 0;

    //link to next one
    public Link next;

    //constructor
    public Link(String city, int population) {
        this.city = city;
        this.population = population;
    }

    //display the link
    public void displayLink() {
        System.out.print("{" + city + ", " + population + "} ");
    }

}

class LinkList {

    // first is a reference / "address" of the first link
    private Link first;

    //constructor
    public LinkList() {
        first = null;
    }

    //Check if the list is empty
    public boolean isEmpty() {
        return (first == null);
    }

    // insert at the front of the list (front[left] -- to --> back[right]) 
    public void insertFirst(String city, int population) {

        //create a new link
        Link newLink = new Link(city, population);

        // the new link is to the left or in front of first
        // the new link will make first in the second spot 
        // so newLink.next has to point to the address first
        newLink.next = first;

        // now that the newLink.next is looking at the seond spot 
        // or the next spot, first can have the address of the newLink
        first = newLink;

    }

//set this up to see what was deleted
    public Link deleteFirst() {

        //temp variable to hold first
        Link temp = first;

        // set variable first to the second spot or the next spot
        first = first.next;

        //c or c++ you would not do  a return
        // make    temp = null;
        return temp;
    }

    public void displayList() {

        System.out.print("\nList (first --> last): ");
        Link current = first;

        while (current != null) {
            current.displayLink();
            //move to the next link
            current = current.next;
        }
        System.out.println();

    }

    public void deleteCity(String city) {
        // need to check if city was found
        boolean found = false;

        Link current = first;
        Link prev = first;
        Link temp;

        // check if city is in the first node
        if (first.city.equals(city)) {
            temp = first;
            first = first.next;
            temp = null;
            return;
        }

        while (current != null) {

            // if found, signal the boolean 
            // that it was found
            // stop the loop at the current node
            // using break
            if (current.city.equals(city)) {
                found = true;
                break;
            }

            prev = current;
            current = current.next;

        }

        // if false city wasn't found and 
        // program returns back to main
        if (found == false) {
            System.out.println("City Not Found - Nothing Deleted");
            return;
        }
        prev.next = current.next;
        current = null;

        System.out.println("City was successfully deleted");

    }

    public boolean findCity(String city) {
        boolean found = false;

        Link temp = first;

        while (temp != null) {
            if (temp.city.equals(city)) {
                found = true;
                break;
            }
            temp = temp.next;
        }

        return found;
    }

    public void insertAfter(String searchCity, String newCity,
            int newPopulation) {

        //flag to see if we found the city
        boolean found = false;

        Link current = first;
        Link temp;

        // create the new node
        Link newNode = new Link(newCity, newPopulation);

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

    public boolean deleteList() {

        String city = "";

        while (!isEmpty()) {
            Link aLink = deleteFirst();
            city = aLink.city;
            //display the deleted link
            System.out.println(city + " Deleted");
        }
        return true;
    }

}

public class SingleLinkList_Rev2 {

    public static void main(String[] args) {

        Link temp = new Link("", 0);
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
        temp.displayLink();
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

        // Delete the list
        System.out.println("\n\ndelete list");
        theList.deleteList();

        System.out.println("\n\nBye");
    }

}

```



---

End Of Topic



