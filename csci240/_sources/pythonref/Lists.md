# Lists



## Overview

[toc]

---

## Definition

>**List**: A collection of data values where each value is identified by an index. It is mutable (values can be modified). The values that make up the list are called elements.   
>
>Designated by the square brackets [ ] 

---

## Lecture Code

### Example 1 - The fundamentals

```python
import sys
import random

"""
LISTS - Lecture 1
"""


def ListExample():
    # Create Lists
    print("\nCreating Lists\n")
    
    aaa = 1
    bbb = 2
    ccc = 3
    ddd = 4
    eee = 5
    
    # or written as a list 
    mynums1  = [1,2,3,4,5]
    print(mynums1)
    
    stooges = ["Larry", "Curly", "Moe"]
    print(stooges)
    
    # also we can use variables
    mynums2 = [aaa, bbb, ccc, ddd, eee]
    sys.stdout.write("mynums2 = " + str(mynums2) + "\n")
    
    # NOT RECOMMENDED AND NOT ALLOWED IN MOST OTHER LANGUAGES
    mixlist = ["car", 42, .5555, True, stooges]
    print(mixlist)
    
    # we can create an empty list
    # used when we want to have a place to store items later
    emptylist  = []
    
    # Characteristics
    # Length
    print(len(mynums1))
    
    # Type
    print(type(mynums1))
    
    # Accessing Elements - indexes start at 1
    print("\nAcessing Elements\n")
    print(stooges[1])           # Curly prints
    print(stooges[-1])          # Count from the back - Moe
    print(mynums1[0])           # first position - prints 1
    print(mynums1[-2])          # counts to from the rear - prints 4
    
   
    
    # check membership
    print("\nCheck Membership\n")
    print("Shemp" in stooges)
    print("Moe" in stooges)
    print(42 in mixlist)
    
    # concantenation
    print("\nConcantenation")
    stooges = stooges + ["Shemp", "Curly Joe"]
    mynums1 = mynums1 + [6,7,8,9,10]
    print(stooges)
    print (mynums1)
    
    # create multiples 
    mynums3 = [42] * 5      # create 5 42's
    print(mynums3)
    
    # slicing - first number is inclusive, the last one is not
    print("\nSlicing\n")
    print(mynums1[1:4])                     # print numbers 2,3,4
    print(mynums1[:3])                      # print first 3 numbers
    print(mynums1[:-3])                     # remove last 3 numbers
    print(mynums1[:])                       # print all numbers
    print(mynums1[0:7:2])                   # print 1,3,5,7
    print(mynums1[0:len(mynums1):3])        # print 1,4,7,10
    print(mynums1[len(mynums1):0:-2])       # print 10,8,6,4,2
    
    # mutable - change data
    print("\nMutable - change data")
    stooges[0] = "Tom"
    print(stooges)              # ['Tom', 'Curly', 'Moe', 'Shemp', 'Curly Joe']
    mynums3[3] = 99     
    print(mynums3)              # [42, 42, 42, 99, 42]
    
    # deleting items
    print("\ndelete items\n")
    del stooges[0]              # delete item - tom
    print(stooges)
    del mynums3[3:5]            # delete last 2 -  last number is not inclusive
    print (mynums3)
    print(mynums2)
    del mynums2                 # del the whole list
    # print(mynums2)            # uncomment this to show the error
    
    # object references
    print("\nobject references\n")
    fruita = ["apples", "bananas", "mangoes", "tomatoes"]
    print(fruita)
    fruitb = fruita             # fruitb is looking at the data of fruita
    print(fruitb)
    
    fruitb[1] = "oranges"       # change it in b which is really a
    print(fruita)               # see the data change in a
    
    # check to see if fruita is actuall fruitb
    print(fruita is fruitb)
    print(fruita == fruitb)
   
    
    
    #clone a copy
    print("\nclone data\n")
    fruitb = fruita[:]          # using slicing - [:] goes through all items
    fruita[1] = "grapes"
    print(fruita)
    print(fruitb)
    print(fruita is fruitb)
    print(fruita == fruitb)
    
    # list methods
    # Appends adds item to end of list
    print("\nlist methods\n")
    mylist = []
    mylist.append(30)           
    mylist.append(50)
    mylist.append(40)
    mylist.append(60)
    sys.stdout.write("Appended \t\t" + str(mylist) + "\n")
    
    # sort list
    mylist.sort()
    sys.stdout.write("Sorted \t\t\t" + str(mylist) + "\n")
    
    # reverse the order of the list
    mylist.reverse()
    sys.stdout.write("Reversed \t\t" + str(mylist)  + "\n")
    mylist.reverse()
    sys.stdout.write("Reversed \t\t" + str(mylist)  + "\n")
    
    # insert - parameters (position, value)
    mylist.insert(0,10)         #insert at the beginning
    sys.stdout.write("Insert 10 \t\t" + str(mylist)  + "\n")
    mylist.insert(2,35)         #insert at the third position
    sys.stdout.write("Insert 35 \t\t" + str(mylist)  + "\n")
    
    # retrieve - index retrieves position of specified value
    print("35 is index \t\t" + str(mylist.index(35)))
    print("50 is index \t\t" + str(mylist.index(50)))     
    
    # count - counts the number of a specified item
    thevalue = 5
    mylist.insert(0,thevalue)
    mylist.insert(2,thevalue)
    mylist.insert(4,thevalue)
    print("Insert 3 " + str(thevalue) + "\'s \t\t" + str(mylist))
    
    cnt = mylist.count(thevalue)       #count the number of fives
    # example shows good use of variables and escape characters
    print("There are " + str(cnt) 
            + " \"" + str(thevalue) + "\'s\" in the list" )    
    
    # remove last item
    print("The list \t\t" + str(mylist)) 
    mylist.pop()
    print("remove last item \t" + str(mylist))
    
    myvar = mylist.pop()           #remove last item and store value in variable
    print("myvar = " + str(myvar))
    print("The list \t\t" + str(mylist)) 
    
    
    # remove the first oocurence of an item
    mylist.remove(thevalue)
    print("The first "+ str(thevalue) + " removed \t" + str(mylist)) 
    
    # remove the rest of the cntvalue in the list
    for i in mylist:
        if thevalue == i:
            mylist.remove(thevalue)
    
    print("The "+ str(thevalue) + " are removed \t" + str(mylist))     
    
    # Extend = add items from a list or iterable object to a list 
    mylist2 = [111,222,333]
    #NOTE if mylist2 is appended it puts mylist2 as an item the list
    mylist.append(mylist2)
    print("\nappend list to mylist \t" + str(mylist))
    mylist.pop()
    mylist.extend(mylist2)
    print("extend list to mylist \t" + str(mylist))
    
    
    #list traveral
    print("\nList Traversal")
    mydata = []
    
    for cntr in range(0,12):
        mydata.append(random.randint(0,101))
    print(mydata)
    
    
    #iterate by object / item
    print("\niterate by item")
    for i in mydata:
        sys.stdout.write(str(i) + " ")
    print() 
    
    #iterate by position
    print("\niterate by position")
    for position in range(len(mydata)):
        sys.stdout.write(str(mydata[position]) + " ")
    print() 
    
    #iterate position print every third
    print("\nprint every 3rd")
    cntr = 1
    for position in range(len(mydata)):
        if (cntr % 3) == 0:
            sys.stdout.write(str(mydata[position]) + " ")
            cntr = 0
        cntr += 1
    print() 
   
    # spit
    print("\nSplitting Strings")
    
   # note = make sure you use straight quotes
    quote = "Python is always fun"
    words = quote.split(" ")
    
    print(words)
    print()
    
    # show how this will include spaces and the new line character
    quote = """Always code as if the guy who ends up maintaining your 
                code will be a violent psychopath who knows where you live"""
    
    words = quote.split(" ")
    print(words)
    print()
    
    newlist = []
    a=""
    # clean up long quotes - remove empty spaces and newlines
    for i in range(0, len(words) - 1):
        if words[i] == '':
            a = ''                        # python expects a code of line
        elif words[i] == '\n':
            a= ''
        else:
            newlist.append(words[i])
    
    print(newlist)
    
    #clear - remove the data of a list
    newlist.clear()
    print(newlist)

def main():
    ListExample()
    

main()

```

