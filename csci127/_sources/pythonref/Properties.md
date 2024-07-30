# Properties



**A Python property is a special construct that allows you to control access to an object attribute through methods, while still using dot notation as if it were a regular attribute.** This means you can perform additional logic, validation, or computations when getting or setting the attribute's value.



**Key points:**

- **Methods disguised as attributes:** Properties are essentially methods that act like attributes, making code more readable and intuitive.
- **Encapsulation:** They promote encapsulation by hiding the implementation details of how an attribute is accessed or modified.
- **Validation and control:** You can add validation or constraints to ensure data integrity, as well as perform side effects when the attribute is accessed or changed.
- **Readability:** They make code cleaner and more maintainable by avoiding explicit getter and setter methods.

(AIJG)



## Lecture Code



```py
class Person:
   """Represents a person with a first and last name."""

   def __init__(self, first_name: str, last_name: str) -> None:
       """Initializes a Person object with the given first and last name."""
       self._first_name = first_name
       self._last_name = last_name

   @property
   def full_name(self) -> str:
       """Returns the full name of the person."""
       return f"{self._first_name} {self._last_name}"

   @property
   def email(self) -> str:
       """Returns the email address of the person."""
       # Replace with actual logic
       return f"{self._first_name}.{self._last_name}@example.com"
   

   # ------------------- Another Class -------------------------------------------
# lazy loading

class Book:
    def __init__(self, title="", author=""):
        self.atitle = title
        self.aauthor = author
    
    # REMEMBER THAT PROPERTY NAMES NEED TO BE UNIQUE
    @property
    def bookTitle(self):
        return self.atitle
    @bookTitle.setter
    def bookTitle(self,title):
        self.atitle = title

    @property
    def bookAuthor(self):
        return self.aauthor
    @bookAuthor.setter
    def bookAuthor(self,author):
        self.aauthor = author
    
# -----------------------------------------------------------------------------

def main():

    print("\nPeson Property Example")

    # create an new person object
    p1 = Person("Bubba","Doe")

    print("Name: {} /nEmail: {}\n\n".format(p1.full_name,p1.email))

    print("\nBook Property Example")

    # create new book object
    b1 = Book("Code Gurus Unleashed")
    b1.bookAuthor = "Jimbo"
    
    print("Title: {}".format(b1.bookTitle))
    print("Author: {}".format(b1.bookAuthor))

    print("\nbye\n")

main()

# Output
"""
Peson Property Example
Name: Bubba Doe /nEmail: Bubba.Doe@example.com

Book Property Example
Title: Code Gurus Unleashed
Author: Jimbo

bye
"""
```

