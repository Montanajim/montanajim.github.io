# Serialization - Pickle - Function


> [!WARNING]
>
> ONLY UNPICKLE FILES FROM A TRUSTED SOURCE. MALICOUS CODE CAN BE EXECUTED IN THE RECONSTRUCTION PROCESS



> [!CAUTION]
>
> Pickling functions is done by reference and not the code itself. If other modules are involved, problems could arise. Also since it doesn't actually read the code, the **marshal** library must be used. Marshal.load will actually read the function code.



## Pickle Function Demo Code

```python
"""
Programmer: James Goudy

***
Pickling functions are NOT reccomended,
espcially if they require other modules.

Pickling functions does it by reference
and not the code itself.

To get around that, using the marshal
library (loads) will read the actual code.
***
"""

import pickle
import marshal
import types

def add(num1, num2):
  """
  Adds two numbers 
  and returns the sum.
  """
  return num1 + num2

def pickle_add_func():
  
  # reads the actual add function code
  # and turns it into bytecode
  mybytecode = marshal.dumps(add.__code__)

  # write the bytecode to a binary file
  with open("add.pickle","wb") as outfile:
    pickle.dump(mybytecode,outfile)
  outfile.close()

  print("\nFunction Pickled")

def de_pickle_add_func():
  
  # read the file contents
  with open('add.pickle','rb') as infile:
    mypickledata = infile.read()
  infile.close()

  # unpickle contents to bytecode / binary
  mybytecode = pickle.loads(mypickledata)

  # get the code marshel bytecode object
  mycode = marshal.loads(mybytecode)

  # create the new function
  newAdd = types.FunctionType(mycode,globals())

  print("Function \'Depickled\'")
  ans = newAdd(10,30)

  print(ans)


def main():

  pickle_add_func()
  

  de_pickle_add_func()

  print("bye")

main()



```

