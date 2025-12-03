

# 🐾 **Pet Search Program — Explanation and Learning Outcomes**

## **Program Overview**

This Python program demonstrates **object-oriented programming (OOP)** through the creation and management of a `Pet` class. Each `Pet` object stores three key attributes — **name, breed, and type** — and the program builds a list of these objects to simulate a simple pet database.
 It then performs three main tasks:

1. **Displays all pets** in a neatly formatted list.
2. **Searches for a pet by name**, using case-insensitive comparison.
3. **Counts and reports the number of dogs and cats** in the dataset.

Through this, students gain hands-on experience with **class construction, object instantiation, encapsulation, list manipulation, and search algorithms** — all core principles in introductory computer science.

------

## **Key Concepts Demonstrated**

1. **Class Design and Object-Oriented Thinking**
   - Introduces the idea of modeling real-world entities (pets) as **objects**.
   - Demonstrates **constructors (`__init__`)**, **instance variables**, and **string representations (`__str__`)**.
2. **Encapsulation and Data Access**
   - Reinforces **data hiding** and controlled access through Python’s `@property` and setter decorators.
   - Encourages writing robust, maintainable code where attributes are accessed safely.
3. **List-Based Data Storage**
   - Demonstrates how to store and traverse lists of objects.
   - Highlights how lists serve as flexible containers for structured data.
4. **Functional Decomposition**
   - Separates logic into reusable functions (`addPetsToList`, `findPetName`, `countTypes`, and `main`).
   - Emphasizes **top-down design** and the importance of a clean, organized program structure.
5. **Search Logic and Conditional Flow**
   - Implements a **case-insensitive search algorithm**.
   - Uses `if` statements and return values to control flow and handle edge cases.
6. **Iteration and Aggregation**
   - Demonstrates looping through objects to perform operations such as counting and filtering.
   - Reinforces accumulation patterns (`dogCount`, `catCount`) in programming logic.
7. **Debugging and Output Formatting**
   - Encourages readable console output and diagnostic print statements.
   - Reinforces understanding of formatted strings (f-strings) for expressive output.
8. **Code Readability and Documentation**
   - Uses clear variable names, meaningful comments, and modular design.
   - Promotes industry-aligned coding habits and Python style conventions (PEP 8).

------

## Example Code

```python
# -------------------------------------------------
# Program: Pet Search Example (Enhanced)
# Author: Jim Goudy
# Description:
#   Demonstrates creating a Pet class, storing Pet objects,
#   searching for pets by name (case-insensitive) and 
#   counting the number of cats and dogs.
#
#   The program lists pets, searches by name, and reports
#   the exact match if found.
# -------------------------------------------------


# -------------------------------------------------
# Class Definition: Pet
# -------------------------------------------------
class Pet:

    def __init__(self, a_petname="", a_petbreed="", a_pettype=""):
        """Constructor initializes the pet's name and breed."""
        self.a_petname = a_petname
        self.a_petbreed = a_petbreed
        self.a_pettype = a_pettype

    def __str__(self):
        """Returns a readable string representation of the pet."""
        return f"{self.a_petname} ({self.a_petbreed} {self.a_pettype})"

    # Property methods for pet name
    @property
    def petname(self):
        """Gets the pet's name."""
        return self.a_petname

    @petname.setter
    def petname(self, value):
        """Sets the pet's name."""
        self.a_petname = value

    # Property methods for pet breed
    @property
    def petbreed(self):
        """Gets the pet's breed."""
        return self.a_petbreed

    @petbreed.setter
    def petbreed(self, value):
        """Sets the pet's breed."""
        self.a_petbreed = value
        
    # Property methods for pet type
    @property
    def pettype(self):
        """Gets the pet's type."""
        return self.a_pettype

    @pettype.setter
    def pettype(self, value):
        """Sets the pet's breed."""
        self.a_pettype = value
        
    # ------------- Methods -----------------------

    def printPet(self):
        """Prints the pet's name and breed in a single line."""
        print(f"{self.petname} - {self.petbreed}")


# ---------------- End Of Class -------------------


# -------------------------------------------------
# Global Variables and Functions
# -------------------------------------------------

# List to store all Pet objects
listOfPets = []


def addPetsToList(nameList, breedList,types):
    """
    Creates Pet objects from name and breed lists
    and appends them to the global listOfPets.
    """
    for i in range(len(nameList)):
        px = Pet(nameList[i], breedList[i],types[i])
        listOfPets.append(px)
        px.printPet()


def findPetName(findName):
    """
    Searches the global list for a pet with the given name.
    Comparison is case-insensitive.
    Returns the Pet object if found, otherwise None.
    """
    for apet in listOfPets:
        if findName.lower() == apet.petname.lower():  # case-insensitive match
            return apet
    return None

def countTypes(alist):
    """
    This function counts how many dogs and cats are in a 
    list of pet objects. It starts by initializing two counters — 
    dogCount and catCount — both set to zero. Then, it loops through 
    each apet in listOfPets (note: the function parameter alist is unused).

    For each pet, it prints its type (apet.pettype) and checks if the 
    pet’s type is "dog". If it is, it increments the dog counter. Otherwise, 
    it assumes the pet is a cat and increments the cat counter.
    """
    
    dogCount = 0
    catCount = 0
    
    for apet in listOfPets:
        print("ttt: " + apet.pettype)
        if(apet.pettype.lower() == "dog" ):
            dogCount +=1
        else:
            catCount = catCount + 1
            
    print(f"Dog count = {dogCount}")
    print(f"Cat count = {catCount}")

# -------------------------------------------------
# Main Program
# -------------------------------------------------
def main():
    """Main driver function for pet creation and search."""

    # 15 pet names (dogs and cats mixed)
    petnames = [
        "Buddy", "Luna", "Charlie", "Bella", "Max",
        "Milo", "Lucy", "Rocky", "Daisy", "Leo",
        "Chloe", "Cooper", "Nala", "Simba", "Zoe"
    ]

    # 15 breeds (dogs and cats mixed together)
    breeds = [
        "Labrador Retriever", "Beagle", "German Shepherd", "Poodle", "Bulldog",
        "Golden Retriever", "Siamese", "Persian", "Mutt", "Sphynx",
        "Bengal", "Ragdoll", "Shih Tzu", "Boxer", "Chihuahua"
    ]

    types = [
        "dog", "dog", "dog", "dog", "dog",
        "dog", "cat", "cat", "dog", "cat",
        "dog", "cat", "dog", "dog", "dog"  
    ]
    
    # Populate list of pets
    print("Pet List:")
    addPetsToList(petnames, breeds,types)

    print("\n")  # Blank line for readability

    # Search for a specific pet name
    searchName = "luCy"  # lower case for demo
    result = findPetName(searchName)

    if result:
        print(f"Pet found: {result.petname} is a {result.petbreed}.")
    else:
        print(f"Pet '{searchName}' was NOT found.")
        
    
    countTypes(listOfPets)

    print("\nbye\n")


# -------------------------------------------------
# Program Entry Point
# -------------------------------------------------
main()

```



