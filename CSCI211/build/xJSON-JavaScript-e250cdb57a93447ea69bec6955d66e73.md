# JSON — Structured Data for Modern Programs

## Introduction

Programs rarely live alone. A browser exchanges data with a server. A mobile app stores user preferences. A web service returns weather data, product information, or search results. In each of these cases, software must move structured information from one place to another in a form that both sides can understand. JSON exists to solve that problem.

JSON, or JavaScript Object Notation, gives programs a compact, readable, language-independent way to represent structured data as text. Although its roots lie in JavaScript, JSON now appears across nearly every area of computing. It serves as the common tongue of APIs, configuration files, web applications, and cloud services. A computer science student who understands JSON gains access to one of the most practical and widely used data formats in software development.

This chapter explains what JSON is, why it was created, what it looks like, how programs use it, and what can go wrong when developers handle it carelessly. The topic may appear simple at first glance, but beginners often confuse JSON with JavaScript objects, misunderstand its syntax rules, or misuse parsing and serialization functions. Those mistakes produce real bugs. This chapter addresses them directly.

## Chapter at a Glance

This chapter introduces JSON as a text-based data format for representing structured information. It explains the historical need for a lightweight alternative to older formats, presents the syntax and structure of JSON values, and shows how programs convert data to and from JSON. It also examines common errors, debugging strategies, and the differences between JSON and related ideas such as JavaScript object literals and XML.

## Learning Goals

By the end of this chapter, you should be able to explain why JSON was created, describe the syntax of valid JSON, distinguish JSON from JavaScript objects, convert data to and from JSON in code, identify common parsing and formatting errors, and apply sound practices when working with JSON in programs.

## What This Concept Is

JSON is a **text format for representing structured data**. It organizes data using key-value pairs, arrays, numbers, strings, Boolean values, and `null`. Because JSON is text, a program can store it in a file, send it across a network, or read it from a database or API response.

A JSON document does not contain executable code. It contains data only. That design is a strength. It makes JSON portable, predictable, and easier to process safely than formats that mix data with behavior.

### Definition

**JSON (JavaScript Object Notation):** a language-independent text format used to represent structured data as objects, arrays, strings, numbers, Boolean values, and `null`.

## Why This Concept Matters

JSON matters because modern programs constantly exchange data. A client sends login information to a server. A server returns user details. A web page requests a list of products. A configuration file defines settings for an application. In each case, software needs a shared representation for data.

Before JSON became dominant, developers often used XML for structured data exchange. XML is powerful, but it is verbose. It requires opening and closing tags, and its syntax tends to become heavy for ordinary application data. JSON offered a leaner alternative. It was easier for humans to read, easier for machines to generate, and especially convenient for JavaScript programs in browsers.

JSON won because it fit the practical needs of real software development. It is compact, expressive enough for common data structures, and widely supported across programming languages.

### Key Point

JSON is not important because it is elegant theory. JSON is important because it is the format that real programs use every day.

## Why JSON Was Created

JSON emerged from the need for a lightweight data interchange format. As web applications became more dynamic, programs needed a simpler way to exchange structured data between browsers and servers. Existing approaches often involved XML, which carried significant syntactic overhead.

Douglas Crockford helped popularize JSON in the early 2000s as a simpler, cleaner alternative. The format borrowed ideas from JavaScript object notation because JavaScript already had a natural way to represent structured data with objects and arrays. The result was a format that browsers could interpret easily and servers could generate without much effort.

The core idea was straightforward: represent data as plain text using a small set of consistent rules. Keep the syntax simple. Exclude executable behavior. Focus on portability and interoperability.

That choice shaped JSON’s success. It did not try to do everything. It tried to do one thing well: carry data cleanly between systems.

## What JSON Looks Like

At first glance, JSON looks very similar to a JavaScript object literal. That similarity helps, but it also causes confusion. Consider the following example:

```
{
  "name": "Elena",
  "age": 20,
  "major": "Computer Science",
  "isFullTime": true
}
```

This example contains an object with four properties. Each property name appears in double quotes. Each property has a value. The values include a string, a number, and a Boolean.

JSON can also contain arrays:

```
[
  "red",
  "green",
  "blue"
]
```

And it can combine objects and arrays:

