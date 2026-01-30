# Lambda Functions



## Key Ideas

* Lambda functions

  

## Readings

[Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)

[Lambda Expression in Java 8](https://www.geeksforgeeks.org/lambda-expressions-java-8/)



```{admonition} Definition
**Lambda functions** are intended as a shorthand for defining functions that can come in handy to write concise code without wasting multiple lines defining a function. They are also known as anonymous functions, since they do not have a name unless assigned one. From *[What’s in a Lambda?](https://towardsdatascience.com/whats-in-a-lambda-c8cdc67ff107)*
```



```{admonition} Definition
**Interface** - In its most common form, an interface is a group of related methods with empty bodies.  The programmer is then responsible for writing the functions
```



```{admonition} Note
In most other languages, lambda functions do not need an interface and can be written as just as an anonmyous function.  They all follow the same structure:

**( ) -> { }** 
```



## Lecture Code



```java
/*

* Program: Lambda Examples
* Programmer: James Goudy

 */



// note that the interface can also be put in their own file
// note that a function is defined (which the programmer can name)
// in the interface.  The actual functin can then be written as 
// a global function or within a function.

interface InchtesToFeet{
    // Input is a double - inches
    // Output is a double executed by the function name "calculate"
    double calculate(double inches);
}

interface FtoC{
    // Input is a double - farh
    // Output is a double executed by the function name "calculate"
    double calculate(double farh);
    
}

interface GalaxayTip{
    // Input is nothing
    // Output is a string executed by the function name "calculate"   
    String run();
}

interface myFormula{
    // Input is two doubles
    // Output is a string executed by the function name "tabulate"      
    String tabulate(double num1,double num2);
    
}

public class Lambda_Lecture {
    
    //Global Lamda functions
    static InchtesToFeet itf =(i)->{return i/12.0;};
    static GalaxayTip  tip = ()->{return "Always bring a towel";};
    
    // multiple 2 numbers, add 50 then concantenate string
    // note this lambda function has multiple lines of code
    static myFormula mf = (n1,n2) ->{
        
        // define local variable
        double ans = 0;
        
        ans = n1* n2 + 50;
        
        return ans+ " units";
    };
    
    
    public static void main(String[] args) {
              
        int i = 36;
        double ft = 212;
        
        double xx = 10;
        double yy = 20;
        
        
        System.out.println(itf.calculate(i) + " feet");
        
        FtoC ftc = (f) -> {return (f-32.0) * 5.0/9.0;};
        System.out.println(ftc.calculate(ft) + " C");
        System.out.println(ftc.calculate(392.0) + " C");
        
        System.out.println(tip.run());
        
        System.out.println(mf.tabulate(xx, yy));     
        
    }
}

/*
3.0 feet
100.0 C
200.0 C
Always bring a towel
250.0 units
 */
```



---

End of Topic