[Top](##Overview)



### Example 2 -  Passing and Returning Lists via Functions

```python
import sys

# -*- coding: utf-8 -*-
"""
    Functions that product lists
    
    initialize a result variable to be an empty list
    loop
       create a new element
       append it to result
    return the result

    
    
"""

def numbers_within_a_range(start,finish):
    # pass a starting and ending number in to the function
    result = []
    
    # create a list of numbers using the start and finish variables
    for i in range(start,finish):
        result.append(i)
    
    # return the list to the calling function
    return result

def print_list(data):
    
    # passs a list into a function and iterate through it
    for i in range(len(data)):
        sys.stdout.write(str(data[i]) + " ")

    print()

def main():
    
    mynums = []
    
    beginning = int(input("Enter start number  "))
    
    #remember last number in range is not inclusive
    end = int(input("Enter end number  ")) + 1
    

    
    mynums = numbers_within_a_range(beginning, end)
    print_list(mynums)    
    
    
    # Add 10 to every number
    # note we adding this to a new list
    mynums2 = [item+10 for item in mynums]
    
    
    print_list(mynums2)


main()
```

[Top](##Overview)

### Pick Data From A List

```python
# -*- coding: utf-8 -*-
"""
@author: jgoudy
"""

List1 = ["Billings", "Boulder", "Bozeman", "Helena", "Kalispell", "Whitefish"]

def pickOne():
    
    global List1
    
    for cntr in range(len(List1)):
        # Remember positions start at zero 
        # we add one to the cntr because most lists start with 1
        # note that we can use the cntr to create an numbered list
        print(str(cntr+1) + ". " + List1[cntr])
       
    # Remember to subtract one, since we added one to display    
    choice = int(input("Pick the number of the city: ")) - 1
    
    # retreive the item by position and store it in variable item
    item = List[choice]
    
    print("You chose " + item)
    
    
        

def main():
    
    choice  = "n"
    
    # writing the != means the only waay to exit the loop is to 
    # enter the letter "y"
    while( choice != "y"):
        pickOne()
        choice = input("Would you like to quit? y/n  ").lower()
        
    print("bye bye")
    
    
main()
```

[Top](##Overview)

### Generate Random Numbers

```python
# -*- coding: utf-8 -*-
"""
Created on Mon Oct 14 00:25:09 2019

@author: jgoudy
"""
import random

def pickARandomNumber():
    
    rn = 0
    
    
    for cntr in range(20):
        rn = random.randint(100, 200)
    
        print("The random number was " + str(rn))
        
    print("-----------------------")
    
    for cntr in range(20):
        rn = random.randint(10, 20)
    
        print("The random number was " + str(rn))    


def main():
    pickARandomNumber()
    
main()
```

[Top](##Overview)

### Split Columns Into Lists

```python
# -*- coding: utf-8 -*-
"""
Created on Sun Oct 13 15:09:46 2019

@author: jgoudy
"""

# Global Variables
text = """
		artless             base-court              apple-john
        bawdy               bat-fowling             baggage
        beslubbering        beef-witted             barnacle
        bootless            beetle-headed           bladder
        churlish            boil-brained            boar-pig
        cockered            clapper-clawed          bugbear
        clouted             clay-brained            bum-bailey
        craven              common-kissing          canker-blossom
        currish             crook-pated             clack-dish
        dankish             dismal-dreaming         clotpole
        dissembling         dizzy-eyed              coxcomb
        droning             doghearted              codpiece
        errant              dread-bolted            death-token
        fawning             earth-vexing            dewberry
        fobbing             elf-skinned             flap-dragon
        froward             fat-kidneyed            flax-wench
        frothy              fen-sucked              flirt-gill
        gleeking            flap-mouthed            foot-licker
        goatish             fly-bitten              fustilarian
        gorbellied          folly-fallen            giglet
        impertinent         fool-born               gudgeon
        infectious          full-gorged             haggard
        jarring             guts-griping            harpy
        loggerheaded        half-faced              hedge-pig
        lumpish             hasty-witted            horn-beast
        mammering           hedge-born              hugger-mugger
        mangled             hell-hated              joithead
        mewling             idle-headed             lewdster
        paunchy             ill-breeding            lout
        pribbling           ill-nurtured            maggot-pie
        puking              knotty-pated            malt-worm
        puny                milk-livered            mammet
        qualling            motley-minded           measle
        rank                onion-eyed              minnow
        reeky               plume-plucked           miscreant
        roguish             pottle-deep             moldwarp
        ruttish             pox-marked              mumble-news
        saucy               reeling-ripe            nut-hook
        spleeny             rough-hewn              pigeon-egg
        spongy              rude-growing            pignut
        surly               rump-fed                puttock
        tottering           shard-borne             pumpion
        unmuzzled           sheep-biting            ratsbane
        vain                spur-galled             scut
        venomed             swag-bellied            skainsmate
        villainous          tardy-gaited            strumpet
        warped              tickle-brained          varlot
        wayward             toad-spotted            vassal
        weedy               unchin-snouted          whey-face
        yeasty              weather-bitten          wagtail
"""


newList = []

firstColumn = []
secondColumn = []
thirdColumn = []

# ----------- End of Global Variables ----------------------

# split the text on spaces
def splitList(text):

    textList = text.split(" ")
    
    # use the global variable    
    global newList
    
    # loop through each chunk in the texlist and remove empty spaces
    # and the new lines
    
    for chunk in textList:
        
        if(chunk != ''):
            newWord = ""
            
            # loop through the chunk and build the word
            # character by character but not including the 
            # "\n" the new word
            for pos in range(len(chunk)):
                check = chunk[pos]
                if(check != "\n"):
                    newWord = newWord + check
            #append the new word to the new list
            #newlist now contains clean data
            newList.append(newWord)
 
# divid the list into the three original lists
def divideIntoThree():

    global newList
    global firstColumn, secondColumn, thirdColumn

    cntr = 1;
    
    
    #Every third is the start of a new column
    for pos in range(len(newList)):
        
        # if we divid by three the remainders will be 1,2 and 0 
        # using the modulus "%" we can get the 1, 2 and 0
        
        if((cntr % 3) == 1):
            firstColumn.append(newList[pos])
        elif((cntr % 3) == 2):
            secondColumn.append( newList[pos])
        else:
            thirdColumn.append(newList[pos])
            
        cntr += 1
        
        # reset the counter back to one
        if(cntr == 4):
            cntr = 1
        
               

def main():
    splitList(text)
    divideIntoThree()
    
    
    
    print (newList)
    
    print()
    
    print(firstColumn)
    
    print()
    
    print(secondColumn)
    
    print()
    
    print(thirdColumn)
    
    
    
main()


```

[Top](##Overview)

