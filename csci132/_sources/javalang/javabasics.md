# Java Basics

## Key Topics
* Comments
* Variables
* Data types
* Operators
* Order of Operations
* Incrementors and Decrementors
* Escape Characters
* Comparative Operators
* Concatenation


# Readings

https://books.trinket.io/thinkjava/chapter1.html



##  Comments 


```{admonition} Definition
**Comment** allows the programmer to document their code. It is not compiled.
```

### Examples

```java
// This is a single line comment

/*
This is 
a multiline
comment
*/
```



## Variables


```{admonition} Definition
**Variable** stores one item of information.
```

### Naming Variables

* Start with a letter, underscore or a dollar sign
* Can not start with an number
* **NO SPACES**
* CASE SENSITIVE
  * All different are different variable names:  fname, Fname, fName, FNAME, fnamE
* Java as a whole is case sensitive

```{admonition} Declaring A Variable
*datatype* variableName;<br>
*datatype* variableName = value;
```

### Examples

```java
// declaring variables
int Age;
String First_Name;
boolean Breathing;

//declaring variables and intializing them with a value
int numberOfStates = 50;
double salary = 50000;

// note that strings get double quotes
// chars get single quotes
String dogName = "Spot";
char middleInital = 'A';

boolean isBreathing = true;

```
```{warning}
A variable is usually declared once within a set of braces{}.
```

### Data Types

| Data Type         | Memory Space | Max Values |
| ----------------- | ------------ | ---------- |
| **Integer Types - whole numbers** |              |            |
|byte8 |bits - 1 byte|-128 to 128||
|short|16 bits – 2 bytes|-32,768 to 32,767|
|int|32 bits – 4 bytes|-2,147,483,648 to 2,147,483,647|
|long|64 bits – 8 bytes|(+-)9,223,372,036,854,775,808)|
|**Real / Floating Point**|             |         |
|float|32 bits - 4 bytes|1.4 E-45 to 3.4 E+38|
|double|64 bits - 8 bytes |4.9 E -324 to 1.7 E 308|
|**Other**|         |          |
|boolean|   |true / false - Use as flags|
|char|   |Individual letters or characters |
|**Acts Like A Variable**|    |    |
|String|     | ~ 2 billion characters|
|Object|    |Store binaries - "anything"     |
|var|   | limited use within functions when datatype is not known|

Note: for precise decimals i.e. currency – use java.math.BigDecimal – reason – rounding accuracy



## Operators

| Sign | Operations |
| ---- | ---------- |
|+| Addition|
|-|Subtraction|
|\*|Multiplication|
|/|Divide|
|%|Modulus (return the remainder of an integer)| 



## Order Of Operations
* Increment and decrement
* Parentheses ()
* Exponents
+ \* /
* \+ \-
* Comparisons > < >= <= == !=
* Logical Operations && ||
* Assignment Expressions



## Incrementors and Decrementors

* use ++ to add the number 1 to a variable.
* use -- to subtract the number one from a variable. 



**Examples**

```java
x++;
age++;

y--;
salary--;
```



## Escape Characters

```{admonition} Definition
**Escape Character** is a backslash \ followed by the character you want to insert into your for printing or inserting into a string.
```
|Escape Character| Definition|
|----------|--------------|
|\n	|new line|
|\t	|tab|
|\b	|backspace|
|\r	|carriage return|
|\f	|form feed|
|\\	|backslash|
|\'	|single quotation mark|
|\”	|double quotation mark|
|\d	|octal|
|\xd	|hexadecimal|
|\ud	|Unicode character|



## **Comparative Operators**

```{admonition} Definition
**Comparative Operators** evaluate is something is true or false.
```
|Operator|Definition|
|--------|------------|
|==	|Equal to   			x==y;   (NOT x=y)|
|!=	|Not Equal to		x != y;|
|<	|Less Than			x < y;|
|>	|Greater Than		x>y.|
|<=	|Less Than or Equal to	x <= y ; (no space between the signs)|
|>=	|Greater Than or Equal to	x >=y;|

## Logical Operators
```{admonition} Definition
**Logica Operators** connect two or more expression together and evalute to true or false.
```
|Operator|Definition|
|--------|------------|
|&&|AND (both sides must be true to evaluate to true) |
|\|\||OR (only one side must be true to evaluate to true)|

### Truth Table

**(x < y && z > 10)**

|expression 1<br>x<y|operator|expression 2<br>z >10| outcome|
|:------------------------------:|:-----------:|:---------:|:--------:|
|**AND**||||
|true|&&|true|true|
|true|&&|false|false|
|false|&&|true|false|
|false|&&|false|false|
|**OR**||||
|true|\|\||true|true|
|true|\|\||false|true|
|false|\|\||true|true|
|false|\|\||false|false|

## Concatenation

```{admonition} Definition
**Concatenation** is the action of putting strings togeher to form a new string.
```

### Example
```java
//Note we concantenate a space " " between the first and last name
String fName = “Bubba”;
String lName =  “Smith”;
String fullName = fName  + “ “ + lname;
```



---



End Of Topic
