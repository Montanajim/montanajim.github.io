# Serialization - CSV



## CSV Files and the Python `csv` Module

### What is a CSV File?

A CSV (Comma-Separated Values) file is a simple text-based format for storing tabular data. Each line in a CSV file represents a record, and each record consists of one or more fields separated by commas. This format is widely used for data exchange between different applications and systems because of its simplicity and readability.

**Example CSV file:**

```
Name,Title,Salary,City
Ally,CEO,2000000,Kalispell
Bob,CFO,1000000,Polson
Charlie,Developer,300000,Big Fork
Daisy,Sec Tech,400000,Libby

```

### Python's `csv` Module

 https://docs.python.org/3/library/csv.html#

Python's `csv` module provides a convenient way to work with CSV files. It offers classes for reading and writing CSV data, making it easy to parse and manipulate data in this format.

**Key functionalities of the `csv` module:**

- Reading CSV files:
  - `csv.reader`: Reads CSV data as a list of lists, where each inner list represents a row.
  - `csv.DictReader`: Reads CSV data as a list of dictionaries, where each dictionary represents a row and keys are the column headers.
- Writing CSV files:
  - `csv.writer`: Writes data to a CSV file as a list of lists.
  - `csv.DictWriter`: Writes data to a CSV file as a list of dictionaries.

**Common use cases for the `csv` module:**

- **Data import/export:** Loading data from CSV files into Python programs, and saving data from Python programs to CSV files.
- **Data cleaning and transformation:** Processing CSV data to clean, filter, or transform it before further analysis.
- **Data analysis:** Using CSV data as input for data analysis and visualization tasks.
- **Data integration:** Combining data from multiple CSV files into a single dataset.



**Additional features:**

- **Dialect customization:** The `csv` module allows you to define custom dialects for CSV files with different delimiters or quoting conventions.
- **Error handling:** The `csv` module provides mechanisms for handling errors that may occur during CSV parsing or writing.



# Lecture Code



