# If and Switch Statements in JavaScript

## Introduction

Programs do not become useful because they can store data or repeat actions. Programs become useful because they can make decisions. A payroll program must decide whether to apply overtime. A grading system must decide which letter grade to assign. A menu-driven application must decide which operation to run based on the user’s choice. In every case, the program examines a condition and then follows one path instead of another.

JavaScript uses **selection statements** to perform this kind of decision-making. Two of the most important selection structures are the `if` statement and the `switch` statement. These statements allow a program to evaluate expressions, compare values, and choose among alternative blocks of code.

Beginning students often see `if` and `switch` as simple syntax features. That view is too shallow. These statements express program logic. They shape control flow, determine which code runs, and affect correctness, readability, and maintainability. Poorly written decision logic creates bugs that hide in plain sight. Clear decision logic makes programs easier to test, debug, and extend.

This chapter explains how `if` and `switch` statements work in JavaScript, why they matter, how JavaScript evaluates conditions, and when one structure fits better than the other. It also addresses execution order, truthy and falsy values, common mistakes, and practical coding strategies.

## Chapter at a Glance

This chapter explains how JavaScript uses `if`, `else if`, `else`, and `switch` to control decision-making. It distinguishes syntax from behavior, shows how JavaScript evaluates conditions, and demonstrates how selection statements influence execution order. It also examines common logic errors, compares `if` and `switch`, and presents best practices for writing clear and reliable branching code.

## Learning Goals

By the end of this chapter, you should be able to:

1. Explain the purpose of selection statements in JavaScript.
2. Write correct `if`, `if...else`, and `if...else if...else` statements.
3. Write correct `switch` statements with `case`, `break`, and `default`.
4. Predict execution order in branching code.
5. Distinguish between Boolean expressions and general expressions used as conditions.
6. Explain how truthy and falsy values affect `if` conditions.
7. Identify common mistakes involving comparison operators, block structure, and fall-through behavior.
8. Choose appropriately between `if` and `switch` for a given programming problem.
9. Debug branching errors in beginner-level JavaScript programs.

------

## 1. What This Concept Is

Selection statements allow a program to choose among alternative actions. Instead of executing every statement in a straight line, the program tests a condition and then decides which block of code to run.

In JavaScript, the two main selection mechanisms are:

- `if` statements, which evaluate one or more conditions in sequence
- `switch` statements, which compare one expression against several possible values

A selection statement does not repeat code. It does not store data. It directs **control flow**.

### Key Point

Control flow determines the order in which a program executes statements. Selection statements change that order by allowing some statements to run and others to be skipped.

### Definition

A **selection statement** is a control structure that chooses one path of execution from multiple possibilities based on a condition or expression.

------

## 2. Why This Concept Matters

Without decision-making, a program behaves like a train on a single fixed track. Real software cannot work that way. Programs must respond to input, state, and context.

A JavaScript program may need to:

- check whether a password is correct
- determine whether a number is positive, negative, or zero
- respond to a menu option
- apply discounts based on purchase amount
- display different messages based on user role
- validate form data before submitting it

Every one of these tasks depends on branching logic.

Poor decision-making code causes real problems. A missing `break` in a `switch` can trigger the wrong operation. A badly ordered `if...else if` chain can make later conditions unreachable. A misunderstood truthy value can make a program behave as though data exists when it does not.

Good selection logic is not decoration. It is structural engineering.

------

## 3. The `if` Statement

The `if` statement is the most flexible decision-making structure in JavaScript. It evaluates a condition. If that condition is true, JavaScript executes the associated block. If the condition is false, JavaScript skips that block.

### Syntax and Basic Form

```javascript
if (condition) {
    // statements to run if condition is true
}
```

The condition appears inside parentheses. The body appears inside braces.

### Simple Example

```javascript
let temperature = 85;

if (temperature > 80) {
    console.log("It is a hot day.");
}
```

If `temperature > 80` evaluates to `true`, JavaScript prints the message. If it evaluates to `false`, JavaScript skips the block.

### Detailed Walkthrough

In the previous example, JavaScript performs these steps:

1. It stores `85` in `temperature`.
2. It evaluates the expression `temperature > 80`.
3. Since `85 > 80` is `true`, it enters the block.
4. It executes `console.log("It is a hot day.");`
5. It continues with the next statement after the block.

That execution order matters. JavaScript does not “look ahead” and run both branches. It evaluates the condition first, then chooses.

### Checkpoint

