# Pandas

- **Pandas** is a Python library that provides fast, flexible, and expressive data structures designed to make working with “relational” or “labeled” data both easy and intuitive. It is built on top of the NumPy library and is particularly well-suited for working with tabular data, such as spreadsheets or SQL tables.

-  Pandas introduces two new data structures to Python - **Series** and **DataFrame** - both of which are built on top of NumPy.

- **Pandas DataFrames** are two-dimensional, size-mutable, tabular data structures with labeled axes (rows and columns) 1. They are built on top of the NumPy library and are designed to handle a wide range of data manipulation tasks, such as filtering, reshaping, merging, and pivoting data 1.

  A **DataFrame** is composed of three main components: the **data**, the **index**, and  **columns**. The data is stored in a two-dimensional array-like structure, while the index is an array of labels that represent the rows of the **DataFrame**. The columns are an array of labels that represent the columns of the **DataFrame**.

- **Pandas Series** is a one-dimensional labeled array-like object that can hold data of any type.  A Pandas **Series** consists of two main components: the **data** and the **index**. The **data** is stored in a one-dimensional array-like structure, while the index is an array of labels that represent the rows of the Series 


---

## Common Panda Functions

Pandas are a powerful library that provides a wide range of functions for data manipulation in Python. Here are some of the most commonly used functions:

- **read_csv**(): Load data from a CSV file.
- **fillna**(): Replace missing values in a DataFrame.
- **max**(): Calculate the max of a Series or DataFrame.
- **mean**(): Calculate the mean of a Series or DataFrame.
- **min**(): Calculate the min of a Series or DataFrame.
- **std**(): Calculate the standard deviation of a Series or DataFrame.
- **value_counts**(): Count unique values in a Series.
- **groupby**(): Group DataFrame or Series using a mapper or by a Series of columns.
- **loc**[]: Access a group of rows and columns by label(s) or a Boolean array.
- **iloc**[]: Access a group of rows and columns by integer position(s).
- **unique**(): Return unique values in a Series.
- **nunique**(): Return the number of unique elements in a Series.
- **cut**(): Bin values into discrete intervals.
- **qcut**(): Quantile-based discretization function .
- **merge**(): Merge DataFrame or named Series objects with a database-style join.
- **concat**(): Concatenate pandas objects along a particular axis.





---

## loc and iloc

In pandas, `loc` and `iloc` are two crucial methods for accessing and manipulating data in DataFrames. While they seemingly achieve similar tasks, they differ in their approach and have distinct strengths and weaknesses. Here's a breakdown of their key differences:



**Indexing method:**

- **loc:** Uses labels (row/column names) to select data. This is intuitive and easy to understand, especially for data exploration and analysis.
- **iloc:** Uses integer positions (indices) to select data. This is more efficient for specific indexing tasks like slicing or iterating through rows/columns.

**Error handling:**

* **loc:** Raises a `KeyError` if the label doesn't exist in the DataFrame. This can be helpful for catching errors in data manipulation.

- **iloc:** Raises an `IndexError` if the integer position doesn't exist in the DataFrame. This can be silent if you're not expecting a specific index, leading to unexpected results.

**Adding/modifying data:**

- **loc:** Can add new rows/columns based on labels, even if they don't exist initially. This makes it flexible for data manipulation.
- **iloc:** Can only modify existing data based on integer positions. It cannot add new rows/columns directly.



**Here's a table summarizing the key differences:**

| Feature               | loc                        | iloc                                        |
| --------------------- | -------------------------- | ------------------------------------------- |
| Indexing method       | Labels (row/column names)  | Integer positions (indices)                 |
| Error handling        | Key error                  | Index error                                 |
| Adding/modifying data | Can add new rows/columns   | Can only modify existing data               |
| Best for              | Data exploration, analysis | Specific indexing tasks, slicing, iteration |



**Choosing the right method depends on your specific needs:**

- Use **loc** when:
  - You want to select data based on labels/names for easier understanding.
  - You need to add new rows/columns to your DataFrame.
  - You want to catch errors related to invalid labels.
- Use **iloc**  when:
  - You need efficient indexing based on specific positions.
  - You are slicing or iterating through rows/columns.
  - You know the exact positions of the data you need.

---

### idxmax()

In pandas, `idxmax()` is a method used to find the index of the maximum value in a DataFrame or Series. It comes in handy for various data analysis tasks involving finding the top values or entries in your data.

Here's a breakdown of what `idxmax()` does:

* **Returns**: It returns a Series containing the index labels for the maximum values in each specified axis.

- **Axis:** By default, it searches for the maximum values **across each column** (axis=0). You can specify `axis=1` to find the maximum for each **row** instead.
- **NA values:** `idxmax()` automatically excludes null/NA values when searching for the maximum.



### idxmin()

In pandas, `idxmin()` is the twin brother of `idxmax()`, but instead of finding the maximum values, it finds the **minimum values** in your data. It's another handy tool for data analysis tasks involving identifying the bottom values or entries.

Here's what you need to know about `idxmin()`:

* **Returns**: Similar to `idxmax()`, it returns a Series containing the **index labels** for the minimum values in each specified axis.

- **Axis:** By default, it searches for the minimums **across each column** (axis=0). You can specify `axis=1` to find the minimum for each **row** instead.
- **NA values:** Just like its partner, `idxmin()` automatically excludes null/NA values when searching for the minimum.



