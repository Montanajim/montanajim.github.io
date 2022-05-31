# Classes and Objects

## Key Ideas

* Classes
* Objects
* Constructors
* Methods



## Readings

https://books.trinket.io/thinkjava2/chapter11.html

https://www.geeksforgeeks.org/classes-objects-java/



## Concepts

### Class Definition

```{admonition} Definition
**Class** is a blueprint or template that is used to create objects. That template is considered to be a "data type" and can include functions/methods.  
```

### Attributes

```{admonition} Definition
**Attributes** This is the data that describes our class.
```

For example, if we wanted to create a class to make dogs, we might describe a dog by having a breed, a name, and a color. The attributes would be breed, name, and color.

### Constructors 

```{admonition} Definition
**Constructor** A constructor is a function(s) that allows us to set initial values to our attributes. It can be overloaded pending the values we need to set at the time of creating the object. Note that the constructor matches the name of the class and has no return value.
```

```java
class Dog{
    
    // Define the attributes of a dog

    String breed;
    String name;
    String Color;
    
    // NOTE: we can have as many constructors as we need.  
    // If one is not defined,
    // the a "default" constructor is generated behind the scenes.
    // It is always good form to include constructors
    
    // if no constructor is defined, then this one is the default
    public Dog()
    {
    }

    // constructor if we know the breed and name at the time of creation
    // optional
    public Dog(String breed, String name)
    {
        this.breed = breed;
        this.name = name;
    }

    // constructor if we know the breed, name, color at the time of creation
    // optional
    public Dog(String breed, String name, String Color)
    {
        this.breed = breed;
        this.name = name;
        this.Color = Color;
    }   

}
```



## Setters and Getters

```{admonition} Definition
**Setters and Getters** - *Setters* are methods that allow a programmer to set the value of an attribute of an object. Setters allow the programmer to check a value before changing its value.  *Getters* are methods that allow a programmer to retrieve the value of an attribute of an object.
```



```java
class Dog{
    
    // Define the attributes of a dog
   
    // -------- ******** ---------
    // Values can initially be set by the constructor
    // and changed via the Set function 
    
    String breed;
    String name;
    String color;
    
    // NOTE: we can have as many constructors as we need.  
    // If one is not defined,
    // the a "default" constructor is generated behind the scenes.
    // It is always good form to include constructors
    
    // if no constructor is defined, then this one is the default
    public Dog()
    {
    }

    // constructor if we know the breed and name at the time of creation
    // optional
    public Dog(String breed, String name)
    {
        this.breed = breed;
        this.name = name;
    }

    // constructor if we know the breed, name, color at the time of creation
    // optional
    public Dog(String breed, String name, String Color)
    {
        this.breed = breed;
        this.name = name;
        this.color = color;
    }
    // ----------------------------------------------
    
    // Setters and Getters
    
    public String getBreed()
    {
        return breed;
    }

    public void setBreed(String breed)
    {
        this.breed = breed;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String name)
    {
        this.name = name;
    }

    public String getColor()
    {
        return Color;
    }

    public void setColor(String Color)
    {
        this.Color = Color;
    }
    
    // --------------------------------

}
```



## Methods

```{admonition} Defintion
**Method** This is a public function that can be accessed by the object. It allows the object to excecute code pertanent to the object.
```

In our dog example, if we want to make the dog bark we could write a method to do so. 

```java
class Dog{
    
    // Define the attributes of a dog
   
    // -------- ******** ---------
    // Values can initially be set by the constructor
    // and changed via the Set function 
    
    String breed;
    String name;
    String color;
    
    // NOTE: we can have as many constructors as we need.  
    // If one is not defined,
    // the a "default" constructor is generated behind the scenes.
    // It is always good form to include constructors
    
    // if no constructor is defined, then this one is the default
    public Dog()
    {
    }

    // constructor if we know the breed and name at the time of creation
    // optional
    public Dog(String breed, String name)
    {
        this.breed = breed;
        this.name = name;
    }

    // constructor if we know the breed, name, color at the time of creation
    // optional
    public Dog(String breed, String name, String Color)
    {
        this.breed = breed;
        this.name = name;
        this.color = color;
    }
    // ----------------------------------------------
    
    // Setters and Getters
    
    public String getBreed()
    {
        return breed;
    }

    public void setBreed(String breed)
    {
        this.breed = breed;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String name)
    {
        this.name = name;
    }

    public String getColor()
    {
        return Color;
    }

    public void setColor(String Color)
    {
        this.Color = Color;
    }
    
    // -------------Methods-------------------
    public void Bark()
    {
        System.out.println("Woof Woof");
    }

}
```



## Dog Completed Code

```java
/*
 * Programmer: James Goudy
 * Project: Dog Example
 * 
 * Show how we can make multiple dogs using classes
 * Name the project: DogExample
 */

// Create a blueprint of a dog
// The characteristics(attributes) of a dog is:
// Breed, Name, Color
class Dog{
    
    // Define the attributes of a dog
    String breed;
    String name;
    String color;
    
    // Constructor
    // A constructor is a function(s)allows us to set initial values 
    // to our attributes. It can be overloaded pending the values
    // we need to set at the time of creating the object. Note that 
    // the constructor matches the name of the class and has no 
    // return value.

    // NOTE: can have as many constructors as we need.  If one is not defined,
    // the a "default" constructor is generated behind the scenes.
    // It is always good form to include constructors when you write a class.
    
    // if no constructor is defined, then this one is the default
    public Dog()
    {
    }

    // constructor if we know the breed and name at the time of creation
    public Dog(String breed, String name)
    {
        this.breed = breed;
        this.name = name;
    }

    // constructor if we know the breed, name, color at the time of creation
    public Dog(String breed, String name, String color)
    {
        this.breed = breed;
        this.name = name;
        this.color = color;
    }
    
    // Setters and Getters

    public String getBreed()
    {
        return breed;
    }

    public void setBreed(String breed)
    {
        this.breed = breed;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String name)
    {
        this.name = name;
    }

    public String getcolor()
    {
        return color;
    }

    public void setcolor(String color)
    {
        this.color = color;
    }
    
    // --------- methods -------
    
    public void Bark()
    {
        System.out.println("Woof Woof");
    }
    
    public String allInfo()
    {
        String info = "";
        info = this.breed + " " + this.name + " " + this.color;
        return info;
     }

}

public class DogExample {

    public static void main(String[] args) {
        
        // Create a dog
        Dog myDog1 = new Dog();
        
        myDog1.setBreed("Collie");
        myDog1.setName("Fido");
        myDog1.setcolor("Brown");
        
        //Use getters to output information
        System.out.println(myDog1.getBreed() + " " 
                            + myDog1.getName() + " "
                            + myDog1.getcolor());
        
        // use a method to output information
        System.out.println(myDog1.allInfo());
        
        // make the dog bark
        myDog1.Bark();
        
        // creat another dog
        // note this time, the breed, name, and color are known
        // at the time of creation
        
        Dog myDog2 = new Dog("Shepard", "Spot", "White");
        
        //Use getters to output information
        System.out.println(myDog2.getBreed() + " " 
                            + myDog2.getName() + " "
                            + myDog2.getcolor());
        
        // use a method to output information
        System.out.println(myDog2.allInfo());
        
        // make the dog bark
        myDog2.Bark();             
    }
}

```



## In-class Exercise Suggestion

* Make cars



---

End Of Topic