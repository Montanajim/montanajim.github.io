# More Loop Examples



## Key Ideas

**for loop**

​	

​	**for c in range(10):**

​		10 - loops for iterations 0 thru 9

​		c is the counter, it keeps track of each iteration/loop

​	**for c in range(10,20):**

​		c / counter starts at 10 and ends at 19

​	**for c in range(10,20,2)**

​		c / counter starts at 10 and counts to 19 via 2s



In the examples below, note how the counter is being used to represent different things.



```py
# -*- coding: utf-8 -*-
"""
Created on Fri Sep 22 11:44:03 2023
Programmer: James Goudy
Title: Programming Guru

@author: jgoudy

"""
import random
import sys


def loopDaysOfWeek():

    # loop through the days of the week
    # where a number represents a day
    # 0  - Sunday
    # 1  - Monday
    # 2  - Tuesday
    # 3  - Wednesday
    # 4  - Thursday
    # 5  - Frday
    # 6  - Saturday

    # If we do not give a starting number
    # the for statement will the counter (c)
    # with the number 0

    print("\nNUMBER\nLoop through the days of the week using numbers")

    # numOfDays in a week starting at zero
    numOfDays = 6

    for c in range(numOfDays):

        if (c == 0):
            print("c = " + str(c) + "\tSunday")
            print("\t\tPicnic Day")

        elif (c == 1):
            print("c = " + str(c) + "\tMonday")
            print("\t\tStart of Work Week")

        elif (c == 2):
            print("c = " + str(c) + "\tTuesday")
            print("\t\t2nd day of work week")

        elif (c == 3):
            print("c = " + str(c) + "\tWednesday")
            print("\t\tHump Day ")

        elif (c == 4):
            print("c = " + str(c) + "\tThursday")
            print("\t\tTime to get things done")

        elif (c == 5):
            print("c = " + str(c) + "\tFriday")
            print("\t\tLast day of the work week")

        elif (c == 6):
            print("c = " + str(c) + "\tSaturday")
            print("\t\tIt's the weekend")

        # loop to the top of the list where c is increment to the next number


def loopDaysOfWeek_List():

    print("\nLIST\nLoop through the days of the week using a list")

    weekdays = ["Sunday", "Monday", "Tuesday",
                "Wednesday", "Thursday", "Friday", "Saturday"]

    # In this case, the for statement only uses the
    # key word "in"
    # c represents a day for each item in the list

    for c in weekdays:

        if (c == "Sunday"):
            print("c = " + str(c) + "\t\tSunday")
            print("\t\t\t\tPicnic Day")

        elif (c == "Monday"):
            print("c = " + str(c) + "\t\tMonday")
            print("\t\t\t\tStart of Work Week")

        elif (c == "Tuesday"):
            print("c = " + str(c) + "\t\tTuesday")
            print("\t\t\t\t2nd day of work week")

        elif (c == "Wednesday"):
            print("c = " + str(c) + "\tWednesday")
            print("\t\t\t\tHump Day ")

        elif (c == "Thursday"):
            print("c = " + str(c) + "\tThursday")
            print("\t\t\t\tTime to get things done")

        elif (c == "Friday"):
            print("c = " + str(c) + "\t\tFriday")
            print("\t\t\t\tLast day of the work week")

        elif (c == "Saturday"):
            print("c = " + str(c) + "\tSaturday")
            print("\t\t\t\tIt's the weekend")

    # loop to the for statement for the next item in the list


def rolladice():

    print("Roll a dice")

    rollagain = "y"

    # while loop is for program control
    # as long as the value of quit is "y"
    # the function will continue to all the user to roll dice

    while (rollagain == "y"):

        # declare some variables
        numberOfRolls = int(input("\nEnter the number of rolls: ")) + 1

        rollValue = 0

        # c is keeping track of the number of rolls
        # note that 1 is the starting value and
        # numberOfRolls is the ending value

        for c in range(1, numberOfRolls):

            # roll the dice which is created by getting a random number
            # from 1 to 6

            rollValue = random.randint(1, 6)

            print("Roll number " + str(c) +
                  " | dice value is " + str(rollValue))

        rollagain = input("Do you want to roll again y/n? ").lower()

        # loop to the while statement


def countby():

    # below is an example of a
    # multilined string. The """ must
    # be on the same line as the equal sign

    description = """
    COUNT BY
    
    The purpose of this function
    is to allow the user to enter
    a range of numbers and count
    them by a multiple that they
    select.
    
    For instance a user enters
    a range starting at 0 and
    ends 10 and they want to count
    by 2\'s the output would like 
    the following:
        
    0 2 4 6 8 10    
    
    """
    print(description)

    runAgain = "y"

    # while loop is for program control
    # as long as the value of quit is "y"
    # the function will continue to all the user to run the function

    while (runAgain == "y"):

        # ************* VARIABLES FOR THE FOR STATEMENT ***********
        numStart = int(input("Enter your start number: "))
        numEnd = int(input("Enter your end number: "))
        numCountBy = int(input("Enter your countby number: "))

        # *********************************************************

        numCols = int(input("\nEnter the number of " +
                            "columns to display output: "))

        # get the length of the number and add 2 to the length
        numLen = len(str(numEnd)) + 2

        # column count
        colcount = 0

        # print the range using a for statement
        for c in range(numStart, numEnd, numCountBy):

            # print the number
            sys.stdout.write(str(c).rjust(numLen, " "))

            # increment column count by 1
            colcount = colcount + 1

            # track columns and start new row if colcount
            # is greater than numcols value
            if (colcount >= numCols):
                print()
                # reset column count
                colcount = 0

        # End of for loop

        runAgain = input("\n\nDo you want to run again y/n? ").lower()

   # loop to the while statement


def menu():

    mnu = """
    LOOP EXAMPLES
    1. Days of week by number
    2. Days of week by list
    3. Roll a dice
    4. Number Range with Countby (step)
    """

    print(mnu)

    choice = int(input("Enter 1,2,3 or 4: "))

    if (choice == 1):
        loopDaysOfWeek()
    elif (choice == 2):
        loopDaysOfWeek_List()
    elif (choice == 3):
        rolladice()
    elif (choice == 4):
        countby()
    else:
        print("That wasn't a choice")


def main():
    print("\n")

    quit = "n"

    # while loop for program control
    while (quit != "y"):

        try:

            menu()

            quit = input("Would you like to quit y/n : ")

        except Exception as e:
            print("\n" + e)
            print("\nYou had a error, please try again\n")

    print("\n\nbye")


main()


"""
OUTPUT 

    LOOP EXAMPLES
    1. Days of week by number
    2. Days of week by list
    3. Roll a dice
    4. Number Range with Countby (step)
    
Enter 1,2,3 or 4: 

NUMBER
Loop through the days of the week using numbers
c = 0	Sunday
		Picnic Day
c = 1	Monday
		Start of Work Week
c = 2	Tuesday
		2nd day of work week
c = 3	Wednesday
		Hump Day 
c = 4	Thursday
		Time to get things done
c = 5	Friday
		Last day of the work week
Would you like to quit y/n : 

LIST
Loop through the days of the week using a list
c = Sunday		Sunday
				Picnic Day
c = Monday		Monday
				Start of Work Week
c = Tuesday		Tuesday
				2nd day of work week
c = Wednesday	Wednesday
				Hump Day 
c = Thursday	Thursday
				Time to get things done
c = Friday		Friday
				Last day of the work week
c = Saturday	Saturday
				It's the weekend
Would you like to quit y/n : 

Roll a dice

Enter the number of rolls: 4
Roll number 1 | dice value is 4
Roll number 2 | dice value is 3
Roll number 3 | dice value is 5
Roll number 4 | dice value is 1
Do you want to roll again y/n? 

    COUNT BY
    
    The purpose of this function
    is to allow the user to enter
    a range of numbers and count
    them by a multiple that they
    select.
    
    For instance a user enters
    a range starting at 0 and
    ends 10 and they want to count
    by 2's the output would like 
    the following:
        
    0 2 4 6 8 10    
    
    
Enter your start number: 12
Enter your end number: 144
Enter your countby number: 6

Enter the number of columns to display output: 4
   12   18   24   30
   36   42   48   54
   60   66   72   78
   84   90   96  102
  108  114  120  126
  132  138

Do you want to run again y/n? 

"""

```

