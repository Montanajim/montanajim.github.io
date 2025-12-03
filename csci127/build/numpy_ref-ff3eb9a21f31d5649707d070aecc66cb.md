# NumPy / Arrays



## What is an array?

An array is a data structure that stores a collection of items of the same data type and usually stores them in a continuous memory location.  Each item in an array is assigned a unique index, which is used to access and manipulate the item. Arrays are a fundamental data structure in computer science and are used in a wide variety of applications, such as sorting, searching, and data processing.



## What is NumPy?

NumPy stands for Numerical Python. It is the Python library that is used for working with arrays.



## Array Examples

```python
"""
Programmer: James Goudy

This code shows examples of
multi-dimesional arrays

"""

import numpy as np
import sys


# Global Variables

# one dimensional array
arr1 = np.array([1, 2, 3])


# two dimensional array
arr2 = np.array([[1, 2, 3], [4, 5, 6]])

# three dimensional array
arr3 = np.array([[[1, 2, 3],
                  [4, 5, 6],
                  [7, 8, 9]],
                 [[10, 11, 12],
                  [13, 14, 15],
                  [16, 17, 18]]])

# four dimensional array
arr4 = np.array([[[[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]],
                  [[10, 11, 12],
                   [13, 14, 15],
                   [16, 17, 18]],
                  [[19, 20, 21],
                   [22, 23, 24],
                   [25, 26, 27]]],
                 [[[28, 29, 30],
                   [31, 32, 33],
                   [34, 35, 36]],
                  [[37, 38, 39],
                   [40, 41, 42],
                   [43, 44, 45]],
                  [[46, 47, 48],
                   [49, 50, 51],
                   [52, 53, 54]]]])


def one_dimension():

    # one dimensional array

    print("\n1 Dimensional - Output")

    # print the shape
    print(str(arr1.shape))

    # Iterate through each box
    for c in range(3):

        sys.stdout.write(str(arr1[c]) + " ")

    print("\n")


def two_dimension():

    # two dimensional array
    print("\n2 Dimensional - Output")

    # print the shape
    print(str(arr2.shape))

    # Iterate through each box
    for r in range(2):
        for c in range(3):

            sys.stdout.write(str(arr2[r][c]) + " ")

        print()

    print("\n")


def three_dimesion():

    # three dimensional array
    print("\n3 Dimensional - Output")

    # print the shape
    print(str(arr3.shape))

    # Iterate through each box
    for dd in range(2):

        for r in range(3):

            for c in range(3):

                sys.stdout.write(str(arr3[dd][r][c]) + " ")

    print("\n")


def fourth_dimension():

    # fourth dimensional array

    print("\n4 Dimensional - Output")

    print("Shape " + str(arr4.shape) + "\n")

    # iterate through each box
    for ff in range(2):
        for tt in range(3):
            for r in range(3):
                for c in range(3):

                    sys.stdout.write(str(arr4[ff][tt][r][c]) + " ")

    print("\n")


def main():

    one_dimension()

    two_dimension()

    # note three and four dimensioanl arrays
    # are being printed in a linear fashion
    
    three_dimesion()

    fourth_dimension()


main()

"""
1 Dimensional - Output
(3,)
1 2 3 


2 Dimensional - Output
(2, 3)
1 2 3 
4 5 6 



3 Dimensional - Output
(2, 3, 3)
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 


4 Dimensional - Output
Shape (2, 3, 3, 3)

1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 
"""
```



## NumPy Functions

