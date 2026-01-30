# Classes  - Inheritance



## Key Ideas

* Inheritance
* *Multiple Classes*



## Readings

https://books.trinket.io/thinkjava2/chapter14.html

https://www.geeksforgeeks.org/inheritance-in-java/

https://www.mygreatlearning.com/blog/polymorphism-in-java/



# Concepts

```{admonition} Definition
**Inheritance**  It is the ability in JAVA where *one* class is allowed to inherit the fields and methods of another class. It allows the programmer to build upon existing classes
```

```{admonition} Definition
 **Encapsulation**  In object-oriented computer programming (OOP) languages, the notion of encapsulation (or OOP Encapsulation) refers to the bundling of data, along with the methods that operate on that data, into a single unit. Many programming languages use encapsulation frequently in the form of classes. By [Sumo Logic](https://www.sumologic.com/glossary/encapsulation/#:~:text=What%20does%20encapsulation%20mean%3A%20In,in%20the%20form%20of%20classes.)
```



```{admonition} Definition
**Polymorphism** is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.
```

[See Reference Reading](PolymorphismInJavaWithExamples)





## Lecture Code

```java

import java.util.ArrayList;
import java.util.Scanner;

/*
 * Programmer: James Goudy
 * Project: PersonWorker Voter Class Lecture
 */



/*
    A class is like a blueprint.  It allows programes to 
    create an "object" based on a class.  It follows the following
    naming schema.

	In main or a class other than itself.

    classname  yourObjectname = new classname();

    example in main or other class other than PersonWorker

            PersonWorker myPerson = new PersonWorker();

    Classes usually start with a Capital Letter.
   
 */
class Person {

    /*
    These are private members - 
    these variables can only be used 
    by the functions within the class.
     */
    private String xFname;
    private String xLname;
    private String xCity;
    private String xState;

    /*
    Constructor 
    This is used by the class in order to create a class.
    The constructor can also used to set defaults default values.
    
    All constructors are public and they match the name of the function.
     */
    public Person() {
        //This is the default construct.            
    }

    //If the name of the of the person is known when we create the class
    //a constructor can be written to set it at the time of creation.   
    public Person(String firstName, String lastName) {
        xFname = firstName;
        xLname = lastName;

    }

    //Note we can have as many constructors as we need, just as long
    //as we change the parameters of the function.
    public Person(String firstName, String lastName, String City, String State) {
        xFname = firstName;
        xLname = lastName;
        xCity = City;
        xState = State;
    }

    /*
        These are getters and setters.  
        Setters allow other programs to set the values of the class object.
        Getters allow other programs to retrieve the values of the class object.
     */
    public String getFirstName() {
        return xFname;
    }

    public void setFirstName(String FirstName) {
        xFname = FirstName;
    }

    public String getLastName() {
        return xLname;
    }

    public void setLastName(String LastName) {
        xLname = LastName;
    }

    public String getCity() {
        return xCity;
    }

    public void setCity(String City) {
        xCity = City;
    }

    public String getState() {
        return xState;
    }

    public void setState(String State) {
        xState = State;
    }

    //--------------------- We can include methods in our functions-----------
    /* Methods  members can be of three types.
        1. public -     can be used anywhere. Visible to all classes.
        2. private -    used only within the class. 
                        Visible only within the class.
        3. protected -  used only within the package.  
                        Visible only within package.
     */
    //Here is a method for concatenating the first and last name;
    public String getFullName() {
        String xFullName;
        xFullName = xFname + " " + xLname;
        return xFullName;
    }

    //Here is a method to calculate the value of income
    public double IncomeCalculateor(double NumberOfYears, double YearlySalary) {
        double ans = 0;
        try {
            ans = NumberOfYears * YearlySalary;
        } catch (Exception e) {
            System.out.println("\n\n****"
                    + "You had a error, please try again"
                    + "\n****\n");
        }
        return ans;
    }

    //Here is a method for printing a mailing label 
    public void MailingAddress()
    {
        System.out.println(xFname + " " + xLname + "\n"
                           + xCity + ", " + xState);
        
    }
       
}

// Example of inheritance
class Worker extends Person {

    //private members
    private String xCompany;
    private String xJobTitle;

    private double xSalary;
    //------------------------------------------------
    
    //constructors
    //default constructor
    public Worker() {

    }

    public Worker(String FirstName, String LastName,
            String Company, String Title) {

        //notice that we use this to call the function
        //of the inherited class PersonWorker
        this.setFirstName(FirstName);
        this.setLastName(LastName);
        
        //set company name and title
        xCompany = Company;
        xJobTitle = Title;
    }

    //------------------------------------------------
    //setters and getters
    public void setCompanyName(String CompanyName) {
        xCompany = CompanyName;
    }
    
    public String getCompanyName() {
        return xCompany;
    }
    
    public void setSalary(double Salary) {
        xSalary = Salary;
    }

    public double getSalary() {
        return xSalary;
    }



}


public class PersonWorker {

    public static void main(String[] args) {
         // TODO code application logic here
        String full1, full2 = "";
        Scanner sc = new Scanner(System.in);
        double ans = 0;

        //Create A person
        Person p1 = new Person();
        //Add values to the person
        p1.setFirstName("Jim");
        p1.setLastName("Smith");
        ans = p1.IncomeCalculateor(5, 1000000.0);
        
        //Create a second person
        Person p2 = new Person();
        p2.setFirstName("Axle");
        p2.setLastName("Rod");

        full1 = p1.getFullName() + " " + ans;
        full2 = p2.getFullName();
        System.out.println(full1 + "\n" + full2);

        
        
        //Storing Objects in  an arraylist       
        ArrayList<Person> myAl = new ArrayList();
        
        /* Notice how <Person> Here we are casting the
            arraylist to only take the datatype Person. This
            can also be done with every other data type. For example- 
            Arraylist<double> myAl = new ArrayList();   //only accept doubles
            Arraylist<String> myAl = new ArrayList();   //only accept Strings
            Arraylist<int> myAl = new ArrayList();      //only accept ints
        */
        
        for (int cnt = 0; cnt < 4; cnt++) {
            Person xx = new Person();           //create a new person
            
            xx.setFirstName("Bob" + cnt);       //concantenate the counter
                                                //to the name so all the 
                                                //Bobs will be unique
                                                
            xx.setLastName("Smith" + cnt);      //concantenate the counter
                                                //to the name so all the 
                                                //Smiths will be unique 
                                                
            myAl.add(xx);                       //Add person xx to arraylist
        }
        
        
        for (int cntrx = 0; cntrx < myAl.size(); cntrx++) {
            
            System.out.println(  myAl.get(cntrx).getFullName());
          
        }
    
    
        Worker w1 = new Worker();
        w1.setFirstName("Bubbba");
        w1.setLastName("Smith");
        w1.setCompanyName("Police Academy");
        w1.setSalary(65000);
        full1 = w1.getFullName() + " " + w1.getSalary();
        System.out.println(full1);
        //</editor-fold>

        //create a worker using a constructor
        Worker w2 = new Worker("Jim", "Rodes", "Mickey's Brews", "Brewer");
        System.out.println("\n\n" + w2.getFullName() + "\n\n");
        


        //Create an array of workers
        Worker[] workers = new Worker[3];

        //Data for one worker in the array
        workers[0] = new Worker();
        workers[0].setFirstName("Billy");
        workers[0].setLastName("TheKid");
        System.out.println("Name = " + workers[0].getFullName());
        
        //Input workers in to the array by 
        //asking the user for information
        //Note this can be done the same way for an arraylist
        for (int cnt = 0; cnt < workers.length; cnt++) {
            workers[cnt] = new Worker();
            System.out.println("Enter First Name");
            workers[cnt].setFirstName(sc.nextLine().toString());

            System.out.println("Enter Last Name");
            workers[cnt].setLastName(sc.nextLine());

            System.out.println("Enter Company Name");
            workers[cnt].setCompanyName(sc.nextLine());

            try {
                System.out.println("Enter Salary");
                workers[cnt].setSalary(sc.nextDouble());
                sc.nextLine();
            } catch (Exception e) {
                System.out.println("Error with salary - data not entered");
                sc.nextLine();
            }

        }

        //Print out the contents of the array
        for (int cnt = 0; cnt < workers.length; cnt++) {
            full1 = workers[cnt].getFullName() + " "
                    + workers[cnt].getSalary() + " "
                    + workers[cnt].getCompanyName();

            System.out.println(full1 + "\n");
        }

    }
    
}

```



---

End Of Topic



