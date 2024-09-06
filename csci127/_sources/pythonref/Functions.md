# Functions



```{admonition} Definition - Function
A __Function__ is a segment of code that can be "called" upon and run repeatedly as required. A function has a name, can take optional inputs, and may return data to whichever function called it.
```



**A function is a block of organized, reusable code that is used to perform a specific task.** It helps to break down a complex problem into smaller, manageable functions.

## Structure of a Function

```python
def function_name(parameters):
  """Docstring: Explains what the function does"""
  # Function body
  return value  # Optional
```

 Use code [with caution.]()

- **`def`**: Keyword to define a function.
- **`function_name`**: The name you give to the function.
- **`parameters`**: Optional input values for the function.
- **`docstring`**: Optional string explaining the function's purpose.
- **`return`**: Optional keyword to return a value from the function.





```python
# The code pattern of a function
def functionName(input):
    # function code here
    # function code here
    # function code goes here
    
    # return is optional depending the
    # requirements of the function
    return somedata
```

##  Function Names

Function names follow the same rules as variable names:

- must start with a letter
- may contain the underscore
- may contain numbers
- case sensitive
- no spaces in the name




`````{admonition} Special Function - Main 
:class: tip
__main()__ This is a special function. Most languages have a function called main(). This is where a program will start and end. While it is not required in python, it is good form and practice to use a __main__ function in python.
`````



##  Program Structure

```python

def function1(input):
    # function code here
    # ...
    # function code goes here
    return somedata

def function2(input):
    # function code here
    # ...
    # function code goes here

def function3():
    # function code here
    # ...
    # function code goes here
    return somedata

def function4():
    # function code here
    # ...
    # function code goes here
    
def main():
    
    # variables
    x = 0
    ans = 0;
    
    # assume that the functions 1 and 3
    # will return an integer
    
    ans = function1(x)
    
    function2(x)
    
    ans= function3()
    
    function4()

    
# program will start here
main()

```



_Can you put the functions below the main?_ The answer is yes.  However, if you code between languages, you may code in a language where it uses a one-pass compiler. This means the compiler will run once from the top to the bottom of the code.  So any function calls, the functions need to be "introduced" first before they can be called.  Placing the functions at the top will introduce to the compiler the functions before they are called.   So if you code between a lot of languages, you might want to adopt a style that will work for the majority of languages.



```{admonition} Definition - Compiler
__Compiler__ a program that converts your source code into  machine-code form (ones and zeros) so that they can be read and executed by a computer.
```





## Lecture Code

### Example 1