```
{
  "course": "CSCI 211",
  "students": [
    {
      "name": "Elena",
      "year": 2
    },
    {
      "name": "Marcus",
      "year": 1
    }
  ]
}
```

These examples illustrate the small but powerful vocabulary of JSON.

## Syntax and Basic Form

JSON supports exactly six kinds of values:

1. objects
2. arrays
3. strings
4. numbers
5. Booleans
6. `null`

An **object** is a collection of key-value pairs enclosed in curly braces.

```
{
  "city": "Kalispell",
  "state": "Montana"
}
```

An **array** is an ordered list of values enclosed in square brackets.

```
[
  "apple",
  "banana",
  "orange"
]
```

A **string** must appear in double quotes.

```
"hello"
```

A **number** can be an integer or floating-point value.

```
42
3.14159
-7
```

A **Boolean** is either `true` or `false`.

```
true
false
```

The value **`null`** represents the intentional absence of a value.

```
null
```

The syntax rules are strict. JSON does not permit comments. JSON does not allow trailing commas. JSON requires double quotes for property names and string values.

### Warning

Students often assume that anything that looks like a JavaScript object is valid JSON. That assumption is false. JSON is stricter than JavaScript object notation.

## Core Behavior

Programs usually work with JSON in two major directions.

First, a program may take an internal data structure, such as an object in memory, and convert it into JSON text. This process is called **serialization**.

Second, a program may receive JSON text and convert it into an internal data structure it can use. This process is called **parsing** or **deserialization**, depending on context.

In JavaScript, the built-in `JSON` object provides two essential methods:

`JSON.stringify()` converts a JavaScript value into a JSON string.

`JSON.parse()` converts a JSON string into a JavaScript value.

Here is the basic pattern:

```
const student = {
  name: "Elena",
  age: 20,
  major: "Computer Science"
};

const jsonText = JSON.stringify(student);
console.log(jsonText);

const parsedStudent = JSON.parse(jsonText);
console.log(parsedStudent.name);
```

Execution proceeds in a clear order. The program first creates a JavaScript object in memory. It then serializes that object into a string of JSON text. Later, it parses that JSON text back into a JavaScript object. At the end, the program accesses a property from the parsed object.

The crucial point is this: the JSON string is text. The parsed result is a JavaScript object. They are not the same thing, even when they look similar.

## Key Terminology

A student working with JSON should know the following terms precisely.

**Serialization:** the process of converting an in-memory data structure into a text representation such as JSON.

**Parsing:** the process of analyzing text and converting it into a usable internal data structure.

**Deserialization:** the process of reconstructing a data structure from a serialized format.

**Key-value pair:** a property name paired with a corresponding value, commonly used inside an object.

**Schema:** an expected structure or pattern for data, including required fields, types, and nesting rules.

## Simple Example

Consider a program that stores information about a book.

```
const book = {
  title: "Data Structures in Practice",
  author: "R. Lopez",
  pages: 384,
  available: true
};

const jsonBook = JSON.stringify(book);
console.log(jsonBook);

const restoredBook = JSON.parse(jsonBook);
console.log(restoredBook.title);
```

The output from `JSON.stringify(book)` will be a JSON string similar to this:

```
{"title":"Data Structures in Practice","author":"R. Lopez","pages":384,"available":true}
```

This example shows the essential workflow. The program begins with a JavaScript object. It converts the object to JSON text. Then it converts the JSON text back into a JavaScript object.

The string is suitable for storage or transmission. The parsed object is suitable for computation.

## Detailed Walkthrough

Now consider a slightly richer example involving an API-style response.

```
const responseText = `
{
  "course": "CSCI 211",
  "semester": "Fall 2026",
  "students": [
    {
      "name": "Ava",
      "gpa": 3.8
    },
    {
      "name": "Noah",
      "gpa": 3.4
    }
  ]
}
`;

const courseData = JSON.parse(responseText);

console.log(courseData.course);
console.log(courseData.students[0].name);
console.log(courseData.students[1].gpa);
```

Let us walk through the execution carefully.

The variable `responseText` stores a string. That string happens to contain JSON text. At this moment, the program does not yet have a nested JavaScript object structure it can navigate with dot notation. It merely has text.

Next, `JSON.parse(responseText)` reads the string and interprets it according to JSON syntax rules. If the syntax is valid, the method returns a JavaScript object. That returned object contains properties such as `course`, `semester`, and `students`.

