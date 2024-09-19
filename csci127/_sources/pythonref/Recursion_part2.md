# Recursion - Loops vs Recursion



## Recursion vs. Loops: A Comparative Analysis

Recursion and loops are both programming techniques used to execute code multiple times. However, they differ in their approach and implementation.

### Recursion

- **Definition:** A recursive function is a function that calls itself directly or indirectly.
- **Mechanism:** It breaks down a problem into smaller, similar subproblems and solves each subproblem recursively.
- **Termination:** A base case is defined to stop the recursion and prevent an infinite loop.
- **Example:** Factorial calculation, Fibonacci sequence.

### Loops

- **Definition:** A loop is a programming construct that repeatedly executes a block of code until a certain condition is met.
- **Types:** While loops, for loops, do-while loops.
- **Mechanism:** The loop condition is evaluated at the beginning or end of each iteration.
- **Example:** Iterating over an array, counting numbers.

**Comparison Table:**

| Feature         | Recursion                                               | Loops                                                   |
| --------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| **Mechanism**   | Function calls itself                                   | Iterates over a block of code                           |
| **Termination** | Base case                                               | Loop condition                                          |
| **Performance** | Can be slower due to function calls                     | Generally faster                                        |
| **Readability** | Can be harder to understand for complex problems        | Often more straightforward                              |
| **Use Cases**   | Divide-and-conquer algorithms, tree and graph traversal | Iterating over collections, performing repetitive tasks |

**When to Use Which:**

- **Recursion:**
  - Problems that can be naturally divided into smaller, similar subproblems.
  - Tree and graph traversal.
  - Divide-and-conquer algorithms.
- **Loops:**
  - Iterating over collections (arrays, lists, etc.).
  - Performing repetitive tasks with a known number of iterations.
  - Simple, straightforward calculations.

**Note:** In some cases, both recursion and loops can be used to solve the same problem. However, one approach might be more efficient or easier to understand than the other depending on the specific circumstances. It's often a good practice to consider both options and choose the one that best suits the problem at hand.



```python
import datetime
# Developer: James Goudy
# Date: 9/13/24

# The purpose of this program is to show that
# recursion uses memory resources. It also
# compares this to using a traditional loop.

# global variables
gcntr = 0
lcntr = 0

def runLoop():
      
        # variables
        loopCntr = 1
        run = True
        choice = "y"

        while(run):

            global lcntr 

            # increment counter
            lcntr += 1

            # print count
            print(f"c Loop counter: {lcntr}")

            # check to see if user wants to stop
            # stops every 100,000
            if(lcntr % 100000 == 0):
                choice = input("Continue y/n : ").lower()
                if(choice == "n"):
                    run = False


def runLoopsByTime(secsToRun):
     
    run = True
    global lcntr

    startTime = datetime.datetime.now()
    endTime = datetime.datetime.now()

    try:
        while(run):
            
            # increment counter
            lcntr += 1

            # print counter
            print(f"t Loop Counter: {lcntr}")
            
            endTime = datetime.datetime.now()

            mytimeDif = int((endTime - startTime).total_seconds())

            if(mytimeDif >= secsToRun):
                run = False

    except Exception as e:
            print(f"\n*** error***\n{e}\n")
            print(f"Max number of loops: {gcntr}")
            input("Press enter to continue")
         
def runRecursion():

    global gcntr
    run = True

    # this needs to be in try statement.
    # eventually, the resources will run out
    # and cause a crash. the try prevents this.
    # the purpose here is to show the limited 
    # resources and purposely run them out
    # so you are aware of this condition.

    try:

        if(run):
            # increment counter
            gcntr = gcntr + 1

            # print count
            print(f"r Recursion counter: {gcntr}")

            # call itself
            runRecursion()
    except Exception as e:
            print(f"\n*** error***\n{e}\n")
            print(f"Max number of recursive loops: {gcntr}")
            input("Press enter to continue:  ")

def summary():
     
    global gcntr
    global lcntr

    print(f"Recursion ran" + str(gcntr).rjust(9," ") + " times")
    print(f"Loops     ran" + str(lcntr).rjust(9," ") + " times")
     

def menu():
     
    choice = -1
    
    
    menuText = """
    Recursion Example
    1. Count loops by increments of 100,000
    2. Count loops by time in seconds
    """
    print(menuText)

    choice = int(input("Enter 1 or 2: "))

    if(choice == 1):
        runRecursion()
        runLoop()
    else:
        secs = int(input("Enter number of secs to run: "))
        runRecursion()
        runLoopsByTime(secs)




def main():

    mySecs = 120

    menu()

    summary()

    print("\nbye\n")

main()
```



## Analysis of the Code:

This code provides a basic example of loops and recursion in Python. Here's a breakdown of each function:

**1. Global Variables:**

- `gcntr`: This global variable keeps track of the number of times the `runRecursion` function is called.
- `lcntr`: This global variable tracks the number of iterations in both `runLoop` and `runLoopsByTime` functions.

**2. Functions:**

- `runLoop()`:

  - This function uses a `while` loop to continuously increment the `lcntr` and print its value.
  - It checks every 100,000 iterations if the user wants to continue (stops on "n").

- `runLoopsByTime(secsToRun)`:

  - It uses a `while` loop to keep iterating as long as `run` is True.
  - It increments `lcntr` and prints its value.
  - It calculates the elapsed time using `datetime` and stops the loop if it reaches `secsToRun`.

- `runRecursion()`:

  - This function demonstrates recursion by calling itself within the loop. 

    > :::Note
    > **Important Note:** This version deliberately lacks a base case, causing an intentional Stack Overflow Error when ran. This is to show that resources do get consumed each time the function is recursively called.
:::



  - It increments `gcntr` and prints its value.

- `summary()`:

  - This function simply displays the final count of both `gcntr` and `lcntr`.

- `menu()`:

  - This function displays a menu and takes user input (1 or 2).
  - Based on the choice, it calls `runRecursion` and then either `runLoop` or `runLoopsByTime` with user-defined seconds.

- `main()`:

  - This function sets a default time (120 seconds) for `runLoopsByTime`.
  - It calls the `menu` function to get user input.
  - Finally, it calls `summary` to display the final counts and prints a goodbye message.

**Key Points:**

- The code uses global variables, which can be a bad practice for larger projects as it can lead to unintended side effects. Consider using arguments or local variables within functions.
- The `runRecursion` function lacks a base case, leading to an infinite loop and eventually a "Stack Overflow Error" when run.  A base case is essential for recursion to terminate.
- The code demonstrates how loops and recursion can be used for counting iterations.

**Overall:**

This code provides a basic introduction to loops and recursion. However, it's important to understand the limitations of recursion and implement proper base cases to avoid infinite loops. Additionally, consider using local variables or arguments instead of global variables for better code maintainability.