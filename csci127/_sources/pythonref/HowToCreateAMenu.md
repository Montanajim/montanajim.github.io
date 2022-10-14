# How To Create A Menu





```python
# -*- coding: utf-8 -*-
"""
Menu Template
Created on Tue Sep 17 17:06:05 2019

@author: jgoudy
"""

def Function1():
    print("This is function 1")
    
def Function2():
    print("This is function 2")

def Function3():
    print("This is function 3")
    WinAPrize()
    
def WinAPrize():
    print("You have won 5000 live grasshoppers - Enjoy")
    
def Menu():
    print("\nMenu Example\n" + \
          "1. Function 1\n" + \
          "2. Function 2\n" + \
          "3. Function 3" )
    
    choice = int(input("Choose a number:  "))
    
    if(choice == 1):
        Function1()
    elif(choice == 2):
        Function2()
    elif(choice == 3):
        Function3()
    else:
        print("That was not a choice")
    

def main():
    Menu()
    
    print("\nbye bye")


main()

'''
Program choices
1. Happy Function 1
2. Happy Function 2
3. Happy Function 3
Please choose 1, 2, or 3:  
'''
```