The `students` property holds an array. The first element of that array is an object representing Ava. The second element is an object representing Noah.

After parsing, the program can use ordinary JavaScript access:

`courseData.course` retrieves the course name.
 `courseData.students[0].name` retrieves the first student’s name.
 `courseData.students[1].gpa` retrieves the second student’s GPA.

This execution order matters. If you try to access `responseText.course`, the result will be `undefined`, because `responseText` is just a string. The parse must happen first.

### Checkpoint

Before parsing, do you have structured program data or plain text?
 You have plain text. That distinction drives everything else.

## Behind the Scenes

Although JSON appears simple, parsing and serialization involve real work.

When a parser reads JSON text, it processes the text character by character according to a formal grammar. It checks whether braces and brackets match. It verifies that strings begin and end properly. It recognizes numbers, Booleans, and `null`. It enforces commas and colons in the correct places. If any rule fails, the parser throws an error.

When a serializer converts an object to JSON, it traverses the structure of that object. It writes opening braces for objects, square brackets for arrays, quoted strings for property names, and correctly formatted literal values for numbers and Booleans.

However, not every JavaScript value converts cleanly to JSON. Functions do not belong in JSON. Values such as `undefined` behave differently from ordinary values during serialization. Some objects, such as those with circular references, cannot be serialized by standard `JSON.stringify()` at all.

That limitation is not a bug. JSON was designed to represent data, not arbitrary program state.

## JSON and JavaScript Objects

The resemblance between JSON and JavaScript object literals causes one of the most common beginner mistakes. They look similar, but they are not identical.

A JavaScript object literal may appear like this:

```
const user = {
  name: "Ava",
  age: 21,
  greet() {
    console.log("Hello");
  }
};
```

This is valid JavaScript, but it is not valid JSON. JSON would reject the method entirely, and it would also require quotes around all property names.

Here is valid JSON representing similar data:

```
{
  "name": "Ava",
  "age": 21
}
```

### Comparison

**JavaScript object literal**

- lives inside a JavaScript program
- may include methods
- may omit quotes around property names
- may include expressions and more complex syntax

**JSON**

- is plain text
- contains data only
- requires double-quoted property names
- follows stricter syntax rules

This difference matters in practice. Students often paste a JavaScript object literal into a context that expects JSON and then wonder why parsing fails. The parser is correct. The syntax is wrong.

## Common Mistakes and Debugging Problems

JSON errors are usually not subtle. They tend to fail loudly. That is good. But students still need to know what to look for.

### Common Mistake: Using Single Quotes

This is invalid JSON:

```
{
  'name': 'Ava'
}
```

JSON requires double quotes for strings and property names.

Correct form:

```
{
  "name": "Ava"
}
```

### Common Mistake: Leaving a Trailing Comma

This is invalid JSON:

```
{
  "name": "Ava",
  "age": 21,
}
```

Many programming languages permit trailing commas in some contexts. JSON does not.

### Common Mistake: Adding Comments

This is invalid JSON:

```
{
  "name": "Ava"
  // student name
}
```

JSON does not support comments. Developers often want comments in configuration files, but raw JSON does not allow them.

### Common Mistake: Confusing Text with Objects

Consider this code:

```
const jsonText = '{"name":"Ava","age":21}';
console.log(jsonText.name);
```

This code does not work as intended because `jsonText` is a string, not an object. The correct approach is:

```
const jsonText = '{"name":"Ava","age":21}';
const user = JSON.parse(jsonText);
console.log(user.name);
```

### Common Mistake: Expecting Functions in JSON

This is not valid JSON:

```
{
  "name": "Ava",
  "greet": function() {
    console.log("Hello");
  }
}
```

JSON does not represent behavior. It represents data.

### Common Mistake: Ignoring Parse Errors

If JSON text is malformed, `JSON.parse()` throws an error.

```
const badJson = '{"name":"Ava", age:21}';
const user = JSON.parse(badJson);
```

This will fail because `age` is not quoted as a property name.

### Debugging Note

When `JSON.parse()` fails, read the error message carefully. The parser often identifies the approximate position of the problem. That location usually reveals a missing comma, a bad quote, or invalid syntax nearby.

### Debugging Note

When a program receives JSON from an outside source, inspect the raw text before parsing if possible. Developers often assume the server returned valid JSON when the actual problem lies in the response itself.

