# Programming To The Interface, Not The Implementation"



**"Programming to the interface, not the implementation," including the definitions  of Interface and Abstract**



## Background Information 

**1. Definitions**

- **Abstract Class:**

  - An abstract class is a class declared with the `abstract` keyword.

  - It **cannot be instantiated** directly using `new`.

  - It **can contain** both **abstract methods** (methods without implementation) and **concrete methods** (methods with implementation).

  - 

  - It1 can also have instance variables (state) and constructors, just like a regular class.

  - A (concrete) class `extends` an abstract class and *must* provide implementations for any inherited abstract methods.

  - Abstract classes are often used as a **base class** for a group of related subclasses, providing some common implementation details or state while leaving other parts for the subclasses to define. They represent an "is-a" relationship with some shared structure or partial implementation.

- **Interface:**
  - In Java, an interface is a **reference type** that acts as a **contract** or a blueprint for classes.
  - It defines a set of **abstract methods** (methods without implementations, prior to Java 8) and/or **constants** (`static final` fields).
  - Since Java 8, interfaces can also contain **`default` methods** (methods with an implementation that implementing classes inherit) and **`static` methods**. Since Java 9, they can also include `private` methods.
  - A class `implements` an interface, promising to provide concrete implementations for all the abstract methods declared in that interface (unless the class itself is abstract).
  - Interfaces **cannot be instantiated** directly using `new`.
  - Their primary purpose is to define a common set of behaviors (a contract) that multiple, potentially unrelated classes can adhere to. They enable polymorphism and achieve abstraction.
  
  

**Key Difference Summary:** Interfaces primarily define a *contract* (what methods must exist), focusing on *what* a class can do. Abstract classes can provide a *partial implementation* and common *state*, often serving as a structural base for related classes. A class can implement multiple interfaces but can only extend one class (abstract or concrete).



## Programming to the Interface, Not the Implementation

This is a fundamental design principle in object-oriented programming. It means:

**When you declare variables, write method parameters, or specify return types, you should use the most general type possible that provides the necessary functionality – usually an interface type – rather than a specific concrete class type.**

- **"Programming to the Interface":** Your code depends on the *contract* defined by the interface (e.g., `Set`, `List`, `Map`). It interacts with objects based *only* on the methods and behaviors guaranteed by that interface.

  Java

  ```
  // GOOD: Programming to the 'Set' interface
  Set<String> names = new HashSet<>();
  processSet(names);
  
  public void processSet(Set<String> data) { // Accepts any kind of Set
      // Code here only uses methods defined in the Set interface
      if (data.contains("Alice")) {
           data.remove("Alice");
      }
      // ...
  }
  ```

- **"Not the Implementation":** You avoid tying your code directly to a specific concrete class (e.g., `HashSet`, `ArrayList`, `HashMap`) unless you absolutely need functionality unique to that specific class (which is rare for general use).

  Java

  ```
  // LESS FLEXIBLE: Programming to the 'HashSet' implementation
  HashSet<String> names = new HashSet<>();
  processSpecificSet(names);
  
  public void processSpecificSet(HashSet<String> data) { // Only accepts HashSets
     // Code might potentially use HashSet-specific methods (if any existed beyond Set)
     // or implicitly rely on HashSet's behavior (like lack of order).
     // ...
  }
  ```

**Why follow this principle?**

1. **Flexibility/Maintainability:** Your code becomes much easier to change. If you decide you need a different implementation later (e.g., you need sorted elements), you only change the object creation part (`new ...()`), not the rest of the code that uses the object via its interface.
2. **Loose Coupling:** Components of your system depend on abstract contracts rather than concrete details of other components. This reduces dependencies and makes the system more modular. Changes in one part are less likely to break others.
3. **Testability:** It's easier to substitute mock objects (for testing) that implement the same interface.
4. **Abstraction:** It hides unnecessary implementation details, making the code cleaner and focusing on the essential behavior.

