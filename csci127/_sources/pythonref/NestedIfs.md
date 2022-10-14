# Nested Ifs



## Lecture Code

### Example I - Should I Post This

```python
# -*- coding: utf-8 -*-
"""
Program - Should I post this?

Created on Fri Sep 20 11:49:44 2019

@author: jgoudy

NOTE: lower converts input into lower case

Cases have to match when comparing for true
"""

def PostPhoto():
    
    choice = input("Is everyone clothed? y/n  ").lower()
    
    if(choice == "y"):
        #person is fully clothed
        #ask if doing anything embarrassing
        choice = input("are you doing anything "  \
                       + "illegal or embarrassing? y/n  ").lower()
    
        if(choice == "y"):
            print("Stop - do not post")
        elif(choice == "n"):
            print("Ok to post")
        else:
            print("That was not a choice")
            
            
    elif(choice == "n"):
       # Person is not fully clothed
       print("Stop - do not post")
    else:
       print("That was not a choice") 
    
    
def PostText():
    
    choice = input("Are there expletives or abrasive content? y/n  ").lower()
    
    if(choice == "y"):
       # Text has objectionable content
       print("Stop - do not post")
            
    elif(choice == "n"):  
        # Text has no objectionable content
        #ask if they were partying
        choice = input("Have you been partying?  y/n  ").lower()
    
        if(choice == "y"):
            print("Stop - do not post")
        elif(choice == "n"):
            print("Ok to post")
        else:
            print("That was not a choice")      
       
       
       
def ShouldIPost():

    print("Should I post this?")
    choice = int(input("Press 1 for text and 2 for photo: "))

    if(choice == 1):
        PostText() 
    elif(choice == 2):
        PostPhoto()
    else:
        print("That was not a choice")
        

def main():
    ShouldIPost()
    

main()
   
```



### Example 2 - Get Out Of Bed

```python
# -*- coding: utf-8 -*-
"""
Spyder Editor
By James Goudy


The program assumes that if the user picks anything but a y
the answer will be no

Remember .lower() converts the input to lowercase
"""
import random

# ui = variable name short for user input
def weekend():
    
    #
    ui = input("Is it the weekend y/n ").lower()
    
    if(ui == "y"):
        
        ui = input("Own a dog  y/n ").lower()
    
        if(ui == "y"):
            print("Get out of bed and let the dog out")
        else:
            print("Stay in bed")
    else:
        vacation()

def vacation():
    
    ui = input("Are you on vacation y/n ").lower()

    if(ui == "y"):
        print("Stay in bed")
    else:
        job()




def job():
    
    ui = input("Do you have a job y/n ").lower()
    
    if(ui == "n"):
        print("Stay in bed")
    else:
        print("Get out of bed.\nPrepare for work.")
        leaveforwork()
    
def leaveforwork():
    # We will generate a random number 
    # and let that determine if we have to
    # grab the keys or the transit card
    # will will gamify this by not telling
    # the user what the computer has chosen
    # the user will have to guess
    
    
    # Generate a random integer
    aRandomInteger = random.randint(0,10)
    
    # % is the modulus operator
    # in integer division it returns the remainder
    # note we are dividing by 2 and will return
    # the remainder. Since we are dividing by two
    # if the random integer is even, the remainder
    # will be 0
    
    carstatus = (aRandomInteger % 2)
    
    print("Pick up either the car keys or transit pass")
    ui = int(input("press 1 for keys or 2 for transit pass"))
    
    # We will make the following assumption
    # if carstatus equals 0 
    #    then the car is gone and
    #    the transit pass is needed to go to work
    # else cartstatus does not equal 0
    #    then the car is here 
    #    the keys are needed to go to work
    
    if(carstatus == 0):
        # this means that the car is gone
        # person needs the transit pass
        print("The car is gone")
        if(ui == 2):
            print("You picked up the transit pass")
            print("and you are off to work")
        else:
            print("You picked up the keys")
            print("\nGo back choose again")
            leaveforwork()
    else:
        # this means that the car is here
        # person needs the keys
        print("The car is here")
        if(ui == 1):
            print("You picked up the keys")
            print("and you are off to work")
        else:
            print("You picked up the transit pass")
            print("\nGo back choose again")
            leaveforwork()
    
    
    
    
def main():
     print("Get Out Of Bed Program")
     
     status = "y"
     while(status == "y"):
         weekend()
         
         status = input("would you like " \
                        +"to run the program again y/n ").lower()
         
     print("\nBye bye enjoy your day")

main()

```

