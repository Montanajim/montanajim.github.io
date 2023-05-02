# Menu Shell

This is an example of how to create a basic menu system.  Note the while statement for program control in the main function.

```python
# happy menu

def happyfunction1():
    print("This is happy function 1")

def happyfunction2():
    print("This is happy function 2")

def happyfunction3():
    print("This is happy function 3")


def menu():

    choice = -1

    print("Program choices")
    print("1. Happy Function 1")
    print("2. Happy Function 2")
    print("3. Happy Function 3")
    choice = int(input("Please choose 1, 2, or 3:  "))

    if(choice == 1):
        happyfunction1()
    elif(choice ==2):
        happyfunction2()
    elif(choice == 3):
        happyfunction3()
    else:
        print("That wasn't a choice")


def main():
 
    choice = "n"

    # program control
    while(choice == "n"):
        menu()

        choice = input("Would you like to quit y/n ")


main()


```

