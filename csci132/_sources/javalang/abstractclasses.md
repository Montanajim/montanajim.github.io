# Abstract Classes



## Key Ideas

* Abstract Classes

## Readings

[Abstract Classes by JournalDev](https://www.journaldev.com/1582/abstract-class-in-java#:~:text=Java%20Abstract%20class%20can%20implement,or%20to%20provide%20default%20implementation.)

[Using an Interface vs. Abstract Class in Java by Baeldung](https://www.baeldung.com/java-interface-vs-abstract-class)





```{admonition} Definition
Abstract Class - this is a class that is designated by the *abstract* keyword.  This is a class that can only be used when it is inherited. The abstract class is mostly used to provide a base for subclasses.
```



## Lecture Code

```java
/*
 * Project: Abstract Classes Lecture Code
 * Programmer: James Goudy
 *
 */

// abstract class cannot be instantiated
// it must be inherited
abstract class Person {

    // Note that the properties are public
    // meaning they do not need a setter or getter and
    // can be accessed directly. 
    public String firstName;
    public String lastName;

    // constructor
    public Person(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

}

class Worker extends Person {

    // Note that the properties are public
    // meaning they do not need a setter or getter and
    // can be accessed directly. 
    public String jobTitle;
    public String company;

    // constructor
    public Worker(String jobTitle, String company,
            String firstName, String lastName) {
        super(firstName, lastName);
        this.jobTitle = jobTitle;
        this.company = company;
    }

    // super is telling the class to include the constructor 
    // parent class - thus we can initalize firstName and lastName
    // in the constructor of the child class.
    
    public String allInfo()
    {
        return(firstName +" " + lastName +" " + jobTitle +" " +company);
    }
}

public class J1_Abstract_Classes {

    public static void main(String[] args) {

        System.out.println("\n\"Person myPerson = "
                + "new Person(\"John\",\"Doe\");\"");
        System.out.println("Will not compile since it is an "
                + "abstract class\n");

        // Person myPerson = new Person("John","Doe");
        // This will not compile since it is an abstract class
        
        // Worker will compile since it inherits Person
        Worker myWorker = new Worker("Programmer","XYZ Company","Joe", "Doe");
        System.out.println(myWorker.allInfo());
        
        System.out.println("\n\nbye\n");
    }
}

```



---

End Of Topic

