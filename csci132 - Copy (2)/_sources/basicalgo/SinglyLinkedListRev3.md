# Singly Linked List



[Ternary Operator](TernaryOperator)

[Singly Linked List](# Singly-Linked-List-Code)



```{admonition} Definition
**singly linked list** is a type of linked list that is *unidirectional*. It can be traversed in only one direction from the head to the last node (tail). The last node always points to null
```



## Ternary Operator


>**Ternary Operator** is an instruction that consists of three parts.
>  *Condition Part* - test if something is true or false
>  *True Part* - what is returned if the condition is true
>  *False Part* - what is returned if the condition is false
>
>  x = **(**Conditional Part**) ** **?** True Part **:** False Part;

```java
// Example
y = 3;
x = (y < 4) ? "y is less than four": "y is greater than four"
System.out.write(x);

// Output
// y is less than four
```



## Lecture Code

### Singly Linked List Code

The *Link* and the controlling *Linked List* are written as two separate classes



```java
/*
 * Singly Linked List
 *
 * singlylinkedlists_rev3
 * Programmer: James Goudy
 *
 */
package singlylinkedlists_rev3;

class Link
{

    // Data goes here
    public String city = "";
    public int population = 0;

    // link to next node
    public Link next;

    // constructor
    public Link(String city, int population)
    {
        this.city = city;
        this.population = population;
    }

    // display the link
    public void displayLink()
    {
        System.out.print("{" + city + ", " + population + "} ");
    }

}


class LinkedList
{

    // first is a reference / "address" of the first link
    private Link first;

    // constructor
    public LinkedList()
    {
        first = null;
    }

    //Check if the list is empty
    public boolean isEmpty()
    {
        return (first == null);
    }

    // insert at the front 
    // of the list (front[left] -- to --> back[right]) 
    public void insertFirst(String city, int population)
    {

        // create a new link
        Link newLink = new Link(city, population);

        // the new link is to the left or in front of first
        // the new link will make first in the second spot
        // so newLink.next has to point to the address first
        newLink.next = first;

        // now that the newLink.next is looking at the seond spot
        // or the next spot, first can have the address of the newLink
        first = newLink;

    }

    //This function displays the linked list
    public void displayList()
    {
        System.out.print("\nList\n(first --> last): ");

        //temp variable to hold first
        Link current = first;

        while (current != null)
        {
            current.displayLink();

            // move to the next  link
            current = current.next;
        }

        System.out.println();
    } //end of display list

    public boolean findCity(String city)
    {
        boolean found = false;

        Link current = first;
        // iterate through the loop
        while (current != null)
        {
            // check if current city matches search city
            // set found to true and break out of the loop
            if (current.city.equals(city))
            {
                found = true;
                break;
            }

            current = current.next;

        }

        return found;
    }

    // delete first
    public Link deleteFirst()
    {

        // temp variable to hold first address
        // temp is pointing to an address
        Link temp = first;

        if (!isEmpty())
        {
            // set variable to second spot
            first = first.next;
        }

        // return a link to object 
        // in case calling program wants
        // to retreive the deleted data
        return temp;
    }

    public void deleteCity(String city)
    {
        // assumes the data does not have duplicates

        //need to check if the city was found
        boolean found = false;

        Link current = first;
        Link prev = first;
        Link temp;

        // check if city is in the first node
        if (first.city.equals(city))
        {
            temp = first;
            first = first.next;
            temp = null;
            System.out.println("City was deleted");
            return;
        }

        // start at the beginning of list
        while (current != null)
        {
            // check if the current city matches the search city
            if (current.city.equals(city))
            {
                found = true;

                // break out of the while statement
                break;
            }

            // set the prev variable
            prev = current;

            // move to the next node
            current = current.next;
        }

        // check if the while statment made it to 
        // the end of the loop
        if (found == false)
        {
            System.out.println("\n*** City not found - Nothing deleted");
            return;
        }

        // delete process
        prev.next = current.next;

        current = null;
        System.out.println("\n*** City was successfully delete");

    }

    public void deleteList()
    {
        while (first != null)
        {
            deleteFirst();
        }

    }

    // city is the location of where the new data 
    // will be inserted (after)
    // newCity and newPop are the new city and new population
    public void insertAfter(String city, String newCity, int newPop)
    {
        boolean found = false;
        Link current = first;

        //create a new link
        Link NewLink = new Link(newCity, newPop);

        try
        {
            // iterate through loop
            while (current != null)
            {
                // break out of the loop if found
                // stops the loop at the found city
                // sets found to true
                if (current.city.equals(city))
                {
                    found = true;
                    break;
                }

                // move to next node
                current = current.next;
            }

            // insert process
            NewLink.next = current.next;
            current.next = NewLink;

        } catch (Exception e)
        {
            System.out.println("**Error**\n" + e.getMessage() + "\n***\n");
        }

    }

} // end of class

public class SinglyLinkedLists_Rev3
{

    public static void main(String[] args)
    {
        LinkedList theList = new LinkedList();


        theList.insertFirst("Kali", 32000);
        theList.insertFirst("Whitefish", 7700);
        theList.insertFirst("Polson", 20000);
        theList.insertFirst("Chicago", 13000000);
        theList.insertFirst("Convoy", 500);

        theList.displayList();

        System.out.println("Find Kali : " + theList.findCity("Kali"));

        // ternary operator
        String output = (theList.findCity("Polson") == true)
                ? "City Found" : "City Not Found";
        System.out.println("Polson: " + output);

        output = (theList.findCity("Somers") == true)
                ? "City Found" : "City Not Found";
        System.out.println("Somers: " + output);

        theList.deleteFirst();
        theList.displayList();

        theList.deleteCity("Chicago");
        theList.displayList();

        theList.insertAfter("Polson", "New York", 10000000);
        theList.displayList();

        theList.deleteList();
        theList.displayList();
    }

}

```

### Singly Linked List - Nested Link Class

```java
/*
 * Single Link List
 *
 * SingleLinkList_nested_Rev3
 * Programmer: James Goudy
 *
 */
package singlylinkedlists_nested_rev3;

class LinkedList
{

    class Link
    {

        // Data goes here
        public String city = "";
        public int population = 0;

        // link to next node
        public Link next;

        // constructor
        public Link(String city, int population)
        {
            this.city = city;
            this.population = population;
        }

        // display the link
        public void displayLink()
        {
            System.out.print("{" + city + ", " + population + "} ");
        }

    }

    // first is a reference / "address" of the first link
    private Link first;

    // constructor
    public LinkedList()
    {
        first = null;
    }

    //Check if the list is empty
    public boolean isEmpty()
    {
        return (first == null);
    }

    // insert at the front 
    // of the list (front[left] -- to --> back[right]) 
    public void insertFirst(String city, int population)
    {

        // create a new link
        Link newLink = new Link(city, population);

        // the new link is to the left or in front of first
        // the new link will make first in the second spot
        // so newLink.next has to point to the address first
        newLink.next = first;

        // now that the newLink.next is looking at the seond spot
        // or the next spot, first can have the address of the newLink
        first = newLink;

    }

    //This function displays the linked list
    public void displayList()
    {
        System.out.print("\nList\n(first --> last): ");

        //temp variable to hold first
        Link current = first;

        while (current != null)
        {
            current.displayLink();

            // move to the next  link
            current = current.next;
        }

        System.out.println();
    } //end of display list

    public boolean findCity(String city)
    {
        boolean found = false;

        Link current = first;
        // iterate through the loop
        while (current != null)
        {
            // check if current city matches search city
            // set found to true and break out of the loop
            if (current.city.equals(city))
            {
                found = true;
                break;
            }

            current = current.next;

        }

        return found;
    }

    // delete first
    public Link deleteFirst()
    {

        // temp variable to hold first address
        // temp is pointing to an address
        Link temp = first;

        if (!isEmpty())
        {
            // set variable to second spot
            first = first.next;
        }

        // return a link to object 
        // in case calling program wants
        // to retreive the deleted data
        return temp;
    }

    public void deleteCity(String city)
    {
        // assumes the data does not have duplicates

        //need to check if the city was found
        boolean found = false;

        Link current = first;
        Link prev = first;
        Link temp;

        // check if city is in the first node
        if (first.city.equals(city))
        {
            temp = first;
            first = first.next;
            temp = null;
            System.out.println("City was deleted");
            return;
        }

        // start at the beginning of list
        while (current != null)
        {
            // check if the current city matches the search city
            if (current.city.equals(city))
            {
                found = true;

                // break out of the while statement
                break;
            }

            // set the prev variable
            prev = current;

            // move to the next node
            current = current.next;
        }

        // check if the while statment made it to 
        // the end of the loop
        if (found == false)
        {
            System.out.println("\n*** City not found - Nothing deleted");
            return;
        }

        // delete process
        prev.next = current.next;

        current = null;
        System.out.println("\n*** City was successfully delete");

    }

    public void deleteList()
    {
        while (first != null)
        {
            deleteFirst();
        }

    }

    // city is the location of where the new data 
    // will be inserted (after)
    // newCity and newPop are the new city and new population
    public void insertAfter(String city, String newCity, int newPop)
    {
        boolean found = false;
        Link current = first;

        //create a new link
        Link NewLink = new Link(newCity, newPop);

        try
        {
            // iterate through loop
            while (current != null)
            {
                // break out of the loop if found
                // stops the loop at the found city
                // sets found to true
                if (current.city.equals(city))
                {
                    found = true;
                    break;
                }

                // move to next node
                current = current.next;
            }

            // insert process
            NewLink.next = current.next;
            current.next = NewLink;

        } catch (Exception e)
        {
            System.out.println("**Error**\n" + e.getMessage() + "\n***\n");
        }

    }

} // e

public class Singlylinkedlists_nested_rev3
{

    public static void main(String[] args)
    {

        LinkedList theList = new LinkedList();
        
        // how to create a Link from a nested class
        // note that the new link has to be created from the
        // outer link ('theList')
        LinkedList.Link aLink =  theList.new Link("Detroit", 2000000);
        
        // display the created link
        System.out.println("Created Inner Link");
        aLink.displayLink();
        System.out.println("\n\n");
        
        

        theList.insertFirst("Kali", 32000);
        theList.insertFirst("Whitefish", 7700);
        theList.insertFirst("Polson", 20000);
        theList.insertFirst("Chicago", 13000000);
        theList.insertFirst("Convoy", 500);

        theList.displayList();

        System.out.println("Find Kali : " + theList.findCity("Kali"));

        // ternary operator
        String output = (theList.findCity("Polson") == true)
                ? "City Found" : "City Not Found";
        System.out.println("Polson: " + output);

        output = (theList.findCity("Somers") == true)
                ? "City Found" : "City Not Found";
        System.out.println("Somers: " + output);

        theList.deleteFirst();
        theList.displayList();

        theList.deleteCity("Chicago");
        theList.displayList();

        theList.insertAfter("Polson", "New York", 10000000);
        theList.displayList();

        theList.deleteList();
        theList.displayList();

    }

}

```





---

End Of Topic



