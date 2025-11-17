# Encapsulation vs Non-Encapsulation

This program is a Java demonstration designed to illustrate the core Object-Oriented Programming (OOP) concept of Encapsulation using the contrast between private and public access modifiers. It primarily shows how data hiding and controlled access are used to maintain an object's integrity.

## The Encapsulated Person Class (Good Practice)

The Person class exemplifies proper encapsulation, also known as data hiding.

> Private Data Fields: The class's data (firstName and lastName) are declared as private. This prevents any code outside the class from directly reading or modifying them, effectively protecting the data.
>
> Public Accessors (Getters and Setters): The class provides public methods—getters (like getFirstName()) for safely reading the data, and setters (like setFirstName()) for safely writing the data.
>
> Controlled Integrity: The key benefit is that the setFirstName() method includes validation logic. If an external caller attempts to set a first name that is null or shorter than two characters, the setter detects the invalid input, prints an error message, and prevents the private field from being changed. This ensures the Person object remains in a valid, consistent state.

## The Non-Encapsulated Dog Class (Risky Practice)

The Dog class demonstrates the pitfalls of breaking encapsulation by using public fields.

> Public Data Fields: The class's data (dogName and dogBreed) are declared as public. Any external code can directly access and modify these variables without any mediation.
>
> No Control or Validation: Because external code bypasses any methods to change the data, the Dog class has no opportunity to validate the new values. As demonstrated in the main method, an external caller can directly set the dogName to a potentially disastrous value like null. This makes the object's internal state vulnerable and potentially invalid, and the class cannot prevent it.



## The main Demonstration

The main method creates instances of both classes to showcase the difference:

> It attempts to set an invalid, short first name ("S") on the encapsulated Person object. The setter rejects the change, and the object's name remains the previous valid value ("Jane Doe").
>
> It directly sets an invalid, null name on the non-encapsulated Dog object. The public field is directly overwritten, allowing the object to enter an inconsistent, invalid state ("null Mutt"), demonstrating the lack of control.



## Demo Code

```java
/*
 * Developer: James Goudy
 *
 * This file demonstrates the key Object-Oriented Programming (OOP)
 * concept of ENCAPSULATION using access modifiers (private vs. public).
 */
package classpublicprivateelements;

// The Person class demonstrates ENCAPSULATION (Data Hiding)
class Person {

    // 1. Data Hiding: The fields are private, protecting them from
    // direct external modification. This forces users to go through
    // our controlled public interface.
    private String firstName;
    private String lastName;

    public Person() {
    }
    
    public Person(String firstName, String lastName) {
        // Use setters in the constructor to ensure validation runs!
        setFirstName(firstName);
        setLastName(lastName);
    }

    // Getters: Public methods to safely READ the private data.
    public String getFirstName() {
        return firstName;
    }

    // 2. Controlled Access (Setters): Public methods to safely WRITE 
    // the private data. Setters give you the opportunity to VALIDATE
    // data and maintain the object's integrity. If the input is 
    // invalid, the field is not changed.
    public void setFirstName(String firstName) {
        // ENHANCEMENT: Simple validation logic
        if (firstName != null && firstName.length() >= 2) {
            this.firstName = firstName;
        } else {
            // Note: In real production code, you might throw an
            // IllegalArgumentException.
            System.out.println("Error: First name '" + firstName + 
                               "' is invalid. Value ignored.");
        }
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        
        // The same checks as setFirstName could also be applied here.
        this.lastName = lastName; 
    }
    
    public String allInfo() {
        return (this.firstName + " " + this.lastName);
    }
}

// The Dog class demonstrates the dangers of PUBLIC ACCESS
class Dog {

    // 1. Public Fields: The elements are PUBLIC - they can be accessed 
    // and changed directly by any external code. This breaks 
    // encapsulation.
    public String dogName;
    public String dogBreed;

    // THERE IS NO OPPORTUNITY TO VALIDATE! A user can set these fields
    // to any value (like null or an empty string), potentially making
    // the object's state INVALID without the class having any control.
    
    public Dog() {
    }

    public Dog(String dogName, String dogBreed) {
        // If we wanted validation here, we would have to duplicate the
        // logic in every constructor, instead of just using a Setter.
        this.dogName = dogName;
        this.dogBreed = dogBreed;
    }
    
    public String allInfo() {
        return (this.dogName + " " + this.dogBreed);
    }
}

public class ClassPublicPrivateElements {

    public static void main(String[] args) {
        
        // --- Demonstration of Encapsulation (Person) ---
        Person p1 = new Person();
        
        // Use the public interface (Setters) to change the private fields.
        p1.setFirstName("Jane");
        p1.setLastName("Doe");
        System.out.println("Person 1 (Initial Set): " + p1.allInfo());
        
        // Attempting to set an invalid value - The Setter PROTECTS the data!
        System.out.println("\nAttempting to set an INVALID first name ('S'):");
        p1.setFirstName("S"); 
        
        // The field remains unchanged because of the validation in the setter.
        System.out.println("Person 1 (After Invalid Set): " + p1.allInfo()); 
        
        // --- Demonstration of Public Access (Dog) ---
        
        Dog dog = new Dog();
        
        // Directly setting the public elements - NO validation possible.
        dog.dogName = "Fido";
        dog.dogBreed = "Mutt";
        System.out.println("\nDog (Initial Set): " + dog.allInfo());
        
        // Directly setting an invalid value - The public field is VULNERABLE!
        System.out.println("Directly setting an INVALID name (null):");
        
        // This is legal but potentially disastrous!
        dog.dogName = null; 
        
        // The object's state is now inconsistent, and the Dog class 
        // could not prevent it.
        System.out.println("Dog (After Invalid Set): " + dog.allInfo()); 
    }
}
```

10/2025