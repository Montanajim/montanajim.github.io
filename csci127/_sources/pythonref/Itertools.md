# Itertools #

## Key Points

- **itertools:**  A module providing functions for creating efficient iterators for various tasks.
- **count([start[, step]])**: Creates an infinite iterator that starts at a specified value and increments by a specified step (defaults to 1).
- **cycle(p)**: Creates an infinite iterator that endlessly repeats the elements from an iterable.
- **permutations(iterable, r=None)**: Generates all possible arrangements (permutations) of elements from an iterable, with a specified length if provided. (Order does matter.)
- **combinations(iterable, r)**: Generates all possible combinations of elements from an iterable, with a specified length. (Order doesn't matter unlike permutations)
- **accumulate(p[, func])**: Applies a function (default is addition) cumulatively to elements in an iterable, yielding the sums at each step.
- **filterfalse(predicate, sequence)**: Creates an iterator that filters out elements from an iterable based on a predicate function (keeps elements that return False).
- **lru_cache(maxsize=128, typed=False)**: Creates a function decorator that caches the results of the function based on the arguments (Least Recently Used cache with size limit).
- **batched(p, n)**: Creates an iterator that yields fixed-size chunks of elements from an iterable.

## Concept ##

In computer programming, an iterable is essentially a container that holds elements and allows you to access them one by one in a specific order.  Think of it like a box with items you can take out, one at a time.

Here's a breakdown of what iterables are and how they work:

- **Usable with loops:** The key feature of iterables is that you can use them in 'for' loops to process elements efficiently. The loop automatically iterates over the iterable, retrieving each element on each pass.
- **Examples:** Common examples of iterables include lists, tuples, strings, sets, and dictionaries (in some languages).
- **Behind the scenes:**  Iterables typically implement a special method (often named `__iter__`) that creates an iterator object. This iterator keeps track of the current position within the iterable and provides access to elements one at a time.

Here's an analogy: Imagine a bookshelf (iterable) containing books (elements). You can't grab all the books at once, but you can go through them one by one (iteration) using a ladder (iterator) to reach each book on the shelf.

Iterables are fundamental for processing sequences of data in programming and form the backbone of many powerful techniques.

## Itertools Library ##

The `itertools` module in Python is a toolbox specifically designed to work with iterables. It provides functions that create new iterators based on existing iterables.  These new iterators can perform various manipulations on the original data in a memory-efficient way.



Here is a sample of how they work. This is the accumulate function. Note that it returns an  iterator.

The `itertools.accumulate()` function in Python is a powerful tool for performing cumulative operations on iterables. It creates an iterator that yields the sum (by default) or any other function applied cumulatively to the elements of the iterable.

Here's a breakdown of how `itertools.accumulate()` works:

- **Cumulative Operations:** It applies a function to successive elements of the iterable, keeping track of a running total. This total is then yielded by the iterator at each step.
- **Default Behavior (Sum):** If you don't provide a custom function, `accumulate()` performs addition by default. This is useful for calculating running sums, like finding the total sales up to a certain point in a list.
- **Custom Functions:** You can provide a custom function to `accumulate()` to perform different cumulative operations. This function should take two arguments: the current accumulated value and the next element from the iterable. The function's return value becomes the new accumulated value for the next iteration.

Here are some key points to remember about `itertools.accumulate()`:

- ***Returns an Iterator:** It's important to note that `accumulate()` returns an iterator, not a list. This means the elements are generated on-demand, saving memory compared to creating a new list to store all the results.*
- **Optional Initial Value (Python 3.8+):** In Python versions 3.8 and later, you can specify an initial value using the `initial` argument. This value will be prepended to the beginning of the accumulated results.

## Documentation

https://docs.python.org/3.12/library/itertools.html# 

Note there are more itertools listed  in the official document



## Code

```python
"""
Itertools 
Programmer: James Goudy
Date: 07/19/2024

This script demonstrates various functionalities from the itertools library in Python.
"""

# Import libraries
import itertools
import operator
import functools

import sys

# Function to generate a count loop (runs indefinitely)
def iter_count():
  """
  This function demonstrates the itertools.count() function
  which generates an unending sequence of numbers.

  Parameters:
      None

  Returns:
      None (prints the sequence to the console)
  """
  print("\nCount Example")

  start = 0
  stop = 500
  step = 100

  for i in itertools.count(start, step):
    print(i)

    # Break the loop when reaching the stop value
    if i >= stop:
      break

# Function to cycle through elements in a list repeatedly
def iter_cycle():
  """
  This function demonstrates the itertools.cycle() function
  which iterates through a list repeatedly.

  Parameters:
      None

  Returns:
      None (prints the cycled elements to the console)
  """
  print("\nCycle Example")

  cntr = 0
  myList = [10, 20, 30, 40]
  myList2 = ["AA", "BB", "CC", "DD"]
  repeatCycle = 2

  for i in itertools.cycle(myList):
    print(i)
    cntr += 1

    # Break the cycle after a specified number of repetitions
    if cntr >= (repeatCycle * len(myList)):
      break

  cntr = 0
  print()
  for i in itertools.cycle(myList2):
    print(i)
    cntr += 1

    # Break the cycle after a specified number of repetitions
    if cntr >= (repeatCycle * len(myList)):
      break

# Function to generate permutations (ordered arrangements)
def iter_permutations():
  """
  This function demonstrates the itertools.permutations() function
  which generates all possible ordered arrangements (permutations) of elements.

  Parameters:
      None

  Returns:
      None (prints the permutations to the console)
  """
  print("\nPermutation Example")

  myList = [1, 2, 3]

  for prm in itertools.permutations(myList):
    print(prm)

# Function to generate combinations (unordered arrangements)
def iter_combinations():
  """
  This function demonstrates the itertools.combinations() function
  which generates all possible unordered arrangements (combinations) of elements.

  Parameters:
      None

  Returns:
      None (prints the combinations to the console)
  """
  print("\nCombinations Example")

  myList = [1, 2, 3, 4]

  combLen = len(myList)

  for cSize in range(1, combLen + 1):

    print("\nCombination size = {}".format(cSize))

    for prm in itertools.combinations(myList, cSize):
      print(prm)

# Function to calculate accumulated sums
def iter_accumulate():
  """
  This function demonstrates the itertools.accumulate() function
  which returns a sequence of partial sums.

  Parameters:
      None

  Returns:
      None (prints the accumulated sums to the console)
  """
  print("\nAccumulation Example")

  myList = [2, 4, 5, 10]
  print("Data is - {}".format(myList))

  # Rolling total using accumulate
  myAcc = itertools.accumulate(myList)
  print(list(myAcc))

  # Iterate through each item in the accumulated sequence
  print("\nIterate through \neach item in Acc")
  for x in itertools.accumulate(myList):
    print("item is {}".format(x))

  print("\nMultiple instead of add")
  myAcc = itertools.accumulate(myList, operator.mul)
  print(list(myAcc))

# --------------------------------------------------
# Filter out data based on a specific criteria

# Helper function for iter_filterfalse
def divByTwo(a):
  """
  This function checks if a number is odd (not divisible by 2). 
  It's a helper function used by iter_filterfalse.

  Parameters:
      a (int): The number to check

  Returns:
      bool: True if the number is odd, False otherwise
  """

def iter_filterfalse():
  """
  This function demonstrates the itertools.filterfalse() function
  which filters out elements based on a condition.

  Parameters:
      None

  Returns:
      None (prints the filtered elements to the console)
  """
  myList = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

  # Filter out odd numbers (elements not divisible by 2) using divByTwo function
  evenNums = itertools.filterfalse(divByTwo, myList)
  print("Evens", list(evenNums))

  # Filter out even numbers (elements divisible by 2) using lambda function
  evenNums = itertools.filterfalse(lambda x: x % 2, myList)
  print("Evens", list(evenNums))

# --------------------------------------------------

# ---------- leave recursion in cache --------------

global countFastSteps
global countSlowSteps

countFastSteps = 0
countSlowSteps = 0

@functools.lru_cache()
def fibfast(n):
  """
  This function calculates the nth Fibonacci number using recursion 
  with memoization (lru_cache) for efficiency.

  Parameters:
      n (int): The index of the Fibonacci number to calculate

  Returns:
      int: The nth Fibonacci number
  """
  global countFastSteps
  countFastSteps = countFastSteps + 1
  return fibfast(n-2) + fibfast(n-1) if n > 1 else 1

def fibslow(n):
  """
  This function calculates the nth Fibonacci number using recursion 
  without memoization (slower approach).

  Parameters:
      n (int): The index of the Fibonacci number to calculate

  Returns:
      int: The nth Fibonacci number
  """
  global countSlowSteps
  countSlowSteps += 1
  return fibslow(n-2) + fibslow(n-1) if n > 1 else 1

def lru_cache_example(i):
  """
  This function demonstrates the performance improvement of memoization (lru_cache)
  by comparing the number of function calls needed to calculate the nth Fibonacci number 
  with and without memoization.

  Parameters:
      i (int): The index of the Fibonacci number to calculate

  Returns:
      None (prints the number of function calls to the console)
  """
  # Initialize variables globally to avoid errors
  global countSlowSteps
  global countFastSteps
  countSlowSteps = 0
  countFastSteps = 0

  fibfast(i)
  fibslow(i)

  print(countFastSteps)
  print('With lru_cache total function steps: ', countFastSteps)
  print('Without lru_cache total function steps: ', countSlowSteps)

# --------------------------------------------------

def itr_batch():
  """
  This function demonstrates the itertools.batched() function
  which groups elements from an iterable into fixed-size chunks.

  Parameters:
      None

  Returns:
      None (prints the batched elements and manipulates them to the console)
  """

  print("\nBatch Process")

  # Create a list of numbers
  my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17]

  # Use itertools.batched() to group elements in the list into chunks of size 4
  for batch_item in itertools.batched(my_list, 4):
    # Convert the batched item (generator) to a list and print it
    print(list(batch_item))  # Print the batched elements

    # Loop through each item within the current batch
    for item in batch_item:
      # Multiply the item by 10 and print it with a space
      sys.stdout.write(str(item * 10) + " ")
    # Add a newline and separator after processing each batch
    print("\n---\n")

  # Define a multi-line string containing a quote
  quote = """
  Never argue with stupid people, 
  they will drag you down to their level 
  and beat you with experience. - Mark Twain
  """

  # Use itertools.batched() again to group characters in the quote into chunks of size 7
  for chunk in itertools.batched(quote, 7):
    # Print each chunk of the quote
    print(chunk)
def main():

    iter_count()

    iter_cycle()

    iter_permutations()

    iter_combinations()

    iter_accumulate()

    iter_filterfalse()

    lru_cache_example(25)

    itr_batch()

    print("\n\nbye\n")

main()

'''
Count Example
0
100
200
300
400
500

Cycle Example
10
20
30
40
10
20
30
40

AA
BB
CC
DD
AA
BB
CC
DD

Permutation Example
(1, 2, 3)
(1, 3, 2)
(2, 1, 3)
(2, 3, 1)
(3, 1, 2)
(3, 2, 1)

Combinations Example

Combination size = 1
(1,)
(2,)
(3,)
(4,)

Combination size = 2
(1, 2)
(1, 3)
(1, 4)
(2, 3)
(2, 4)
(3, 4)

Combination size = 3
(1, 2, 3)
(1, 2, 4)
(1, 3, 4)
(2, 3, 4)

Combination size = 4
(1, 2, 3, 4)

Accumulation Example
Data is - [2, 4, 5, 10]
[2, 6, 11, 21]

Iterate through
each item in Acc
item is 2
item is 6
item is 11
item is 21

Multiple instead of add
[2, 8, 40, 400]
Evens [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Evens [2, 4, 6, 8, 10]
26
With lru_cache total function steps:  26
Without lru_cache total function steps:  242785

Batch Process
[1, 2, 3, 4]
10 20 30 40
---

[5, 6, 7, 8]
50 60 70 80
---

[9, 10, 11, 12]
90 100 110 120
---

[13, 14, 15, 16]
130 140 150 160
---

[17]
170
---

('\n', ' ', ' ', 'N', 'e', 'v', 'e')
('r', ' ', 'a', 'r', 'g', 'u', 'e')
(' ', 'w', 'i', 't', 'h', ' ', 's')
('t', 'u', 'p', 'i', 'd', ' ', 'p')
('e', 'o', 'p', 'l', 'e', ',', ' ')
('\n', ' ', ' ', 't', 'h', 'e', 'y')
(' ', 'w', 'i', 'l', 'l', ' ', 'd')
('r', 'a', 'g', ' ', 'y', 'o', 'u')
(' ', 'd', 'o', 'w', 'n', ' ', 't')
('o', ' ', 't', 'h', 'e', 'i', 'r')
(' ', 'l', 'e', 'v', 'e', 'l', ' ')
('\n', ' ', ' ', 'a', 'n', 'd', ' ')
('b', 'e', 'a', 't', ' ', 'y', 'o')
('u', ' ', 'w', 'i', 't', 'h', ' ')
('e', 'x', 'p', 'e', 'r', 'i', 'e')
('n', 'c', 'e', '.', ' ', '-', ' ')
('M', 'a', 'r', 'k', ' ', 'T', 'w')
('a', 'i', 'n', '\n', ' ', ' ')


bye
'''
```



