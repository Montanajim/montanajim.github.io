# Debugger



A debugger is a computer program used to test and identify errors (bugs) in other programs. It acts as a troubleshooting tool for programmers by providing a controlled environment to examine a program's execution and pinpoint malfunctions.

Here's a breakdown of its key functionalities:

- **Execution Control:** Debuggers allow you to pause the program's execution at specific points, typically called breakpoints. This enables you to inspect the program's state at that moment.
- **Variable Inspection:** Debuggers provide ways to examine the values of variables at breakpoints. This helps you understand how data is flowing through your program and identify potential issues with calculations or assignments.
- **Stepping Through Code:** Debuggers offer features like single-stepping, where you can execute the program one line of code at a time. This allows you to follow the program's logic step by step and see how it interacts with variables.
- **Stack Trace Analysis:** When an error occurs, debuggers often display a stack trace. This information reveals the chain of function calls that led to the error, making it easier to pinpoint the problematic section of code.

In essence, a debugger acts as a bridge between the programmer and the running program. By offering insights into the program's internal state and execution flow, it empowers developers to effectively identify, understand, and fix bugs, ultimately leading to more reliable and efficient software



## Demo Code

```python
'''
Programmer: James Goudy
'''
def add(num1, num2):
  """Adds two numbers and returns the sum."""
  breakpoint()  # Add breakpoint before the calculation
  return num1 + num2

def subtract(num1, num2):
  """Subtracts two numbers and returns the difference."""
  breakpoint()  # Add breakpoint before the calculation
  return num1 - num2

def loop_function():
  """Runs a loop for 5 times, printing a message each time."""
  breakpoint()  # Add breakpoint before the loop
  for i in range(5):
    print(f"Loop iteration: {i+1}")

def main():
  """Main function to call other functions and start the program."""
  print("Welcome to the calculator program!")
  
  # Get user input for numbers
  number1 = float(input("Enter the first number: "))
  number2 = float(input("Enter the second number: "))
  
  # Call add and subtract functions
  sum = add(number1, number2)
  difference = subtract(number1, number2)
  
  # Print the results
  print(f"The sum of {number1} and {number2} is: {sum}")
  print(f"The difference of {number1} and {number2} is: {difference}")
  
  # Call the loop function
  loop_function()

# Call the main function to start the program
if __name__ == "__main__":
  main()

```



This program defines four functions:

- `add`: Takes two numbers as arguments and returns their sum.
- `subtract`: Takes two numbers as arguments and returns their difference.
- `loop_function`: Runs a loop for 5 times, printing the current iteration number.
- `main`: The main function that welcomes the user, gets input for numbers, calls the `add` and `subtract` functions with the user input, prints the results, and then calls the `loop_function`.

The `if __name__ == "__main__":` block ensures that the `main` function only runs when the script is executed directly, not when imported as a module.



## Commands

The built-in Python debugger, `pdb`, offers a variety of commands to control program execution and inspect variables during debugging. Here's a breakdown of some essential commands:

**Setting Breakpoints:**

- `b (break)`: Sets a breakpoint at a specific line number or function name. You can optionally specify a condition for the breakpoint to trigger only when the condition evaluates to `True`.

**Navigating Code Execution:**

- `c (continue)`: Continues program execution until the next breakpoint is hit.
- `s (step)`: Steps into the next line of code, including function calls.
- `n (next)`: Steps over the next line of code, without entering functions.

**Examining Values:**

- `p (print)`: Prints the value of an expression in the current context.

**Stack Management:**

- `u (up)`: Moves the debugger up one level in the call stack (useful for inspecting function arguments).
- `d (down)`: Moves the debugger down one level in the call stack (helpful for following function calls).

**Other Useful Commands:**

- `l (list)`: Lists the source code surrounding the current line (default: 11 lines).
- `q (quit)`: Exits the debugger.
- `h (help)`: Provides help on available debugger commands.

**Starting the Debugger:**

There are two main ways to launch the debugger:

1. **Using `python -m pdb your_script.py`**: This runs your script (`your_script.py`) under the control of `pdb`.
1. **Using `breakpoint()`**: Inside your code, add `breakpoint()` at the desired breakpoint location. *This automatically launches `pdb` when the program execution reaches that line (available in Python 3.7 and later).*

For a comprehensive list of commands and their functionalities, refer to the official `pdb` documentation: https://docs.python.org/3/library/pdb.html



