# Doubly Linked List - Links as Sub Class

## Key Ideas

- The doubly linked list allows the list to be traversed in both directions; forwards and backwards



```{Note}
Not all languages support subclasses. 
```




## Lecture Code

```java
/*
 * Programmer: James Goudy
 * Project: Doubly Linked List written
 * with  Links / Nodes as SubClass
 */

class Doubly {

    Link first = null;
    Link last = null;

    // ---------------------------------
    // sub class - Link / Nodes
    // NOTE: this can be a separate class as well
    
    class Link {

        Link first = null;
        Link last = null;

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
    public Doubly() {

        first = null;
        last = null;
    }

    // add link at the beginning of the list
    public boolean addFirst(String city) {
        Link newLink = new Link(city);

        if (first == null) {
            // if list is empty
            first = newLink;
            last = newLink;
        } else {
            newLink.next = first;
            first.prev = newLink;
            first = newLink;
        }

        return true;
    }

    // add link to the end of the list
    public boolean addLast(String city) {

        Link newLink = new Link(city);

        if (first == null) {
            // if list is empty
            first = newLink;
            last = newLink;
        } else {
            newLink.prev = last;
            last.next = newLink;
            last = newLink;
        }

        return true;
    }

    public boolean findCity(String citySearch) {

        if (first == null) {

            // if list is empty
            return false;
        } else {
            Link current = first;

            while (current != null) {
                if (current.city.equals(citySearch)) {
                    return true;
                }
                current = current.next;
            }

            return false;
        }
    }

    public boolean insertAfter(String citySearch, String insertCity) {

        Link newLink = new Link(insertCity);

        if (first == null) {

            // list is empty - add the link
            first = newLink;
            last = newLink;

            // NOTE: there is an option not to insert
            // a link then the code above would be replaced
            // with return false
            
        } else {
            Link current = first;

            while (current != null) {
                if (current.city.equals(citySearch)) {

                    // check if last link
                    if (current.next == null) {
                        // check if last link
                        current.next = newLink;
                        newLink.prev = current;

                        last = newLink;

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
            last = newLink;

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

            while (current != null) {
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
                        last = current;
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
            }

            return false;
        }
    } //end of function

    public void displayList() {
        Link current = first;

        System.out.println("");
        while (current != null) {
            current.displayNode();
            current = current.next;
        }
        System.out.println("");
    }
        
    public void displayListBackwards() {
        Link current = last;

        System.out.println("");
        while (current != null) {
            current.displayNode();
            current = current.prev;
        }
        System.out.println("");
    }
    
}

public class J2_SubClass {

    static Doubly dl = new Doubly();

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

        // insert data at end of list
        dl.addLast("Chicago");
        dl.addLast("Denver");
        dl.addLast("Sandiego");

        dl.displayList();

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

        dl.displayList();

        System.out.println("\n----- Insert Examples------\n");

        searchCity = "Missoula";
        insertCity = "Dayton";
        dl.insertAfter(searchCity, insertCity);

        searchCity = "Denver";
        insertCity = "Boulder";
        dl.insertAfter(searchCity, insertCity);

        dl.displayList();

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
 OUTPUT 
 
 Whitefish Missoula Polson Kali Chicago Denver Sandiego 

----- Find Examples------


Chicago is in list

Bozeman not found

----- Delete Examples------

Polson was deleted
Bozeman was NOT deleted
Sandiego was deleted
Whitefish was deleted

Missoula Kali Chicago Denver 

----- Insert Examples------


Missoula Dayton Kali Chicago Denver Boulder 

Libby Missoula Dayton Kali Springfield Chicago Denver Boulder 

bye
 
 */
```



---

End Of Topic





