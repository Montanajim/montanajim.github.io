# Serialization - Pickle - Data



```{Danger}
ONLY UNPICKLE FILES FROM A TRUSTED SOURCE. MALICOUS CODE CAN BE EXECUTED IN THE RECONSTRUCTION PROCESS
```



## Pickle Data  Demo Code

```python
import pickle

# Define a class to represent a person with name, city, state
class Person:
  def __init__(self, name, city, state):
    self.name   = name
    self.city   = city
    self.state  = state

# Function to serialize a list of people to JSON
def serialize_to_pickle(people,filename):
  with open(filename, "wb") as f:
    pickle.dump(people, f)

# Function to deserialize JSON data back to a list of people
def deserialize_from_pickle(filename):
  people = []
  try:
    # open the file as read binary
    with open(filename, "rb") as f:
      people = pickle.load(f)
  except FileNotFoundError:
    print(f"Error: '{filename}' file not found.")
  return people

def main():
  # Example usage
  people = [ Person("Alice",    "Albany",   "AL"), 
            Person("Bob",      "Boston", "MT"),
            Person("Charlie",  "Chico",  "IL"),
            Person("Gwen",     "Gaines",  "GA"),
            Person("James",    "Jordon",   "MT")]


  myfilename = "people.pickle"
  serialize_to_pickle(people, myfilename)

  deserialized_people = deserialize_from_pickle("people.pickle")

  # Print the deserialized data
  for person in deserialized_people:
    print(f"Name: {person.name}, " +   
          f"\t{person.city}, " + 
          f"\t\t{person.state}")

main()

```

