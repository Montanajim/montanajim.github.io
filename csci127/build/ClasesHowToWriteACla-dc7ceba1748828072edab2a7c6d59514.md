# How to Write a Class in Python



## What is a class?

A **class** in Python is a blueprint for creating objects (a specific instance of a class). Classes allow us to encapsulate data (attributes) and functions (methods) that operate on that data. They help organize code in a structured way, making it reusable and easier to maintain.

When we say that *classes allow us to encapsulate data and functions that operate on that data*, we mean that a class groups together related pieces of information (called *attributes*) and the actions (called *methods*) that can be performed on that information. Encapsulation is a core concept in object-oriented programming (OOP) that helps in organizing and structuring code in a way that makes it more modular and manageable.

Let’s break down these ideas:

1. **Attributes (Data)**: 
   Attributes represent the properties or characteristics of an object created from a class. In our `Car` example, attributes like `make`, `model`, `year`, and `color` represent data about a specific car. These attributes are encapsulated within the class, meaning they are directly associated with the class and any objects made from it. For instance, if you create a `Car` object, you can think of `make`, `model`, etc., as data that specifically belongs to that object.

2. **Methods (Functions)**: 
   Methods are functions defined inside a class that operate on its attributes or perform actions related to the class. For instance, methods like `start` and `stop` are actions that a `Car` object can perform. These methods may use or change the class's attributes, creating a relationship between the data and the actions associated with that data.

3. **Encapsulation**:
   Encapsulation is the idea that all related attributes and methods are "wrapped up" within the class, forming a distinct, self-contained unit. This provides several benefits:
   - **Organization**: All relevant data and functions for a specific concept (e.g., a car) are organized within a single class.
   - **Data Protection**: By keeping data within a class, we can control how it’s accessed and modified. For instance, using *getter* and *setter* methods lets us add validation or restrictions.
   - **Reusability and Modularity**: Once a class is defined, it can be used as a standalone component. If we want to create multiple `Car` objects, each object will have its own data and can operate independently of others.

In short, encapsulation helps to bundle related information and functions together in a way that protects the data and keeps code organized, readable, and reusable.



We will create a class called `Car` that represents a car with attributes such as `make`, `model`, `year`, and `color`. We will also add methods to work with these attributes. Finally, we will test our class using the `if __name__ == "__main__"` method.

---

## 1. Declare the Class

To create a class, use the `class` keyword followed by the name of the class.

```python
class Car:
    """A class to represent a car."""
```



## 2. Declare the Attribute Variables

Attributes are the characteristics of the class. Here, `make`, `model`, `year`, and `color` are attributes that define each car.

```python
class Car:
    """A class to represent a car."""

    def __init__(self, make, model, year, color):
        self._make = make
        self._model = model
        self._year = year
        self._color = color
```



## 3. Create the Constructor

A **constructor** in Python is a special method called `__init__`. It is automatically called when a new object of the class is created. The purpose of the constructor is to initialize the object's attributes.

```python
def __init__(self, make, model, year, color):
    """Initialize the car's attributes."""
    self._make = make
    self._model = model
    self._year = year
    self._color = color
```



## 4. Create `__str__`

The `__str__` method is a special method that returns a string representation of the object. This is useful when you want a readable output for instances of the class.

```python
def __str__(self):
    """Return a string representation of the car."""
    return f"{self._year} {self._make} {self._model} in {self._color} color"
```



## 5. Create `__repr__`

The `__repr__` method is used for a developer-oriented string representation of an object. While similar to `__str__`, `__repr__` is generally intended for debugging.

```python
def __repr__(self):
    """Return a detailed string representation for debugging."""
    return f"Car(make={self._make}, model={self._model}, year={self._year}, color={self._color})"
```



## 6. Create Properties

Properties provide controlled access to attributes by defining getter and setter methods. This is useful for validating or processing data before assigning it to an attribute.

```python
@property
def make(self):
    """Get the make of the car."""
    return self._make

@make.setter
def make(self, value):
    """Set the make of the car."""
    self._make = value

@property
def model(self):
    """Get the model of the car."""
    return self._model

@model.setter
def model(self, value):
    """Set the model of the car."""
    self._model = value
```



## 7. Create Methods

Methods define actions or behaviors for objects of the class. Here, we define two methods: `start` and `stop`.

```python
def start(self):
    """Start the car."""
    return f"{self._make} {self._model} has started."

def stop(self):
    """Stop the car."""
    return f"{self._make} {self._model} has stopped."
```





## Full Code with Testing

Here's the full code, including the class definition, properties, methods, and a test block.

```python
class Car:
    """A class to represent a car."""

    # ------------ CONSTRUCTOR ------------
    def __init__(self, make, model, year, color):
        """Initialize the car's attributes."""
        self._make = make
        self._model = model
        self._year = year
        self._color = color

    # ------------ DEBUGGING TOOLS ------------
    def __str__(self):
        """Return a string representation of the car."""
        return f"{self._year} {self._make} {self._model} in {self._color} color"

    def __repr__(self):
        """Return a detailed string representation for debugging."""
        return f"Car(make={self._make}, model={self._model}, year={self._year}, color={self._color})"

    # # ------------ PROPERTIES  ------------
    @property
    def make(self):
        """Get the make of the car."""
        return self._make

    @make.setter
    def make(self, value):
        """Set the make of the car."""
        self._make = value

    @property
    def model(self):
        """Get the model of the car."""
        return self._model

    @model.setter
    def model(self, value):
        """Set the model of the car."""
        self._model = value

    # ------------ METHODS ------------
    def start(self):
        """Start the car."""
        return f"{self._make} {self._model} has started."

    def stop(self):
        """Stop the car."""
        return f"{self._make} {self._model} has stopped."


# Testing the Car class
if __name__ == "__main__":
    my_car = Car("Toyota", "Camry", 2022, "blue")
    print(my_car)                                       # Output the car's information
    print(f"My car is a {my_car.make} {my_car.model}")  # Using the car's properties
    print(my_car.start())                               # Start the car
    print(my_car.stop())                                # Stop the car
    my_car.make = "Honda"                               # Changing the car's make
    print(my_car)                                       # Output the car's information after change
    
    
'''
OUTPUT
2022 Toyota Camry in blue color
Toyota Camry has started.
Toyota Camry has stopped.
2022 Honda Camry in blue color
'''
```



## Summary

In this guide, we explored how to write a class in Python. We learned:

1. **Class Declaration**: Using the `class` keyword to create a new class.
2. **Constructor**: Initializing an object's attributes with `__init__`.
3. **Special Methods**: Using `__str__` for readable string representation and `__repr__` for debugging output.
4. **Properties**: Using getter and setter methods to manage access to private attributes.
5. **Methods**: Defining actions for the class, like `start` and `stop`.
6. **Testing the Class**: Verifying functionality using `if __name__ == "__main__"`.

This framework enables us to build and interact with custom objects in a structured way.