```python
"""
Function Demo
"""
# Add two numbers - Functions requires 2 numbers
# and returns the total
def add2nums_a(num1, num2):
    ans = 0
    ans = num1 + num2
    return ans

# add two numbers B
# Add two numbers - Functions requires 2 numbers
# returns nothing, and displays the answer
def add2nums_b(num1, num2):
    ans = 0
    ans = num1 + num2
    print("The answer is " + str(ans))

# add two numbers C
# Add two numbers - the asks for the numbers
# and returns the answer
def add2nums_c():
    ans = 0
    num1 = float(input("Enter first number " ))
    num2 = float(input("Enter second  number " ))
    ans = num1 + num2
    return ans

# add two numbers d
# Add two numbers - the function does everything
# Function asks for the numbers and displays the answer
def add2nums_d():
    ans = 0
    num1 = float(input("Enter first number " ))
    num2 = float(input("Enter second  number " ))
    ans = num1 + num2
    print("The answer is " + str(ans))


# -------------- InClass Dogyears ----------------
def dogYears_a(humanYears):
    ans = 0
    ans = humanYears * 7
    return ans

def dogYears_d():
    ans = 0.0
    humanYears = 0.0

    humanYears = float(input(" Please enter human years  "))
    
    ans = humanYears * 7
    
    print("DogYears D - Dogs years is equal to " + str(ans))


# ------------- Greetings A --------------------------
def Greetings_A( firstName,  lastName,  PlayerNum):

    ans = ""
    
    ans = "Welcome " + firstName + " " + lastName + " player " + str(PlayerNum)
       
    return ans

def main(): 

    #variables
    xNum1 = 0
    xNum2 = 0
    xAns = 0
    
    xhumanYears = 0
    
    xFirstName = ""
    xLastName = ""
    xAnsString = ""
    xPlayerNumber = 0
    
    
    # Base Code
    print("Add two numbers");
    xnum1 = float(input("Please enter first number  "))
    
    xnum2 = float(input("Please enter second number  "))
    
    xAns = xNum1 + xNum2
    
    print("The answer is " + str(xAns))
    
    # Example A
    print("\n\n--------- Example A ---------\n\n")
    
    xnum1 = float(input("A Please enter first number  "))
    
    xnum2 = float(input("A Please enter second number  "))
    
    xAns = add2nums_a(xnum1, xnum2)
    
    print("A The answer for add2nums_A is " + str(xAns))
    
    # Example B
    print("\n\n--------- Example B ---------\n\n")
    
    xnum1 = float(input("B Please enter first number  "))
    
    xnum2 = float(input("B Please enter second number  "))
    
    add2nums_b(xnum1, xnum2)






    
    # EXample C
    print("\n\n--------- Example c ---------\n\n")
    
    xAns = add2nums_c()
    
    print("C The answer for add2nums_c is " + str(xAns))
    
    # Example D
    print("\n\n--------- Example d ---------\n\n")
    
    add2nums_d();
    
    # Inclass - Dog Years
    print("\n\n--------- Example dogyears A---------\n\n")
    
    
    xhumanYears = float(input("DogYears A Please enter human years  "))
    
    xAns = dogYears_a(xhumanYears)
    
    print("DogYears A Dogyears " + str(xAns))
    
    print("\n\n--------- Example dogyears D---------\n\n")
    
    dogYears_d()
    
    # ----------------- Greeting_A ---------------------
    
    print("\n\nGreeting")
    xFirstName= input("Please enter your first name  ")
    
    
    xLastName = input("Please enter your last name  ")
    
    xPlayerNumber = int(input("Please enter your player number  "))
    
    xAnsString = Greetings_A(xFirstName, xLastName, xPlayerNumber)
    
    print(xAnsString)
    
    # -------------- End Of Program ----------------------------
    
    print("Thank you for using Goudy Software - good bye")



# The function where a program starts and ends    
main()


```



### Example 2

```python
"""
Function Demo 2

@author: jgoudy
"""

import math

# calcuate the volume of a cylinder
# pR^2h
def cylinderVolume(radius, height):
    
    ans = 0.0
    
    ans = math.pi * radius * radius * height
    
    ans = round(ans, 2)
    
    return ans

    # ---------   End of Volume of Cylinder -----------
    
# calculate the volume of a cone
# v = p r^2(h/3.0)
def coneVolume():
    
    # variables
    r = 0.0
    h = 0.0
    ans = 0.0
    
    print("\nCalculate Volume of a Cone")
    
    # get data
    r = float(input("Enter radius of cone: "))
    h = float(input("Enter height of cone: "))
    
    ans = math.pi * r * r *(h / 3.0)
    ans = round(ans, 2)
    
    print("The volumen the cone is " + str(ans))
    
    # ------- End of Volume of Cone --------------
        
def main():

    # variables
    r = 0.0
    h = 0.0
    ans = 0.0
    
    print("\nCalculate Volume of a Cylinder")
    
    # get data
    r = float(input("Enter radius of cylinder: "))
    h = float(input("Enter height of cylinder: "))
    
    # call the function
    ans = cylinderVolume(r,h)
    
    print("The volume of a cylinder is " + str(ans))
    
    # ----------------------------------
    
    coneVolume()


    # ------- End of main ----------------
    
#program starts here    
main()
```



## Exercise

Program the following:

```python
"""
volumeRecPrism  - (1enght, width, height) has a return
rec/prism volume = (l * w) * h
(do like cylinder)

volumeTriPrism - ()  no return
triangle/prism =  1.0/2.0 *(l * w) * h
(do like cone)
"""
```



---

End of topic