### Common Mistake: Mishandling `undefined`

Consider this object:

```
const data = {
  name: "Ava",
  score: undefined
};

console.log(JSON.stringify(data));
```

The result will omit the `score` property rather than preserving it as an explicit value. That behavior surprises beginners.

If you need an intentional “no value” marker in JSON, use `null`, not `undefined`.

### Common Mistake: Circular References

```
const person = {};
person.self = person;

JSON.stringify(person);
```

This code throws an error because the object refers to itself. JSON serialization cannot represent circular structures with the standard serializer.

## Comparison to Related Ideas

### Comparison

**JSON vs JavaScript Objects**

JSON is text. JavaScript objects are runtime data structures. They may resemble each other, but JSON must be parsed before code can use it as an object.

**JSON vs XML**

XML uses nested tags and supports a wide range of document-oriented structures. JSON is lighter, less verbose, and easier to map to ordinary programming data structures. XML still matters in some domains, but JSON dominates most modern web APIs.

**JSON vs CSV**

CSV stores tabular data in rows and columns. JSON supports nested objects and arrays. CSV is useful for flat datasets. JSON is better for hierarchical or nested information.

**JSON vs YAML**

YAML aims for human readability and supports configuration scenarios well, but its whitespace-sensitive syntax can create subtle problems. JSON is more rigid and less pleasant to hand-edit, but its rules are clearer and its parsers are widely available.

## Best Practices

When you work with JSON, accuracy matters more than cleverness.

Use valid syntax every time. Quote property names. Use double quotes for strings. Remove trailing commas. Avoid comments in raw JSON.

Treat external JSON as untrusted input. A program should not assume that incoming data has the expected structure or types. Parsing valid JSON does not guarantee meaningful data. A field can exist but still carry the wrong type or a nonsense value.

Use `null` intentionally. Do not rely on `undefined` if the data must survive serialization.

Keep JSON focused on data, not behavior. If your design depends on storing methods, closures, or executable logic, JSON is the wrong format.

Validate important JSON structures. In small programs, a few conditional checks may suffice. In larger systems, schema validation becomes essential.

Format JSON for readability when humans need to inspect it. JavaScript allows pretty-printing with `JSON.stringify(value, null, 2)`.

```
const student = {
  name: "Ava",
  major: "Computer Science",
  year: 2
};

console.log(JSON.stringify(student, null, 2));
```

This version produces indented output that is much easier to read.

### Key Point

A JSON document can be syntactically valid and still be semantically wrong. Correct punctuation does not guarantee correct meaning.

## A More Realistic Example

Consider a program that receives user profile data from a server.

```
const responseText = `
{
  "id": 1042,
  "username": "ajordan",
  "email": "ajordan@example.edu",
  "active": true,
  "roles": ["student", "tutor"]
}
`;

try {
  const profile = JSON.parse(responseText);

  console.log("User ID:", profile.id);
  console.log("Username:", profile.username);
  console.log("First role:", profile.roles[0]);

  const savedText = JSON.stringify(profile, null, 2);
  console.log(savedText);
} catch (error) {
  console.log("Failed to parse JSON:", error.message);
}
```

This example introduces one more important practice: error handling. The `try` block attempts to parse the JSON. If parsing fails, the `catch` block handles the error instead of crashing the entire program without explanation.

Execution order matters here as well. The parser runs first. If parsing succeeds, the program accesses object properties and later serializes the object again for output. If parsing fails, the control flow jumps directly to the `catch` block.

That behavior is exactly what a robust program should do.

## Misconceptions That Beginners Often Carry

Many students think JSON is “just a JavaScript object.” That is wrong. JSON is text.

Many students think a file with braces and colons is automatically JSON. That is also wrong. The syntax must satisfy JSON’s exact rules.

Many students assume that successful parsing means the data is trustworthy. It does not. A parser checks syntax, not domain meaning.

Many students believe JSON can store any program structure. It cannot. JSON handles common data structures, not executable code or arbitrary object graphs.

These misconceptions are common because JSON looks simple. The surface is simple. The bugs are not.

## Key Terms

JSON, object, array, string, number, Boolean, null, serialization, parsing, deserialization, key-value pair, schema, syntax, data interchange, circular reference.

## Chapter Summary

