#  Panda Data Transformation



## **Explanation of Each Function**

1. **`df.sort_values(by='column')`**:
   - Sorts the DataFrame rows based on the specified column.
   - Example: Sort rows by the `Age` column.
1. **`df.sort_index()`**:
   - Sorts the rows or columns by their index.
   - Example: Sort rows in descending order by their index.
1. **`df.groupby()`**:
   - Groups the data by a specified column and applies aggregation functions (e.g., `mean`, `sum`, etc.).
   - Example: Group data by `Department` and calculate the average `Salary`.
1. **`df.pivot_table()`**:
   - Creates a pivot table to summarize and aggregate data.
   - Example: Show the average `Salary` grouped by `Department` and `City`.
1. **`df.apply()`**:
   - Applies a custom function to each element in a column or row.
   - Example: Increase each `Salary` by 10%.
1. **`df.astype()`**:
   - Changes the data type of a column.
   - Example: Convert the `Age` column to a string type.



```python
# Data Transformation

import pandas as pd

# Create sample data
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'Age': [25, 30, 35, 40, 22],
    'City': ['New York', 'Los Angeles', 'Chicago', 'Houston', 'Phoenix'],
    'Department': ['HR', 'Finance', 'HR', 'IT', 'Finance'],
    'Salary': [70000, 80000, 120000, 90000, 75000]
}

# Create a DataFrame
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("\n")

# ------------------------------
# 1. df.sort_values(by='column'): Sort rows by a specified column
# ------------------------------
print("Sorting rows by 'Age':")
df_sorted = df.sort_values(by='Age')
print(df_sorted)
print("\n")

# ------------------------------
# 2. df.sort_index(): Sort rows by their index
# ------------------------------
print("Sorting rows by index in descending order:")
df_index_sorted = df.sort_index(ascending=False)
print(df_index_sorted)
print("\n")

# ------------------------------
# 3. df.groupby(): Group data for aggregation
# ------------------------------
print("Grouping by 'Department' and calculating mean 'Salary':")
df_grouped = df.groupby('Department')['Salary'].mean()
print(df_grouped)
print("\n")

# ------------------------------
# 4. df.pivot_table(): Create a pivot table
# ------------------------------
print("Creating a pivot table for average 'Salary' by 'Department' and 'City':")
df_pivot = df.pivot_table(values='Salary', index='Department', columns='City', aggfunc='mean')
print(df_pivot)
print("\n")

# ------------------------------
# 5. df.apply(): Apply a custom function
# ------------------------------
print("Applying a custom function to increase 'Salary' by 10%:")
df['Salary'] = df['Salary'].apply(lambda x: x * 1.1)
print(df)
print("\n")

# ------------------------------
# 6. df.astype(): Change data type of a column
# ------------------------------
print("Changing 'Age' column to string type:")
df['Age'] = df['Age'].astype(str)
print(df)
print("\n")


'''
OUTPUT
Original DataFrame:
      Name  Age  ... Department  Salary
0    Alice   25  ...         HR   70000
1      Bob   30  ...    Finance   80000
2  Charlie   35  ...         HR  120000
3    David   40  ...         IT   90000
4      Eve   22  ...    Finance   75000

[5 rows x 5 columns]


Sorting rows by 'Age':
      Name  Age  ... Department  Salary       
4      Eve   22  ...    Finance   75000       
0    Alice   25  ...         HR   70000       
1      Bob   30  ...    Finance   80000       
2  Charlie   35  ...         HR  120000       
3    David   40  ...         IT   90000       

[5 rows x 5 columns]


Sorting rows by index in descending order:    
      Name  Age  ... Department  Salary
4      Eve   22  ...    Finance   75000       
3    David   40  ...         IT   90000       
2  Charlie   35  ...         HR  120000       
1      Bob   30  ...    Finance   80000       
0    Alice   25  ...         HR   70000       

[5 rows x 5 columns]


Grouping by 'Department' and calculating mean 
'Salary':
Department
Finance    77500.0
HR         95000.0
IT         90000.0
Name: Salary, dtype: float64


Creating a pivot table for average 'Salary' by 'Department' and 'City':
City         Chicago  ...  Phoenix
Department            ...
Finance          NaN  ...  75000.0
HR          120000.0  ...      NaN
IT               NaN  ...      NaN

[3 rows x 5 columns]


Applying a custom function to increase 'Salary' by 10%:
      Name  Age  ... Department    Salary     
0    Alice   25  ...         HR   77000.0     
1      Bob   30  ...    Finance   88000.0     
2  Charlie   35  ...         HR  132000.0     
3    David   40  ...         IT   99000.0     
4      Eve   22  ...    Finance   82500.0     

[5 rows x 5 columns]


Changing 'Age' column to string type:
      Name Age  ... Department    Salary      
0    Alice  25  ...         HR   77000.0      
1      Bob  30  ...    Finance   88000.0      
2  Charlie  35  ...         HR  132000.0      
3    David  40  ...         IT   99000.0      
4      Eve  22  ...    Finance   82500.0      

[5 rows x 5 columns]
'''
```

