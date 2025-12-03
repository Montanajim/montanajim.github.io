# Serialization - JSON



**JSON serialization** is the process of converting complex data structures, like objects or arrays, into a simple text format called JSON (JavaScript Object Notation). This text-based representation is easy to store, transmit, and parse.

## Why Use JSON Serialization?

- **Data Exchange:** It's widely used for data interchange between different systems and applications.
- **Data Storage:** JSON files can be used to store data persistently.
- **Data Transmission:** It's efficient for sending data over networks.
- **Readability:** JSON is human-readable, making it easy to inspect and debug.

## How Does It Work?

1. **Data Structure:** You have a complex data structure, like an object with properties and values.
1. **Serialization:** A serializer converts this data structure into a JSON string. This string adheres to specific JSON syntax rules.
1. **Transmission or Storage:** The JSON string can be sent over a network or stored in a file.
1. **Deserialization:** When you need to use the data again, a deserializer converts the JSON string back into its original data structure.

### Key Points

- JSON is a lightweight data-interchange format.
- Serialization converts data to JSON, deserialization converts JSON back to data.
- Widely used in web applications, APIs, and data storage.



## Lecture Code

```python
import json

# Define a class to represent a person with name, city, state
class Person:
  def __init__(self, name, city, state):
    self.name   = name
    self.city   = city
    self.state  = state

# Function to serialize a list of people to JSON
def serialize_to_json(people):
  data = []
  for person in people:
    data.append({"name": person.name, "city": person.city,"state":person.state})
  with open("people.json", "w") as f:
    json.dump(data, f)

# Function to deserialize JSON data back to a list of people
def deserialize_from_json():
  people = []
  try:
    with open("people.json", "r") as f:
      data = json.load(f)
    for item in data:
      people.append(Person(item["name"], item["city"],item["state"]))
  except FileNotFoundError:
    print("Error: 'people.json' file not found.")
  return people

def main():
  # Example usage
  people = [ Person("Alice",    "Albany",   "AL"), 
            Person("Bob",      "Boston", "MT"),
            Person("Charlie",  "Chico",  "IL"),
            Person("Gwen",     "Gaines",  "GA"),
            Person("James",    "Jordon",   "MT")]


  serialize_to_json(people)

  deserialized_people = deserialize_from_json()

  # Print the deserialized data
  for person in deserialized_people:
    print(f"Name: {person.name}, " +   
          f"\t{person.city}, " + 
          f"\t\t{person.state}")

main()

'''
JSON FILE
people.json
(Note the output below has been prettified for readablity)

[
{"name": "Alice", "city": "Albany", "state": "AL"}, 
{"name": "Bob", "city": "Boston", "state": "MT"}, 
{"name": "Charlie", "city": "Chico", "state": "IL"}, 
{"name": "Gwen", "city": "Gaines", "state": "GA"}, 
{"name": "James", "city": "Jordon", "state": "MT"}
]

-----------
Output
Name: Alice,    Albany,         AL
Name: Bob,      Boston,         MT
Name: Charlie,  Chico,          IL
Name: Gwen,     Gaines,         GA
Name: James,    Jordon,         MT

'''
```



##  Code Summary

**Person Class:**

- Defines a `Person` class with attributes `name`, `city`, and `state`.

**`serialize_to_json` Function:**

- Takes a list of `Person` objects as input.
- Iterates through the list, creating dictionaries for each person with their attributes as key-value pairs.
- Creates a list `data` containing these dictionaries.
- Opens a file named "people.json" in write mode (`"w"`).
- Uses `json.dump` to convert the `data` list to a JSON string and write it to the file.

**`deserialize_from_json` Function:**

- Initializes an empty list `people` to store deserialized `Person` objects.
- Tries to open "people.json" in read mode (`"r"`).
- If successful, uses `json.load` to read the JSON data from the file and store it as a list in `data`.
- Iterates through the `data` list (containing dictionaries).
- For each dictionary, creates a new `Person` object using the values for "name", "city", and "state".
- Appends the created `Person` object to the `people` list.
- If the file is not found, it catches a `FileNotFoundError` and prints an error message.
- Finally, returns the list of deserialized `Person` objects.

**`main` Function:**

- Creates a sample list of `Person` objects with names, cities, and states.
- Calls `serialize_to_json` to convert this list to JSON and store it in "people.json".
- Calls `deserialize_from_json` to read the data back from "people.json" and get a list of deserialized `Person` objects.
- Prints the information of each deserialized person (name, city, state) in a formatted way.
