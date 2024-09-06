# Software Testing  Unit Testing



## Unit Testing

- **Definition:** Unit testing involves testing individual components or units of code in isolation. These units could be functions, methods, or classes.
- **Purpose:** To verify that each unit works as expected and meets its specific requirements.
- Benefits:
  - Early detection of defects
  - Improved code quality
  - Increased code maintainability
  - Supports regression testing

## Integration Testing

- **Definition:** Integration testing combines multiple units or components to test their interactions and communication.
- **Purpose:** To verify that different parts of the software work together as expected.
- Benefits:
  - Identifies interface-related defects
  - Ensures data integrity and flow
  - Improves system stability



## UnitTest

**Unittest** is Python's standard library for writing and running unit tests. It provides a structured approach to testing individual units of code (functions, methods, classes) to ensure they behave as expected.



https://docs.python.org/3/library/unittest.html



### Key Features:

- **Test Cases:** Define individual test scenarios using the `TestCase` class.
- **Test Suites:** Organize test cases into collections for efficient execution.
- **Assertions:** Verify expected outcomes using methods like `assertEqual`, `assertTrue`, etc.
- **Fixtures:** Set up and tear down test environments using `setUp()` and `tearDown()` methods.



## UnitTest Examples

### Basic Example: Testing a Simple Function

Python

```python
"""
Unit Testing is for the testing of functions
and methods
"""

import unittest

def add(x, y):
    return x + y

class TestAdd(unittest.TestCase):


    def test_add_positive_true(self):
        result = add(2, 3)
        self.assertEqual(result, 5)

    def test_add_positive_true_bad(self):
        result = add(2, 3)
        self.assertEqual(result, 100) 

    def test_add_negative(self):
        result = add(-1, 2)
        self.assertEqual(result, 1)
        
# ------ Examples of comparitive values
        
    def test_3_gt_2(self):
        self.assertGreater(3,2);

    def test_2_gt_3(self):
        self.assertGreater(2,3);
    
if __name__ == '__main__':
    # Setting the verbosity to 2
    # Gives details on what tests 
    # were ran and the outcomes
    unittest.main(verbosity=2)


"""
output:


test_2_gt_3 (__main__.TestAdd.test_2_gt_3) ... FAIL
test_3_gt_2 (__main__.TestAdd.test_3_gt_2) ... ok
test_add_negative (__main__.TestAdd.test_add_negative) ... ok
test_add_positive_true (__main__.TestAdd.test_add_positive_true) ... ok
test_add_positive_true_bad (__main__.TestAdd.test_add_positive_true_bad) ... FAIL    

======================================================================
FAIL: test_2_gt_3 (__main__.TestAdd.test_2_gt_3)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "e:\My Drive\0_CSCI_127_JBD\Teaching_Modules\Module_Testing\unitTesting_example1.py", line 30, in test_2_gt_3
    self.assertGreater(2,3);
    ^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: 2 not greater than 3

======================================================================
FAIL: test_add_positive_true_bad (__main__.TestAdd.test_add_positive_true_bad)       
----------------------------------------------------------------------
Traceback (most recent call last):
  File "e:\My Drive\0_CSCI_127_JBD\Teaching_Modules\Module_Testing\unitTesting_example1.py", line 20, in test_add_positive_true_bad
    self.assertEqual(result, 100)
AssertionError: 5 != 100

----------------------------------------------------------------------
Ran 5 tests in 0.004s

FAILED (failures=2)

"""
```



### Testing a Class Method

Python

