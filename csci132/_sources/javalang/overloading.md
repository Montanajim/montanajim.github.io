# Overloading



```{admonition} Definition
**Overloading** Overloading a function is to use the same function name, but give it different parameters. 
```



## Lecture Code

Note in the lecture code below how *funct1()* has different parameters passed to it.  It first has *String* data passed to it, then *double* data, followed by *int* data, and then both *String* and *int* data.  Same function name with different data types. 

Overloading a function is used mostly in creating JAVA constructors when building *classes*.



```java



public class Overload_demo {


    //func1 with no parameters
    static void func1() {
        System.out.println("This is function 1 with no arguments");
        return;
    }
    //func1 with a string parameter
    static void func1(String mydata) {
        System.out.println("This is function 1 with a string");
        return;
    }
    //func1 with a double parameter
    static void func1(double mydata) {
        System.out.println("This is function 1 with a double");
        return;
    }
    //func1 with an int parameter
    static void func1(int mydata) {
        System.out.println("This is function 1 with a double");
        return;
    }
    //func1 with a string and int parameter
    //note that this one also returns a string
    //where the other one did not.
    static String func1(String mystring, int mydata) {
        String Ans = "";
        Ans = ("This is function 1 with a string and an int");
        return Ans;
    }
    //add2 - add two doubles
    static double add2(double num1, double num2)
    {
        return (num1 + num2);
    }
    //add2 - concatenate two strings
    static String add2(String text1,String text2)
    {
        return (text1 + " " + text2 + " - is great!");
    }
            
    public static void main(String[] args) {
        //func1 examples
        func1();
        func1("Bubba");
        func1(22.5);
        func1(999);
        System.out.println(func1("Bob", 59));

        //add2 examples
        System.out.println(add2(100.00,6000.00)); 
        System.out.println(add2("hot","dog"));
         
    }
}

```



---

End Of Topic