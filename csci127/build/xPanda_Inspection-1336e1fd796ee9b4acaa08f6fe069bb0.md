# Panda Inspection



## **Explanation of Each Function**

1. **`df.head(n)`**: Displays the first `n` rows of the DataFrame. If `n` is not specified, it defaults to 5.
1. **`df.tail(n)`**: Displays the last `n` rows of the DataFrame. If `n` is not specified, it defaults to 5.
1. **`df.info()`**: Provides a concise summary of the DataFrame, including the number of non-null values, data types of each column, and memory usage.
1. **`df.describe()`**: Generates descriptive statistics (e.g., mean, standard deviation, min, max) for all numeric columns.
1. **`df.shape`**: Returns the dimensions of the DataFrame as a tuple `(number of rows, number of columns)`.
1. **`df.dtypes`**: Displays the data type of each column in the DataFrame.





```python
import pandas as pd

# Create sample data
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Age': [25, 30, 35, 40, 22],
    'City': ['New York', 'Los Angeles', 'Chicago', 'Houston', 'Phoenix'],
    'Salary': [70000, 80000, 120000, 90000, 75000]
}

# Create a DataFrame
df = pd.DataFrame(data)

# ------------------------------
# Data Inspection Functions
# ------------------------------

# 1. df.head(n): First `n` rows (default: 5)
print("First 3 rows of the DataFrame:")
print(df.head(3))
print("\n")

# 2. df.tail(n): Last `n` rows (default: 5)
print("Last 2 rows of the DataFrame:")
print(df.tail(2))
print("\n")

# 3. df.info(): Summary of the DataFrame
print("DataFrame Info:")
print(df.info())
print("\n")

# 4. df.describe(): Descriptive statistics for numeric columns
print("Descriptive Statistics:")
print(df.describe())
print("\n")

# 5. df.shape: Dimensions of the DataFrame (rows, columns)
print("Shape of the DataFrame:")
print(df.shape)
print("\n")

# 6. df.dtypes: Data types of each column
print("Data Types of Each Column:")
print(df.dtypes)
print("\n")

'''
OUTPUT

First 3 rows of the DataFrame:
      Name  Age         City  Salary
0    Alice   25     New York   70000
1      Bob   30  Los Angeles   80000
2  Charlie   35      Chicago  120000


Last 2 rows of the DataFrame:       
    Name  Age     City  Salary      
3  David   40  Houston   90000      
4    Eve   22  Phoenix   75000      


DataFrame Info:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5 entries, 0 to 4
Data columns (total 4 columns):
 #   Column  Non-Null Count  Dtype
---  ------  --------------  -----
 0   Name    5 non-null      object
 1   Age     5 non-null      int64
 2   City    5 non-null      object
 3   Salary  5 non-null      int64
dtypes: int64(2), object(2)
memory usage: 292.0+ bytes
None


Descriptive Statistics:
             Age         Salary
count   5.000000       5.000000
mean   30.400000   87000.000000
std     7.300685   19874.606914
min    22.000000   70000.000000
25%    25.000000   75000.000000
50%    30.000000   80000.000000
75%    35.000000   90000.000000
max    40.000000  120000.000000


Shape of the DataFrame:
(5, 4)


Data Types of Each Column:
Name      object
Age        int64
City      object
Salary     int64
dtype: object

'''
```

