

# Decorators



Decorators are:

A design pattern that allows you to modify the behavior of a function or method without directly changing its code.
They are essentially functions that wrap other functions, adding extra functionality before, after, or around the original function's execution.

How they work:

Decorator function:

- Takes another function as an argument.
- Returns a modified version of the original function.

Applying a decorator:

- Use the ''@'decorator_name syntax above a function definition.
- This is shorthand for function_name = decorator_name(function_name).



**Remember:**

- Decorators are functions that take another function as an argument and return a modified version of that function.
- They provide a powerful way to add functionality to existing functions without modifying their code directly.
- Use them to enhance code readability, maintainability, and reusability.

(AIJG)



```py
# Decorator Example 1

# a list to hold the log entries
listOfFunctionCalls = []

# log every function call
# in testing etc, this easily could be written
# to a log file

def log_function_call(func):
    def wrapper(*args):
        result = func(*args)
        # print(f"Function '{func.__name__}' called with arguments {args} and {kwargs}. Returned {result}")
        xFunCall = (f"Function '{func.__name__}' called with arguments {args}. Returned {result}")
        listOfFunctionCalls.append(xFunCall)
        return result
    return wrapper

@log_function_call
def add(x, y):
    return x + y

@log_function_call
def sub(x,y):
    return x - y

@log_function_call
def multiply(x,y):
    return x * y

def printFunctionsCalled():

    print("A list of functions called")
    for i in listOfFunctionCalls:
        print(i)

def main():

    print(add(5, 3))
    print(sub(10,6))
    print(multiply(25,4))

    print('\n')

    printFunctionsCalled()
main()

"""
Output

8
4
100


A list of functions called
Function 'add' called with arguments (5, 3). Returned 8        
Function 'sub' called with arguments (10, 6). Returned 4       
Function 'multiply' called with arguments (25, 4). Returned 100
"""

```





Example2

```py
import time



listOfFunctionCalls = []


def timeit(func):
    """Decorator to time the execution of a function."""

    def wrapper(*args, **kwargs):
        start_time = time.time_ns()
        result = func(*args, **kwargs)
        end_time = time.time_ns()
        timedef = (f"Function '{func.__name__}' took {(end_time - start_time)} nano sec to execute.")
        listOfFunctionCalls.append(timedef)
        return result

    return wrapper

def printFunctionsCalled():

    print("A list of functions called")
    for i in listOfFunctionCalls:
        print(i)
    print()


@timeit
def loopcount1(n):

    a = 0

    for x in range(n):
        a = a + x

    print(a)

@timeit
def loopcount2(n):

    a = 0

    for x in range(0,n,50):
        a = a + (x)
    print(a)

def main():

    x = 1000000

    loopcount1(x)
    loopcount2(x)

    printFunctionsCalled()


main()

"""
499999500000
9999500000
A list of functions called
Function 'loopcount1' took 38899200 nano sec to execute. 
Function 'loopcount2' took 1033200 nano sec to execute. 
"""
```