JSON provides a standard way to represent structured data as text. It emerged as a lightweight alternative to heavier data formats and became the dominant format for web APIs, configuration data, and general data interchange.

JSON supports objects, arrays, strings, numbers, Booleans, and `null`. Its syntax is strict: property names must appear in double quotes, comments are not allowed, and trailing commas are invalid.

Programs typically use JSON in two directions. They serialize internal data structures into JSON text for storage or transmission, and they parse JSON text into usable data structures. In JavaScript, `JSON.stringify()` performs serialization and `JSON.parse()` performs parsing.

Students must understand that JSON is not the same as a JavaScript object literal. JSON is text. JavaScript objects are runtime structures. Confusing the two leads to parsing errors, invalid syntax, and faulty assumptions about behavior.

Common problems include single quotes, trailing commas, comments, unquoted property names, misuse of `undefined`, and attempts to serialize circular references. Strong debugging habits, careful validation, and disciplined syntax help prevent these failures.

### Final Takeaway

JSON succeeds because it is narrow, strict, and practical. It does not try to represent everything. It represents data clearly enough that different systems can exchange it reliably. Learn that distinction well, and a great deal of modern programming becomes easier.

## Multiple-Choice Review Questions

1. What is the primary purpose of JSON?
    A. To execute JavaScript code across networks
    B. To represent structured data as text
    C. To replace all database systems
    D. To compress binary files
2. Why was JSON widely adopted in web development?
    A. It stores executable functions efficiently
    B. It is more verbose than XML
    C. It provides a lightweight format for data exchange
    D. It requires no parsing
3. Which of the following is valid JSON?
    A. `{name: "Ava", age: 21}`
    B. `{'name': 'Ava', 'age': 21}`
    C. `{"name": "Ava", "age": 21}`
    D. `{ "name": "Ava", age: 21, }`
4. Which JSON value type represents the intentional absence of a value?
    A. `undefined`
    B. `void`
    C. `empty`
    D. `null`
5. What does `JSON.parse()` do in JavaScript?
    A. Converts a JavaScript object into a JSON string
    B. Converts JSON text into a JavaScript value
    C. Validates network credentials
    D. Formats text for printing
6. What does `JSON.stringify()` do in JavaScript?
    A. Converts a JavaScript value into JSON text
    B. Converts JSON text into an array
    C. Checks whether a file is secure
    D. Adds comments to a JSON document
7. Which of the following is not allowed in standard JSON?
    A. Arrays
    B. Numbers
    C. Functions
    D. Boolean values
8. Why does the following fail?

```
const text = '{"name":"Ava"}';
console.log(text.name);
```

A. Strings cannot contain braces
 B. `text` must be parsed before property access
 C. JSON objects do not support names
 D. The code requires a loop

1. What is a circular reference in the context of JSON serialization?
    A. A string value that repeats
    B. An array with duplicate values
    C. An object structure that refers to itself
    D. A property name that appears twice
2. Which statement best describes the difference between JSON and a JavaScript object literal?
    A. There is no difference
    B. JSON can contain methods, but object literals cannot
    C. JSON is plain text with stricter syntax rules
    D. JavaScript object literals must always be parsed

## Answer Key

1. B
2. C
3. C
4. D
5. B
6. A
7. C
8. B
9. C
10. C

## Glossary

**Array:** An ordered list of values. In JSON, arrays appear inside square brackets.

**Boolean:** A logical value that is either `true` or `false`.

**Circular reference:** A structure in which an object directly or indirectly refers to itself, preventing ordinary JSON serialization.

**Data interchange:** The transfer of structured information between systems or programs.

**Deserialization:** The reconstruction of usable program data from a serialized format such as JSON text.

**JSON:** A text format for representing structured data using objects, arrays, strings, numbers, Boolean values, and `null`.

**Key-value pair:** A property name and its associated value within an object.

**Null:** A special value representing the intentional absence of a value.

**Object:** A collection of named properties. In JSON, objects appear inside curly braces.

**Parse:** To analyze text according to formal rules and convert it into a usable structure.

**Schema:** A formal or informal description of the expected structure and types of data.

**Serialization:** The conversion of in-memory data into a text representation for storage or transmission.

**String:** A sequence of characters enclosed in double quotes in JSON.

**Syntax:** The formal rules that determine whether data or code is written correctly.