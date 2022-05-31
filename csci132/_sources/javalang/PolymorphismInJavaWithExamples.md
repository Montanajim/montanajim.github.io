# Polymorphism in Java (With Examples)

By  [Great Learning Team](https://www.mygreatlearning.com/blog/author/greatlearning/)

https://www.mygreatlearning.com/blog/polymorphism-in-java/



 

Polymorphism is the ability of an object to take on different forms. In Java, polymorphism refers to the ability of a class to provide different implementations of a method, depending on the type of object that is passed to the method.

To put it simply, polymorphism in Java allows us to perform the same action in many different ways. Any [Java](https://www.mygreatlearning.com/blog/web-stories/how-can-a-beginner-start-with-java-programming/) object that can pass more than one IS-A test is polymorphic in Java. Therefore, all the Java objects are polymorphic as it has passed the IS-A test for their own type and for the class Object.

This article also talks about two types of polymorphism in Java: compile time polymorphism and runtime polymorphism, Java polymorphism examples, [method overloading](https://www.mygreatlearning.com/blog/method-overloading-in-java/), method overriding, why to use polymorphism in java,[ java programming](https://www.mygreatlearning.com/academy/learn-for-free/courses/java-programming?gl_blog_id=26164), and many more.

Polymorphism is a feature of the object-oriented programming language, Java, which implies that you can perform a single task in different ways. In the technical world, polymorphism in Java allows one to do multiple implementations by defining one interface. 

1. **[What is Polymorphism?](https://www.mygreatlearning.com/blog/polymorphism-in-java/#what-is-polymorphism)**
2. **[What is Polymorphism in Java?](https://www.mygreatlearning.com/blog/polymorphism-in-java/#what-is-polymorphism-in-Java)**
3. **[Real-Life Examples of Polymorphism](https://www.mygreatlearning.com/blog/polymorphism-in-java/#real-life-examples-of-polymorphism)**
4. **[Types of Polymorphism](https://www.mygreatlearning.com/blog/polymorphism-in-java/#types-of-polymorphism)**
5. **[Method Overloading in Java](https://www.mygreatlearning.com/blog/polymorphism-in-java/#method-overloading-in-java)**
6. **[Method Overriding in Java](https://www.mygreatlearning.com/blog/polymorphism-in-java/#method-overriding-in-java)**
7. **[Runtime Polymorphism in Java](https://www.mygreatlearning.com/blog/polymorphism-in-java/#runtime-polymorphism-in-java)**
8. **[Compile-Time Polymorphism in Java](https://www.mygreatlearning.com/blog/polymorphism-in-java/#compile-time-polymorphism-in-java)**
9. **[Polymorphism in programming](https://www.mygreatlearning.com/blog/polymorphism-in-java/#Polymorphism-in-programming)**
10. **[Polymorphism variables](https://www.mygreatlearning.com/blog/polymorphism-in-java/#what-is-polymorphism-variables)**
11. **[Why use Polymorphism in Java?](https://www.mygreatlearning.com/blog/polymorphism-in-java/#why-use-polymorphism-in-java)**
12. **[Characteristics of Polymorphism](https://www.mygreatlearning.com/blog/polymorphism-in-java/#characteristics-of-polymorphism)**
13. [**Problems with Polymorphism**](https://www.mygreatlearning.com/blog/polymorphism-in-java/#problems-with-polymorphism)
14. [**Conclusion**](https://www.mygreatlearning.com/blog/polymorphism-in-java/#conclusion)

## **What is Polymorphism?**

The derivation of the word Polymorphism is from two different Greek words- poly and morphs. “Poly” means numerous, and “Morphs” means forms. So, polymorphism means innumerable forms. Polymorphism, therefore, is one of the most significant features of Object-Oriented Programming.

## **What is Polymorphism in Java?**

**Polymorphism in Java** is the task that performs a single action in different ways.

So, languages that do not support polymorphism are not ‘Object-Oriented Languages’, but, ‘Object-Based Languages’. Ada, for instance, is one such language. Since Java supports polymorphism, it is an [Object-Oriented Language](https://www.mygreatlearning.com/academy/learn-for-free/courses/oops-in-java/?gl_blog_26164).

Polymorphism occurs when there is inheritance, i.e. there are many classes that are related to each other.

[Inheritance](https://www.mygreatlearning.com/academy/learn-for-free/courses/inheritance-in-java/?gl_blog_26164) is a powerful feature in Java.[ Java Inheritance](https://www.mygreatlearning.com/blog/inheritance-in-java/) lets one class acquire the properties and attributes of another class. Polymorphism in Java allows us to use these inherited properties to perform different tasks. Thus, allowing us to achieve the same action in many different ways.

## **Real-Life Examples of Polymorphism**

An individual can have different relationships with different people. A woman can be a mother, a daughter, a sister, a friend, all at the same time, i.e. she performs other behaviours in different situations.

The human body has different organs. Every organ has a different function to perform; the heart is responsible for blood flow, lungs for breathing, brain for cognitive activity, and kidneys for excretion. So we have a standard method function that performs differently depending upon the organ of the body. 

#### **Polymorphism in Java Example**

A superclass named “Shapes” has a method “area()”. Subclasses of “Shapes” can be “Triangle”, “circle”, “Rectangle”, etc. Each subclass has its way of calculating area. Using Inheritance and Polymorphism means, the subclasses can use the “area()” method to find the area’s formula for that shape.

```java
class Shapes {
  public void area() {
    System.out.println("The formula for area of ");
  }
}
class Triangle extends Shapes {
  public void area() {
    System.out.println("Triangle is ½ * base * height ");
  }
}
class Circle extends Shapes {
  public void area() {
    System.out.println("Circle is 3.14 * radius * radius ");
  }
}
class Main {
  public static void main(String[] args) {
    Shapes myShape = new Shapes();  // Create a Shapes object
    Shapes myTriangle = new Triangle();  // Create a Triangle object
    Shapes myCircle = new Circle();  // Create a Circle object
    myShape.area();
    myTriangle.area();
    myShape.area();
    myCircle.area();
  }
}
```

**Output:**

The formula for the area of Triangle is ½ * base * height
The formula for the area of the Circle is 3.14 * radius * radius

**Also Read: [OOPs concepts in Java](https://www.mygreatlearning.com/blog/oops-concepts-in-java/?highlight=polymorphism )**

## **Types of Polymorphism**

You can perform Polymorphism in Java via two different methods:

1. Method Overloading
2. Method Overriding

### **What is Method Overloading in Java?**

**Method overloading** is the process that can create multiple methods of the same name in the same class, and all the methods work in different ways. Method overloading occurs when there is more than one method of the same name in the class.

#### **Example of Method Overloading in Java**

```java
class Shapes {
  public void area() {
    System.out.println("Find area ");
  }
public void area(int r) {
    System.out.println("Circle area = "+3.14*r*r);
  }
 
public void area(double b, double h) {
    System.out.println("Triangle area="+0.5*b*h);
  }
public void area(int l, int b) {
    System.out.println("Rectangle area="+l*b);
  }
 
 
}
 
class Main {
  public static void main(String[] args) {
    Shapes myShape = new Shapes();  // Create a Shapes object
     
    myShape.area();
    myShape.area(5);
    myShape.area(6.0,1.2);
    myShape.area(6,2);
     
  }
}
```

**Output:**

Find area
Circle area = 78.5
Triangle area=3.60
Rectangle area=12

### **What is Method Overriding in Java?**

Method overriding is the process when the subclass or a child class has the same method as declared in the parent class.

### **Example of Method Overriding in Java**

```
class Vehicle{  
  //defining a method  
  void run(){System.out.println("Vehicle is moving");}  
}  
//Creating a child class  
class Car2 extends Vehicle{  
  //defining the same method as in the parent class  
  void run(){System.out.println("car is running safely");}  
  
  public static void main(String args[]){  
  Car2 obj = new Car2();//creating object  
  obj.run();//calling method  
  }  
}  
```

**Output:**

```
Car is running safely
```

Also, Polymorphism in Java can be classified into two types, i.e:

1. Static/Compile-Time Polymorphism
2. Dynamic/Runtime Polymorphism

### **What is Compile-Time Polymorphism in Java?**

**Compile Time Polymorphism In** Java is also known as **Static Polymorphism.** Furthermore, the call to the method is resolved at compile-time. Compile-Time polymorphism is achieved through **Method Overloading**. This type of polymorphism can also be achieved through **Operator Overloading**. However, Java does not support Operator Overloading.

Method Overloading is when a class has multiple methods with the same name, but the number, types, and order of parameters and the return type of the methods are different. Java allows the user freedom to use the same name for various functions as long as it can distinguish between them by the type and number of parameters. 

### **Example of Compile-Time Polymorphism in Java**

*We will do addition in Java and understand the concept of compile time polymorphism using subtract()* 

```
package staticPolymorphism; 
public class Addition 
{ 
void sum(int a, int b) 
{ 
int c = a+b; 
System.out.println(“ Addition of two numbers :” +c); } 
void sum(int a, int b, int e) 
{ 
int c = a+b+e; 
System.out.println(“ Addition of three numbers :” +c); } 
public static void main(String[] args) 
{ 
Addition obj = new Addition(); 
obj.sum ( 30,90); 
obj.sum(45, 80, 22); 
} 
}
```

***The output of the program will be:*** 

*Sum of two numbers: 120* 

*Sum of three numbers: 147* 

*In this program, the sum() method overloads with two types via different parameters.* 

*This is the basic concept of compile-time polymorphism in java where we can perform various operations by using multiple methods having the same name.*

### **What is Runtime Polymorphism in Java?**

**Runtime polymorphism** in Java is also popularly known as **Dynamic Binding or Dynamic Method Dispatch.** In this process, the call to an overridden method is resolved dynamically at runtime rather than at compile-time. You can achieve Runtime polymorphism via **Method Overriding**.

Method Overriding is done when a child or a subclass has a method with the same name, parameters, and return type as the parent or the superclass; then that function overrides the function in the superclass. In simpler terms, if the subclass provides its definition to a method already present in the superclass; then that function in the base class is said to be overridden.

Also, it should be noted that runtime polymorphism can only be achieved through functions and not data members. 

Overriding is done by using a reference variable of the superclass. The method to be called is determined based on the object which is being referred to by the reference variable. This is also known as **Upcasting**.

Upcasting takes place when the Parent class’s reference variable refers to the object of the child class. For example:

```
class` `A{} ``class` `B ``extends` `A{} ``A a=``new` `B(); ``//upcasting
```

#### **Examples of Runtime Polymorphism in Java**

**Example 1:**

In this example, we are creating one superclass Animal and three subclasses, Herbivores, Carnivores, and Omnivores. Subclasses extend the superclass and override its eat() method. We will call the eat() method by the reference variable of Parent class, i.e. Animal class. As it refers to the base class object and the base class method overrides the superclass method; the base class method is invoked at runtime. As Java Virtual Machine or the JVM and not the compiler determines method invocation, it is, therefore, runtime polymorphism.

```java
class Animal{  
  void eat(){
System.out.println("Animals Eat");
}  
}  
class herbivores extends Animal{  
  void eat(){
System.out.println("Herbivores Eat Plants");
} 
  }
class omnivores extends Animal{  
  void eat(){
System.out.println("Omnivores Eat Plants and meat");
} 
  }
class carnivores extends Animal{  
  void eat(){
System.out.println("Carnivores Eat meat");
} 
  }
class main{
  public static void main(String args[]){ 
    Animal A = new Animal();
    Animal h = new herbivores(); //upcasting  
    Animal o = new omnivores(); //upcasting  
    Animal c = new carnivores(); //upcasting  
    A.eat();
    h.eat();
    o.eat();  
    c.eat();  
   
  }  
} 
```

**Output:**

Animals eat
Herbivores Eat Plants
Omnivores Eat Plants and meat
Carnivores eat meat

**Example 2:**

In this example, we are creating one superclass Hillstations and three subclasses Manali, Mussoorie, Gulmarg. Subclasses extend the superclass and override its location() and famousfor() method. We will call the location() and famousfor() method by the Parent class’, i.e. Hillstations class. As it refers to the base class object and the base class method overrides the superclass method; the base class method is invoked at runtime. Also, as Java Virtual Machine or the JVM and not the compiler determines method invocation, it is runtime polymorphism.

```java
class Hillstations{  
  void location(){
System.out.println("Location is:");
}  
void famousfor(){
System.out.println("Famous for:");
}  
 
}  
class Manali extends Hillstations {  
  void location(){
System.out.println("Manali is in Himachal Pradesh");
}  
void famousfor(){
System.out.println("It is Famous for Hadimba Temple and adventure sports");
}  
  }
class Mussoorie extends Hillstations {  
  void location(){
System.out.println("Mussoorie is in Uttarakhand");
}  
void famousfor(){
System.out.println("It is Famous for education institutions");
}  
  }
class Gulmarg extends Hillstations {  
  void location(){
System.out.println("Gulmarg is in J&K");
}  
void famousfor(){
System.out.println("It is Famous for skiing");
}  
  }
class main{
  public static void main(String args[]){ 
    Hillstations A = new Hillstations();
    Hillstations M = new Manali();
 
    Hillstations Mu = new Mussoorie();
 
    Hillstations G = new Gulmarg();
 
    A.location();
A.famousfor();
 
M.location();
M.famousfor();
 
Mu.location();
Mu.famousfor();
 
G.location();
G.famousfor();
  }  
}  
```

**Output:**

Location is:
Famous for:
Manali is in Himachal Pradesh
It is Famous for Hadimba Temple and adventure sports
Mussoorie is in Uttarakhand
It is Famous for education institutions
Gulmarg is in J&K
It is Famous for skiing

### **Example of run-time polymorphism in java**

We will create two classes Car and Innova, Innova class will extend the car class and will override its run() method.

```
class Car 
{ 
void run() 
{ 
System.out.println(“ running”); 
} 
}
class innova extends Car 
{ 
void run(); 
{ 
System.out.println(“ running fast at 120km”); 
} 
public static void main(String args[]) 
{ 
Car c = new innova(); 
c.run(); 
} 
} 
```

*The output of the following program will be;* 

*Running fast at 120 km.* 

Another example for run-time polymorphism in Java

*Now, let us check if we can achieve runtime polymorphism via data members.* 

```
class car 
{ 
int speedlimit = 125; 
} 
class innova extends car 
{ 
int speedlimit = 135; 
public static void main(String args[]) 
{ 
car obj = new innova(); 
System.out.println(obj.speedlimit);
}
```

***The output of the following program will be :*** 

*125* 

*This clearly implies we can’t achieve Runtime polymorphism via data members. In short, a method is overridden, not the data members.*

### **Runtime polymorphism with multilevel inheritance**

```
class grandfather 
{ 
void swim() 
{ 
System.out.println(“ Swimming”); 
} 
} 
class father extends grandfather 
{ 
void swim() 
{ 
System.out.println(“ Swimming in river”); 
} 
} 
class son extends father 
{ 
void swim() 
{ 
System.out.println(“ Swimming in pool”);
} 
public static void main(String args[]) 
{ 
grandfather f1,f2,f3; 
f1 =new grandfather(); 
f2 = new father(); 
f3 = new son(); 
f1.swim(); 
f2.swim(); 
f3.swim(): 
} 
} 
```

***The output of the following program will be:*** 

*Swimming*, *Swimming in river*, *Swimming in pool*

**Another runtime polymorphism with multilevel inheritance example**

```
class soundAnimal 
{ 
public void Sound() 
{ 
System.out.println("Different sounds of animal"); }
} 
class buffalo extends soundAnimal 
{ 
public void Sound() 
{ 
System.out.println("The buffalo sound- gho,gho"); } 
} 
class snake extends soundAnimal 
{ 
public void Sound() 
{ 
System.out.println("The snake sound- his,his"); } 
} 
class tiger extends soundAnimal
{ 
public void Sound() 
{ 
System.out.println("The tiger sounds- roooo, rooo"); } 
} 
public class Animal Main 
{ 
public static void main(String[] args) 
{ 
soundAnimal Animal = new soundAnimal(); soundAnimal buffalo = new buffalo(); 
soundAnimal snake = new snake(); 
soundAnimal tiger = new tiger(); 
Animal.Sound(); 
buffalo.Sound();
snake.Sound(); 
tiger.Sound(); 
} 
} 
```

***The output of the following program will be;*** 

*The buffalo sound- gho,gho* 

*The snake sound- his,his* 

*The tiger sound- roooo,roooo* 

We hope you got an idea about runtime and compile-time polymorphism.

## **Polymorphic Subtypes**

Subtype basically means that a subtype can serve as another type’s subtype, sounds a bit complicated? 

Let’s understand this with the help of an example:

Assuming we have to draw some arbitrary shapes, we can introduce a class named ‘shape’ with a draw() method. By overriding draw() with other subclasses such as circle, square, rectangle, trapezium, etc we will introduce an array of type ‘shape’ whose elements store references will refer to ‘shape’ subclass references. Next time, we will call draw(), all shapes instances draw () method will be called.

This Subtype polymorphism generally relies on upcasting and late binding. A casting where you cast up the inheritance hierarchy from subtype to a supertype is termed upcasting.

To call non-final instance methods we use late binding. In short, a compiler should not perform any argument checks, type checks, method calls, etc, and leave everything on the runtime. 

## **What is Polymorphism in Programming?**

Polymorphism in programming is defined usage of a single symbol to represent multiple different types.

## **What is Polymorphism Variables?**

A **polymorphic variable** is defined as a variable that can hold values of different types during the course of execution.

## **Why use Polymorphism in Java?**

Polymorphism in Java makes it possible to write a method that can correctly process lots of different types of functionalities that have the same name. We can also gain consistency in our code by using polymorphism.

### **Advantages of Polymorphism in Java**

1. It provides reusability to the code. The classes that are written, tested and implemented can be reused multiple times. Furthermore, it saves a lot of time for the coder. Also, the one can change the code without affecting the original code.
2. A single variable can be used to store multiple data values. The value of a variable you inherit from the superclass into the subclass can be changed without changing that variable’s value in the superclass; or any other subclasses.
3. With lesser lines of code, it becomes easier for the programmer to debug the code.

### **Characteristics of Polymorphism**

Polymorphism has many other characteristics other than Method Overloading and Method Overriding. They include:

- Coercion
- Internal Operator Overloading
- Polymorphic Variables or Parameters

#### **1. Coercion**

Coercion deals with implicitly converting one type of object into a new object of a different kind. Also, this is done automatically to prevent type errors in the code. 

Programming languages such as [C](https://www.mygreatlearning.com/blog/learn-c-programming-online-for-free/), java, etc support the conversion of value from one data type to another data type. Data type conversions are of two types, i.e., implicit and explicit. 

Implicit type conversion is automatically done in the program and this type of conversion is also termed coercion. 

For example, if an operand is an integer and another one is in float, the compiler implicitly converts the integer into float value to avoid type error.

**Example :**

```java
class coercion {
 
  public static void main(String[] args) {
    Double area = 3.14*5*7;
System.out.println(area);
String s = "happy";
int x=5;
String word = s+x;
System.out.println(word);
 
  }
}
```

**Output:**

109.9
happy5

####  **2. Internal Operator Overloading**

In Operator Overloading, an operator or symbol behaves in more ways than one depending upon the input context or the type of operands. It is a characteristic of static polymorphism. Although Java does not support user-defined operator overloading like C++, where the user can define how an operator works for different operands, there are few instances where Java internally overloads operators.

Operator overloading is the concept of using the operator as per your choice. Therefore, an operator symbol or method name can be used as a ‘user-defined’ type as per the requirements. 

For example, ‘+’ can be used to perform the addition of numbers (same data type) or for concatenation of two or more strings.

In the case of +, can be used for addition and also for concatenation.

For example:

```
class coercion {
 
  public static void main(String[] args) {
     
String s = "happy";
String s1 = "world";
int x=5;
int y=10;
 
System.out.println(s+s1);
System.out.println(x+y);
 
  }
}
```

**Output :**

happyworld
15

Similarly, operators like**! &, and |** are also in the overload position for logical and bitwise operations. In both of these cases, the type of argument will decide how the operator will interpret.

####  **3. Polymorphic Variables or Parameters**

In Java, the object or instance variables represent the polymorphic variables. This is because any object variables of a class can have an IS-A relationship with their own classes and subclasses.

The Polymorphic Variable is a variable that can hold values of different types during the time of execution.

Parametric polymorphism specifies that while class declaration, a field name can associate with different types, and a method name can associate with different parameters and return types.

**For example:**

```java
class Shape
{
public void display()
{
System.out.println("A Shape.");
}
}
class Triangle extends Shape
{
public void display()
{
System.out.println("I am a triangle.");
}
}
class Main{
public static void main(String[] args)
{
Shape obj;
obj = new Shape();
obj.display();
obj = new Triangle();
obj.display();
}
}
```

**Output:**

A Shape.
I am a triangle.

Here, the obj object is a polymorphic variable. This is because the superclass’s same object refers to the parent class (Shape) and the child class (Triangle). 

## **Problems with Polymorphism** 

With lots of advantages, there are also a few disadvantages of polymorphism.

- Polymorphism is quite challenging while implementation.
- It tends to reduce the readability of the code.
- It raises some serious performance issues in real-time as well.

**Type Identification During Downcasting** 

Downcasting is termed as casting to a child type or casting a common type to an individual type.

So, we use downcasting whenever we need to access or understand the behaviour of the subtypes. 

**Example,** 

This is a hierarchical example 

Food> Vegetable> Ladyfinger, Tomato 

Here, tomato and ladyfinger are two subclasses. 

In downcasting, we narrow the type of objects, which means we are converting common type to individual type. 

Vegetable vegetable = new Tomato(); 

Tomato castedTomato = (Tomato) vegetable; 

Here we are casting common type to an individual type, superclass to subclass which is not possible directly in java.

We explicitly tell the compiler what the runtime type of the object is.

**Fragile base class problem** 

Fragile base class problem is nothing but a fundamental architectural problem. 

Sometimes the improper design of a parent class can lead a subclass of a superclass to use superclass in some unpredicted ways. 

The fragility of inheritance will lead to broken codes even when all the criteria is met. 

This architectural problem is termed as a fragile base class problem in object-oriented programming systems and language. 

Basically, the reason for the fragile base problem is that the developer of the base class has no idea of the subclass design. There is no solution yet for this problem. 

## **Conclusion**

We hope you must have got a basic idea of polymorphism in Java and how we use it as well as problems related to them. 



---

End Of Topic
