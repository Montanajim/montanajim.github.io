#  Panel Data - Dog Example



Panel Data is a tool for handling mixed data types. Here is an example of some data involving dogs.



## Dog Data

|       | Owner      | Breed        | Dog Name | Height | Weight | Age  |
| ----- | ---------- | ------------ | -------- | ------ | ------ | ---- |
| Dog1  | Rowan      | Spaniel      | Ziggy    | 23     | 19     | 9    |
| Dog2  | Amari      | Newfoundland | Pepper   | 17     | 60     | 6    |
| Dog3  | Zev        | Afghan       | Finn     | 29     | 27     | 14   |
| Dog4  | Juniper    | Mudi         | Willow   | 35     | 43     | 10   |
| Dog5  | Kai        | Borzoi       | Scout    | 18     | 14     | 13   |
| Dog6  | Elodie     | Terrier      | Riley    | 32     | 31     | 2    |
| Dog7  | Silas      | Terrier      | Milo     | 12     | 46     | 5    |
| Dog8  | Nova       | Leonberger   | Juniper  | 30     | 22     | 1    |
| Dog9  | Emery      | Terrier      | Jasper   | 11     | 12     | 3    |
| Dog10 | Clementine | Spaniel      | Mochi    | 26     | 16     | 4    |



## Information to find

- find the dog that weighs the most (with attached data )
- find the dog that weighs the least  (with attached data )
- find the average dog weight
- find only max dog weight with no other information
- list the dog names
- list dog information based on a breed



## Example

### Source Code

```python
# examples of panel data

import sys
import pandas as pd


# global variables

# data
mydata = [
    ['Rowan', 'Spaniel', 'Ziggy', 23, 19, 9],
    ['Amari', 'Newfoundland', 'Pepper', 17, 60, 6],
    ['Zev', 'Afghan', 'Finn', 29, 27, 14],
    ['Juniper', 'Mudi', 'Willow', 35, 43, 10],
    ['Kai', 'Borzoi', 'Scout', 18, 14, 13],
    ['Elodie', 'Terrier', 'Riley', 32, 31, 2],
    ['Silas', 'Terrier', 'Milo', 12, 46, 5],
    ['Nova', 'Leonberger', 'Juniper', 30, 22, 1],
    ['Emery', 'Terrier', 'Jasper', 11, 12, 3],
    ['Clementine', 'Spaniel', 'Mochi', 26, 16, 4]
    ]

# column headers
mycols = ["Owner", "Breed", "Dog Name", "Height", "Weight", "Age"]

# indexes / row headers
myindexes = ["Dog1","Dog2","Dog3","Dog4","Dog5",
             "Dog6","Dog7","Dog8","Dog9","Dog10"]

df = None


# -------------------------------------------------------------------------------------

def setupPanelData():

    global df

    # create a dataframe with just data
    df = pd.DataFrame(mydata)

    print("\n")
    print(df)
    print("\n")

    # add columns headers to the dataframe
    df.columns = mycols 

    print("\n")
    print(df)
    print("\n")

    # add indexes / row titles to dataframe
    df.index = myindexes

    print("\n")
    print(df)
    print("\n")

    # *** Alternative Method for Above ***************************

    # create a dataframe with data, column headings 
    # and row indexes at once

    df = pd.DataFrame(mydata, columns = mycols, index = myindexes)


def dogWeights():

    # This function demonstrates the various ways to get
    # a dog weight.  NOTE the ".idxmax()" will bring
    # the whole row

    # find the dog that weighs the most
    print("\nHeaviest Dog")
    maxDogWeight = df.loc[df['Weight'].idxmax()]
    print("Max Dog Weight is \n{}\n".format(maxDogWeight))
    print("{} weighs {} lbs".format(maxDogWeight['Dog Name'], maxDogWeight['Weight']))


    # find the dog that weighs the least
    print("\nLightest Dog")
    minDogWeight = df.loc[df['Weight'].idxmin()]
    print("Minimum Dog Weight is \n{}\n".format(minDogWeight))
    print("{} weighs {} lbs".format(minDogWeight['Dog Name'], minDogWeight['Weight']))

    # find the average dog weight
    print("\nAverage Dog Weight")
    meanDogWeight = df['Weight'].mean()
    print("The average dog weight is {} lbs".format(meanDogWeight))

    # find only max dog weight with no other information
    print("\nfind only max dog weight with no other information")
    maxdw= df['Weight'].max()
    print("The max dog weight is {} lbs\n".format(maxdw))


def listDogNames():

    # list the dog names
    theDogNames = df['Dog Name']
    # print the dog names
    sys.stdout.write("\nDog Names: \n")
    for c in range(len(theDogNames)):
        
        # print 2 names per line
        if (((c % 2) == 0) and (c > 0)):
            print()
            
		# print the dog name
        sys.stdout.write("{} ".format(theDogNames.iloc[c]))


    print()

def dogBreedInfo():

    # list dog information based on a breed
    # shape returns rows and columns

    # List the dog breeds
    # get the dog breeds from panel and store as list
    dgbreeds = df['Breed'].to_list()
    dgbreeds.sort()
    print()
    lastDog = None

    for i in range(len(dgbreeds)):
        
        # the if statement prevents duplicate 
        # dogs from being printed - note
        # the list has to be sorted

        if(lastDog != dgbreeds[i] ):
            print("{}".format(dgbreeds[i]))
            lastDog = dgbreeds[i]

    # ------------------------------------------------

    # flag to see whether there was any matches
    notFoundCheck = True

    # note that if the user enters nothing - "Afgan" will be the default
    dbreed = input("\nEnter the dog breed: ").lower().capitalize() or "Afghan"
    print("You entered: {}".format(dbreed))

    for r in range(df.shape[0]):
        # get row and convert it to dictionary - keys and values 
        rowInfo = df.iloc[r].to_dict()

        if(rowInfo['Breed'] == dbreed):
            notFoundCheck = False

            # the key and value
            for key,value in rowInfo.items():
                sys.stdout.write("{} - {} | ".format(key,value))
            print("\n")

    # check if nothing was found
    if notFoundCheck:
        print("\nBreed was not found\n")


def menu():

    print("Please select an option:")
    print("1. Dog Weights")
    print("2. List Dog Names")
    print("3. Dog Breed Info")

    choice = input("Enter your choice (1/2/3): ")
    
    if choice == '1':
        dogWeights()
    elif choice == '2':
        listDogNames()
    elif choice == '3':
        dogBreedInfo()
    else:
        print("Invalid choice. Please try again.")

def main():
    
    setupPanelData()

    quit = "n"

    while quit != "y":

        menu()
        quit = input("Would you like to quit y/n ").lower()


    print("\nbye\n")


main()
```



