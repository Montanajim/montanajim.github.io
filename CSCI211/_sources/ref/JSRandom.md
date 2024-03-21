# Random Functions



JavaScript random always returns a number between 0 ( inclusive) and 1 (exclusive).

```javascript
Math.random()
```



`Math.floor` is a function commonly found in programming languages that deals with numbers. It's specifically used for rounding down a number to the nearest whole integer (whole number).

Here's what `math.floor` does:

- It takes a number (integer or decimal) as input.
- It ignores any digits after the decimal point.
- It returns the largest integer that is less than or equal to the input number.



```javascript
    function RandomIntMax(max)
    {
        // to make the max inclusive we add one
        return Math.floor(Math.random() * (max + 1));
    }

    function RandomIntMinMax(min,max)
    {
        // to make the max inclusive we add one
        return Math.floor(Math.random() * ((max+1) - min) ) + min;
    }
```

