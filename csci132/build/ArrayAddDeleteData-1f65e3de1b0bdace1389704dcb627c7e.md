# Array Add and Delete Data



## Key Ideas

* In working with arrays, keeping data continuous is a good practice the majority of the time.  If data in an element is deleted, the data in the elements to the right should be shifted left to remove the empty space.  

* Also, there may be times when data has to be inserted into an array that has continuous data elements.  In this case, data is shifted to the right to create a space where the new data can be inserted.

  

```{tip}
In many cases, arrays are usually set to have more elements than is needed. Therefore, it is important to create a variable that will alway track the number of items in the array. 
```





## Lecture Code

```java
/*
 *
 * Project: Add Delete In an Array
 * Programmer: J Goudy
 
 */


public class DS_ArraysAddDelete {

    static String[] arrString;
    static int arrStrDataCount = 0;

    static void loadStringArray() {
    // this is a helper function to setup our example array
        
        String[] names = {"Adam", "Bobby", "Howard", "Mary", "Zuzu"};

        //load names
        for (int c = 0; c < names.length; c++) {
            arrString[c] = names[c];
        }

		//set our number of data items
        arrStrDataCount = names.length;

        // print number of items
        System.out.println("DataCount = " + arrStrDataCount);

        printArray(arrString, arrStrDataCount);

    }

    static void printArray(String[] theArray, int dataCount) {
    // This function prints the array. 
    // Note that an array is being passed to it.
        
        // for spacing
        System.out.println();
        
        // iterate through the array and print the data
        for (int i = 0; i < dataCount; i++) {
            System.out.print(theArray[i] + " ");
        }

        System.out.println("\n------------\n");

    }

    static void insertStringByPos(int pos, String aName) {
        // ---------- Do some checks ---------------------

        // check if position is withing array bounds
        if (pos > arrStrDataCount) {
            System.out.println("Error out array bounds");

            // exit the function
            return;
        }

        // check if the array is full
        if (arrStrDataCount >= arrString.length) {
            System.out.println("Array is full");
            return;
        }

        // -------------- Insert Code --------------------------
        // shift to right
        // note that the loop is starting at the end and 
        // working backwards to the insert spot (pos)
        for (int i = arrStrDataCount; i > pos; i--) {

            arrString[i] = arrString[i - 1];
        }

        // insert the new name
        arrString[pos] = aName;

        // increment our data Count
        arrStrDataCount++;

        // print the array to show data was inserted
        printArray(arrString, arrStrDataCount);

    }

    static void deleteByPos(int pos) {
        // check if there is contents
        if (arrStrDataCount <= 0) {
            System.out.println("Array is empty\n");
            return;
        }

        // check if the position to delete is out of bounds
        if (pos >= arrStrDataCount) {
            System.out.println("Pos is out of bounds\n");
            return;
        }

        // -----------  Delete Code ---------------------
        // shift loop
        // note that the loop starts at the element location 
        // that is being deleted
        for (int i = pos; i < arrStrDataCount; i++) {
            arrString[i] = arrString[i + 1];
        }

        // decrease the item count by 1
        arrStrDataCount--;

        printArray(arrString, arrStrDataCount);

    }

    public static void main(String[] args) {

        // instantiate the data array
        arrString = new String[8];

        try {
            
            // setup the demo array
            loadStringArray();

            // insert "Bubba" in the third positon of the array
            insertStringByPos(2, "Bubba");

            // delete the data in the second 
            // element/position of the array
            deleteByPos(1);
            
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
        
        System.out.println("\n\nbye\n");
    }
}

```



------

End Of Topic