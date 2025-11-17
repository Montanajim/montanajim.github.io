# Priority Queue

## Key Ideas

* Priority Queue



```{admonition} Definition
A __Priority Queue__ is a queue where there is a mechanism to place data at the start or in front of other data.
```



## Lecture Code

``` java
// priorityQ.java
// demonstrates priority queue

/**
 *
 * @author jgoudy
 */
class PriorityQ {

    private int maxSize;
    private int[] queArr;
    private int nItems;

    // constructor
    public PriorityQ(int maxSize) {
        this.maxSize = maxSize;
        queArr = new int[maxSize];
        nItems = 0;
    }

    public boolean isFull() {
        return (nItems == maxSize);
    }

    public boolean isEmpty() {
        return (nItems == 0);
    }

    // enqueue - add to queue
    // lower numbers take a higher place in the queue
    
    public void enqueue(int key) {
        int c;

        if (isEmpty()) {
            queArr[nItems++] = key;
        } else {
            for (c = nItems - 1; c >= 0; c--) {
                if (key > queArr[c]) {
                    queArr[c + 1] = queArr[c];
                } else {
                    break;
                }
            }// end of for

            queArr[c + 1] = key;

            nItems++;
        }
    }

    // retreive the next item from the queue
    // and remove it from the queue
    public int dequeue() {
        return queArr[--nItems];
    }

    // reteive the data from the next item in the queue
    // but does NOT remove it
    public int peek() {
        return queArr[nItems - 1];
    }

    // print the queue
    public void printPriorityQ() {
        System.out.println();
        for (int c = 0; c < nItems; c++) {
            System.out.print(queArr[c] + " ");
        }
        System.out.println();

    }

} // end of class

public class Ds_priorityQueue {

    public static void main(String[] args) {

// assumption lower the number - higher the priority
        PriorityQ thePQ = new PriorityQ(10);

        // add data items to the queue
        thePQ.enqueue(30);
        thePQ.enqueue(50);
        thePQ.enqueue(10);
        thePQ.enqueue(40);
        thePQ.enqueue(20);
        thePQ.enqueue(60);
        thePQ.enqueue(5);

        // print the queue
        thePQ.printPriorityQ();

        System.out.println("\n-----------\n");

        // peek at the next data item
        System.out.println("Peek " + thePQ.peek());

        System.out.println("\n-----------\n");

        // remove all the items from the queue
        while (!thePQ.isEmpty()) {
            int x = thePQ.dequeue();
            System.out.print(x + " ");
        }

        System.out.println("\n-----------\n");

    }
}

/* Output
  
 60 50 40 30 20 10 5 

-----------

Peek 5

-----------

5 10 20 30 40 50 60 
-----------
 
 */
```



---

End Of Topic



