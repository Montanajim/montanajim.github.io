# Software Testing - Pytest



***Pytest*** is a powerful and flexible Python testing framework that simplifies the process of writing and running tests. It offers a clean syntax, rich features, and extensive plugin support, making it a popular choice for testing Python applications.  



```Admonition NOTE
Pytest needs to be installed. 
```



```bash
pip install pytest
```





## Basic Example

Let's start with a simple example:

Python

```
import pytest

def add(x, y):
    return x + y

def test_add():
    assert add(2, 3) == 5
```

- ***\*Test File Naming:\**** Pytest automatically discovers test files and functions. Test files typically start with `test_` or end with `_test.py`.  
- **Test Function Naming:** Test functions usually start with `test_`.
- **Assertion:** The `assert` statement checks if the actual result matches the expected result.



```python
"""
# Below assumes a windows machine
# MUST CALL FROM THE COMMAND LINE:

pytest pytesting_example1.py/ -v

# Writes to a text file
pytest pytesting_example1.py/ -v > outputfilename.txt

# Display text file
type outputfilename.txt


"""
import pytest


def add(x, y):
    return x + y

def test_1():

    result= add(2,3)
    assert result == 5

    result= add(1,4)
    assert result == 5

    result= add(8,-3)
    assert result == 5

def test_2():
    result= add(2,3)
    assert result == 5

    result= add(1,4)
    assert result == 5

    # I'm asserting the answer is 5
    # when the reality is 41
    # as written will cause a pytest error
    result= add(1,40)
    assert result == 5

    result= add(8,-3)
    assert result == 5

def test_3():
    result= add(2,3)
    assert result == 5

    result= add(1,4)
    assert result == 5

if __name__ == '__main__':

    test_1()
    test_2()
    test_3()
    print('\n\nbye\n')


"""
OUTPUT
============================= test session starts =============================
platform win32 -- Python 3.12.4, pytest-8.3.2, pluggy-1.5.0 -- C:\Program Files\Python312\python.exe
cachedir: .pytest_cache
rootdir: E:\My Drive\0_CSCI_127_JBD\Teaching_Modules\Module_Testing
collecting ... collected 3 items

pytesting_example1.py::test_1 PASSED                                     [ 33%]
pytesting_example1.py::test_2 FAILED                                     [ 66%]
pytesting_example1.py::test_3 PASSED                                     [100%]

================================== FAILURES ===================================
___________________________________ test_2 ____________________________________

    def test_2():
        result= add(2,3)
        assert result == 5

        result= add(1,4)
        assert result == 5

        result= add(1,40)
>       assert result == 5
E       assert 41 == 5

pytesting_example1.py:47: AssertionError
============================== warnings summary ===============================
pytesting_example1.py:73
  E:\My Drive\0_CSCI_127_JBD\Teaching_Modules\Module_Testing\pytesting_example1.py:73: SyntaxWarning: invalid escape sequence '\M'
    """

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
=========================== short test summary info ===========================
FAILED pytesting_example1.py::test_2 - assert 41 == 5
=================== 1 failed, 2 passed, 1 warning in 0.11s ====================
"""
```







## Parametrized Tests

To test a function with different inputs, use `pytest.mark.parametrize`:

Python

```
import pytest

def add(x, y):
    return x + y

@pytest.mark.parametrize("x, y, expected", [
    (2, 3, 5),
    (-1, 1, 0),
    (0, 0, 0)
])
def test_add(x, y, expected):
    assert add(x, y) == expected
```

## Fixtures

Fixtures are functions that provide setup and teardown for tests. They help manage shared resources:  

Python

```
import pytest

@pytest.fixture
def my_fixture():
    # Setup code
    return some_value

def test_something(my_fixture):
    # Use the fixture
    assert my_fixture == expected_value
```

## Test Classes

You can organize tests into classes using `pytest.mark.usefixtures`:

Python

```
import pytest

class TestClass:
    @pytest.fixture(autouse=True)
    def setup(self):
        print("Setting up")

    def test_one(self):
        assert True

    def test_two(self):
        assert False
```

## Additional Features

- **Skipping Tests:** `pytest.skip` or `pytest.xfail` to skip tests conditionally.
- **Grouping Tests:** Use `pytest.mark` for custom markers to group tests.
- **Capturing Output:** Use `capsys` fixture to capture stdout and stderr.
- ***\*Monkeypatching:\**** Modify modules or functions for testing purposes.  
- ***\*Plugins:\**** Extend pytest functionality with plugins.  

**Running Tests:**

You can run tests from the command line:

Cmd

```bash
pytest
```

Or specify a test file or directory:

Cmd

```bash
pytest test_module.py
```

**Key Points:**

- Pytest is easy to learn and use.  
- It offers a rich feature set for various testing scenarios.  
- It integrates well with other Python tools and libraries.  

By understanding these basics and exploring the extensive documentation, you can effectively use Pytest to write comprehensive and maintainable tests for your Python projects.

**Would you like to explore a specific feature or use case in more detail?**