# Circular Linked List



```java
package com.mycompany.linkedlistcircular;

/*
 * Programmer: James Goudy
 * Project Circular LinkedList
 *
 */
class Doubly {

    Link first = new Link("xx");
    Link last = new Link("yy");

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

            newLink.next = newLink;
            newLink.prev = newLink;

            first = newLink;
            last = newLink;

        } else {

            if (first == last) {

                Link temp = new Link("");
                temp = newLink;

                last.prev = temp;
            }

            newLink.next = first;
            newLink.prev = last;
            first.prev = newLink;

            first = newLink;
            last.next = first;

            //last = tempLast;
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

            newLink.next = first;

            newLink.prev = first.prev;

            first.prev.next = newLink;

            first.prev = newLink;

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

            do {
                if (current.city.equals(citySearch)) {
                    return true;
                }
                current = current.next;

                if (current.next == first) {
                    break;
                }

            } while (current != null);

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
            } while (current != first);

            return false;
        }
    } //end of function

    public void displayList() {
        Link current = first;

        System.out.println("");

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

        //Link current = last;
        Link current = first.prev;

        do {
            current.displayNode();
            current = current.prev;
            if (current == last) {
                System.out.println("\n-----------\n");
                return;
            }

        } while (current.prev != null);
    } // end of method

    public void displayListReverse(String startCity) {

        //Link current = last;
        Link current = first;
        Link start = null;

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
        dl.addFirst("Plains");

        // insert data at end of list
        dl.addLast("Chicago");
        dl.addLast("Denver");
        dl.addLast("Sandiego");

        dl.displayList();

        dl.displayList("Missoula");
        //dl.displayList("Wolfcreek");

        System.out.println("\nReverse");
        dl.displayListReverse();
        dl.displayListReverse("Whitefish");

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
cd E:\My Drive\NetBeansProjects\DS_Algorithms\LinkedListCircular; "JAVA_HOME=C:\\Program Files\\Java\\jdk-18" cmd /c "\"C:\\Program Files\\NetBeans-13\\netbeans\\java\\maven\\bin\\mvn.cmd\" -Dexec.vmArgs= \"-Dexec.args=${exec.vmArgs} -classpath %classpath ${exec.mainClass} ${exec.appArgs}\" -Dexec.appArgs= -Dexec.mainClass=com.mycompany.linkedlistcircular.DS_LinkedListCircular \"-Dexec.executable=C:\\Program Files\\Java\\jdk-18\\bin\\java.exe\" \"-Dmaven.ext.class.path=C:\\Program Files\\NetBeans-13\\netbeans\\java\\maven-nblib\\netbeans-eventspy.jar\" org.codehaus.mojo:exec-maven-plugin:3.0.0:exec"
Running NetBeans Compile On Save execution. Phase execution is skipped and output directories of dependency projects (with Compile on Save turned on) will be used instead of their jar artifacts.
Scanning for projects...

--------< com.mycompany.linkedlistcircular:LinkedListCircular >---------
Building DS_LinkedListCircular 1.0-SNAPSHOT
--------------------------------[ jar ]---------------------------------

--- exec-maven-plugin:3.0.0:exec (default-cli) @ LinkedListCircular ---

Plains Whitefish Missoula Polson Kali Chicago Denver Sandiego 
-----------


Missoula Polson Kali Chicago Denver Sandiego Plains Whitefish 
-----------


Reverse
Sandiego Denver Chicago Kali Polson Missoula Whitefish Plains 
-----------


Whitefish Plains Sandiego Denver Chicago Kali Polson Missoula 
-----------


----- Find Examples------


Missoula is in list

Bozeman not found

----- Delete Examples------

Polson was deleted
Bozeman was NOT deleted
Sandiego was deleted
Whitefish was deleted

Plains Missoula Kali Chicago Denver 
-----------


----- Insert After Examples------


Plains Missoula Dayton Kali Chicago Denver Boulder 
-----------


----- Insert After Examples------


Plains Libby Missoula Dayton Kali Springfield Chicago Denver Boulder 
-----------


bye
------------------------------------------------------------------------
BUILD SUCCESS
------------------------------------------------------------------------
Total time:  0.522 s
Finished at: 2022-07-18T17:53:35-06:00
------------------------------------------------------------------------


 */

```

