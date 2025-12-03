# Panda IO



The provided Python script demonstrates how to create, manipulate, and export data using the Pandas library in various file formats. It begins by creating a sample DataFrame with columns for `Name`, `Age`, and `City`, which is then exported to a CSV file, an Excel file (using `openpyxl`), and a JSON file. The script also reads data back from these files into new DataFrames, showcasing how Pandas handles different file formats efficiently.

Additionally, the script demonstrates data manipulation by creating a copy of the original DataFrame, filtering rows where the `Age` column value is greater than 25. This process is akin to simulating a SQL-like read and write operation. The output showcases the data's consistent structure across file formats and highlights the use of Pandas for data analysis tasks. The script also mentions a potential `openpyxl` dependency issue for Excel operations and provides a solution for its installation.



```python
# if not installed
# pip install pandas
# pip install openpyxl

import pandas as pd

# Create sample data to use in the program
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}

# Creating a DataFrame
df = pd.DataFrame(data)

# ------------------------------
# 1. Exporting to a CSV File
# ------------------------------
df.to_csv('data.csv', index=False)
print("Data exported to 'data.csv'")

# ------------------------------
# 2. Reading from a CSV File
# ------------------------------
df_csv = pd.read_csv('data.csv')
print("\nData read from CSV file:")
print(df_csv)


# ------------------------------
# 3. Exporting to an Excel File
# ------------------------------

df.to_excel('data.xlsx', index=False, sheet_name='Sheet1')
print("\nData exported to 'data.xlsx'")

# ------------------------------
# 4. Reading from an Excel File
# ------------------------------
df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet1')
print("\nData read from Excel file:")
print(df_excel)

# ------------------------------
# 5. Exporting to a JSON File
# ------------------------------
df.to_json('data.json', orient='records')
print("\nData exported to 'data.json'")

# ------------------------------
# 6. Reading from a JSON File
# ------------------------------
df_json = pd.read_json('data.json')
print("\nData read from JSON file:")
print(df_json)

# ------------------------------
# 7. Copying DataFrame to Simulate SQL Read/Write
# ------------------------------
# Simulating a "write" operation by creating a new DataFrame
df_copy = df.copy()
print("\nData copied to a new DataFrame:")
print(df_copy)

# Simulating a "read" operation by modifying the copied DataFrame
df_modified = df_copy[df_copy['Age'] > 25]
print("\nFiltered DataFrame with Age > 25:")
print(df_modified)

'''
OUTPUT:
Data exported to 'data.csv'

Data read from CSV file:    
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago

Data exported to 'data.xlsx'

Data read from Excel file:
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago

Data exported to 'data.json'

Data read from JSON file:
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago

Data copied to a new DataFrame:
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago

Filtered DataFrame with Age > 25:
      Name  Age         City
1      Bob   30  Los Angeles
2  Charlie   35      Chicago

'''



'''
The error ModuleNotFoundError: No module named 'openpyxl' means that the Python module openpyxl, which is used for working with Excel files in .xlsx format, is not installed in your environment.

To resolve this, follow these steps:
Install openpyxl: Run the following command in your terminal or command prompt:

pip install openpyxl
Verify Installation: After installation, verify that the module has been installed correctly by running:

pip show openpyxl
This should display the installed version and location of the openpyxl module.

'''
```

