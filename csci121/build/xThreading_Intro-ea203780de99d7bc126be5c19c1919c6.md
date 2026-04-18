# **Chapter: Multithreading in Java — Concurrency, Control, and Correctness**

------

## **Introduction**

Modern software does not wait politely. It responds, streams, computes, and listens—often all at once. Java threading is the mechanism that allows a single program to execute multiple paths of logic concurrently. Used well, it delivers responsiveness and performance. Used poorly, it quietly corrupts data and leaves bugs that only appear under pressure.

This chapter builds a precise mental model of Java threads: what they are, how they behave, and how to control them without breaking your program.

------

## **Chapter at a Glance**

- What threads are and how Java implements them
- Why multithreading improves responsiveness and throughput
- Two core approaches: `extends Thread` vs `implements Runnable`
- What an interface is and why `Runnable` uses one
- Thread lifecycle and execution flow
- Critical methods: `start()`, `run()`, `sleep()`, `join()`
- Race conditions and synchronization
- Practical patterns and common pitfalls

------

## **Learning Goals**

By the end of this chapter, you will be able to:

- Define and explain Java threads and concurrency
- Explain what an interface is and how it differs from a class
- Implement threads using both inheritance and interfaces
- Analyze execution order and thread interleaving
- Identify and fix race conditions
- Apply synchronization correctly
- Debug multithreaded behavior

------

## **What This Concept Is**

A **thread** is a lightweight unit of execution within a process. Multiple threads share the same memory space but execute independently.

### **Definition**

A thread is an independent path of execution within a program that shares memory with other threads in the same process.

------

## **Why This Concept Matters**

Single-threaded programs are predictable—but slow and unresponsive under load. Multithreading enables:

- Responsive user interfaces
- Parallel computation
- Efficient resource utilization

**Key Point**
Concurrency is not about doing more work—it is about doing work more effectively.

------

## **Syntax and Basic Form**

Java provides two primary ways to create threads:

### 1. Extending `Thread`

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Running thread");
    }
}

MyThread t = new MyThread();
t.start();
```

### 2. Implementing `Runnable`

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Running runnable");
    }
}

Thread t = new Thread(new MyRunnable());
t.start();
```

------

## **What Is an Interface? (And Why Runnable Uses One)**

Before comparing `Thread` and `Runnable`, you need a precise understanding of interfaces—because this design choice is not accidental. It is one of the most important design decisions in Java’s concurrency model.

### **Definition**

An interface is a reference type in Java that defines a contract—a set of method signatures that a class must implement, without providing full implementation details (with some modern exceptions like default methods).

At its core, an interface answers one question:

> *What must this object be able to do?*

—not

> *What is this object?*

------

### **Basic Syntax**

```java
interface Flyable {
    void fly();
}
```

A class that implements the interface must provide the behavior:

```java
class Bird implements Flyable {
    public void fly() {
        System.out.println("Flapping wings");
    }
}
```

------

### **Key Properties of Interfaces**

- A class can implement multiple interfaces
- Interfaces define behavior, not state (traditionally)
- Methods are abstract by default (pre-Java 8)
- They enable loose coupling and flexible design

------

### **Why Runnable Is an Interface**

Now the important part: why did Java make `Runnable` an interface instead of a class?

```java
public interface Runnable {
    void run();
}
```

Because Java already has single inheritance.

If `Runnable` were a class, you would be forced into this:

```java
class MyTask extends Runnable { } // impossible in Java
```

Which means you could not extend anything else.

Instead, Java allows:

```java
class MyRunnable extends Smile implements Runnable
```

From your program:

- `MyRunnable` inherits behavior from `Smile`
- It *also* defines thread behavior via `Runnable`

That is flexibility. That is why this design wins.

------

### **Key Point**

Interfaces separate *what you do* from *how you run it*.

- `Runnable` = the task
- `Thread` = the execution mechanism

------

### **Checkpoint**

Why is `Runnable` preferred?

If your answer is “because it’s cleaner,” you’re missing it.

Correct answer:
It preserves inheritance flexibility and promotes better separation of concerns.

------

## **Core Behavior**

When you call `start()`, the JVM:

1. Allocates a new thread
2. Calls `run()` on that thread
3. Schedules execution alongside other threads

**Checkpoint**
Calling `run()` directly does **not** start a new thread—it executes in the current thread.

------

## **Key Terminology**

- Thread
- Interface
- Runnable
- Concurrency
- Synchronization
- Race condition
- Shared state
- Atomic operation
- Thread lifecycle

------

## **Simple Example**

```java
Thread t = new Thread(() -> {
    System.out.println("Hello from another thread!");
});
t.start();
```

------

## **Full Program Example**

The following program demonstrates all core concepts: thread creation, runnable usage, race conditions, and synchronization.

