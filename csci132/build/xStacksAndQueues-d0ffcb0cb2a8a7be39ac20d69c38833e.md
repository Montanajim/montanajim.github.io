# Stacks and Queues



## Key Ideas

* Stacks
* Queues



## Discussion

Stacks and queues are a way of organizing data and consuming data. The data can be stored in an array or linked list. 

### Stack ###

> [!NOTE]
>
> A __Stack__ is a way of organizing and consuming data where the Last In is the First Out (LIFO). Or it can be thought of as First In is the Last Out (FILO). 
>
> 


Most people think of a stack as a stack of plates, where each plate represents data. Data is _**pushed**_ onto the stack. Meaning. it is added to the array or linked list. Data is consumed by _**popping**_ it off of the stack. Meaning, that the last piece of data added to the stack is removed from the array or linked list. This data is usually used by the part of the program that is popping/removing it from the stack.  _**Peeking**_ is looking at the last/next piece of data, but _not_ removing it from the stack. An example is [Stack Array](StackUsingArrayOfObjects)

Methods usually associated with a __stack__ are as follows:

* __Push__ - adds data to the stack
* __Pop__ - removes data from the stack
* __Peek__ - retrieves the next piece/top data from the stack, but does not remove it.
* __isFull__ - this is used when making a stack with an array since an array has a limited number of elements.
* __isEmpty__ - this is used to determine if the stack is empty.

In computer science, a stack is a LIFO (Last In, First Out) data structure that stores elements in a linear order. This means that the last element added to the stack is the first one to be removed. Stacks are often used to manage a sequence of operations, such as function calls or undo/redo functionality.

Here are some of the key properties of stacks:

- **LIFO order**: Elements are removed in the reverse order they were added.
- **Bounded capacity**: Stacks have a limited size, and adding more elements than the stack can hold will result in an error.
- **Efficient access**: Pushing and popping elements from the top of the stack is a very efficient operation, typically taking constant time.

Stacks are used in a variety of applications in computer science, including:

- **Function calls**: When a function is called, its arguments and local variables are pushed onto a stack. When the function returns, its stack frame is popped off the stack.
- **Expression evaluation**: Stacks are used to evaluate expressions in many programming languages. For example, when evaluating arithmetic expressions, operands are pushed onto the stack, and then operators are popped off the stack and applied to the operands.
- **Backtracking algorithms**: Stacks are used to store the history of decisions made in backtracking algorithms, such as depth-first search. This allows the algorithm to backtrack to previous states if it reaches a dead end.
- **Undo/redo functionality**: Stacks are used to implement undo/redo functionality in many applications. When an action is performed, the state of the application is pushed onto the undo stack. To undo the action, the state is popped off the undo stack and restored.

Here are some examples of how stacks are used in real-world applications:

- **Compilers**: Compilers use stacks to keep track of the current state of the program being compiled.
- **Interpreters**: Interpreters use stacks to evaluate expressions and statements in the program being interpreted.
- **Web browsers**: Web browsers use stacks to keep track of the history of visited web pages.
- **Operating systems**: Operating systems use stacks to manage memory allocation and process scheduling.

Stacks are a versatile and powerful data structure that is used in a wide variety of applications in computer science. Their LIFO order and efficient access make them well-suited for managing sequences of operations and storing the history of decisions made in algorithms.



### Queue ###

> [!NOTE]
>
>
> A __Queue__ is a way of organizing and consuming data where the First In is the First Out (FIFO). 
>


Most people think of a queue as people standing in a line, where people represent data.  Data is consumed in the order in which it was added. 

Methods usually associated with a __queue__ are as follows:

* __Enqueue__ - add data to the queue. 
* __Dequeue__ - remove data from the queue
* __Peek__ - retrieves the next piece/"head" data from the queue, but does not remove it.
* __isFull__ - this is used when making a queue with an array since an array has a limited number of elements.
* __isEmpty__ - this is used to determine if the queue is empty.