If `temperature` were `72`, would the `console.log()` statement execute? No. The condition would evaluate to `false`, so JavaScript would skip the block.

------

## 4. The `if...else` Statement

An `if` statement by itself provides a single optional path. An `if...else` statement provides two alternatives.

### Syntax and Basic Form

```javascript
if (condition) {
    // runs if condition is true
} else {
    // runs if condition is false
}
```

### Example

```javascript
let age = 17;

if (age >= 18) {
    console.log("You may vote.");
} else {
    console.log("You are not old enough to vote.");
}
```

If the condition is true, JavaScript runs the first block. Otherwise, it runs the `else` block.

### Core Behavior

An `if...else` statement always chooses one of the two blocks. It never executes both, and it never skips both.

### Common Mistake

Students often assume that `else` checks another condition. It does not. `else` means “if the earlier condition was false, do this instead.”

That distinction matters. `else` does not have its own test expression.

------

## 5. The `if...else if...else` Chain

When a program must choose from more than two possibilities, JavaScript can test conditions in sequence.

### Syntax and Basic Form

```javascript
if (condition1) {
    // runs if condition1 is true
} else if (condition2) {
    // runs if condition1 is false and condition2 is true
} else if (condition3) {
    // runs if previous conditions are false and condition3 is true
} else {
    // runs if all previous conditions are false
}
```

### Example

```javascript
let score = 84;
let grade;

if (score >= 90) {
    grade = "A";
} else if (score >= 80) {
    grade = "B";
} else if (score >= 70) {
    grade = "C";
} else if (score >= 60) {
    grade = "D";
} else {
    grade = "F";
}

console.log("Grade:", grade);
```

### Execution Order Carefully Explained

JavaScript evaluates these conditions from top to bottom.

For `score = 84`, here is what happens:

1. Check `score >= 90` → `false`
2. Check `score >= 80` → `true`
3. Assign `"B"` to `grade`
4. Skip the rest of the chain
5. Print `Grade: B`

Once one condition succeeds, JavaScript stops testing the remaining `else if` conditions.

### Warning

Order matters in an `if...else if...else` chain. If you place broader conditions before narrower ones, you can accidentally block later cases.

Bad example:

```javascript
let score = 95;

if (score >= 60) {
    console.log("Passed");
} else if (score >= 90) {
    console.log("Excellent");
}
```

This code will print `"Passed"`, not `"Excellent"`, because the first condition already matches. The second condition never gets a chance.

This logic is flawed. It works syntactically but fails conceptually.

------

## 6. Boolean Expressions, Truthy Values, and Falsy Values

Students often think an `if` condition must literally produce `true` or `false`. That is incomplete. JavaScript allows any expression in a condition. It then converts that expression to a Boolean value.

### Definition

A **Boolean expression** is an expression that evaluates to either `true` or `false`.

### Example of a Boolean Expression

```javascript
let x = 10;

if (x > 5) {
    console.log("x is greater than 5");
}
```

The expression `x > 5` already evaluates to `true` or `false`.

### Truthy and Falsy

JavaScript also allows non-Boolean values in conditions. It converts them internally.

Values commonly treated as **falsy** include:

- `false`
- `0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

Most other values are **truthy**.

### Example

```javascript
let username = "";