```java
package j2_threadingconsole;

import java.util.Scanner;

// ------------------------------------------------------------
// CLASS: MyThread
// Demonstrates creating a thread by EXTENDING the Thread class
// ------------------------------------------------------------
class MyThread extends Thread {

    private final String name;

    public MyThread(String name) {
        this.name = name;
    }

    // run() executes when start() is called
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("MyThread | " + name + " | Count: " + i);
            try {
                Thread.sleep(500); // slow output so interleaving is visible
            } catch (InterruptedException e) {
                System.out.println(name + " was interrupted.");
            }
        }
    }
}

// Simple inheritance example (not required for threading)
class Smile {
    public String happyFace() {
        return "Smile";
    }
}

// ------------------------------------------------------------
// CLASS: MyRunnable
// Demonstrates implementing Runnable (preferred approach)
// ------------------------------------------------------------
class MyRunnable extends Smile implements Runnable {

    private final String name;

    public MyRunnable(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("MyRunnable | " + name + " | Count: " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println(name + " was interrupted.");
            }
        }
    }
}

// ------------------------------------------------------------
// CLASS: Counter (UNSAFE)
// Shared mutable state without synchronization
// ------------------------------------------------------------
class Counter {

    private int count = 0;

    public void increment() {
        count++; // NOT thread-safe (read → modify → write)
    }

    public int getCount() {
        return count;
    }
}

// ------------------------------------------------------------
// CLASS: SafeCounter (SAFE)
// Uses synchronized to prevent race conditions
// ------------------------------------------------------------
class SafeCounter {

    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

// ------------------------------------------------------------
// MAIN DRIVER CLASS
// ------------------------------------------------------------
public class J2_ThreadingConsole {

    // Demo 1: Extending Thread
    static void threadDemo() {
        System.out.println("\n===== Demo 1: Extending Thread =====");

        MyThread t1 = new MyThread("Thread-T1");
        MyThread t2 = new MyThread("Thread-T2");

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println("Thread demo interrupted.");
        }

        System.out.println("Demo 1 complete.\n");
    }

    // Demo 2: Implementing Runnable
    static void runnableDemo() {
        System.out.println("\n===== Demo 2: Implementing Runnable =====");

        Thread t1 = new Thread(new MyRunnable("Runnable-T1"));
        Thread t2 = new Thread(new MyRunnable("Runnable-T2"));

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println("Runnable demo interrupted.");
        }

        System.out.println("Demo 2 complete.\n");
    }

    // --------------------------------------------------------
    // DEMO 3: Race Condition
    //
    // The statement count++ looks like one step, but it is really three steps:
    // 1. read the current value of count
    // 2. add 1
    // 3. write the new value back to memory
    //
    // If two threads interleave those steps, one thread can overwrite the other
    // thread's update. When that happens, an increment is "lost", and the final
    // count can be less than expected.
    //
    // This is called a race condition because 
    // the threads are effectively "racing"
    // to update the same shared data without synchronization.
    // --------------------------------------------------------
    static void raceConditionDemo() {

        System.out.println("\n===== Demo 3: Race Condition =====");

        for (int trial = 1; trial <= 5; trial++) {

            Counter counter = new Counter();

            Thread t1 = new Thread(() -> {
                for (int i = 0; i < 2_000_000; i++) {
                    counter.increment();
                }
            });

            Thread t2 = new Thread(() -> {
                for (int i = 0; i < 2_000_000; i++) {
                    counter.increment();
                }
            });

            t1.start();
            t2.start();

            try {
                t1.join();
                t2.join();
            } catch (InterruptedException e) {
                System.out.println("Race condition demo interrupted.");
            }

            System.out.println("Trial " + trial +
                    " - Expected: 4000000, Actual: " + counter.getCount());
        }

        System.out.println("Demo 3 complete.\n");
    }

    // Demo 4: Fix with synchronized
    static void safeCounterDemo() {
        System.out.println("\n===== Demo 4: Safe Counter with synchronized =====");

        SafeCounter counter = new SafeCounter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 2_000_000; i++) {
                counter.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 2_000_000; i++) {
                counter.increment();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println("Safe counter demo interrupted.");
        }

        System.out.println("Expected: 4000000, Actual: " + counter.getCount());
        System.out.println("Demo 4 complete.\n");
    }

    public static void main(String[] args) {

        Scanner myScan = new Scanner(System.in);

        threadDemo();
        System.out.println("Press Enter to continue...");
        myScan.nextLine();

        runnableDemo();
        System.out.println("Press Enter to continue...");
        myScan.nextLine();

        raceConditionDemo();
        System.out.println("Press Enter to continue...");
        myScan.nextLine();

        safeCounterDemo();

        myScan.close();
    }
}

```



