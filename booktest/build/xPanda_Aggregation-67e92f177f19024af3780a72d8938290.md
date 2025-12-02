# Panda Aggregation

## **Explanation of Each Function**

1. **`df.mean()`**:
   - Calculates the average (mean) of numeric columns.
   - Ignores non-numeric columns and missing values (NaN) by default.
1. **`df.sum()`**:
   - Computes the sum of numeric columns.
   - Ignores non-numeric columns and missing values by default.
1. **`df.count()`**:
   - Counts the number of non-NA/null entries in each column.
1. **`df.min()` / `df.max()`**:
   - Finds the minimum/maximum value for each column. Use `numeric_only=True` to include only numeric columns.
1. **`df.median()`**:
   - Calculates the median of numeric columns, ignoring NaN values.
1. **`df.mode()`**:
   - Finds the mode(s) (most frequent value) for each column. If multiple values are modes, all are returned.

```python
# Panda Data Aggregation

import pandas as pd
import numpy as np

# Create sample data
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Age': [25, 30, 35, 40, np.nan],
    'Salary': [70000, 80000, 120000, 90000, 75000],
    'Department': ['HR', 'Finance', 'HR', 'IT', 'Finance']
}

# Create a DataFrame
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("\n")

# ------------------------------
# 1. df.mean(): Compute the mean of numeric columns
# ------------------------------
print("Mean of numeric columns:")
print(df.mean(numeric_only=True))  # Excludes non-numeric columns
print("\n")

# ------------------------------
# 2. df.sum(): Compute the sum of numeric columns
# ------------------------------
print("Sum of numeric columns:")
print(df.sum(numeric_only=True))
print("\n")

# ------------------------------
# 3. df.count(): Count non-NA/null entries in each column
# ------------------------------
print("Count of non-NA/null entries in each column:")
print(df.count())
print("\n")

# ------------------------------
# 4. df.min() / df.max(): Find the minimum and maximum values
# ------------------------------
print("Minimum values of numeric columns:")
print(df.min(numeric_only=True))
print("\n")

print("Maximum values of numeric columns:")
print(df.max(numeric_only=True))
print("\n")

# ------------------------------
# 5. df.median(): Compute the median of numeric columns
# ------------------------------
print("Median of numeric columns:")
print(df.median(numeric_only=True))
print("\n")

# ------------------------------
# 6. df.mode(): Find the mode(s) of columns
# ------------------------------
print("Mode of each column:")
print(df.mode())
print("\n")

'''
OUTPUT
Original DataFrame:
      Name   Age  Salary Department
0    Alice  25.0   70000         HR
1      Bob  30.0   80000    Finance
2  Charlie  35.0  120000         HR
3    David  40.0   90000         IT
4      Eve   NaN   75000    Finance


Mean of numeric columns:
Age          32.5
Salary    87000.0
dtype: float64


Sum of numeric columns:
Age          130.0
Salary    435000.0
dtype: float64


Count of non-NA/null entries in each column:
Name          5
Age           4
Salary        5
Department    5
dtype: int64


Minimum values of numeric columns:
Age          25.0
Salary    70000.0
dtype: float64


Maximum values of numeric columns:
Age           40.0
Salary    120000.0
dtype: float64


Median of numeric columns:
Age          32.5
Salary    80000.0
dtype: float64


Mode of each column:
      Name   Age  Salary Department
0    Alice  25.0   70000    Finance
1      Bob  30.0   75000         HR
2  Charlie  35.0   80000        NaN
3    David  40.0   90000        NaN
4      Eve   NaN  120000        NaN

'''
```

