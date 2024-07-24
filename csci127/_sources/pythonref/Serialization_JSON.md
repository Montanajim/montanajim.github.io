# Serialization - JSON



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

