# Iteration



## Key Ideas

- For Loops
- While Loops
- Loops are for program and flow control



```{admonition} Definition 
 **Iteration** - loops - This is the process of having code repeat itself
```
---

"For" loops are used if you have a set number of times or items to run.

"While" loops are used if  you don't have a specific number of times to run.  They will run while a condition is true.



> In most other languages there is a loop that will always run once. It may run more than once, but is set to always run at least once.  That loop is the "Do" loop.  Python does not have this loop.



---

## Lecture Code

### Example 1

```py

import sys

def for_example():

    # c is a counter and 10 is the stop
    # in this example, the counter starts a 0
    # and ends at nine. 10 is the stop or boundary

    # loops 0 through 10 times
    for c in range(10):
        sys.stdout.write(str(c) + " ")
    print()
    
    # change starting and ending points
    # for the loop
    # loops for numbers 50 - 59
    for c in range(50,60):
            sys.stdout.write(str(c) + " ")

    print("\n------------\n")

    a = 40
    b = 50
    # note the starting and ending points
     # can be variables
    for c in range(a,b):
            sys.stdout.write(str(c) + " ")
            
    print("\n------------\n")
    
    # how to loop through a string
    for x in "Python":
        if(x == "h"):
            print(" Boom ")

        print(x)

    print("\n------------\n")

    # using two for statements to create a grid

    # grid of stars
    numRows = 5
    numColumns = 10
    
    # This for loop controls the number of rows
    for row in range(numRows):
        
        # This for loop controls the number or column and
        # one individual row
        for col in range(numColumns):
            sys.stdout.write("* ")
        print()


    print("\n------------\n")
    
    # grid showing the coordinate of the row and column
    for row in range(numRows):
        for col in range(numColumns):
            sys.stdout.write("("+ str(row) + "," + str(col) + ") ")
        print()

    print("\n------------\n")
    
    
    # this form of the for loop allows the programmer
    # to set the start - 0, the end 100(actual ends at 99)
    # and the counting interval 10 (called the "step")
    for cc in range(0,100,10):
        sys.stdout.write(str(cc) + " ")
        
    # to count backwards, set the first number higer
    # than the middle number and then use a negative
    # counter or step
    
    print("\n******** Count Backwards **********")
    for ccc in range(100,-1, -10):
        sys.stdout.write(str(ccc) + " ")
        

def while_example():
    
    print("\n ******** While *********")

    run = True

    i = 0
    # this loop will continue to repeat itself
    # as long as "i" is less than 60
    while i < 60:
        print(i) 
        # i = i + 5
        i += 10
  
    print("\n------------\n")
  
    # while statement using a boolean variable
    # this loop will continue to repeate itself
    # as long as "run" is true
    i = 0;
    while run:
        print("Whoopee it works")
        i+=1
        if(i>10):
            run = False
    

def main():

    
    quit = "n"
    
    # this way the only letter that lets the user quit is y
    while(quit != "y"):
        
        for_example()
    
        while_example()
        
        quit = input("Would you like to quit y / n ").lower()
     
    print('bye')

main()

'''
Output
0 1 2 3 4 5 6 7 8 9 
50 51 52 53 54 55 56 57 58 59 
------------

40 41 42 43 44 45 46 47 48 49 
------------

P
y
t
 Boom 
h
o
n

------------

* * * * * * * * * * 
* * * * * * * * * * 
* * * * * * * * * * 
* * * * * * * * * * 
* * * * * * * * * * 

------------

(0,0) (0,1) (0,2) (0,3) (0,4) (0,5) (0,6) (0,7) (0,8) (0,9) 
(1,0) (1,1) (1,2) (1,3) (1,4) (1,5) (1,6) (1,7) (1,8) (1,9) 
(2,0) (2,1) (2,2) (2,3) (2,4) (2,5) (2,6) (2,7) (2,8) (2,9) 
(3,0) (3,1) (3,2) (3,3) (3,4) (3,5) (3,6) (3,7) (3,8) (3,9) 
(4,0) (4,1) (4,2) (4,3) (4,4) (4,5) (4,6) (4,7) (4,8) (4,9) 

------------

0 10 20 30 40 50 60 70 80 90 
******** Count Backwards **********
100 90 80 70 60 50 40 30 20 10 0 
 ******** While *********
0
10
20
30
40
50

------------

Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Whoopee it works
Would you like to quit y / n 
'''

```



### Example 2

```python
"""
Iteration / Loops
"""
import sys

def for_example():
    
    for cntr in range(10):
        sys.stdout.write(str(cntr) + " ")
    # 0 1 2 3 4 5 6 7 8 9 
    print()

    for cntr in range(50, 60):
        sys.stdout.write(str(cntr) + " ")
    # 50 51 52 53 54 55 56 57 58 59 

    print()

    for letter in "Python":
        print(letter)
    print()

    myWord = "Banana"
    for letter in myWord:
        print(letter)

    for x in range(100):
        sys.stdout.write(str(x) + " ")
        if(x == 20):
            break
        # sys.stdout.write(str(x) + " ")

        # continue - if you stopped a loop, 
        # if you are still in the loop


def while_example():
    print("\nWhile Loops")

    cntr = 0
    while cntr < 10:
        sys.stdout.write(str(cntr) + " ")
        # cntr += 1
        cntr = cntr + 1

    print()
    bb = "ba"
    sys.stdout.write(bb)


    cntr = 0
    while cntr < 100000:
        sys.stdout.write(" na ")
        cntr +=1
        if(cntr == 20):
            break


def main():
    for_example()
    while_example()

main()

```



