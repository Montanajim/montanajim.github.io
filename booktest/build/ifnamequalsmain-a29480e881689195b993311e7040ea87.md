# If  `__name_ == __main__`

In Python, the `if __name__ == '__main__':` construct is used to control the execution of code based on whether the script is being run directly or being imported as a module.

How it works:

- `__name__`:

  This is a special variable in Python that gets assigned a value depending on how the script is being used.

  - If the script is being run directly, `__name__` is set to `'__main__'`.
  - If the script is being imported as a module, `__name__` is set to the name of the module.

- `if __name__ == '__main__':`:

  This conditional statement checks if the `__name__` variable is equal to `'__main__'`. If it is, the code within the indented block will be executed.

Why is it useful?

- Separating executable code from module code:

  This construct allows you to include code that should only be executed when the script is run directly, while keeping other code (functions, classes, etc.) available for use when the script is imported as a module.

- Organizing code:

  It helps to structure your code in a way that separates the main execution logic from the reusable components.

- Testing:

  It is a common practice to place unit tests within an `if __name__ == '__main__':` block, so they are only executed when the script is run directly, and not when it's imported.

  

## Example:

NOTE: both files need to be in the same directory



**FILE ONE** "add2.py"

*When add2 is ran by itself, only the  explanation() function runs*

```python
# if __name__ lecture code
# Developer: James Goudy

def add2Nums(num1,num2):
    try:
        num1 = float(num1)
        num2 = float(num2)

        return (num1 + num2)

    except Exception as e:

        print(f"\nERROR: {e}\n")

        return None

def explain():
    msg = '''
    A python script can be ran by itself.
    Or it can be imported as a module in 
    another script.

    If they script is ran by itself,
    then the python special variable __name__
    will automatically be named "__main__".

    When it is "main", then other code
    underneath that if statement will run.

    '''
    print("\n")
    print(__name__)
    print(msg)

# this acts like  main()
if __name__ == '__main__':

    print(f"\nThis is add2.py")

    # The following will only run
    # if the code is ran separately
    # and not imported into another 
    # file
    explain()
    
    print("\n\nbye\n")

# ----------- Output -----------
'''

This is add2.py

__main__

    A python script can be ran by itself.
    Or it can be imported as a module in
    another script.

    If they script is ran by itself,
    then the python special variable __name__
    will automatically be named "__main_".

    When it is "main", then other code
    underneath that if statement will run.


bye
'''
```



**FILE TWO** "testadd2.py"

```python
# Developer: Jame Goudy
# add2.py file is imported

import add2

def addMyNums():
    print("\nAdd 2 numbers")
    n1 = input("Enter 1st number: ")
    n2 = input("Enter 2nd number: ")

    # add2.add2Nums is imported
    ans = add2.add2Nums(n1,n2)

    print(f"Sum = : {ans}" )

    
# this acts like  main()
if __name__=='__main__':
    
    # NOTE: explanation does not run
    # from add2.py
    
    print(f"\nThis is testadd2.py")
    print(__name__)

    addMyNums()

    print("\n\nbye\n")

# ----------- Output -----------    
'''
This is testadd2.py
__main__

Add 2 numbers     
Enter 1st number: 20
Enter 2nd number: 80
Sum = : 100.0


bye
'''
```



In summary:

- The `if __name__ == '__main__':` construct is a valuable tool for controlling code execution and creating modular, reusable Python scripts.
- It is widely used in Python development and is considered a best practice for writing well-structured code.

(JGGEM)