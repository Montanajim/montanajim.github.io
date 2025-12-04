# Serialization HDF5

**HDF5** (Hierarchical Data Format 5) is a file format designed to store and organize massive amounts of data in a structured and efficient way. It's particularly well-suited for scientific and engineering applications where data can be complex, heterogeneous, and immense.

## Key Features of HDF5

* **Hierarchical structure:** Data can be organized into groups and subgroups, similar to directories in a file system.
* **Data types:** Supports a wide range of data types, including numerical arrays, strings, and even complex data structures.
* **Metadata:** Allows for embedding descriptive information about data, making it self-describing.
* **Large datasets:** Can handle datasets of virtually any size, efficiently storing and accessing data.
* **Compression:** Offers various compression methods to reduce file size without compromising data integrity.
* **Portability:** HDF5 files can be read and written on different platforms and operating systems.

## Common Use Cases

* **Scientific data:** Storing experimental results, simulations, and images.
* **Image and signal processing:** Managing large image and signal datasets.
* **Bioinformatics:** Handling genomic and proteomic data.
* **Machine learning:** Storing and accessing training data.
* **Remote sensing:** Managing satellite and sensor data.

In essence, HDF5 provides a robust and flexible solution for managing and preserving large, complex datasets, making it a popular choice in various scientific and data-intensive fields.



##  Installing HDF5

```shell
  pip install h5py numpy
```

---



## Creating a Sample HDF5 File with People, Jobs, and Residencies

### Understanding the Structure

Before we dive into the code, let's outline the structure of our HDF5 file:

- **Root Group:** The top-level container.

- People Group:

   Contains information about individuals.

  - **Datasets:** Names, IDs, ages, etc.
  - **Attributes:** General information about the people group.

- Jobs Group:

   Contains information about jobs.

  - **Datasets:** Job titles, companies, salaries, etc.
  - **Attributes:** General information about the jobs group.

- Residencies Group:

   Contains information about residencies.

  - **Datasets:** City, state, zip code, etc.
  - **Attributes:** General information about the residencies group.

### Python Code Using h5py

Python

