# Stacks and Queues



## Key Ideas

* Stacks
* Queues



## Discussion

Stacks and queues are a way of organizing data and consuming data. The data can be stored in an array or linked list. 

### Stack ###

```{Admonition} Definition
A __Stack__ is a way of organizing and consuming data where the Last In is the First Out (LIFO). Or it can be thought of as First In is the Last Out (FILO). 
```



Most people think of a stack as a stack of plates, where each plate represents data. Data is _**pushed**_ onto the stack. Meaning. it is added to the array or linked list. Data is consumed by _**popping**_ it off of the stack. Meaning, that the last piece of data added to the stack is removed from the array or linked list. This data is usually used by the part of the program that is popping/removing it from the stack.  _**Peeking**_ is looking at the last/next piece of data, but _not_ removing it from the stack. An example is [Stack Array](StackUsingArrayOfObjects)

Methods usually associated with a __stack__ are as follows:

* __Push__ - adds data to the stack
* __Pop__ - removes data from the stack
* __Peek__ - retrieves the next piece/top data from the stack, but does not remove it.
* __isFull__ - this is used when making a stack with an array since an array has a limited number of elements.
* __isEmpty__ - this is used to determine if the stack is empty.

### Queue ###

```{Admonition} Definition
A __Queue__ is a way of organizing and consuming data where the First In is the First Out (FIFO).
```

Most people think of a queue as people standing in a line, where people represent data.  Data is consumed in the order in which it was added. 

Methods usually associated with a __queue__ are as follows:

* __Enqueue__ - add data to the queue. 
* __Dequeue__ - remove data from the queue
* __Peek__ - retrieves the next piece/"head" data from the queue, but does not remove it.
* __isFull__ - this is used when making a queue with an array since an array has a limited number of elements.
* __isEmpty__ - this is used to determine if the queue is empty.

### Priority Queue

```{admonition} Definition
A __Priority Queue__ is a queue where there is a mechanism to place data at the start or infront of other data.
```




---

End Of Topic



