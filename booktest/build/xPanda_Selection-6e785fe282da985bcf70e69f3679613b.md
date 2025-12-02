# Panda Selection

## **Explanation of Each Code Block**

1. **`df['column_name']`**:
   - Retrieves a single column as a Series.
   - Example: Access the `Name` column.
1. **`df[['col1', 'col2']]`**:
   - Retrieves multiple columns as a DataFrame.
   - Example: Access the `Name` and `City` columns.
1. **`df.iloc[]`**:
   - Selects rows and columns by integer-based index positions.
   - Example: Select the first 3 rows (index 0 to 2) and columns 1 (`Age`) and 2 (`City`).
1. **`df.loc[]`**:
   - Selects rows and columns by labels or applies conditions.
   - Example 1: Select rows where the `Age` column is greater than 30 and retrieve `Name` and `Salary`.
   - Example 2: Select all columns for a specific row by its index label.



```python
# Data Selection
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
# Data Selection Examples
# ------------------------------

# 1. Access a single column as a Series
print("Accessing the 'Name' column:")
print(df['Name'])
print("\n")

# 2. Access multiple columns as a DataFrame
print("Accessing 'Name' and 'City' columns:")
print(df[['Name', 'City']])
print("\n")

# 3. Select rows/columns by index positions using iloc
print("Selecting specific rows and columns using iloc (rows 0 to 2, columns 1 and 2):")
print(df.iloc[0:3, 1:3])  # Rows 0 to 2, columns 1 to 2
print("\n")

# 4. Select rows/columns by labels or conditions using loc
print("Selecting rows where 'Age' > 30 and specific columns using loc:")
print(df.loc[df['Age'] > 30, ['Name', 'Salary']])  # Rows with Age > 30 and specific columns
print("\n")

print("Selecting a specific row and all columns using loc (row with label 3):")
print(df.loc[3])  # Row with index label 3

'''
OUTPUT
Accessing the 'Name' column:
0      Alice
1        Bob
2    Charlie
3      David
4        Eve
Name: Name, dtype: object


Accessing 'Name' and 'City' columns:
      Name         City
0    Alice     New York
1      Bob  Los Angeles
2  Charlie      Chicago
3    David      Houston
4      Eve      Phoenix


Selecting specific rows and columns using iloc (rows 0 to 2, columns 1 and 2):
   Age         City
0   25     New York
1   30  Los Angeles
2   35      Chicago


Selecting rows where 'Age' > 30 and specific columns using 
loc:
      Name  Salary
2  Charlie  120000
3    David   90000


Selecting a specific row and all columns using loc (row with label 3):
Name        David
Age            40
City      Houston
Salary      90000
Name: 3, dtype: object
'''
```

