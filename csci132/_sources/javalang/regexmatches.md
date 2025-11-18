# Regex - Using Java Matches



```{admonition} Definition
A __regular expression__ (shortened as regex or regexp; sometimes referred to as rational expression) is a sequence of characters that specifies a search pattern in text. Usually such patterns are used by string-searching algorithms for "find" or "find and replace" operations on strings, or for input validation. _https://en.wikipedia.org/wiki/Regular_expression_
```





## From Stack Overflow

https://stackoverflow.com/questions/8923398/regex-doesnt-work-in-string-matches

Welcome to Java's misnamed [`.matches()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#matches-java.lang.String-) method... It tries and matches ALL the input. Unfortunately, other languages have followed suit :(

If you want to see if the regex matches an input text, use a `Pattern`, a `Matcher` and the `.find()` method of the matcher:

```java
Pattern p = Pattern.compile("[a-z]");
Matcher m = p.matcher(inputstring);
if (m.find())
    // match
```

If what you want is indeed to see if an input only has lowercase letters, you can use `.matches()`, but you need to match one or more characters: append a `+` to your character class, as in `[a-z]+`. Or use `^[a-z]+$` and `.find()`.

---

## Lecture Code

```java
/*
 * Programmer: James Goudy
 * Project: Using Regex to determine valid characters in a string
 */
package com.mycompany.java_regexexpressions;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 *
 * @author jgoudy
 */
public class Java_RegExExpressions {

    public static void main(String[] args) {
        boolean status = true;

        // Test - only want a string expression to only allow 
        // the any capital letters of A B C D,
        // the any lowercase letters of l m n o p,
        // and any numbers of 4 5 6 7 8
        // The regex Expression looks like this ^[A-Dl-p4-8]+$
        
        // Note in order to work correctly in JAVA
        // it must start with the ^ and end with the $
        
        String regex_Expression = "^[A-Dl-p4-8]+$";
        System.out.println("Regex Expression = " + regex_Expression);

        // this string should test false since FF is not allowed
        String testPattern = "AAFFlmno78";
        System.out.println("\nFalse test pattern: " + testPattern);

        Pattern p = Pattern.compile(regex_Expression);
        Matcher m = p.matcher(testPattern);
        status = m.find();
        System.out.println("status = " + status);

        // this pattern should test true
        testPattern = "BBDDoooml55447";
        System.out.println("\nTrue test pattern: " + testPattern);
        
        p = Pattern.compile(regex_Expression);
        m = p.matcher(testPattern);
        status = m.find();
        System.out.println("status = " + status);

        // note that m.find() is a boolean and could be used
        // in if statements, loops, etc.
    }
}

/* Output

Regex Expression = ^[A-Dl-p4-8]+$

False test pattern: AAFFlmno78
status = false

True test pattern: BBDDoooml55447
status = true

 */
```

---

## Regular Expression References

[Regular Expressions - Java](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html)

[Regular Expressions - Microsoft](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference)

[Regular Expression - Google / Python](https://developers.google.com/edu/python/regular-expressions)

[Regular Expressions - Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

---

Endo Of Topic





