# Recursion



## Key Topics

* Recursion
* Tail Recursion



## Readings

* [Recursion - Geeks For Geeks](https://www.geeksforgeeks.org/recursion/?ref=gcse)
* [Recursion - Wikipedia](https://en.wikipedia.org/wiki/Recursion_(computer_science))
* [Tail vs Non-Tail Recursion by Baeldung](https://www.baeldung.com/cs/tail-vs-non-tail-recursion)
* [Recursive by Computer Hope](https://www.computerhope.com/jargon/r/recursive.htm)



```{admonition} Definition
**Recursion** A function that calls itself.
```

```{admonition} Definition
**[Tail Recursion](https://www.pixelstech.net/article/1474689232-Traditional-recursion-vs-Tail-recursion)**  A tail recursion is also a kind of recursion but it will make the return value of the recursion call as the last statement of the method.
```

```{warning}
Java does not optimize for tail recursion
```



````{tip}
In order to trap a stack over flow error, it has to be specified in the catch statment as shown below:

```java
        try {
          // posible code that could stack overflow
        } catch (StackOverflowError e) {

            System.out.println("RECURSION: STACK OVERFLOW ERROR");
            System.out.println(e.getMessage());
        }
```
````



## Lecture Code

Any recursive function can always be written as a loop.  Note there is an example of what a tail-recursive function would look like if Java supported it.  Many languages do not support tail-recursion. Scala, Haskell, and some others do support it. This is  important to know because sometimes this is asked in interview questions.

```java
/*
 *
 * Project: Recursion Lecture Code
 * Programmer: James Goudy
 *
 */


public class Ds_recursion {

    static double sumNums_Loop(int n) {

        double sum = 0;

        for (int i = n; i > 0; i--) {
            sum = sum + i;
        }

        return sum;
    }

    // This will eventually cause a stack overflow error for big "n"'s. 
    // Every time the function is called recursively and
    // intermediate n is saved in the program stack which
    // will result in running out of resources / stackoverflow error
    
    static double sumNums_Recursive(int n) {

        if (n == 0) {
            return n;
        }

        return n + sumNums_Recursive(n - 1);

    }

    // TAIL Recursion
    // NOTE: Java as of JDK 17 does not optimization for tail recursion
    // If it did, it would look like the following:
    // The reason this is a tail recursion is the sum
    // is being calculated everytime and the function 
    // does not have to store any temp values to retreive the calculated answer
    
    static double sumNums_TailRecursive(int n, double sum) {

        if (n <= 1) {
            return sum;
        }

        return sumNums_TailRecursive(n - 1, sum + 1);

    }

    public static void main(String[] args) {

        int n = Integer.MAX_VALUE;
        double ans = 0;

        n = 200;

        System.out.println("Max integer: " + Integer.MAX_VALUE);
        System.out.println("n = " + n + "\n");

        System.out.println("Loop: Sum of all numbers " + n
                + " = " + sumNums_Loop(n));

        System.out.println("Recursive: Sum of all numbers " + n
                + " = " + sumNums_Recursive(n));
        

        System.out.println("\n *************\n");
        
        // set a very big "n"
        n = 200000000;
        
        System.out.println("n = " + n + "\n");

        System.out.println("Loop: Sum of all numbers " + n
                + " = " + sumNums_Loop(n));

        // The following will fail recursively.
        //  This will error because it will run out of resources
        //  on the program stack.
        // Note how we are catching specifically for a StackOverFlow error.
        
        try {
            System.out.println("Recursive: Sum of all numbers " + n
                    + " = " + sumNums_Recursive(n));
        } catch (StackOverflowError e) {

            System.out.println("RECURSION: STACK OVERFLOW ERROR");
            System.out.println(e.getMessage());
        }

        System.out.println("\nbye\n");
    }
}


/*
Max integer: 2147483647
n = 200

Loop: Sum of all numbers 200 = 20100.0
Recursive: Sum of all numbers 200 = 20100.0

 *************

n = 200000000

Loop: Sum of all numbers 200000000 = 2.0000000174137712E16
RECURSION: STACK OVERFLOW ERROR
null

bye
 */
```



## Lecture Code  II

Note that in this example a recursive function as another recursive function called within it.  Note that it will print the output of the first recursive function first all at once. Then it goes back for each time and prints the outcome separately starting with the last iteration of the "top" recursive function.

```java
/*
 * Programmer: James Goudy
 * Project: Lecture Code Recursion II
 */


/**
 *
 * @author jgoudy
 */
public class DS_Recursion_Example_II {

    static String alp = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghicklmnopqrstuvwxyz";
    static int stop = 4;

    static void recursiveLetter(int a) {
        if (a > stop) {
            return;
        }
        
        System.out.println("a = " + alp.charAt(a) + " - " + a);
        a++;
        recursiveLetter(a);
        
        
    }

    static void recursiveCount(int n) {
        if (n > stop) {

            return;
        }

        System.out.println("n = " + n);
        n++;

        recursiveCount(n);
        System.out.println("----------");
        recursiveLetter(n);

    }

    public static void main(String[] args) {

        System.out.println("L = " + alp.length());
        System.out.println("");

        recursiveCount(0);
        
        System.out.println("\n****** Call recursive letters only *********\n");
        
        recursiveLetter(0);

    }
}
/*

Output

L = 52

n = 0
n = 1
n = 2
n = 3
n = 4
----------
----------
a = E - 4
----------
a = D - 3
a = E - 4
----------
a = C - 2
a = D - 3
a = E - 4
----------
a = B - 1
a = C - 2
a = D - 3
a = E - 4

****** Call recursive letters only *********

a = A - 0
a = B - 1
a = C - 2
a = D - 3
a = E - 4
------------
 */
```



---

End Of Topic