if (username) {
    console.log("Username exists.");
} else {
    console.log("Username is empty.");
}
```

Because `username` contains an empty string, JavaScript treats it as falsy.

### Behind the Scenes

When JavaScript evaluates `if (username)`, it performs an internal Boolean conversion. It does not require the programmer to write:

```javascript
if (Boolean(username)) {
```

but that is effectively the idea.

### Debugging Note

Truthy and falsy behavior makes code compact, but it also creates traps. A value of `0` may be a valid numeric input, but JavaScript treats it as falsy. If you write code carelessly, you may reject valid data by mistake.

Bad example:

```javascript
let quantity = 0;

if (quantity) {
    console.log("Quantity entered.");
} else {
    console.log("No quantity entered.");
}
```

This code prints `"No quantity entered."` even though `0` is a real value.

That is not JavaScript being broken. That is the programmer choosing the wrong test.

Better version:

```javascript
if (quantity !== null && quantity !== undefined) {
    console.log("Quantity entered.");
}
```

------

## 7. Comparison and Logical Operators in Conditions

Selection statements rely heavily on operators that build conditions.

### Common Comparison Operators

```javascript
>   greater than
<   less than
>=  greater than or equal to
<=  less than or equal to
=== strictly equal to
!== strictly not equal to
```

For beginning JavaScript work, `===` and `!==` are usually the correct equality operators to use.

### Common Logical Operators

```javascript
&&  logical AND
||  logical OR
!   logical NOT
```

### Example

```javascript
let age = 20;
let hasID = true;

if (age >= 18 && hasID) {
    console.log("Entry allowed.");
}
```

This condition succeeds only if both parts are true.

### Common Mistake

Students often confuse `=` with `===`.

```javascript
if (x = 5) {
    console.log("This is wrong.");
}
```

This code assigns `5` to `x` instead of comparing values. In JavaScript, the assignment expression itself has a value, and `5` is truthy, so the block runs. That bug is sneaky and ugly.

Correct version:

```javascript
if (x === 5) {
    console.log("This is correct.");
}
```

------

## 8. Nested `if` Statements

A program may place one `if` statement inside another.

### Example

```javascript
let age = 20;
let hasTicket = true;

if (age >= 18) {
    if (hasTicket) {
        console.log("You may enter.");
    } else {
        console.log("You need a ticket.");
    }
} else {
    console.log("You must be at least 18.");
}
```

### Core Behavior

The outer `if` must succeed before JavaScript evaluates the inner `if`.

### Comparison

Nested `if` statements can express layered decision-making, but they can also become messy fast. If nesting becomes deep, the code often needs redesign. Sometimes a compound condition or a different program structure reads more clearly.

------

## 9. The `switch` Statement

The `switch` statement provides another way to choose among multiple paths. It works best when one expression can take several discrete values.

### Syntax and Basic Form

```javascript
switch (expression) {
    case value1:
        // statements
        break;
    case value2:
        // statements
        break;
    default:
        // statements
}
```

### What It Does

JavaScript evaluates the `expression` once. Then it compares that result to each `case` value. If it finds a match, it begins executing statements from that case.

### Simple Example

```javascript
let dayNumber = 3;
let dayName;

switch (dayNumber) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    case 4:
        dayName = "Thursday";
        break;
    case 5:
        dayName = "Friday";
        break;
    default:
        dayName = "Invalid day";
}

console.log(dayName);
```

### Detailed Walkthrough

For `dayNumber = 3`, JavaScript proceeds as follows:

1. Evaluate `dayNumber`
2. Compare it to `1` → no match
3. Compare it to `2` → no match
4. Compare it to `3` → match
5. Execute `dayName = "Wednesday";`
6. Encounter `break`
7. Exit the `switch`
8. Print `"Wednesday"`

The crucial detail is the `break`. Without it, JavaScript continues into later cases.

------

## 10. Fall-Through in `switch`

The `switch` statement has one behavior that beginners frequently misunderstand: **fall-through**.

### Definition

**Fall-through** occurs when JavaScript continues executing the statements in subsequent `case` blocks because no `break` ends the current case.

### Example of Unintended Fall-Through

```javascript
let option = 2;

switch (option) {
    case 1:
        console.log("Add");
    case 2:
        console.log("Edit");
    case 3:
        console.log("Delete");
    default:
        console.log("Done");
}
```

If `option` is `2`, this code prints:

```javascript
Edit
Delete
Done
```

That surprises many beginners. It should not. Once JavaScript matches `case 2`, it starts there and keeps going until the `switch` ends or a `break` appears.

### Corrected Version

```javascript
switch (option) {
    case 1:
        console.log("Add");
        break;
    case 2:
        console.log("Edit");
        break;
    case 3:
        console.log("Delete");
        break;
    default:
        console.log("Done");
}
```

### Common Mistake

Forgetting `break` is one of the classic `switch` errors. It is the programming equivalent of leaving a gate open and acting surprised when the goats escape.

### Intentional Fall-Through

Sometimes programmers use fall-through on purpose.

```javascript
let month = 2;
let days;

switch (month) {
    case 4:
    case 6:
    case 9:
    case 11:
        days = 30;
        break;
    case 2:
        days = 28;
        break;
    default:
        days = 31;
}
```

Here, several `case` labels share the same code. That is valid and often useful.

------

## 11. How `switch` Compares Values

In modern JavaScript, `switch` compares the expression and `case` values using strict comparison semantics. That means type matters.

### Example

```javascript
let value = "2";

