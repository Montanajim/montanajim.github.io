# Queue  - Using Array Of Objects



## Queue Methods

Methods usually associated with a __queue__ are as follows:

* __Enqueue__ - add data to the queue. 
* __Dequeue__ - remove data from the queue
* __Peek__ - retrieves the next piece/"head" data from the queue, but does not remove it.
* __isFull__ - this is used when making a queue with an array since an array has a limited number of elements.
* __isEmpty__ - this is used to determine if the queue is empty.



```{tip}
isFull is not needed if a Stack is created using a Linked List
```



```
 // make a new queue object

 Queue theQue = new Queue(5);

 /*
  NOTICE THE CODE BELOW - 
  make an object from the sub class
 */

Queue.Town theTown = theQue.new Town("", 0);
```






Details discussed 

## Lecture Code

```java
/*
 *Programmer: James Goudy
 *Project: Queue of Objects
 *
 */
package com.mycompany.ds132su_queue;

/**
 *
 * @author jgoudy
 */
class Queue {

    class Town {
        // subclass
        public String city;
        public int population;

        public Town(String city, int population) {
            this.city = city;
            this.population = population;
        }

        public void displayTown() {
            System.out.print("{" + city + " - " + population + "} ");
        }

    }// end of town

    private int maxSize;
    private Town[] queArray;
    private int numItems;
    private int head;
    private int tail;

    // Queue Constructor
    public Queue(int maxSize) {
        this.maxSize = maxSize;
        queArray = new Town[maxSize];
        head = 0;
        tail = -1;
        numItems = 0;
    }

    public boolean isFull() {
        return (numItems == maxSize);
    }

    public boolean isEmpty() {
        return (numItems == 0);
    }

    public boolean enqueue(String city, int population) {

        // insert at tail
        // "enqueue"
        if (isFull()) {
            return false;
        }

        // create town
        Town newTown = new Town(city, population);

        // wrap to front if neccessary
        if (tail == maxSize - 1) {
            tail = -1;
        }

        // add object to array
        queArray[++tail] = newTown;

        // increment the count of objects in the array
        numItems++;

        return true;
    }

    public Town dequeue() {
        // remove from the front - the head 
        // "dequeue"

        if (isEmpty()) {
            System.out.print("Queue is empty");
            return null;
        }

        // retreive the next in queue and move the head to
        // the next data item.
        Town temp = queArray[head++];

        if (head == maxSize) {
            head = 0;
        }

        // decrease the count of objects in the array
        numItems--;

        return temp;
    }

    public Town peek() {
        // retreive the head information but do not remove 
        return queArray[head];
    }

    public void displayQueue() {
        int cntr = 0;
        int pos = head;
        while (cntr < numItems) {
            queArray[pos].displayTown();
            cntr++;

            pos++;
            // loop to the start of the array if necessary
            if (pos == maxSize) {
                pos = 0;
            }

        }
        System.out.println("\n");
    }

} // end of queue

public class DS132SU_Queue {

    public static void main(String[] args) {

        // make a new queue object
        Queue theQue = new Queue(5);

        // make an object from the sub class
        Queue.Town theTown = theQue.new Town("", 0);

        String acity;

        theQue.enqueue("Bozeman", 100000);
        theQue.enqueue("Culver", 100001);
        theQue.enqueue("Dover", 100002);
        theQue.enqueue("Edger", 100003);

        System.out.println("\n------ Queue--------\n");

        theQue.displayQueue();

        System.out.println("\nDequeue the first two items in the queue");

        // return next item from the queue
        theTown = theQue.dequeue();
        System.out.println("\n" + theTown.city + " - " + theTown.population);

        theTown = theQue.dequeue();
        System.out.println("\n" + theTown.city + " - " + theTown.population);

        System.out.println("\n--------------\n");

        System.out.println("\nDequeue and retreive only the city");

        // another option to dequeue and retrieve city only
        acity = theQue.dequeue().city;
        System.out.println(acity);

        System.out.println("\n------ Queue--------\n");

        theQue.displayQueue();

        theQue.enqueue("Franklin", 104);
        theQue.enqueue("Georgetown", 105);
        theQue.enqueue("Highland", 106);

        System.out.println("\n------- Queue -------\n");
        theQue.displayQueue();

        System.out.println("\n----- Peek just city ---------\n");

        acity = theQue.peek().city;
        System.out.println(acity);

        System.out.println("\n----- Peek city population ---------\n");

        theTown = theQue.peek();
        System.out.println("\n" + theTown.city + " - " + theTown.population);

        System.out.println("\n------ Queue --------\n");
        // notice that peek did not remove any towns
        theQue.displayQueue();

    }
}

/*
 Output
 
------ Queue--------

{Bozeman - 100000} {Culver - 100001} {Dover - 100002} {Edger - 100003} 


Dequeue the first two items in the queue

Bozeman - 100000

Culver - 100001

--------------


Dequeue and retreive only the city
Dover

------ Queue--------

{Edger - 100003} 


------- Queue -------

{Edger - 100003} {Franklin - 104} {Georgetown - 105} {Highland - 106} 


----- Peek just city ---------

Edger

----- Peek city population ---------


Edger - 100003

------ Queue --------

{Edger - 100003} {Franklin - 104} {Georgetown - 105} {Highland - 106} 
  
 
 
 */
```



---

End Of Topic