```python
"""
Programmer: James Goudy
Program: CSV Demo

Documentation: https://docs.python.org/3/library/csv.html#

"""

import csv
import sys

def write_csv(filename, data):
  """Writes data to a CSV file.

  Args:
    filename: The name of the CSV file to write to.
    data: A list of lists, where each inner list represents a row of data.
  """

  # remember that file open attribute of 'a' will
  # allow the file to be appended
  with open(filename, 'w', newline='') as csvfile:
    csv_writer = csv.writer(csvfile)
    csv_writer.writerows(data)
    csvfile.close()

def read_csv(filename):

  """Reads data from a CSV file.

  Args:
    filename: The name of the CSV file to read from.

  Returns:
    A list of lists, where each inner list represents a row of data.
  """

  with open(filename, 'r') as csvfile:
    csv_reader = csv.reader(csvfile)
    data = list(csv_reader)
    csvfile.close()
  return data

def write_Dict(data, filename,thefieldnames) :
  with open(filename,'w',newline='')as csvfile:
    writer = csv.DictWriter(csvfile,fieldnames=thefieldnames)
    writer.writeheader()
    writer.writerows(data)

def read_dict(filename,thefieldnames):
  with open(filename,'r') as csvfile:
    reader = csv.DictReader(csvfile,thefieldnames)
    data = list(reader)
    return data

def display_dict(dataDict):
  
  print("\n--- Data Dictionary Values ---")
  tempDict = dict()

  for arow in dataDict:

    arow = dict(arow)
    
    for key, val in arow.items():
      sys.stdout.write(str(val).ljust(12,' ') + "\t")
    print()

def main():
    # Example usage:
    data = [
        ['Name', 'Title', 'Salary','City'],
        ['Ally', 'CEO', 2000000, 'Kalispell'],
        ['Bob', 'CFO', 1000000,'Polson'],
        ['Charlie', 'Developer', 300000, 'Big Fork'],
        ['Daisy', 'Sec Tech',400000, 'Libby']
    ]

    data2_fieldNames = ['Name', 'Title', 'Salary','City']
    data2 = [
        {'Name':'Ally2', 'Title':'CEO', 'Salary':2000000, 'City':'Kalispell'},
        {'Name':'Bob2', 'Title':'CFO', 'Salary':1000000,'City':'Polson'},
        {'Name':'Charlie2', 'Title':'Developer', 'Salary':300000, 'City':'Big Fork'},
        {'Name':'Daisy2', 'Title':'Sec Tech','Salary':400000, 'City':'Libby'}
    ]

    # filenames
    filename1 = "csv_example.txt"
    filename2 = "csv_example_dict.txt"

    # reading and writing csv file
    write_csv(filename1, data)
    read_data = read_csv(filename1)

    print("\n--- Dictionary Variable - read_data ---")
    print(read_data)

    print("\n--- Iterate Through Data ---")
    # iterate through each row
    for arow in read_data:
      # iterate through each item in that row
      for aitem in arow:
        sys.stdout.write(aitem.ljust(12,' ') + "\t")
      sys.stdout.write("\n")

    print("\n--- Dictionary ---")
   
    write_Dict(data2,"example_dict.csv",data2_fieldNames)
    thedata = read_dict("example_dict.csv",data2_fieldNames)
 
    print("\n--- Dictionary Variable - theData ---")
    print(thedata)

    print("\n--- iterate through data dictionary variable ---")
    display_dict(thedata)

    print("\n\nBye CSV\n")

main()

'''
--- Dictionary Variable - read_data ---
[['Name', 'Title', 'Salary', 'City'], ['Ally', 'CEO', '2000000', 'Kalispell'], ['Bob', 'CFO', '1000000', 'Polson'], ['Charlie', 'Developer', '300000', 'Big 
Fork'], ['Daisy', 'Sec Tech', '400000', 'Libby']]

--- Iterate Through Data ---
Name            Title           Salary          City        
Ally            CEO             2000000         Kalispell   
Bob             CFO             1000000         Polson      
Charlie         Developer       300000          Big Fork    
Daisy           Sec Tech        400000          Libby       

--- Dictionary ---

--- Dictionary Variable - theData ---
[{'Name': 'Name', 'Title': 'Title', 'Salary': 'Salary', 'City': 'City'}, {'Name': 'Ally2', 'Title': 'CEO', 'Salary': '2000000', 'City': 'Kalispell'}, {'Name': 'Bob2', 'Title': 'CFO', 'Salary': '1000000', 'City': 'Polson'}, {'Name': 'Charlie2', 'Title': 'Developer', 'Salary': '300000', 'City': 'Big Fork'}, {'Name': 'Daisy2', 'Title': 'Sec Tech', 'Salary': '400000', 'City': 'Libby'}]      

--- iterate through data dictionary variable ---

--- Data Dictionary Values ---
Name            Title           Salary          City        
Ally2           CEO             2000000         Kalispell   
Bob2            CFO             1000000         Polson      
Charlie2        Developer       300000          Big Fork    
Daisy2          Sec Tech        400000          Libby       


Bye CSV
'''
```



# Program Summary

The program is a CSV (Comma-Separated Values) demonstration script written by James Goudy. It shows how to work with CSV files for storing and manipulating tabular data. Here's a breakdown of its functionalities:

**Functions:**

- **write_csv(filename, data):** Writes a list of lists (where each inner list represents a row) to a CSV file.
- **read_csv(filename):** Reads data from a CSV file and returns it as a list of lists.
- **write_Dict(data, filename, thefieldnames):** Writes a list of dictionaries to a CSV file, where each dictionary represents a row and keys define column names.
- **read_dict(filename, thefieldnames):** Reads data from a CSV file containing dictionaries and returns it as a list of dictionaries.
- **display_dict(dataDict):** Iterates through a list of dictionaries and prints their values in a formatted table.

**Main Program:**

1. Defines sample data as lists and dictionaries with employee information (Name, Title, Salary, City).
1. Demonstrates writing and reading a regular CSV file (write_csv & read_csv functions).
1. Shows iterating through the read data and printing it in a table format.
1. Demonstrates writing and reading a CSV file with dictionaries (write_Dict & read_dict functions).
1. Uses the display_dict function to print the data from the dictionary in a formatted table.

