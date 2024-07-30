# Serialization - YAML



**YAML** stands for **YAML Ain't Markup Language** (originally Yet Another Markup Language). It's a data serialization language designed to be human-readable and easy to understand. Think of it as a way to store structured information in a text file, similar to JSON or XML, but with a more intuitive syntax.  



### How is it used?

YAML files are commonly used for:

- Configuration files:

   YAML's readability makes it ideal for storing application settings, database connections, and other configuration parameters.

- Data serialization:

   You can use YAML to store complex data structures like lists, dictionaries, and objects in a portable format.

- Document formats:

   YAML can be used to represent structured documents, such as those used in content management systems or data exchange formats.

  

**Key advantages of YAML:**

- Readability:

   YAML's syntax is designed to be human-friendly, making it easy to write, read, and modify.

- Flexibility:

  It supports various data types, including scalars, sequences, mappings, and more complex structures.

- Simplicity:

   YAML's syntax is relatively straightforward compared to other serialization formats.

    

## Python Example: Writing and Reading a YAML File

**Prerequisites:**

- Python installed
- `pyyaml` library installed (`pip install pyyaml`)

Python

```python
'''
Programmer: James Goudy
Project: yaml demo

'''

import yaml

def write_yaml_file(data, filename):
  """Writes data to a YAML file.

  Args:
    data: The data to be written.
    filename: The name of the YAML file.
  """

  with open(filename, 'w') as yaml_file:
    yaml_file.write('# Demographics')
    yaml.dump(data, yaml_file, default_flow_style=False)
    yaml_file.close()

  # NOTE: if more items are created in stages
  # calling the file the next time to add items,
  # use the 'a' attribute. 'w' first time, 'a' next time on

def read_yaml_file(filename):
  """Reads data from a YAML file.

  Args:
    filename: The name of the YAML file.

  Returns:
    The data loaded from the YAML file.
  """
  with open(filename, 'r') as yaml_file:
    data = yaml.safe_load(yaml_file)
    yaml_file.close()
  return data



def main():
  # creating embedded dictionaries
  uk_c = {'UK':['London','Bath','York']}
  fr_c = {'FR':['Paris','Lyon','Nice','Metz']}
  travel_c = {'travel' : [uk_c,fr_c,'GR']}

  data = {
    'name': 'Jimbo',
    'age': 30,
    'city': 'New York',
    'hobbies': ['reading', 'coding', travel_c,'cooking']
  }

  # Write data to a YAML file
  yaml_file = 'data.yaml'
  write_yaml_file(data, yaml_file)

  # Read data from the YAML file
  loaded_data = read_yaml_file(yaml_file)

  print('\nAll Data\nNote the embedded dictionaries')
  print(loaded_data)

#   show the progression on how
#   to access a specific city
  print('\nAll hobbies')
  td = loaded_data['hobbies']
  print(td)

  print('\nAll Travel Data')
  td = loaded_data['hobbies'][2]
  print(td)

  print('\nAll Travel Countries')
  td = loaded_data['hobbies'][2]['travel']
  print(td)

  print('\nAll French Items (dictionary)')
  td = loaded_data['hobbies'][2]['travel'][1]
  print(td)

  print('\nAll French Cities')
  td = loaded_data['hobbies'][2]['travel'][1]['FR']
  print(td)

  print('\nFrench City of Lyon')
  td = loaded_data['hobbies'][2]['travel'][1]['FR'][1]
  print(td)

  print('\n yaml bye\n')

main()

'''
Output file

# Demographicsage: 30
city: New York
hobbies:
- reading
- coding
- travel:
  - UK:
    - London
    - Bath
    - York
  - FR:
    - Paris
    - Lyon
    - Nice
    - Metz
  - GR
- cooking
name: Jimbo
'''

```



## Explanation:

This Python program demonstrates how to use the `yaml` library to read and write data to a YAML file.

**Key functionalities:**

- Defines two functions:
  - `write_yaml_file`: Writes data to a YAML file in a human-readable format.
  - `read_yaml_file`: Reads data from a YAML file and returns it as a Python object.
- **Creates a sample data structure:** A Python dictionary containing various data types, including nested dictionaries.
- **Writes the data to a YAML file:** Uses the `write_yaml_file` function to create a YAML file named 'data.yaml'.
- **Reads the data from the YAML file:** Uses the `read_yaml_file` function to load the YAML data into a Python object.
- **Demonstrates data access:** Shows how to access different parts of the loaded data, including nested dictionaries, to illustrate how to work with YAML data in Python.

