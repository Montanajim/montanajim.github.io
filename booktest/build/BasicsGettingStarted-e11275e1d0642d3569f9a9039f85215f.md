# Basics - Getting Started


```{index} single: references
```


## Concepts

* Scripted language - does not compile to machine code
    note: there are separate programs that will compile it into machine code
* Case sensitive
* Space-based - tabbing has meaning



## Expanded Comments

**Triple quotes**  part of the program's documentation.  They allow you to have multi-lined comments

````python

"""
This is comment line 1
This is comment line 2
This is comment line 3
etc
"""
print("Comments are an essential part of programming")

````



## Editors

- ​    Idle
- ​    Spyder
- ​    Pycharm
- ​    others....

Run in interactive mode
```{index} single: Editors
```


## Coding Format

List appropriate use of white space and tabbing
Do not go more than 80 characters
Escape characters \n and \t

Two or more physical lines may be joined 
into logical lines using backslash characters (\)
```{index} single: Coding Format
```

## Variable names

- must start with a letter
- may contain the underscore
- may contain numbers
- case sensitive
```{index} single: Variable Names
```

## Lecture Code 

```python
"""
Concepts 
* Scripted language - does not compile to machine code
    note: there are sperate programes that will compile it into machine code
* Case sensitive
* Space based - tabbing has meaning

Explain comments
    triple quotes part of program's documenation system

Editors
    Idle
    Spyder
    pycharm
    others....
Run in interactive mode

List appropriate use of white space and tabbing
Do not go more than 80 characters
Escape characters \n and \t

Two or more physical lines may be joined 
into logical lines using backslash characters (\)

variable names
must start with a letter
may contain the underscore
may contain numbers
case sensitive

input

Discuss operations
() parenthesis
** power
+ - add subtract
* / multiple divide
//   integer division
% mod


"""
# first program
print ("hello world")

"""
data types
storing variables
    variable names should be descriptive
"""

#integers
a = 42
print(a)
print(type(a))

# = floats
b = 42.0
print(b)
print(type(b))

# = strings
c = "forty two"
print(c)
print(type(c))

# = booleans  True / False
d = True
print(d)
print(type(d))

# = null
e = None
print(e)
print(type(e))

# ---------------------------------------
#   containers - discuss more in future - just show
# ---------------------------------------

print("\n*** Lists ***\n")      # Explain \n and \t

### LISTS ###
## properties: ordered, iterable, mutable, can contain multiple data types
mylista = [1,2,3,4]
print(mylista)

mylistb = ["larry", "curly", "moe"]
print(mylistb)

mylistc = [42, 42.0, "forty two", True, ['Tom', 'Dick', 'Harry']]
print(mylistc)

### TUPLES ###
## properties: ordered, iterable, immutable, can contain multiple data types
## like lists, but they don't change size
mytuplea = (1,2,3)
print(mytuplea)

mytupleb = ("Ducks", "Goats", "Cows")
print(mytupleb)

mytuplec = (1, 1.1, "one", False, [42, 43, 44, 45])
print(mytuplec)
print(type(mytuplec))


### DICTIONARIES ###
## properties: unordered, iterable, mutable, can contain multiple data types
## made of key-value pairs
## keys must be unique, and can be strings, numbers, or tuples
## values can be any type

# ---------------------------------------

print("\n*** Dictionaries ***\n")

### DICTIONARIES ###
## properties: unordered, iterable, mutable, can contain multiple data types
## made of key-value pairs
## keys must be unique, and can be strings, numbers, or tuples
## values can be any type

mydict = {"key1": "value1", "key2": "value2", "key3": "value3" }
print(mydict)

# student number, last name
mydict1 = {111 : "Smith", 222 : "Doe", 333 : "Baker"}
print(mydict1)
print(type(mydict1))

#show error
mydict1 = {111 : "Smith", 222 : "Doe", 333 : "Baker", 111 : "Adam"}

# ---------------------------------------

print("\n*** Sets ***\n")

### SETS ###
## properties: unordered, iterable, mutable, can contain multiple data types
## made of unique elements (strings, numbers, or tuples)
## like dictionaries, but with keys only (no values)

#like dictionaries, but leave of the values
myset1 = {'python', 'r', 'java', 'c#'} 
print(myset1)

myset2 = {1, 2, 3, 4, 5, 6}
print(myset2)
print(type(myset2))

#show error
myset3 = {11,22,33,33, 44,55}
print(myset3)

# -------------------------------------

print("Get and display input " )
dogname = input("Enter a dog name ")
dogage = float(input("Enter the dog age in years  "))

# numbers must be in a str() function
print("Dog name = " +  dogname + "  age = " + str(dogage))
print("\n\n")



print("-- operations review --")
print("Parenthesis 2 + 5 * 7 vs (2 + 5) * 7")
x = 2 + 5 * 7
print(x)
x = (2 + 5) * 7
print(x)

print("3 to the power of 3 3**3")
x = 3**3
print(x)

a = 10.5
b = 2.5


print("Add and subtract 10.5 2.5")
x = a + b
print(x)

x = a - b
print(x)

print("Multiple and divide 10.5 2.5")

x = a * b
print(x)


# End of program




```



---

End of Topic