### Output

```


            0             1        2   3   4   5
0       Rowan       Spaniel    Ziggy  23  19   9
1       Amari  Newfoundland   Pepper  17  60   6
2         Zev        Afghan     Finn  29  27  14
3     Juniper          Mudi   Willow  35  43  10
4         Kai        Borzoi    Scout  18  14  13
5      Elodie       Terrier    Riley  32  31   2
6       Silas       Terrier     Milo  12  46   5
7        Nova    Leonberger  Juniper  30  22   1
8       Emery       Terrier   Jasper  11  12   3
9  Clementine       Spaniel    Mochi  26  16   4




        Owner         Breed Dog Name  Height  Weight  Age
0       Rowan       Spaniel    Ziggy      23      19    9
1       Amari  Newfoundland   Pepper      17      60    6
2         Zev        Afghan     Finn      29      27   14
3     Juniper          Mudi   Willow      35      43   10
4         Kai        Borzoi    Scout      18      14   13
5      Elodie       Terrier    Riley      32      31    2
6       Silas       Terrier     Milo      12      46    5
7        Nova    Leonberger  Juniper      30      22    1
8       Emery       Terrier   Jasper      11      12    3
9  Clementine       Spaniel    Mochi      26      16    4




            Owner         Breed Dog Name  Height  Weight  Age
Dog1        Rowan       Spaniel    Ziggy      23      19    9
Dog2        Amari  Newfoundland   Pepper      17      60    6
Dog3          Zev        Afghan     Finn      29      27   14
Dog4      Juniper          Mudi   Willow      35      43   10
Dog5          Kai        Borzoi    Scout      18      14   13
Dog6       Elodie       Terrier    Riley      32      31    2
Dog7        Silas       Terrier     Milo      12      46    5
Dog8         Nova    Leonberger  Juniper      30      22    1
Dog9        Emery       Terrier   Jasper      11      12    3
Dog10  Clementine       Spaniel    Mochi      26      16    4


Please select an option:
1. Dog Weights
2. List Dog Names
3. Dog Breed Info
Enter your choice (1/2/3): 1

Heaviest Dog
Max Dog Weight is
Owner              Amari
Breed       Newfoundland
Dog Name          Pepper
Height                17
Weight                60
Age                    6
Name: Dog2, dtype: object

Pepper weighs 60 lbs

Lightest Dog
Minimum Dog Weight is
Owner         Emery
Breed       Terrier
Dog Name     Jasper
Height           11
Weight           12
Age               3
Name: Dog9, dtype: object

Jasper weighs 12 lbs

Average Dog Weight
The average dog weight is 29.0 lbs

find only max dog weight with no other information
The max dog weight is 60 lbs

Would you like to quit y/n n
Please select an option:
1. Dog Weights
2. List Dog Names
3. Dog Breed Info
Enter your choice (1/2/3): 2

Dog Names:
Ziggy Pepper
Finn Willow
Scout Riley
Milo Juniper
Jasper Mochi
Would you like to quit y/n n
Please select an option:
1. Dog Weights
2. List Dog Names
3. Dog Breed Info
Enter your choice (1/2/3): 3

Afghan
Borzoi
Leonberger
Mudi
Newfoundland
Spaniel
Terrier

Enter the dog breed:
You entered: Afghan
Owner - Zev | Breed - Afghan | Dog Name - Finn | Height - 29 | Weight - 27 | Age - 14 |

Would you like to quit y/n y

bye

```