```python
# -*- coding: utf-8 -*-
"""
Created on Fri Sep 29 11:06:03 2023
Programmer: James Goudy
Title: Programming Guru

@author: jgoudy

"""

# note that we are assigning np as an alias/handle
import numpy as np
import sys


def printArray(theArray, rows, cols):

    maxStringLen = 0

    # the numpy function max() cannot work on a string array
    # in order to find the largest string, one has to iterate
    # through each individual item.  len() can be used on a string.
    # So each item is checked and the largest is kept in the
    # variable maxStringLen

    # the code checks to see if the array is a string or numbers
    # if it is a string ('<U8') then the strings are iterated one
    # by one checking the length and recording the largest

    # else - the array is a number, in which the numpy.max() and numpy.mni()
    # function will work and it will find the largest smallest value.
    # However, the absolute value needs to be used to take in account if
    # it is positive or negative.

    if theArray.dtype == '<U8':
        for r in range(rows):
            for c in range(cols):
                ilen = len(theArray[r][c])
                if (ilen > maxStringLen):
                    maxStringLen = ilen

        maxStringLen += 2

        if rows == 1:

            for c in range(cols):
                sys.stdout.write(str(theArray[c]).rjust(maxStringLen, " "))

        else:

            for r in range(rows):
                for c in range(cols):
                    sys.stdout.write(theArray[r][c].rjust(maxStringLen, " "))
                print()

    else:

        # save max and min lengths account for the sign
        # for instance -320 has greater length than 75
        # abs -> str so the len() function can be used

        maxVal = len(str(abs(theArray.max())))
        minVal = len(str(abs(theArray.min())))

        maxValLen = 0

        # ternary operator in python
        maxValLen = maxVal if maxVal > minVal else minVal

        # add to to the separation
        maxValLen += 2

        # get the max value and turn it into a string
        # value = str(theArray.max())

        # get the length of the string and add 1
        # maxLen = len(value)+ 2

        if rows == 1:

            for c in range(cols):
                sys.stdout.write(str(theArray[c]).rjust(maxValLen, " "))

        else:

            for r in range(rows):
                for c in range(cols):
                    sys.stdout.write(str(theArray[r][c]).rjust(maxValLen, " "))
                print()

    print("\n----------------\n")


def numpydemo():

    # create a two dimensional array
    arr = np.array([[11, 12, 13, 14],
                   [21, 22, 23, 24],
                   [31, 32, 33, 34]])

    rows = 3
    cols = 4

    # print 2 dimensional array

    # this for statement keeps track of the row
    for row in range(rows):

        # this for statement keeps track of the col
        for col in range(cols):
            sys.stdout.write(str(arr[row, col]) + " ")

        # When inner forstatement is done we are at the end of the row
        print()

    print("\n")

    # print an individual element arrayname[row,column]
    print("second row, third column " + str(arr[1, 2]))
    print("\n")

    # number of dimensions .ndim
    print("Number of dimensions = " + str(arr.ndim))
    print("\n")

    # shape of the array .shape
    print("Shape of array " + str(arr.shape))
    print("\n")

    # print the length of the array len(arrayname)
    # note that length does not take in account the rows
    print("The length is " + str(len(arr)))
    print()

    # print the sum of the array .sum()
    print("The sum of the array is " + str(arr.sum()))
    print()

    # print the max value of the array .max()
    print("The max of the array is " + str(arr.max()))
    print()

    # print the min value of the array .min()
    print("The min of the array is " + str(arr.min()))
    print()

    # print the mean value of the array .mean()
    print("The mean of the array is " + str(arr.mean()))
    print()

    # print the standard deviation value of the array .std()
    print("The standard deviation of the array is " + str(arr.std()))
    print()

    # print add row 1 column 2 value with
    # row 2 column 2 value
    sum = arr[0, 1] + arr[1, 1]
    print("The sum of row 1 column 2 \n" +
          "with row 2 column 2 is " + str(sum))

    # create a 2 dimensional array that is filled with random numbers
    rows = 5
    cols = 6

    print("\nArray with random integers")
    arr55 = np.arange(rows*cols).reshape(rows, cols)
    print("\narr55")
    printArray(arr55, rows, cols)

    # create an empty array filled with zeros
    arr66 = np.zeros((rows, cols))
    print("arr66 empty array with zeros")
    # print(arr66)
    printArray(arr66, rows, cols)

    # String array
    print("\nStates and Capitals")
    arr77 = np.array([["Helena", "Albany", "Columbus"],
                      ["MT", "NY", "OH"]], dtype=np.dtype('U'))

    printArray(arr77, 2, 3)

    # this creates a one dimensional array
    # with 16 elements filled with  random ints form 0 to 24
    arr2 = np.random.randint(0, 25, 16)

    print("\nArr2\n")
    for i in arr2:
        sys.stdout.write(str(i) + " ")

    print("\n")

    # convert the one dimensional array in to a 4 x 4
    arr2.resize(4, 4)

    rows = 4
    cols = 4

    printArray(arr2, rows, cols)

    print("\n")

    # boolean indexing
    print("Print values that are greater than 10")
    print(arr2[arr2 > 10])

    # Generate random letters - 65-90 A-Z
    arr3 = np.random.randint(65, 90, 15)

    # generate a blank array
    arr4 = np.zeros(len(arr3), dtype=np.str_)
    # arr4 = np.empty(15, dtype = np.unicode)

    print("\nBlank Array arr4")
    print(arr4)
    print("\nPrint the random ascii codes in arr3")
    printArray(arr3, 1, 15)

    # populate the empty arr4 with the characters
    # from arr3
    for i in range(len(arr3)):
        arr4[i] = chr(arr3[i])

    print(arr4)
    print()

    # for i in range(len(arr4)-1):
    #     sys.stdout.write(str(arr4[i]) + " ")

    # print()

    # default is empty
    arr44 = np.empty([4, 4], dtype=np.int16)
    print(arr44)

    print()
    arr44.fill(42)
    print(arr44)


def main():

    numpydemo()


main()


"""
11 12 13 14 
21 22 23 24 
31 32 33 34 


second row, third column 23


Number of dimensions = 2


Shape of array (3, 4)


The length is 3

The sum of the array is 270

The max of the array is 34

The min of the array is 11

The mean of the array is 22.5

The standard deviation of the array is 8.241156876717412

The sum of row 1 column 2 
with row 2 column 2 is 34

Array with random integers

arr55
   0   1   2   3   4   5
   6   7   8   9  10  11
  12  13  14  15  16  17
  18  19  20  21  22  23
  24  25  26  27  28  29

----------------

arr66 empty array with zeros
  0.0  0.0  0.0  0.0  0.0  0.0
  0.0  0.0  0.0  0.0  0.0  0.0
  0.0  0.0  0.0  0.0  0.0  0.0
  0.0  0.0  0.0  0.0  0.0  0.0
  0.0  0.0  0.0  0.0  0.0  0.0

----------------


States and Capitals
    Helena    Albany  Columbus
        MT        NY        OH

----------------


Arr2

15 3 7 20 2 2 15 13 10 9 9 4 16 8 5 24 

  15   3   7  20
   2   2  15  13
  10   9   9   4
  16   8   5  24

----------------



Print values that are greater than 10
[15 20 15 13 16 24]

Blank Array arr4
['' '' '' '' '' '' '' '' '' '' '' '' '' '' '']

Print the random ascii codes in arr3
  68  74  84  85  89  83  82  89  87  73  70  88  78  70  89
----------------

['D' 'J' 'T' 'U' 'Y' 'S' 'R' 'Y' 'W' 'I' 'F' 'X' 'N' 'F' 'Y']

[[42 42 42 42]
 [42 42 42 42]
 [42 42 42 42]
 [42 42 42 42]]

[[42 42 42 42]
 [42 42 42 42]
 [42 42 42 42]
 [42 42 42 42]]
"""
```

