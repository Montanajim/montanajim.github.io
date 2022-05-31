# ArrayLists

## Key Ideas

* ArrayLists



## Readings

https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html

https://www.geeksforgeeks.org/arraylist-in-java/



## Concepts



```{admonition} Definition
**ArrayList** is a resizable one-dimensional array that can store any data type in any element.  
```



```{admonition} Tip
The best practice is to make all the data the same type. This is done using the <datatype> classifier. 
```

```java

    // only accept data that is a double
    ArrayList<Double> myArrayList = new ArrayList();

    // only accept data that is an int
    ArrayList<Integer> myArrayList = new ArrayList();

    // only accept data that is a String
    ArrayList<String> myArrayList = new ArrayList();

    // accepts any type of data including mixed
    ArrayList myArrayList = new ArrayList();
```



## Lecture Code

### Observations:

* We create an ArrayList with the following syntax:

 ```java
  ArrayList<datatype> arraylistname = new ArrayList();
 ```

* *.add(value)* method is used to add a data to the ArrayList

* *.remove(index)* method will remove data by position

* *.remove(value)* method will remove data by value

* *.clear()* method will clear the ArrayList of all elements - "emptying it"

* We iterate/loop through the array using a for statement:

```java
/*
Project: ArrayLists
Programmer: James Goudy
 */

import java.util.ArrayList;
import java.util.Collections;


public class Arraylist_Lecture {

    public static void main(String[] args) {
        // Variables
        String stryy;
        
        
        //////////////////////////////////////////////////
        //
        // Array List
        //
        //////////////////////////////////////////////////

        // create the Array List
        // Note: <String> is telling the arraylist to only
        // accept data that is a String
        ArrayList<String> cars = new ArrayList();

        // use the add method to add data
        cars.add("Ford");
        cars.add("Chevy");
        cars.add("Scion");
        cars.add("Honda");

        //Retrieve one item - use the .get(x) where x is an int index location
        System.out.println(cars.get(3));

        //print out all items
        for (int CarCntr = 0; CarCntr < cars.size(); CarCntr++) {
            System.out.println("This is " + cars.get(CarCntr));
        }

        ///////////////////////////////////////
        // Sort an Arraylist
        ///////////////////////////////////////

        // To sort an Arraylist, you must do it through the collections
        // library.  Add imports java.util.collections

        Collections.sort(cars);
        // print out all items
        System.out.println("\n\nCars sorted list ");
        for (int CarCntr = 0; CarCntr < cars.size(); CarCntr++) {
            System.out.println("This is " + cars.get(CarCntr));
        }

        System.out.println("\n----------------\n");
        // Remove Scion by referencing the index
        cars.remove(3);

        for (int CarCntr = 0; CarCntr < cars.size(); CarCntr++) {
            System.out.println("This is " + cars.get(CarCntr));
        }

        System.out.println("\n----------------\n");

        // Remove Chevy by using the actual data
        stryy = "Chevy";
        cars.remove(stryy);

        for (int CarCntr = 0; CarCntr < cars.size(); CarCntr++) {
            System.out.println("This is " + cars.get(CarCntr));
        }

        System.out.println("\n----------------\n");

        // insert an item - here we are inserting Dodge at the beginning of the list
        cars.add(0, "Dodge");

        for (int CarCntr = 0; CarCntr < cars.size(); CarCntr++) {
            System.out.println("This is " + cars.get(CarCntr));
        }

        // To empty or clear the arraylist
        cars.clear();
        System.out.println("The number of elements is cars is " + 
        cars.size());
    
    }
}

```





---

End Of Topic