In computer science, a queue is a LIFO (First In, First Out) data structure that stores elements in a linear order. This means that the first element added to the queue is the first one to be removed. Queues are often used to manage a sequence of tasks or events, such as printing jobs or network traffic.

Here are some of the key properties of queues:

- **FIFO order**: Elements are removed in the order they were added.
- **Bounded capacity**: Queues have a limited size, and adding more elements than the queue can hold will result in an error.
- **Efficient access**: Adding and removing elements from the front and back of the queue are efficient operations, typically taking constant time.

Queues are used in a variety of applications in computer science, including:

- **Task scheduling**: Queues are used to schedule tasks in operating systems and other systems. For example, a print queue is used to manage the order in which print jobs are processed.
- **Network traffic**: Queues are used to manage the flow of data in networks. For example, a network buffer is used to store data packets that are waiting to be sent over a network.
- **Buffering**: Queues are used to buffer data between different components of a system. For example, a keyboard buffer is used to store characters typed on a keyboard until they can be processed by the operating system.
- **Message passing**: Queues are used to pass messages between different processes or threads. For example, a message queue is used to store messages that are waiting to be processed by a consumer process.

Here are some examples of how queues are used in real-world applications:

- **Operating systems**: Operating systems use queues to manage task scheduling, memory allocation, and device drivers.
- **Networking**: Networking protocols use queues to manage the flow of data packets.
- **Multimedia applications**: Multimedia applications use queues to buffer audio and video data.
- **Messaging applications**: Messaging applications use queues to store messages that are waiting to be delivered to recipients.

Queues are a versatile and powerful data structure that is used in a wide variety of applications in computer science. Their FIFO order and efficient access make them well-suited for managing sequences of tasks or events.



### Priority Queue

```{admonition} Definition
A __Priority Queue__ is a queue where there is a mechanism to place data at the start or infront of other data.
```

In computer science, a priority queue is a specialized type of queue where elements are prioritized based on their associated priority values. Elements with higher priority values are served before elements with lower priority values. Priority queues are often implemented using heap data structures, which allow for efficient insertion and extraction operations.

Here are some of the key properties of priority queues:

- **Priority-based ordering**: Elements are served based on their priority values, with higher priority elements being served first.
- **Efficient insertion and extraction**: Priority queues can efficiently insert and extract elements, typically taking logarithmic time.
- **Dynamic priority updates**: Priority values can be updated dynamically, allowing for reprioritization of elements within the queue.

Priority queues are used in a variety of applications where prioritization is important, including:

- **Task scheduling**: Priority queues are used to schedule tasks based on their urgency or importance. For example, a critical job processing system might use a priority queue to prioritize high-priority tasks over less urgent ones.
- **Network traffic management**: Priority queues can be used to prioritize network traffic based on its importance or quality of service requirements. For instance, real-time voice or video traffic might be prioritized over non-real-time data transfers.
- **Event handling**: Priority queues can be used to manage a sequence of events, ensuring that high-priority events are handled first. For example, an event-driven system might use a priority queue to prioritize system alerts or critical user interactions.
- **Algorithm optimization**: Priority queues are used in various algorithms, such as Dijkstra's algorithm for shortest path finding and A* search for pathfinding in graph-based problems.

Here are some real-world examples of how priority queues are used:

- **Operating systems**: Operating systems use priority queues to manage task scheduling, ensuring that high-priority tasks, such as system processes, are executed before less urgent user tasks.
- **Network routers**: Network routers use priority queues to manage network traffic, prioritizing real-time audio or video traffic over non-real-time data transfers.
- **Emergency response systems**: Emergency response systems might use priority queues to prioritize dispatching emergency responders based on the severity of incidents.
- **Hospital patient care**: Critical care units in hospitals might use priority queues to manage patient care, ensuring that patients with the most urgent medical needs are seen first.

Priority queues are a valuable data structure that plays a crucial role in various applications that require efficient prioritization and management of tasks, events, or data. Their ability to handle dynamic priority updates and their efficient insertion and extraction operations make them a well-suited choice for prioritizing elements in a variety of contexts.


---

End Of Topic