### Example 3

```python
# -*- coding: utf-8 -*-
"""
Created on Tue Feb 18 17:49:15 2020

@author: jgoudy
"""
import sys


def main():
  
    
    aword = "Bubba"
    
    # len() this prints the lenght of the variable
    # starting at 1 so bubba has a length of 5
    print(len(aword))
    
    # note the key word "in" 
    # aword is made up of 5 chars
    # c which is the counter will iterate through 
    # each object - which in this case is each letter
    
    # ord gives the ascii decimal number for the char
    # asciitable.com
    for c in aword:
        print(c + " " +  str(ord(c)) )
     
    print("\n-------------")
    
    # if we use "in range" to work with a string
    # variable, we can use the counter to represent
    # each location of the string
    
    #  aword  = | B | u | b | b | a |
    #           ---------------------
    # position  | 0 | 1 | 2 | 3 | 4 |
    
    # c will start at positon 0 and 
    # go up in value by 1 each time it loops
    
    # to access the specific letter we use the
    # following patter variablename[counterVariable]
    for c in range(len(aword)):
        sys.stdout.write(aword[c] + " ")
     
    print("\n-------------")
    
    # in the following 10 is your starting number (inclusive)
    # 101 is the stop(exclusive)
    # 5 is your countby
    for c in range(10,101,5):
        sys.stdout.write(str(c) + ",")
    
    print("\n-------------")
    
    # chr will print ascii of the integer arguement
    # it is given - in this case it will print out
    # all of the capital letters A - Z
    for c in range(65, 91):
        sys.stdout.write(chr(c))
    print("\n-------------")
  
    
main()

```



### Example 4

```python
import sys
import os

def for_example():

    # number of times
    for c  in range(10):
        sys.stdout.write(str(c) + " ")
    
    print("\n------------\n")

    a = 15
    for c in range(a):
        sys.stdout.write(str(c) + " ")

    print("\n------------\n")

    # count within a range
    for c in range(50,60):
        sys.stdout.write(str(c) + " ")

    print("\n------------\n")
    
    # iterate through a string
    aWord = "Python"
    for ch in aWord:
        sys.stdout.write(ch + " | " )

    print("\n------------\n")
    
    # range(start,finish, countby)
    for x in range(0,20,2):
        sys.stdout.write(str(x) + " | " )

    # iterate backwards by 20    
    print("\n------------\n")
    for x in range(100,0,-20):
        sys.stdout.write(str(x) + " | " )    

    print("\n------------\n")

    # iterate through items in a list
    stooges = ["Larry", "Curly", "Moe", "Shemp","Curly Joe"]
    for aStooge in stooges:
        sys.stdout.write(str(aStooge) + " | " ) 

    print("\n------------\n")
    # iterate through items in a list by position
    stooges = ["Larry", "Curly", "Moe", "Shemp","Curly Joe"]
    for x in range(len(stooges)):
        print(str(x+1) + ". " + stooges[x] )

def while_example():

    # while statement
    print("While Loops")
 
    i = 0

    while(i < 10):
        print("Python")
        
        # Note a counter is needed
        # i = i + 1
        i += 2

    # note how a boolean is used in the parentheses
    
    y = True
    i = 0
    while(y):
        print("bob ross for happy little loops")
        i = i + 1
        if(i >= 12):
             y = False


def try_example():
    
    # example of try and except

    x = "python"

    try:
        print(x[20])
    except:
        print("you had a error")
        

def grid_example():
    
    # grid example
    print("\n-------- grid example ----------\n")
    # print a grid of stars
    cols = 10   
    rows = 10
  
    for r in range(rows):
       # represents one row made up of columns

       for c in range(cols):
           sys.stdout.write("x")
       print()

def triangles():
 
    # triangle example

    print("\n-------- triangles example ----------\n")
    # print a grid of stars
    cols = 10   
    rows = 10
    spaces = 0

    for r in range(rows):
        
        #prints the spaces
        for s in range(spaces):
            sys.stdout.write(" ")
        # prints the xs
        for c in range(cols):
            sys.stdout.write("x")
        # end of a row  - drops the cursor
        print()
        cols = cols -1  
        spaces = spaces + 1

def os_example():
    
    # how to call an operating instruction
    # pending your operating system, the commands may differ
    os.system('dir')

def main():
    for_example()
    while_example()

    try_example()
    
    grid_example()
    triangles()
    
    os_example()
    
    print("\n\n\nbye")
main()


```

