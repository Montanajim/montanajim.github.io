# Decision Trees



## Making Decisions in Your Code

**If statements** are fundamental to programming logic. They allow your code to make decisions based on specific conditions. If a condition is true, a block of code is executed; otherwise, it is skipped.



```python
"""

if statements

NOTE: There are no switch statements in Python
as of version 3

"""

def if_example_one(num):
       
    print("\nExample 1")

    # Check for True only
    if(num < 100):
        # run this code if true
        print("Your number is less than 100")

# -------------------------------
		
def if_example_two(num):

    
    print("\nExample 2")
    # Check for true, else the code will do code if it's false 
    if(num < 100):
        # run this if true
        print("Your number is less than 100")
    else:
        # run this code if false
        print("Your number is greater than 99")

# -------------------------------

def if_example_three(anum):

    print("\nExample 3")

    #check for mutliple cases of true
    if(anum < 10):
        # run this if true
        print(str(anum) + " is less than 10")
    elif(anum < 20):
        # run this if true
        print(str(anum) + " is less than 20")
    elif(anum < 30):
        # run this if true
        print(str(anum) + " is less than 30")
    else:
        # run this if false
        # the else optional - and not required.
        print("Your number is greater than 29")
# -------------------------------
 
def if_range(salary):

    print("\nExample Check a number between a range")
    # Check to see if a number is between a range
    if(salary > 0 and salary <= 50000):
        print("\nNeed to win the lottery")
    elif(salary > 50000 and salary <= 200000):
        print("\nMiddle Class")
    elif(salary > 200000 and salary <= 10000000):
        print("\nTop Ten")
    else:
        print("\nLiving On Easy Street")
        
    # Note: if(salary > 0  <= 50000):
    # Python can write an expression this way
    # However - this is NOT accepted in most other 
    # programming languages.

# -------------------------------

def if_strings(word1, word2):

    print("\nCompare Strings")
    
    # Display the words
    print("Word1 = " + word1 + " | Word2 = " + word2)

    # Check if one word is equal to another  i.e. dog equals dog
    # Text is case sensitive - i.e.  Dog does not equal dog
    if(word1 == word2):
        print(word1 + " equals " + word2)
    else:
        print(word1 + " does not equals " + word2)

    # other features of python (ONLY)!!!!!!!!!!!!!!!!!!!!!!!!!
    # Use Case - if you had a list of words that were of same case
    # meaning they were ALL upper case or lower case
    # you can use the technics below to see if a word
    # came before or after another word.
    if(word1 > word2):
        print(word1 + " greater than " + word2)
    
    if(word1 >= word2):
        print(word1 + " greater than or equal to " + word2) 

    if(word1 < word2):
        print(word1 + " less than " + word2)
    
    if(word1 <= word2):
        print(word1 + " less than or equal to " + word2) 

    if(word1 != word2):
        print(word1 + " not equal to " + word2) 


# -------------------------------


def main():
    

    anum = float(input("Please enter a number:  "))

    if_example_one(anum)

    if_example_two(anum)

    if_example_three(anum)

    mySalary = float(input("Please enter your salary:  "))

    if_range(mySalary)
   
    w1 = input("Enter Word 1 ")
    w2 = input("Enter Word 2 ")

    if_strings(w1,w2)


# -------------------------------

main()



```