switch (value) {
    case 2:
        console.log("Number two");
        break;
    case "2":
        console.log("String two");
        break;
}
```

This code prints `"String two"`.

The string `"2"` does not match the number `2`.

### Debugging Note

If a `switch` statement seems to ignore a matching case, check data types first. The value may look right while the type is wrong.

------

## 12. When to Use `if` Versus `switch`

Students often ask which statement is “better.” That question is sloppy. The right question is which statement fits the problem.

### Comparison

Use `if` when:

- you need ranges such as `score >= 90`
- you need compound logic such as `age >= 18 && hasID`
- conditions differ in structure
- comparisons are not based on a single expression

Use `switch` when:

- one expression is compared against several exact values
- the alternatives are discrete and fixed
- readability improves through a clean menu-like structure

### Example Where `if` Is Better

```javascript
let temperature = 72;

if (temperature < 32) {
    console.log("Freezing");
} else if (temperature < 60) {
    console.log("Cool");
} else if (temperature < 80) {
    console.log("Warm");
} else {
    console.log("Hot");
}
```

This works naturally because the logic depends on ranges.

### Example Where `switch` Is Better

```javascript
let command = "save";

switch (command) {
    case "open":
        console.log("Opening file...");
        break;
    case "save":
        console.log("Saving file...");
        break;
    case "close":
        console.log("Closing file...");
        break;
    default:
        console.log("Unknown command.");
}
```

This is cleaner than a long chain of exact-value comparisons.

------

## 13. A Combined Program Example

The following program demonstrates both `if` and `switch` in one small application.

```javascript
let score = 88;
let menuChoice = 2;
let letterGrade;

// Determine letter grade with if...else if...else
if (score >= 90) {
    letterGrade = "A";
} else if (score >= 80) {
    letterGrade = "B";
} else if (score >= 70) {
    letterGrade = "C";
} else if (score >= 60) {
    letterGrade = "D";
} else {
    letterGrade = "F";
}

console.log("Score:", score);
console.log("Letter grade:", letterGrade);

// Perform an action with switch
switch (menuChoice) {
    case 1:
        console.log("Display student report");
        break;
    case 2:
        console.log("Print student report");
        break;
    case 3:
        console.log("Email student report");
        break;
    default:
        console.log("Invalid menu selection");
}
```

### Walkthrough

First, the program uses an `if...else if...else` chain to classify a score into a grade. This logic depends on numeric ranges, so `if` is the correct structure.

Next, the program uses a `switch` statement to respond to a menu choice. Because `menuChoice` represents one exact value from a small fixed set, `switch` fits well.

This example shows an important design lesson: the two statements are not rivals. They solve different kinds of branching problems.

------

## 14. Common Mistakes and Debugging Problems

### Common Mistake: Using `=` Instead of `===`

```javascript
if (status = "ready") {
    console.log("Go");
}
```

This assigns `"ready"` instead of comparing values.

Correct version:

```javascript
if (status === "ready") {
    console.log("Go");
}
```

### Common Mistake: Forgetting Braces in Multi-Line Blocks

```javascript
if (x > 0)
    console.log("Positive");
    console.log("Done");
```

Only the first statement belongs to the `if`. The second runs every time.

Correct version:

```javascript
if (x > 0) {
    console.log("Positive");
    console.log("Done");
}
```

Even when braces are technically optional for one statement, using them consistently prevents stupid bugs. This is not a style nicety. It is defensive programming.

### Common Mistake: Ordering Conditions Poorly

```javascript
let score = 95;

