# Panel Data - Pandas



The name **Pandas** in Python is derived from the term **"Panel Data"**, which refers to multidimensional structured datasets commonly used in statistics and econometrics. It is not strictly an acronym but rather a nod to the library's functionality for handling such data.

The official definition and purpose of Pandas in Python can be summarized as follows:

- **Definition:** Pandas is an open-source data manipulation and analysis library for Python, providing data structures and operations for manipulating numerical tables, time series, and other structured data formats.

While "Pandas" is often written as though it were an acronym, it is more of a convenient and memorable name linked to its ability to work with **panel data**. It also aligns with the library's playful and accessible branding, making it one of the most recognizable Python libraries.

Python's **Pandas** library provides a vast array of functions for data manipulation and analysis. Below are some of the **main functions** commonly used in Pandas, organized by their purpose:



## **Data Creation in Pandas**

### **1. `pd.Series()`**

The `pd.Series()` function in Pandas is used to create a **one-dimensional labeled array** that can hold data of any type (e.g., integers, floats, strings, etc.). A **Series** is similar to a column in a table or a list in Python, but with **indexing** capabilities.

#### **Key Points:**

- A Series has two components:
  - **Data**: The values you want to store (e.g., numbers, strings, etc.).
  - **Index**: The labels for each data point (default is integer-based, starting from 0).

#### **Example:**

```python
import pandas as pd

# Creating a Series from a list
s = pd.Series([10, 20, 30, 40])
print(s)
```

**Output:**

```
0    10
1    20
2    30
3    40
dtype: int64
```

#### **Specifying Custom Index:**

```python
s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])
print(s)
```

**Output:**

```
a    10
b    20
c    30
d    40
dtype: int64
```

#### **Using a Dictionary:**

```python
data = {'a': 10, 'b': 20, 'c': 30}
s = pd.Series(data)
print(s)
```

**Output:**

```
a    10
b    20
c    30
dtype: int64
```

------

#### **2. `pd.DataFrame()`**

The `pd.DataFrame()` function is used to create a **two-dimensional labeled table** (DataFrame), similar to an Excel spreadsheet or a SQL table. A DataFrame is made up of **rows** and **columns** with both row and column labels.

##### **Key Points:**

- A **DataFrame** is essentially a collection of Series (columns) sharing the same index (rows).
- It can be created from various data structures like dictionaries, lists of lists, NumPy arrays, etc.

#### **Example: Creating a DataFrame from a Dictionary**

```python
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35],
        'City': ['New York', 'Los Angeles', 'Chicago']}
df = pd.DataFrame(data)
print(df)
```

**Output:**

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

#### **Specifying a Custom Index:**

```python
df = pd.DataFrame(data, index=['a', 'b', 'c'])
print(df)
```

**Output:**

```
      Name  Age         City
a    Alice   25     New York
b      Bob   30  Los Angeles
c  Charlie   35      Chicago
```

#### **Creating a DataFrame from a List of Lists:**

```python
data = [['Alice', 25, 'New York'], 
        ['Bob', 30, 'Los Angeles'], 
        ['Charlie', 35, 'Chicago']]
df = pd.DataFrame(data, columns=['Name', 'Age', 'City'])
print(df)
```

**Output:**

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

------

#### **Comparison:**

| Function         | Data Structure   | Dimensionality | Use Case                                                     |
| ---------------- | ---------------- | -------------- | ------------------------------------------------------------ |
| `pd.Series()`    | 1D labeled array | 1-dimensional  | Best for single columns of data with labels (like a single variable). |
| `pd.DataFrame()` | 2D labeled table | 2-dimensional  | Best for tabular data with rows and columns.                 |

These functions are fundamental building blocks for working with data in Pandas.





------

## **1. Data Creation**

- **`pd.Series()`**: Creates a one-dimensional labeled array (Series).
- **`pd.DataFrame()`**: Creates a two-dimensional labeled table (DataFrame).

------

## **2. Data Input/Output (I/O)**

- **`pd.read_csv()`**: Reads data from a CSV file into a DataFrame.
- **`pd.to_csv()`**: Exports a DataFrame to a CSV file.
- **`pd.read_excel()`**: Reads data from an Excel file into a DataFrame.
- **`pd.to_excel()`**: Exports a DataFrame to an Excel file.
- **`pd.read_json()`**: Reads JSON data into a DataFrame.
- **`pd.read_sql()`**: Reads data from an SQL database into a DataFrame.

------

## **3. Data Inspection**

- **`df.head(n)`**: Returns the first `n` rows (default: 5).
- **`df.tail(n)`**: Returns the last `n` rows (default: 5).
- **`df.info()`**: Provides a summary of the DataFrame, including data types and non-null counts.
- **`df.describe()`**: Generates descriptive statistics for numeric columns.
- **`df.shape`**: Returns the dimensions (rows, columns) of the DataFrame.
- **`df.dtypes`**: Lists the data types of each column.

------

## **4. Data Selection**

- **`df['column_name']`**: Accesses a single column as a Series.
- **`df[['col1', 'col2']]`**: Accesses multiple columns as a DataFrame.
- **`df.iloc[]`**: Selects rows/columns by index positions.
- **`df.loc[]`**: Selects rows/columns by labels or conditions.

------

### **5. Data Cleaning**

- **`df.isnull()`**: Detects missing values.
- **`df.notnull()`**: Detects non-missing values.
- **`df.fillna(value)`**: Replaces missing values with the specified value.
- **`df.dropna()`**: Drops rows or columns with missing values.
- **`df.replace(old_value, new_value)`**: Replaces specific values in the DataFrame.
- **`df.rename()`**: Renames columns or rows.

------

## **6. Data Transformation**

- **`df.sort_values(by='column')`**: Sorts rows based on the specified column.
- **`df.sort_index()`**: Sorts rows/columns by their index.
- **`df.groupby()`**: Groups data for aggregation or transformation.
- **`df.pivot_table()`**: Creates a pivot table for aggregating data.
- **`df.apply()`**: Applies a custom function to DataFrame rows or columns.
- **`df.astype()`**: Changes the data type of a column.

------

## **7. Data Aggregation**

- **`df.mean()`**: Computes the mean of numeric columns.
- **`df.sum()`**: Computes the sum of numeric columns.
- **`df.count()`**: Counts non-NA/null entries in each column or row.
- **`df.min()`** / **`df.max()`**: Finds the minimum/maximum value.
- **`df.median()`**: Calculates the median of numeric columns.
- **`df.mode()`**: Finds the mode(s) of columns.

------

## **8. Merging and Reshaping**

- **`pd.merge()`**: Merges two DataFrames based on a common column/key.
- **`pd.concat()`**: Concatenates two or more DataFrames along rows or columns.
- **`df.join()`**: Joins DataFrames on their index or a key.
- **`df.melt()`**: Unpivots a DataFrame from wide to long format.
- **`df.pivot()`**: Pivots a DataFrame from long to wide format.

------

## **9. Statistical Operations**

- **`df.corr()`**: Computes correlation between numeric columns.
- **`df.cov()`**: Computes covariance of numeric columns.
- **`df.std()`**: Calculates the standard deviation.
- **`df.var()`**: Computes variance.
- **`df.cumsum()`**: Calculates the cumulative sum.

------

## **10. Time Series Functions**

- **`pd.to_datetime()`**: Converts data to a datetime object.
- **`df.resample()`**: Aggregates time series data.
- **`df.shift()`**: Shifts data by a specified number of periods.

------

These functions make Pandas an extremely versatile tool for handling and analyzing data efficiently.