```python
"""
HDF5 Code
Programmer: James Goudy

"""

import h5py
import numpy as np

def create_hdf5_file(filename):
  """Creates a sample HDF5 file with people, jobs, and residencies data.

  Args:
    filename: The name of the HDF5 file to create.
  """

  with h5py.File(filename, 'w') as hdf5_file:

    # Create groups - think of groups like folders
    people_group = hdf5_file.create_group('people')
    jobs_group   = hdf5_file.create_group('jobs')
    address_group = hdf5_file.create_group('address')

    # Datasets are like spreadsheets put into the folders
    # Create dataset- storing names, ids, and ages
    num_people = 5
    people_group.create_dataset('names', (num_people,), dtype='S20')
    people_group.create_dataset('ids', (num_people,), dtype='i')
    people_group.create_dataset('ages', (num_people,), dtype='i')

    # NOTE: in the examples below, the index position is the key that ties appropriate
    # data to the appropriate person.

    # load data into dataset
    people_group['names'][...] = np.array(['Alice', 'Bob', 'Charlie', 'David', 'Emily'],dtype='S20')
    # people_group['names'][...] = np.array(['Alice', 'Bob', 'Charlie', 'David', 'Emily'],dtype=h5py.string_dtype('ascii'))
    people_group['ids'][...] = np.array([1, 2, 3, 4, 5])
    people_group['ages'][...] = np.array([30, 25, 35, 40, 28])

    # create datasets - job title information
    jobs_group.create_dataset('jobTitles',(num_people), dtype='S20')

    # load data into dataset - alternative - assign in two steps
    myArrJobTitles = np.array(['Programmer','Cop','Baker','Pilot','Engineer'],dtype='S20')
    jobs_group['jobTitles'][...] = myArrJobTitles

    # Below is like the previous way to assign data to dataset
    # jobs_group['jobTitles'][...] = np.array(['Programmer','Cop','Baker','Pilot','Engineer'],dtype='S20')

    # create datasets - address information
    address_group.create_dataset('cities',(num_people),dtype='S20')
    address_group.create_dataset('states',(num_people),dtype='S20')

    # load data
    address_group['cities'][...] = np.array(['Kali','Polson','Butte','Chicago','Whitefish'],dtype='S20')
    address_group['states'][...] = np.array(['MT','CO','KS','IL','OH'],dtype='S20')


    # Add attributes / meta-data to the specific groups
    people_group.attrs['creation_date'] = "2024-07-25" # np.string_('2024-07-25')
    people_group.attrs['data_source'] = "Job Data"
    jobs_group.attrs['title_dir'] = "Job Title Directory"
    address_group.attrs['census_data'] = "Census Data"
    address_group.attrs['census_date'] = "Census Date"


    # Similar structure for jobs and residencies groups (omitted for brevity)

def read_hdf5_file(filename):
  """Reads the sample HDF5 file and displays the data.

  Args:
    filename: The name of the HDF5 file to read.
  """

  with h5py.File(filename, 'r') as hdf5_file:
    # Access groups
    # To decryppt we need to create the appropriate
    # folders to store information that is taken out of 
    # the hdf5 file
    people_group = hdf5_file['people']
    jobs_group   = hdf5_file['jobs']
    address_group = hdf5_file['address']

    # Print people data
    # Note that the Names and Job Titles are 
    # designated byte data.  This means that to 
    # use them as strings, they need to be decode
    # from bytes to strings.
    print("People Data:")
    print("Names:", people_group['names'][...])
    print("IDs:", people_group['ids'][...])
    print("Ages:", people_group['ages'][...])
    print("Attributes:", people_group.attrs['creation_date'])
    print("Attributes:", people_group.attrs['data_source'])

    # Print jobs data (replace with actual code)
    print("Jobs Titles:",jobs_group['jobTitles'][...])
    # ...

    print("\nIterate through individual data\n-----\n")
    for i in range(5):
      # note you can decode from either utf-8 or ascii
      print(f"{people_group['names'][i].decode('utf-8')}" + "\t" +  
             str(people_group['ages'][i]) +  "\t"  +
            f"{jobs_group['jobTitles'][i].decode('utf-8')}" + "\n" +
            f"{address_group['cities'][i].decode('utf-8')}" + ", " +
            f"{address_group['states'][i].decode('ascii')}" + "\n")

    print("\n-----\nSource Information / Attribution Data" + "\n" +
            "Creation date: " + 
            people_group.attrs['creation_date'] +  "\n" + 
            people_group.attrs['data_source']  + "\n" + 
            jobs_group.attrs['title_dir'] + "\n" + 
            address_group.attrs['census_data'] + "\n" + 
            address_group.attrs['census_date'] + "\n")

if __name__ == '__main__':
  filename = 'sample.h5'
  create_hdf5_file(filename)

  print("\n\n-----------\n\n")

  read_hdf5_file(filename)

print("\nbye\n")



'''
OUTPUT

----- Input Data------

----- Read Data From File------

People Data:
Names: [b'Alice' b'Bob' b'Charlie' b'David' b'Emily'] 
IDs: [1 2 3 4 5]
Ages: [30 25 35 40 28]
Attributes: 2024-07-25
Attributes: Job Data
Jobs Titles: [b'Programmer' b'Cop' b'Baker' b'Pilot' b'Engineer']

Iterate through individual data
-----

Alice   30      Programmer
Kali, MT

Bob     25      Cop
Polson, CO

Charlie 35      Baker
Butte, KS

David   40      Pilot
Chicago, IL

Emily   28      Engineer
Whitefish, OH

-----
Source Information / Attribution Data
Creation date: 2024-07-25
Job Data
Job Title Directory
Census Data
Census Date

bye
'''

```

## Code Summary

**Purpose:**

- Creates and manipulates an HDF5 file containing information about people, their jobs, and addresses.
- Demonstrates how to store, access, and read data from the HDF5 file.

**Key Components:**

- **HDF5 File:** A container for storing large amounts of data in a hierarchical structure.
- **Groups:** Represent folders within the HDF5 file for organizing data.
- **Datasets:** Similar to spreadsheets, storing specific data within groups.
- **Attributes:** Additional metadata associated with groups or datasets.

**Code Functionality:**

1. **`create_hdf5_file(filename)`:**
   - Creates an HDF5 file with the specified filename.
   - Creates groups: `people`, `jobs`, and `address`.
   - Creates datasets within each group for storing names, IDs, ages, job titles, cities, and states.
   - Populates datasets with sample data.
   - Adds attributes to groups for metadata (creation date, data source, etc.).
1. **`read_hdf5_file(filename)`:**
   - Opens the specified HDF5 file for reading.
   - Accesses the `people`, `jobs`, and `address` groups.
   - Prints data from the datasets, including names, IDs, ages, job titles, cities, and states.
   - Prints attributes associated with the groups.

**Overall:**

The code provides a basic example of how to use the `h5py` library to create and interact with HDF5 files. It demonstrates creating groups, datasets, and attributes, as well as reading and accessing data from the file.
