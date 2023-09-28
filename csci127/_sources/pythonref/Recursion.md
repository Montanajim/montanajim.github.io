#  Recursion


## Topics

[Explanation](##Explanation)

[Drawbacks To Recursion](##Drawbacks-To-Recursion)

[Example 1  Bottles Of Beer](##Example-1-Bottles-Of-Beer)

[Example 2  Sum Of List](##Example-2-Sum-Of-List)

[Example 3   Sierpiński triangle](##Example-3-Sierpiński-triangle)

[Example 4  Tree](##Example-4-Tree)

[Example 5  Recursion / Loop / Voice - BOB](##Example-5-Recursion-/-Loop-/-Voice-BOB)



## Explanation

Recursion is the process of defining a problem (or the solution to a problem) in terms of (a simpler version of) itself. It is a powerful technique that can be used to solve a wide variety of problems, from mathematical to computational.

A recursive function is a function that calls itself directly or indirectly. This means that the function can solve a problem by breaking it down into smaller subproblems, each of which is solved using the same function.

Recursion works by having two cases:

- **Base case:** This is the simplest version of the problem, which can be solved directly without using recursion.
- **Recursive case:** This is the case where the problem is broken down into smaller subproblems, each of which is solved using the recursive function itself.

The recursive function will continue calling itself until it reaches the base case, at which point it will return the solution to the problem.



Example:

```python
def factorial(n):
    if n == 0:
        # This is the base case n == 0
        return 1
    else:
        return n * factorial(n - 1)
    
def main():
    
    num = int(input("Enter a whole number: "))
    
    ans = factorial(num)
    
    # note that we can use {} with the .format as placeholders
    print("The factorial of {} is {}".format(num,ans))

main()
```

This function calculates the factorial of a number, which is the product of all the positive integers less than or equal to that number.

The base case is when n is 0, in which case the factorial is 1. Otherwise, the recursive case breaks down the problem into calculating the factorial of n - 1, and then multiplying that result by n.

For example, to calculate the factorial of 5, the function would first call itself to calculate the factorial of 4. This would return 24. The function would then multiply 24 by 5, to return the final answer of 120.

Recursion can be a difficult concept to grasp at first, but it is a very powerful technique that can be used to solve a wide variety of problems.

Here are some other examples of problems that can be solved using recursion:

- Finding the maximum or minimum value in a list
- Searching for an element in a list or tree
- Traversing a tree or graph
- Solving the Towers of Hanoi puzzle
- Implementing a quicksort algorithm



## Drawbacks To Recursion


Recursion is a powerful programming technique that can be used to solve many complex problems in a concise and elegant way. However, it also has some drawbacks:

- **Memory usage:** Recursive functions typically use more memory than iterative functions, because each recursive call creates a new stack frame. This can be a problem for large or complex problems, or for programs that need to run on devices with limited memory.
- **Stack overflow:** If a recursive function is not implemented correctly, it can lead to a stack overflow error. This happens when the call stack exceeds its allocated size, which can cause the program to crash.
- **Difficulty in understanding and debugging:** Recursive code can be difficult to understand and debug, especially for inexperienced programmers. This is because it can be challenging to track the flow of execution and to identify the different cases that the function is handling.
- **Slower execution time:** Recursive functions are often slower than iterative functions, because of the overhead involved in calling the function itself. This can be a problem for performance-critical applications.
- **Limited applicability:** Recursion is not suitable for all problems. Some problems have more efficient iterative solutions, and others may not lend themselves well to recursive solutions at all.

Overall, recursion is a powerful tool that can be used to solve many complex problems. However, it is important to be aware of the drawbacks before using it.

Here are some tips for using recursion effectively:

- **Only use recursion when it is the most efficient or elegant solution.** There are many problems that can be solved both recursively and iteratively (loops). In general, iterative(loops) solutions are more efficient and easier to understand.
- **Be careful of stack overflow.** Make sure that your recursive functions have a base case that will eventually be reached, and that they do not make recursive calls too many times.
- **Write clear and concise recursive code.** Use comments to explain what your code is doing and why.
- **Test your recursive code thoroughly.** Make sure that it works correctly for all possible inputs.



Source:  Google Bard / Edited and Checked by James Goudy



## Example 1 Bottles Of Beer

```python
def BottlesOfBeer(num):
    
    if num > 0:
        temp = num -1 
        print(str(num) + "  bottles of rootbeer on the wall "
              + str(num) + " bottles of rootbeer")
        print("take one down pass it around "  
              + str(temp) + " bottles of rootbeer on the wall")
    
        BottlesOfBeer(num - 1)
    
def main(): 
    numbottles = 50
    BottlesOfBeer(numbottles)
    
main()
```



## Example 2 Sum Of List

```python
def sumlist(numberList):
        
    if len(numberList) == 1:
        return numberList[0]
    else:
        return numberList[0] + \
               sumlist(numberList[1:])
                
def main():
    
    theList = [1,3,5,7,9]
    
    ans = sumlist(theList)
    
    print("The sum of {} is {}".format(theList,ans))

main()
```



## Example 3 Sierpiński triangle

Note: In Spyder set graphics to Automatic

```python
import turtle

def drawTriangle(points,color,myTurtle):
    myTurtle.fillcolor(color)
    myTurtle.up()
    myTurtle.goto(points[0][0],points[0][1])
    myTurtle.down()
    myTurtle.begin_fill()
    myTurtle.goto(points[1][0],points[1][1])
    myTurtle.goto(points[2][0],points[2][1])
    myTurtle.goto(points[0][0],points[0][1])
    myTurtle.end_fill()

def getMid(p1,p2):
    return ( (p1[0]+p2[0]) / 2, (p1[1] + p2[1]) / 2)

def sierpinski(points,degree,myTurtle):
    colormap = ['blue','red','green','white','yellow',
                'violet','orange']
    drawTriangle(points,colormap[degree],myTurtle)
    if degree > 0:
        sierpinski([points[0],
                        getMid(points[0], points[1]),
                        getMid(points[0], points[2])],
                   degree-1, myTurtle)
        sierpinski([points[1],
                        getMid(points[0], points[1]),
                        getMid(points[1], points[2])],
                   degree-1, myTurtle)
        sierpinski([points[2],
                        getMid(points[2], points[1]),
                        getMid(points[0], points[2])],
                   degree-1, myTurtle)

def main():
   myTurtle = turtle.Turtle()
   myWin = turtle.Screen()
   myPoints = [[-100,-50],[0,100],[100,-50]]
   myPoints = [[-150,-100],[0,150],[150,-100]]
   sierpinski(myPoints,3,myTurtle)

   
   turtle.exitonclick()
   turtle.done()
   turtle.bye()
   
main()
```



## Example 4 Tree

```python
import turtle

def tree(branchLen,t):
    if branchLen > 5:
        t.forward(branchLen)
        t.right(25)
        tree(branchLen-10,t)
        t.left(50)
        tree(branchLen-10,t)
        t.right(25)
        t.backward(branchLen)

def main():
    t = turtle.Turtle()
    t.speed(0)
    myWin = turtle.Screen()
    t.left(90)
    t.up()
    t.backward(100)
    t.down()
    t.color("green")
    tree(75,t)
    myWin.exitonclick()
    myWin = None
    t = None 
    
    
    turtle.exitonclick()
    turtle.done()
    turtle.bye()

main()
```



## Example 5 - Recursion / Loop / Voice - BOB

```python
# -*- coding: utf-8 -*-
"""
Created on Fri Feb 25 15:06:44 2022

@author: jgoudy

James Goudy

Text To Speach
https://pypi.org/project/pyttsx3/

Do not use PIP witih ANACONDA
choose pyttsx3 via the Anaconda Navigator

NOTE: You can run this in IDLE if you
install pip and install 
    pip install pyttsx3

"""

import pyttsx3

# global variables
se = pyttsx3.init()
n = 1

# set the number of bottles


def numBottles():

    global n

    try:

        n = int(input("Enter the number of bottles"))

    except:
        n = 3

# text to speech


def sayBottles(numBottles):

    cntr = numBottles

    while cntr > 0:

        se.say(str(cntr) + " bottles of beer on the wall " + str(cntr) +
               " bottles of beer. Take one down pass it around " +
               str(cntr-1) + " bottles of beer on the wall")
        se.runAndWait()
        cntr -= 1


# print the number of bottles using a loop
def bottleloop(numBottles):

    cntr = numBottles

    while cntr > 0:

        print(str(cntr) + " bottles of beer on the wall " + str(cntr) +
              " bottles of beer. Take one down pass it around " +
              str(cntr-1) + " bottles of beer on the wall")
        cntr -= 1


# print the number of bottles usinga recursive loop
def bottlerecursive(numBottles):

    # base case - base case is the condition that stops the loop
    if numBottles < 1:
        return

    print(str(numBottles) + " bottles of beer on the wall " +
          str(numBottles) +
          " bottles of beer. Take one down pass it around " +
          str(numBottles-1) + " bottles of beer on the wall")

    bottlerecursive(numBottles-1)

# play the voices and changle thevoice


def playVoices():

    vchoice = 0

    # get the voices and store them in a list
    v = se.getProperty('voices')

    # print the voices info
    print(v)

    # setProperty is used to change the voice
    for i in range(len(v)):
        se.setProperty("voice", v[i].id)

        se.say("This is voice " + str(i))
        se.runAndWait()

    vchoice = int(input("Please choose a voice"))

    se.setProperty("voice", v[vchoice].id)

# menu system


def menu():

    choice = 0

    menuString = "\n\n1. loop version of Bottles of Beer\n" + \
        "2. Recursive version of Bottles of Beer\n" + \
        "3. Spoken version of Bottles of Beer\n" + \
        "4. Change voice\n" + \
        "5. Cancel\n"

    print(menuString)

    choice = int(input("Please choose 1,2,3,4,5 : "))

    if (choice == 1):

        numBottles()
        bottleloop(n)

    elif (choice == 2):

        numBottles()
        bottlerecursive(n)

    elif (choice == 3):

        numBottles()
        sayBottles(n)

    elif (choice == 4):

        playVoices()

    else:

        return


def main():

    quit = "n"

    while quit != "y":

        # note that a try statement will not tell you
        # where you have a problem.  To be granular, you would
        # need place the  try statment within the individual functions
        try:

            menu()

            quit = input("Would you like to quit? y/n ").lower()

        except:

            print("There was an error try again")

    # notify the user the program is doone
    print("\nbye bye")


main()
```

