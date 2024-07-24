

# Built-in Variable  `__name__`

The Python variable `__name__` is a special built-in variable that is a part of the Python runtime environment. Here’s what it represents:

- When a Python script is executed, the interpreter reads the source file and defines a few special variables before executing the code. One of these special variables is `__name__`.
- If the script is being run as the main program, the value of `__name__` is set to `'__main__'`. This indicates that the script is not being imported from another module but is being executed directly.
- Conversely, if the script is being imported into another module, __name__ is set to the name of the script/module being imported.

This behavior of the `__name__` variable is useful for determining whether a script is being run on its own or being used by another script as a module. It allows developers to control which parts of their code should be executed when the module is run directly and which parts should be executed when the module is imported. **Bold** the relevant parts of the response to improve readability.



Here’s what it does:

```python
if __name__ == "__main__":
    main()
```

- `__name__` is a special built-in variable in Python that represents the name of the current module.
- When a Python script is run directly (for example, `python script.py` from the command line), the `__name__` variable is set to `"__main__"`.
- If the script is being imported into another module, `__name__` will be set to the name of the script/module.
- `main()` is typically a function that contains the code to be executed when the script is run directly. It’s not a built-in function but is often defined by the programmer to organize code.

So, the `if` statement checks: if this script is the main program being executed, then call the `main()` function and run the code inside it. This allows a script to provide functionality for other scripts to import, while also providing a standalone functionality when the script is executed on its own. It’s a way to make a Python file both reusable as a module and executable as a script. **Bold** the relevant parts of the response to improve readability.

​              

## Demo Code

Here's a short Python program demonstrating the `__name__` attribute:

Python

```
def greet(name):
  print(f"Hello, {name}!")

if __name__ == "__main__":
  greet("World")  # Call greet only when running as a script

print("This line is always executed")
```

**Explanation:**

1. We define a function `greet` that takes a name and prints a greeting.
1. The `if __name__ == "__main__":` block checks if the script is being run directly (as the main program) or imported as a module.
1. Inside the `if` block, we call `greet("World")`. This ensures the greeting is printed only when the script is executed directly.
1. Outside the `if` block, we print another message. This line will always be executed, regardless of whether the script is run directly or imported.

**Running the program:**

- Save the code as a Python file (e.g., `demo.py`).
- To run the script directly, open a terminal and navigate to the directory where you saved the file. Then, type:

Bash

```
python demo.py
```

This will print:

```
Hello, World!
This line is always executed
```

- To import the script as a module, create another Python file and use the `import` statement:

Python

```
import demo

demo.greet("Friend")  # Call the greet function from the imported module
```

This will only print:

```
Hello, Friend!
```

The `__name__` check ensures the greeting functionality is only executed when running the script directly, not when imported as a module.