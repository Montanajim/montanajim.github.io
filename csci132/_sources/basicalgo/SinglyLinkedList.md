# Singly Linked List



```{admonition} Definition
**singly linked list** is a type of linked list that is *unidirectional*. It can be traversed in only one direction from the head to the last node (tail). The last node always points to null
```



## Lecture Code

```java
/*
Single Link List

Project: Singly LinkedList Rev2
Programmer: James Goudy

 */
package singlelinklist_rev2;

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
        if (found==false) {
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

}

public class SingleLinkList_Rev2 {

    public static void main(String[] args) {

        LinkList theList = new LinkList();

        theList.insertFirst("Kali", 32000);
        theList.insertFirst("Whitefish", 7700);
        theList.insertFirst("Polson", 20000);
        theList.insertFirst("Chicago", 1320000);
        theList.insertFirst("Convoy", 500);

        theList.displayList();

        System.out.println("Find Result for Kali: " + 
                theList.findCity("Kali"));
        System.out.println("Find Result for Libby: " + 
                theList.findCity("Libby"));

        theList.deleteCity("Chicago");
        theList.displayList();

        while (!theList.isEmpty()) {
            Link aLink = theList.deleteFirst();

            //display the deleted link
            System.out.print("\nDeleted");
            aLink.displayLink();

        }

        System.out.println("\n---------------\n");
        theList.displayList();

        System.out.println("\n\nBye");
    }

}

```



---

End Of Topic



