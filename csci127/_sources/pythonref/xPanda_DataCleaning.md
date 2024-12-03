# Panda Data Cleaning

## **Explanation of Each Function**

1. **`df.isnull()`**:
   - Detects missing (NaN) values in the DataFrame.
   - Returns a DataFrame of the same shape with `True` for missing values and `False` otherwise.
1. **`df.notnull()`**:
   - Detects non-missing values in the DataFrame.
   - Returns a DataFrame of the same shape with `True` for non-missing values and `False` otherwise.
1. **`df.fillna(value)`**:
   - Replaces missing values with a specified value or dictionary of values for different columns.
1. **`df.dropna()`**:
   - Drops rows or columns with missing values. By default, rows with any missing values are removed.
1. **`df.replace(old_value, new_value)`**:
   - Replaces specific values in the DataFrame with new ones.
1. **`df.rename()`**:
   - Renames columns or rows. It requires a dictionary mapping old names to new names.

```python
# Panda Data Cleaning

import pandas as pd
import numpy as np

# Create sample data with missing values
data = {
    'Name': ['Alice', 'Bob', 'Charlie', None, 'Eve'],
    'Age': [25, np.nan, 35, 40, 22],
    'City': ['New York', 'Los Angeles', None, 'Houston', 'Phoenix'],
    'Salary': [70000, 80000, None, 90000, 75000]
}

# Create a DataFrame
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("\n")

# ------------------------------
# 1. Detect missing values with isnull()
# ------------------------------
print("Detecting missing values with isnull():")
print(df.isnull())
print("\n")

# ------------------------------
# 2. Detect non-missing values with notnull()
# ------------------------------
print("Detecting non-missing values with notnull():")
print(df.notnull())
print("\n")

# ------------------------------
# 3. Fill missing values with fillna()
# ------------------------------
print("Filling missing values with a default value:")
df_filled = df.fillna({'Name': 'Unknown', 'Age': 0, 'City': 'Unknown', 'Salary': 50000})
print(df_filled)
print("\n")

# ------------------------------
# 4. Drop rows with missing values using dropna()
# ------------------------------
print("Dropping rows with any missing values:")
df_dropped = df.dropna()
print(df_dropped)
print("\n")

# ------------------------------
# 5. Replace specific values with replace()
# ------------------------------
print("Replacing 'New York' with 'NYC' in the 'City' column:")
df_replaced = df.copy()
df_replaced['City'] = df_replaced['City'].replace('New York', 'NYC')
print(df_replaced)
print("\n")

# ------------------------------
# 6. Rename columns with rename()
# ------------------------------
print("Renaming columns:")
df_renamed = df.rename(columns={'Name': 'Full Name', 'Age': 'Years', 'City': 'Location'})
print(df_renamed)
print("\n")


'''
OUTPUT
Original DataFrame:
      Name   Age         City   Salary 
0    Alice  25.0     New York  70000.0 
1      Bob   NaN  Los Angeles  80000.0 
2  Charlie  35.0         None      NaN 
3     None  40.0      Houston  90000.0 
4      Eve  22.0      Phoenix  75000.0 


Detecting missing values with isnull():
    Name    Age   City  Salary
0  False  False  False   False
1  False   True  False   False
2  False  False   True    True
3   True  False  False   False
4  False  False  False   False


Detecting non-missing values with notnull():  
    Name    Age   City  Salary
0   True   True   True    True
1   True  False   True    True
2   True   True  False   False
3  False   True   True    True
4   True   True   True    True


Filling missing values with a default value:  
      Name   Age         City   Salary
0    Alice  25.0     New York  70000.0        
1      Bob   0.0  Los Angeles  80000.0        
2  Charlie  35.0      Unknown  50000.0        
3  Unknown  40.0      Houston  90000.0        
4      Eve  22.0      Phoenix  75000.0        


Dropping rows with any missing values:        
    Name   Age      City   Salary
0  Alice  25.0  New York  70000.0
4    Eve  22.0   Phoenix  75000.0


Replacing 'New York' with 'NYC' in the 'City' 
column:
      Name   Age         City   Salary        
0    Alice  25.0          NYC  70000.0        
1      Bob   NaN  Los Angeles  80000.0        
2  Charlie  35.0         None      NaN        
3     None  40.0      Houston  90000.0        
4      Eve  22.0      Phoenix  75000.0        


Renaming columns:
  Full Name  Years     Location   Salary
0     Alice   25.0     New York  70000.0      
1       Bob    NaN  Los Angeles  80000.0      
2   Charlie   35.0         None      NaN      
3      None   40.0      Houston  90000.0      
4       Eve   22.0      Phoenix  75000.0 
'''
```

