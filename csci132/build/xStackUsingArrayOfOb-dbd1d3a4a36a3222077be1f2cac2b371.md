# Stack  - Using Array of Objects



## Stack Methods



Methods usually associated with a __stack__ are as follows:

* __Push__ - adds data to the stack
* __Pop__ - removes data from the stack
* __Peek__ - retrieves the next piece/top data from the stack, but does not remove it.
* __isFull__ - this is used when making a stack with an array since an array has a limited number of elements.
* __isEmpty__ - this is used to determine if the stack is empty.


```{tip}
isFull is not needed if a Stack is created using a Linked List
```


Details discussed [here](StacksAndQueues)



## Lecture Code

```java
/*
 * Project: Stack Using Array of Objects
 * Programmer: James Goudy
 * DS132SU_StackArray
 *
 *
 * Stack
 * push
 * pop
 * peek
 * isEmpty
 * isFull
 *
 *
 */

class Town {

    public String city;
    public int population;

    // constructor
    public Town(String city, int population) {
        this.city = city;
        this.population = population;
    }

    public void displayCity() {
        System.out.print("{" + city + ", " + population + "} ");
    }

}

class Stack {

    private int maxSize;
    private Town[] stackArray;
    private int top = -1;

    //constructor
    public Stack(int maxSize) {
        this.maxSize = maxSize;
        stackArray = new Town[maxSize];
        top = -1;
    }

    public boolean push(String city, int population) {
        
        // add data to the stack
        if (isFull()) {
            return false;
        } else {
            Town theTown = new Town(city, population);
            stackArray[++top] = theTown;
            return true;
        }

    }

    public Town pop() {
        // remove data from the stack
        return stackArray[top--];
    }

    public Town peek() {
        // look/peek at the top of the stack
        return stackArray[top];
    }

    public boolean isEmpty() {
        //check if the array is empty
        return (top == -1);
    }

    public boolean isFull() {
        // check if the array is full
        return (top == maxSize - 1);
    }

}

public class DS132SU_StackArray {

    public static void main(String[] args) {

        // create a stack
        Stack myStack = new Stack(10);
        Town tempTown = null;
        
        // add data to the stack
        myStack.push("Kali", 300000);
        myStack.push("Bozeman", 100000);
        myStack.push("Whitefish", 40000);
        myStack.push("Columbia Falls", 30000);

        // peek at the top data
        System.out.print("Peek - ");
        myStack.peek().displayCity();
        System.out.println("");

        // pop one data object from the stack and store it in an object
        tempTown = myStack.pop();
        tempTown.displayCity();
        
        // empty the list
        while (!myStack.isEmpty()) {
            myStack.pop().displayCity();
        }

        System.out.println("");

        //ternary operator
        boolean flag;
        flag = myStack.push("Plains", 15000) ? true : false;

        if (flag) {
            System.out.println("Item added");
        } else {
            System.out.println("Item NOT added");
        }

        System.out.print("\nbye");
    }
}

```



---

End of Topic



