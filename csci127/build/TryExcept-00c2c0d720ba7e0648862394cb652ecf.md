# Try Except - Preventing Errors



## Key Ideas

* try
* except
* finally

---

The goal of writing code is to prevent errors from crashing the program.  A try-and-except statement will catch errors and prevent the program from crashing.

---



> **Attention**
>
> Any code that can possibly cause the code to fail should
> be placed in a try-except statement. Note other languages 
> call this try and catch.



## Example Code

```python
"""
Created on Thu Sep 22 14:57:31 2022

@author: jgoudy

"""

def example():
    
    x = "Bob"
    y = 10.0
    
    print("Error 1 Example")
    try:
        # print the 101 character
        # this will fail because "Bob" only has three characters
        print(x[100])
    except Exception as e:
        print(e)
        

    print("\nError 2 Example\n")
    try:
        # This will fail because you cannot divide by zero
        # the code under finally will always run
        t = y / 0
        print(t)
    except Exception as e:
        print("*** Error ***")
        print(e)
    finally:
        print("finally code - This code will always run")
    
 
    print("\nError 3 Example\n")
    try:
        # note that this code will not fail
        # the code under finally will always run
        t = y / 1
        print(t)
    except Exception as e:
        print("*** Error ***")
        print(e)
    finally:
        print("finally code - This code will always run")   
 
    

def main():
    example()
    
    print("\nbye bye")
    
    
main()
    
'''
Output:

Error 1 Example
string index out of range

Error 2 Example

*** Error ***
float division by zero
This code will always run

Error 3 Example

10.0
This code will always run

bye bye

'''
```