if (score >= 60) {
    console.log("Passed");
} else if (score >= 90) {
    console.log("Excellent");
}
```

The second condition is unreachable for any score of 90 or above.

### Common Mistake: Forgetting `break` in `switch`

```javascript
switch (choice) {
    case 1:
        console.log("One");
    case 2:
        console.log("Two");
}
```

If `choice` is `1`, this prints both lines.

### Debugging Note

When branching code behaves strangely, inspect three things first:

1. the exact value being tested
2. the exact operator being used
3. the order of conditions or cases

Most beginner errors in selection logic come from one of those three causes.

------

## 15. Best Practices

Write conditions that clearly express intent. A program should not feel like a riddle.

Use `===` and `!==` unless you have a specific reason not to. Loose equality introduces type coercion, and type coercion is often where clean logic goes to die.

Order `if...else if` conditions from most specific to most general when overlap exists.

Use braces consistently, even for single-statement blocks. Consistency prevents mistakes and improves readability.

Use `switch` for fixed exact-value branching, not for range testing. Forcing `switch` into jobs meant for `if` usually produces awkward code.

Always include a `default` case in a `switch` when practical. Unexpected input exists. Pretending otherwise is not realism; it is negligence.

Keep branching logic as simple as possible. If a condition becomes hard to read, break it into smaller named variables.

### Final Takeaway

A good selection statement does more than run correct code. It makes the program’s logic visible. When someone reads your `if` or `switch`, they should see the decision structure immediately, not excavate it like an archaeological site.

------

## Key Terms

Selection statement, control flow, condition, Boolean expression, truthy, falsy, `if` statement, `if...else`, `else if`, nested `if`, `switch` statement, `case`, `break`, `default`, fall-through, strict equality, logical operator, comparison operator.

------

## Chapter Summary

`If` and `switch` statements allow JavaScript programs to make decisions and control execution flow. The `if` statement works well for flexible conditions, range checks, compound logic, and ordered tests. The `if...else` structure creates two-way branching, while the `if...else if...else` chain supports multiple alternatives. JavaScript evaluates these conditions in order and stops once it finds a successful branch.

The `switch` statement works best when one expression must be compared to several exact values. Each `case` represents a possible match, `break` prevents unwanted fall-through, and `default` handles unmatched values. Because JavaScript compares `switch` values strictly, type differences matter.

This chapter also emphasized that syntax alone is not enough. Correct branching depends on execution order, operator choice, condition design, and awareness of truthy and falsy values. Clear selection logic improves correctness, readability, and debugging.

------

## Review Questions

### 1. What is the main purpose of an `if` statement in JavaScript?

A. To repeat a block of code
B. To declare variables
C. To choose whether to execute code based on a condition
D. To store multiple values in one variable

### 2. Which statement about `else` is correct?

A. It checks a new condition
B. It runs when the `if` condition is false
C. It always runs after `if`
D. It can only appear inside a `switch`

### 3. What will this code print?

```javascript
let x = 5;

if (x > 3) {
    console.log("A");
} else {
    console.log("B");
}
```

A. A
B. B
C. A and B
D. Nothing

### 4. Which operator should you usually use to test strict equality in JavaScript?

A. `=`
B. `==`
C. `===`
D. `=>`

### 5. In an `if...else if...else` chain, what happens after JavaScript finds the first true condition?

A. It keeps checking the rest
B. It executes all remaining branches
C. It stops checking the rest of the chain
D. It jumps to the `else` branch

### 6. What is the purpose of `break` in a `switch` statement?

A. It repeats the current case
B. It exits the `switch` after a case runs
C. It starts the next case
D. It changes the value being tested

### 7. What is fall-through in a `switch` statement?

A. When all cases are skipped
B. When JavaScript throws an error
C. When execution continues into later cases because no `break` appears
D. When the `default` case runs first

### 8. Which structure is usually better for testing numeric ranges?

A. `switch`
B. `if...else if...else`
C. `default`
D. `break`

### 9. Which of the following values is falsy in JavaScript?

A. `"hello"`
B. `42`
C. `0`
D. `[]`

### 10. Which statement best describes `switch`?

A. It is best for comparing one expression against several exact values
B. It is best for testing complex ranges
C. It can only work with numbers
D. It always runs the `default` case first

------

## Answer Key

1. C
2. B
3. A
4. C
5. C
6. B
7. C
8. B
9. C
10. A

------

## Glossary

**Boolean expression**
An expression that evaluates to either `true` or `false`.

**break**
A statement used in a `switch` to stop execution and exit the structure.

**case**
A labeled branch inside a `switch` statement that matches a possible value.

**condition**
An expression evaluated to determine whether a branch of code should run.

**control flow**
The order in which a program executes its statements.

**default**
The branch in a `switch` statement that runs when no `case` matches.

**else**
A branch that runs when the preceding `if` condition is false.

**else if**
An additional conditional branch checked only if earlier conditions were false.

**falsy**
A value that JavaScript treats as `false` in a Boolean context, such as `0`, `""`, `null`, `undefined`, `false`, or `NaN`.

**fall-through**
The behavior in a `switch` statement where execution continues into subsequent cases because no `break` statement stops it.

**if statement**
A selection statement that runs a block of code only when a condition is true.

**logical operator**
An operator such as `&&`, `||`, or `!` used to combine or modify conditions.

**nested if**
An `if` statement placed inside another `if` statement.

**selection statement**
A control structure that chooses among alternative paths of execution.

**strict equality**
Comparison using `===`, which checks both value and type.

**switch statement**
A selection statement that compares one expression against multiple possible exact values.

**truthy**
A value that JavaScript treats as `true` in a Boolean context.