```python
"""
Unit Testing is for the testing of functions
and methods
"""

import unittest


class AddCaclulator:

    def __init__(self) -> None:
        pass

    def add(x, y):
        return x + y

class TestAdd(unittest.TestCase):

    def test_add_positive_true(self):
        result = myCalculator.add(2, 3)
        self.assertEqual(result, 5)

    def test_add_positive_true_bad(self):
        result = myCalculator.add(2, 3)
        self.assertEqual(result, 100) 

    def test_add_negative(self):
        result = myCalculator.add(-1, 2)
        self.assertEqual(result, 1)

    # ------ Examples of comparitive values
    def test_3_gt_2(self):
        self.assertGreater(3,2);

    def test_2_gt_3(self):
        self.assertGreater(2,3);

# global object
myCalculator = AddCaclulator

if __name__ == '__main__':
    # Setting the verbosity to 2
    # Gives details on what tests 
    # were ran and the outcomes
    unittest.main(verbosity=2)


'''
Output
# -------------------
test_2_gt_3 (__main__.TestAdd.test_2_gt_3) ... FAIL
test_3_gt_2 (__main__.TestAdd.test_3_gt_2) ... ok
test_add_negative (__main__.TestAdd.test_add_negative) ... ok    
test_add_positive_true (__main__.TestAdd.test_add_positive_true) 
... ok
test_add_positive_true_bad (__main__.TestAdd.test_add_positive_true_bad) ... FAIL

======================================================================
FAIL: test_2_gt_3 (__main__.TestAdd.test_2_gt_3)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "e:\My Drive\0_CSCI_127_JBD\Teaching_Modules\Module_Testing\unitTesting_example2.py", line 36, in test_2_gt_3
    self.assertGreater(2,3);
    ^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: 2 not greater than 3

======================================================================
FAIL: test_add_positive_true_bad (__main__.TestAdd.test_add_positive_true_bad)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "e:\My Drive\0_CSCI_127_JBD\Teaching_Modules\Module_Testing\unitTesting_example2.py", line 25, in test_add_positive_true_bad
    self.assertEqual(result, 100)
AssertionError: 5 != 100

----------------------------------------------------------------------
Ran 5 tests in 0.004s

FAILED (failures=2)

'''
```

### Using Assertions

Unittest provides several assertion methods to check different conditions:

| Method                                                       | Checks that            |
| :----------------------------------------------------------- | :--------------------- |
| [`assertEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertEqual) | `a == b`               |
| [`assertNotEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotEqual) | `a != b`               |
| [`assertTrue(x)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertTrue) | `bool(x) is True`      |
| [`assertFalse(x)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertFalse) | `bool(x) is False`     |
| [`assertIs(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIs) | `a is b`               |
| [`assertIsNot(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNot) | `a is not b`           |
| [`assertIsNone(x)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNone) | `x is None`            |
| [`assertIsNotNone(x)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNotNone) | `x is not None`        |
| [`assertIn(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIn) | `a in b`               |
| [`assertNotIn(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotIn) | `a not in b`           |
| [`assertIsInstance(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsInstance) | `isinstance(a, b)`     |
| [`assertNotIsInstance(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotIsInstance) | `not isinstance(a, b)` |
|There are also other methods used to perform more specific checks, such as: ||
| [`assertAlmostEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertAlmostEqual) | `round(a-b, 7) == 0`                                         |
| [`assertNotAlmostEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotAlmostEqual) | `round(a-b, 7) != 0`                                         |
| [`assertGreater(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertGreater) | `a > b`                                                      |
| [`assertGreaterEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertGreaterEqual) | `a >= b`                                                     |
| [`assertLess(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertLess) | `a < b`                                                      |
| [`assertLessEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertLessEqual) | `a <= b`                                                     |
| [`assertRegex(s, r)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertRegex) | `r.search(s)`                                                |
| [`assertNotRegex(s, r)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotRegex) | `not r.search(s)`                                            |
| [`assertCountEqual(a, b)`](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertCountEqual) | *a* and *b* have the same elements in the same number, regardless of their order. |



## Test Fixtures

Unittest provides `setUp()` and `tearDown()` methods to set up and clean up resources before and after each test case:

Python

```
import unittest

class TestDatabase(unittest.TestCase):
    def setUp(self):
        # Connect to database

    def tearDown(self):
        # Close database connection

    def test_query(self):
        # Perform database query

if __name__ == '__main__':
    unittest.main()
```

### Running Tests

To run the tests, you can use the following command in your terminal:

Cmd

```bash
python test_file.py
```

For more detailed output, use the `-v` flag:

Cmd

```bash
python -m unittest -v test_file.py
```

**Remember:**

- Each test case should be independent.
- Test cases should cover different scenarios and edge cases.
- Use clear and descriptive test case names.
- Strive for high test coverage.

