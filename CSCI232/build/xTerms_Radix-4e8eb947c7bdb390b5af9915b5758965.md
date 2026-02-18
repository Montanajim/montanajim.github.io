# Radix - Number Bases



In the context of coding, **radix** (also sometimes called **base**) refers to the **number of unique digits used to represent numbers** in a **positional numeral system**. Here's a breakdown:

**Positional Numeral System:**

This is a system in which the **value of a digit depends on its position within the number**. The most common example is the **decimal system** used in everyday life, where we have 10 digits (0-9) and the position of a digit determines its value by powers of 10. For example, in the number 123, the "1" represents 1 x 10^2 (100), the "2" represents 2 x 10^1 (20), and the "3" represents 3 x 10^0 (3).

**Radix and Digits:**

The **radix** of a system defines the number of unique digits used. So, the decimal system has a radix of **10** because it uses 10 digits. Other common systems include:

- **Binary (base 2):** Uses only 2 digits (0 and 1).
- **Octal (base 8):** Uses 8 digits (0-7).
- **Hexadecimal (base 16):** Uses 16 digits (0-9, A-F).

**Why Radix Matters in Coding:**

Understanding radix is crucial in several coding aspects:

- **Converting between different numeral systems:** Programmers often need to convert between different bases, for example, from decimal to binary (common in computer hardware) or vice versa. Knowing the radix is essential for performing these conversions accurately.
- **Data representation:** Numbers in memory are often stored in binary format using a specific number of bits. Understanding radix allows programmers to interpret and manipulate these binary representations.
- **Error checking:** Some error checking techniques rely on calculating checksums or hash values based on specific radices. Understanding the radix used in these calculations is essential for interpreting the results.
- **Communication protocols:** Sometimes, data is exchanged between systems using different radices (e.g., ASCII uses base-10 for characters). Knowing the radices involved is crucial for proper data transmission and interpretation.

**In summary, understanding radix is a fundamental concept in coding, as it forms the foundation for representing, manipulating, and interpreting numerical data in various contexts.**



 For example:

- In the **decimal system** (the most common system), the radix is **ten**, as it uses the ten digits from 0 through 9.

- In **hexadecimal** (base-16), the radix is **sixteen**, allowing digits from 0 to 15 (where A represents 10, B represents 11, and so on).

- When you perform operations like **parsing integers** or **converting numbers to strings**, the radix determines how the numbers are interpreted or displayed

   For instance:

  - `Integer.parseInt("11", 16)` interprets “11” as a base-16 number, resulting in **17** (1*16 + 1).
  - `Integer.toString(11, 16)` converts the decimal value 11 to hexadecimal, resulting in **B**.