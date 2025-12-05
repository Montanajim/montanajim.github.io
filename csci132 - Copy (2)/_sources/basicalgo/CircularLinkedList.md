# Circular Linked List - Links as Sub Class



## Key Ideas

* The doubly linked list allows the list to be traversed in both directions; forwards and backwards

* In a circular doubly-linked list the last node (next) points to the first. The first node (previous) points to the last node.
* The doubly linked list allows the list to be traversed in both directions; forwards and backwards



![Circular Linked List](images/CircularLinkList.png)



```{Note}
Not all languages support subclasses. 
```




## Lecture Code

```java
package com.mycompany.linkedlistcircular;

/*
 * Programmer: James Goudy
 * Project Circular LinkedList
 *
 * NOTE: last link is referenced as first.prev
 */
class CircularLinkedList {

    Link first = new Link("");

    // ---------------------------------
    // sub class - Link / Nodes
    // NOTE: this can be a separate class as well
    class Link {

        Link first = null;

        // data
        String city = null;

        // link navigation
        Link next = null;
        Link prev = null;

        // constructor
        Link(String city) {
            this.city = city;
            this.next = null;
            this.prev = null;
        }

        public void displayNode() {
            System.out.print(city + " ");
        }
    } // end of link
    // ---------------------------------

    // constructor
    public CircularLinkedList() {

        first = null;
    }

    // add link at the beginning of the list
    public boolean addFirst(String city) {

        Link newLink = new Link(city);

        if (first == null) {
            // empty list
            newLink.next = newLink;
            newLink.prev = newLink;

            first = newLink;

        } else {

            // connect the newLink references
            newLink.next = first;

            newLink.prev = first.prev;

            first.prev = newLink;

            // move first to the new link
            first = newLink;

            // point the last link to the new first
            first.prev.next = first;

        }

        return true;
    }

    // add link to the end of the list
    public boolean addLast(String city) {

        Link newLink = new Link(city);

        if (first == null) {
            //list is empty
            first = newLink;
        } else {
            // set new link references
            newLink.next = first;

            newLink.prev = first.prev;

            // last link is (first.prev)
            first.prev.next = newLink;

            first.prev = newLink;

        }

        return true;
    }

    public boolean findCity(String citySearch) {

        if (first == null) {

            // if list is empty
            return false;
        } else {
            Link current = first;

            do {
                if (current.city.equals(citySearch)) {
                    return true;
                }
                current = current.next;

            } while (current != first);

            return false;
        }
    }

    public boolean insertAfter(String citySearch, String insertCity) {

        Link newLink = new Link(insertCity);

        if (first == null) {

            // list is empty - add the link
            first = newLink;

            // NOTE: there is an option not to insert
            // a link then the code above would be replaced
            // with return false
        } else {
            Link current = first;

            while (current != null) {
                if (current.city.equals(citySearch)) {

                    // check if last link
                    if (current.next == first.prev) {
                        // check if last link
                        current.next = newLink;
                        newLink.prev = current;

                        first.prev = newLink;

                    } else {
                        newLink.next = current.next;
                        newLink.prev = current;

                        current.next.prev = newLink;
                        current.next = newLink;
                    }

                    return true;
                }
                current = current.next;

            }
        }

        return false;

    }

    public boolean insertBefore(String citySearch, String insertCity) {

        Link newLink = new Link(insertCity);

        if (first == null) {

            // list is empty - add the link
            first = newLink;

            // NOTE: there is an option not to insert
            // a link then the code above would be replaced
            // with return false
        } else {
            Link current = first;

            while (current != null) {
                if (current.city.equals(citySearch)) {

                    // check for first link
                    if (current.prev == null) {
                        // check if last link
                        current.prev = newLink;
                        newLink.next = current;

                        first = newLink;

                    } else {
                        newLink.next = current;
                        newLink.prev = current.prev;

                        current.prev.next = newLink;
                        current.prev = newLink;
                    }

                    return true;
                }
                current = current.next;

            }
        }

        return false;
    }

    public boolean deleteCity(String citySearch) {

        if (first == null) {
            return false;
        } else {
            Link current = first;

            do {
                if (current.city.equals(citySearch)) {

                    if (current.prev == null) {
                        // first node
                        current.next.prev = null;
                        first = current.next;
                        current = null;
                        return true;
                    } else if (current.next == null) {
                        // last node
                        current.prev.next = null;
                        first.prev = current;
                        current = null;
                        return true;
                    } else {
                        // a center node
                        current.prev.next = current.next;
                        current.next.prev = current.prev;
                        current = null;

                        return true;
                    }
                }

                current = current.next;
            } while (current != first);

            return false;
        }
    } //end of function

    public void displayList() {
        Link current = first;

        System.out.println("\n** Display List Forward To Back **");

        do {
            current.displayNode();
            current = current.next;
            if (current == first) {
                System.out.println("\n-----------\n");
                return;
            }

        } while (current.next != null);

    } // end of method

    public void displayList(String startCity) {

        Link current = first;
        Link start = null;

        System.out.println("\n ** Display List Forward To Back"
                + " starting at " + startCity + "**");

        // find the city in the list
        do {
            if (current.city.equals(startCity)) {
                break;
            }

            current = current.next;

            if (current == first) {
                System.out.println("City Not Found");
                return;
            }

        } while (current.next != null);

        System.out.println("");

        start = current;

        do {
            current.displayNode();
            current = current.next;
            if (current == start) {
                System.out.println("\n-----------\n");
                return;
            }

        } while (current.next != null);

    } // end of method

    public void displayListReverse() {

        Link current = first.prev;

        System.out.println("\n** Display List in Reverse **\n");

        do {
            current.displayNode();
            current = current.prev;
            if (current == first.prev) {
                System.out.println("\n-----------\n");
                return;
            }

        } while (current.prev != null);
    } // end of method

    public void displayListReverse(String startCity) {

        Link current = first;
        Link start = null;

        System.out.println("\n ** Display list in reverse"
                + " starting at " + startCity + "**");

        // find the city in the list
        do {
            if (current.city.equals(startCity)) {
                break;
            }

            current = current.next;

            if (current == first) {
                System.out.println("City Not Found");
                return;
            }

        } while (current.next != null);

        System.out.println("");

        start = current;

        do {
            current.displayNode();
            current = current.prev;
            if (current == start) {
                System.out.println("\n-----------\n");
                return;
            }

        } while (current.prev != null);
    } // end of method

} // end of class

public class DS_LinkedListCircular {

    static CircularLinkedList dl = new CircularLinkedList();

    public static void citySearch(String searchCity) {

        // note that findCity returns a boolean
        // so it can be used in an "if" statement
        if (dl.findCity(searchCity)) {
            System.out.println("\n" + searchCity + " is in list");
        } else {
            System.out.println("\n" + searchCity + " not found");
        }

    }

    public static void deleteCity(String searchCity) {

        // note that findCity returns a boolean
        // so it can be used in an "if" statement
        if (dl.deleteCity(searchCity)) {
            System.out.println(searchCity + " was deleted");
        } else {
            System.out.println(searchCity + " was NOT deleted");
        }

    }

    public static void main(String[] args) {

        String searchCity = "";
        String insertCity = "";

        // insert data at front of list
        dl.addFirst("Kali");
        dl.addFirst("Polson");
        dl.addFirst("Missoula");
        dl.addFirst("Whitefish");
        dl.addFirst("Plains");

        // insert data at end of list
        dl.addLast("Chicago");
        dl.addLast("Denver");
        dl.addLast("Sandiego");

        dl.displayList();
        dl.displayListReverse();

        dl.displayList("Missoula");
        dl.displayList("Wolfcreek");

        dl.displayListReverse();
        dl.displayListReverse("Missoula");

        System.out.println("\n----- Find Examples------\n");

        searchCity = "Missoula";
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

        dl.displayList();

        System.out.println("\n----- Insert After Examples------\n");

        searchCity = "Missoula";
        insertCity = "Dayton";
        dl.insertAfter(searchCity, insertCity);

        searchCity = "Denver";
        insertCity = "Boulder";
        dl.insertAfter(searchCity, insertCity);

        dl.displayList();

        System.out.println("\n----- Insert After Examples------\n");

        searchCity = "Chicago";
        insertCity = "Springfield";
        dl.insertBefore(searchCity, insertCity);

        searchCity = "Missoula";
        insertCity = "Libby";
        dl.insertBefore(searchCity, insertCity);

        dl.displayList();
        System.out.println("\nbye");
    }
}
/*
 * output
 *
 ** Display List Forward To Back **
 * Plains Whitefish Missoula Polson Kali Chicago Denver Sandiego
 * -----------
 *
 *
 ** Display List in Reverse **
 *
 * Sandiego Denver Chicago Kali Polson Missoula Whitefish Plains
 * -----------
 *
 *
 ** Display List Forward To Back starting at Missoula**
 *
 * Missoula Polson Kali Chicago Denver Sandiego Plains Whitefish
 * -----------
 *
 *
 ** Display List Forward To Back starting at Wolfcreek**
 * City Not Found
 *
 ** Display List in Reverse **
 *
 * Sandiego Denver Chicago Kali Polson Missoula Whitefish Plains
 * -----------
 *
 *
 ** Display list in reverse starting at Missoula**
 *
 * Missoula Whitefish Plains Sandiego Denver Chicago Kali Polson
 * -----------
 *
 *
 * ----- Find Examples------
 *
 *
 * Missoula is in list
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
 ** Display List Forward To Back **
 * Plains Missoula Kali Chicago Denver
 * -----------
 *
 *
 * ----- Insert After Examples------
 *
 *
 ** Display List Forward To Back **
 * Plains Missoula Dayton Kali Chicago Denver Boulder
 * -----------
 *
 *
 * ----- Insert After Examples------
 *
 *
 ** Display List Forward To Back **
 * Plains Libby Missoula Dayton Kali Springfield Chicago Denver Boulder
 * -----------
 *
 *
 * bye
 *
 */

```



---

End Of Topic