------

## **Detailed Walkthrough**

### Demo 1: Extending Thread

Two threads run independently and interleave output. There is no guaranteed order.

### Demo 2: Implementing Runnable

Same behavior, but now logic is decoupled from the thread object.

### Demo 3: Race Condition

Two threads increment a shared counter.

Expected:

```
4000000
```

Actual:

```
3872451 (or some unpredictable number)
```

------

## **Behind-the-Scenes Explanation**

The statement:

```java
count++;
```

Breaks into:

1. Read `count`
2. Add 1
3. Write result

Two threads can interleave these steps and overwrite each other.

### **Definition**

A race condition occurs when multiple threads access shared data and the outcome depends on timing.

------

## **Synchronization**

```java
public synchronized void increment() {
    count++;
}
```

This ensures only one thread executes the method at a time.

**Key Point**
Synchronization enforces mutual exclusion on shared resources.

------

## **Comparison**

| Approach    | Extends Thread | Implements Runnable |
| ----------- | -------------- | ------------------- |
| Inheritance | Required       | Not required        |
| Flexibility | Limited        | High                |
| Reusability | Low            | High                |
| Recommended | Rarely         | Yes                 |

**Verdict:**
Use `Runnable` unless you have a specific reason not to. Inheritance is expensive—don’t spend it casually.

------

## **Common Mistakes and Debugging Problems**

### Common Mistake

Calling `run()` instead of `start()`

### Debugging Note

If output appears sequential instead of interleaved, you are not actually using threads.

------

### Common Mistake

Assuming thread execution order

Reality: The JVM scheduler is not your employee.

------

### Common Mistake

Ignoring shared state

If two threads touch the same data without protection, you have a bug—even if you haven't seen it yet.

------

## **Warning**

Race conditions do not fail consistently. They fail statistically.
That makes them dangerous—they pass tests and fail in production.

------

## **Best Practices**

Use `Runnable` or lambda expressions for thread logic
Minimize shared mutable state
Use synchronization or higher-level concurrency tools
Avoid premature optimization with threads
Test under load, not just correctness

------

## **Key Terms**

- Thread
- Interface
- Runnable
- Synchronization
- Race condition
- Atomicity
- Shared memory

------

## **Chapter Summary**

Java threading enables concurrent execution within a program, improving responsiveness and efficiency. Threads can be created by extending `Thread` or implementing `Runnable`, with the latter offering greater flexibility through the use of interfaces. Interfaces define behavioral contracts, allowing classes to participate in threading without sacrificing inheritance. However, concurrency introduces complexity—especially when threads share data. Without synchronization, race conditions emerge, producing unpredictable results. Proper design minimizes shared state and uses synchronization carefully to ensure correctness.

------

## **Final Takeaway**

Threads are power tools.
Interfaces are the design that makes them usable.
Separate the task from the execution—and your code stays sane under pressure.

------

## **Review Questions**

1. What does `start()` do?
   A. Calls run directly
   B. Creates a new thread and calls run
   C. Pauses execution
   D. Stops a thread
2. Which is preferred?
   A. Extending Thread
   B. Implementing Runnable
   C. Both equally
   D. Neither
3. What is a race condition?
   A. Fast execution
   B. Thread priority issue
   C. Timing-dependent data corruption
   D. Deadlock
4. What is an interface?
   A. A class with only variables
   B. A contract defining required methods
   C. A thread type
   D. A synchronization tool
5. Why is `count++` unsafe?
   A. Syntax error
   B. Too slow
   C. Not atomic
   D. JVM bug
6. What does `join()` do?
   A. Starts thread
   B. Stops thread
   C. Waits for thread to finish
   D. Synchronizes threads
7. Calling `run()` directly:
   A. Starts a thread
   B. Runs in same thread
   C. Causes error
   D. Synchronizes
8. Threads share:
   A. CPU
   B. Memory
   C. Stack
   D. None
9. Why is `Runnable` preferred?
   A. Faster execution
   B. Supports multiple inheritance behavior
   C. Uses less memory
   D. Simpler syntax
10. A synchronized method:
    A. Runs faster
    B. Blocks all threads permanently
    C. Allows one thread at a time
    D. Prevents thread creation

------

## **Answer Key**

1. B
2. B
3. C
4. B
5. C
6. C
7. B
8. B
9. B
10. C

------

## **Glossary**

**Thread**
A unit of execution within a program.

**Interface**
A contract that defines required methods a class must implement.

**Runnable**
An interface representing a task to be executed by a thread.

**Race Condition**
A bug caused by unsynchronized access to shared data.

**Synchronization**
Mechanism to control access to shared resources.

**Atomic Operation**
An operation that completes without interruption.

**Shared State**
Data accessible by multiple threads.