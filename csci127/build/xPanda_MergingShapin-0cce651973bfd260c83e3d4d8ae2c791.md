# Panda Merging and Shaping

## **Explanation of Each Operation**

1. **`pd.merge()`**:
   - Merges two DataFrames on a common column or key.
   - Example: `merged_df` combines `df1` and `df2` on the `ID` column using an inner join.
1. **`pd.concat()`**:
   - Concatenates two or more DataFrames along rows (`axis=0`) or columns (`axis=1`).
   - Example: `concat_rows` stacks `df1` and `df2` vertically, while `concat_columns` appends `df2` as additional columns to `df1`.
1. **`df.join()`**:
   - Joins two DataFrames based on their indices.
   - Example: `joined_df` joins `df1_indexed` and `df3_indexed` on their index values.
1. **`df.melt()`**:
   - Converts a DataFrame from wide format to long format by unpivoting columns.
   - Example: `melted_df` turns `Name` and `Age` columns into rows with corresponding values.
1. **`df.pivot()`**:
   - Converts a DataFrame from long format to wide format by pivoting on a specified column.
   - Example: `pivoted_df` pivots `melted_df` back to wide format with `Name` and `Age` as columns.

```python
# Panda Merging and Shaping

import pandas as pd

# Create sample DataFrames for demonstration
df1 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35]
})

df2 = pd.DataFrame({
    'ID': [2, 3, 4],
    'City': ['New York', 'Chicago', 'Los Angeles'],
    'Salary': [80000, 120000, 75000]
})

df3 = pd.DataFrame({
    'Department': ['HR', 'Finance', 'IT'],
    'Head': ['Alice', 'David', 'Charlie']
})

# ------------------------------
# 1. pd.merge(): Merge two DataFrames on a common column
# ------------------------------
print("Merging df1 and df2 on 'ID':")
merged_df = pd.merge(df1, df2, on='ID', how='inner')  # Inner join
print(merged_df)
print("\n")

# ------------------------------
# 2. pd.concat(): Concatenate two DataFrames along rows or columns
# ------------------------------
print("Concatenating df1 and df2 along rows:")
concat_rows = pd.concat([df1, df2], axis=0)  # Concatenating rows
print(concat_rows)
print("\n")

print("Concatenating df1 and df2 along columns:")
concat_columns = pd.concat([df1, df2], axis=1)  # Concatenating columns
print(concat_columns)
print("\n")

# ------------------------------
# 3. df.join(): Join two DataFrames on their index
# ------------------------------
print("Joining df1 and df3 by index:")
df1_indexed = df1.set_index('Name')
df3_indexed = df3.set_index('Head')
joined_df = df1_indexed.join(df3_indexed, how='left')
print(joined_df)
print("\n")

# ------------------------------
# 4. df.melt(): Unpivot a DataFrame from wide to long format
# ------------------------------
print("Melting df1 to long format:")
melted_df = pd.melt(df1, id_vars=['ID'], value_vars=['Name', 'Age'], var_name='Attribute', value_name='Value')
print(melted_df)
print("\n")

# ------------------------------
# 5. df.pivot(): Pivot a DataFrame from long to wide format
# ------------------------------
print("Pivoting melted_df back to wide format:")
pivoted_df = melted_df.pivot(index='ID', columns='Attribute', values='Value')
print(pivoted_df)
print("\n")


'''
Merging df1 and df2 on 'ID':
   ID     Name  Age      City  Salary      
0   2      Bob   30  New York   80000      
1   3  Charlie   35   Chicago  120000      


Concatenating df1 and df2 along rows:      
   ID     Name   Age         City    Salary
0   1    Alice  25.0          NaN       NaN
1   2      Bob  30.0          NaN       NaN
2   3  Charlie  35.0          NaN       NaN
0   2      NaN   NaN     New York   80000.0
1   3      NaN   NaN      Chicago  120000.0
2   4      NaN   NaN  Los Angeles   75000.0


Concatenating df1 and df2 along columns:
   ID     Name  Age  ID         City  Salary
0   1    Alice   25   2     New York   80000
1   2      Bob   30   3      Chicago  120000
2   3  Charlie   35   4  Los Angeles   75000


Joining df1 and df3 by index:
         ID  Age Department
Name
Alice     1   25         HR
Bob       2   30        NaN
Charlie   3   35         IT


Melting df1 to long format:
   ID Attribute    Value
0   1      Name    Alice
1   2      Name      Bob
2   3      Name  Charlie
3   1       Age       25
4   2       Age       30
5   3       Age       35


Pivoting melted_df back to wide format:
Attribute Age     Name
ID
1          25    Alice
2          30      Bob
3          35  Charlie
'''
```

