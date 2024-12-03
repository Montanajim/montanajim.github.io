# Panda Statistical Operations

## **Explanation of Each Function**

1. **`df.corr()`**:
   - Calculates the pairwise correlation between numeric columns.
   - Correlation values range from -1 (perfect negative correlation) to 1 (perfect positive correlation).
1. **`df.cov()`**:
   - Computes the covariance matrix for numeric columns.
   - Covariance measures how changes in one variable are associated with changes in another.
1. **`df.std()`**:
   - Calculates the standard deviation for each numeric column.
   - The standard deviation measures the amount of variation or dispersion from the mean.
1. **`df.var()`**:
   - Computes the variance for each numeric column.
   - Variance measures the average squared deviation from the mean.
1. **`df.cumsum()`**:
   - Calculates the cumulative sum of numeric columns.
   - Each entry in a column is replaced with the sum of all previous entries up to that point.

```python
# Panda Statistical Operations

import pandas as pd

# Create sample data
data = {
    'ID': [1, 2, 3, 4, 5],
    'Age': [25, 30, 35, 40, 45],
    'Salary': [70000, 80000, 120000, 90000, 75000],
    'Experience': [1, 3, 5, 7, 9]
}

# Create a DataFrame
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("\n")

# ------------------------------
# 1. df.corr(): Compute correlation between numeric columns
# ------------------------------
print("Correlation between numeric columns:")
print(df.corr())
print("\n")

# ------------------------------
# 2. df.cov(): Compute covariance between numeric columns
# ------------------------------
print("Covariance between numeric columns:")
print(df.cov())
print("\n")

# ------------------------------
# 3. df.std(): Calculate standard deviation of numeric columns
# ------------------------------
print("Standard deviation of numeric columns:")
print(df.std())
print("\n")

# ------------------------------
# 4. df.var(): Compute variance of numeric columns
# ------------------------------
print("Variance of numeric columns:")
print(df.var())
print("\n")

# ------------------------------
# 5. df.cumsum(): Calculate cumulative sum for numeric columns
# ------------------------------
print("Cumulative sum of numeric columns:")
print(df.cumsum())
print("\n")


'''
OUTPUT
Original DataFrame:
   ID  Age  Salary  Experience
0   1   25   70000           1
1   2   30   80000           3
2   3   35  120000           5
3   4   40   90000           7
4   5   45   75000           9


Correlation between numeric columns:
                  ID       Age    Salary  Experience
ID          1.000000  1.000000  0.159111    1.000000
Age         1.000000  1.000000  0.159111    1.000000
Salary      0.159111  0.159111  1.000000    0.159111
Experience  1.000000  1.000000  0.159111    1.000000


Covariance between numeric columns:
                ID      Age       Salary  Experience
ID             2.5     12.5       5000.0         5.0
Age           12.5     62.5      25000.0        25.0
Salary      5000.0  25000.0  395000000.0     10000.0
Experience     5.0     25.0      10000.0        10.0


Standard deviation of numeric columns:
ID                1.581139
Age               7.905694
Salary        19874.606914
Experience        3.162278
dtype: float64


Variance of numeric columns:
ID                    2.5
Age                  62.5
Salary        395000000.0
Experience           10.0
dtype: float64


Cumulative sum of numeric columns:
   ID  Age  Salary  Experience
0   1   25   70000           1
1   3   55  150000           4
2   6   90  270000           9
3  10  130  360000          16
4  15  175  435000          25
'''
```





