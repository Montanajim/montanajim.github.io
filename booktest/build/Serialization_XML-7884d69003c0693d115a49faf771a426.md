# Serialization - XML



## XML: Extensible Markup Language

***XML*** stands for ***\*Extensible Markup Language\****. It's a text-based format for storing, transporting, and reconstructing data. Think of it as a way to structure information so that both humans and computers can understand it.  

### Key characteristics of XML:

- **Extensible:**  

  You can create custom tags to describe your data.  This makes it flexible for various applications.

- **Self-describing**: 

  The tags provide information about the data, making it easier to understand without external documentation.

- **Platform-independent:** 

   XML files can be read and processed on different operating systems and software.

- **Hierarchical:** 

  Data is organized in a tree-like structure with parent and child elements.

### How XML works:

XML uses tags to enclose data. These tags define the structure of the data. For example:  



XML

```xml
<book>
  <title>The Hitchhiker's Guide to the Galaxy</title>
  <author>Douglas Adams</author>
  <year>1979</year>
</book>
```

In this example, `book`, `title`, `author`, and `year` are tags. The text between the tags is the data.

### Common uses of XML:

- **Data storage:**

   XML can store data in a structured format for later retrieval.

- **Data exchange:**

  It's used to transfer data between different systems and applications.

- **Configuration files:**

   Many software applications use XML to store configuration settings.

- **Web services:**

   XML is widely used for exchanging data between web services.

    

## Example code

```python
'''
Programmer: James Goudy
Project: XML 


you must know the xml schema

library
    book
        title
        author
        year
'''

import xml.etree.ElementTree as ET

def create_xml_file1(filename):
    """Creates a sample XML file with book information."""
    root = ET.Element("library")
    book1 = ET.SubElement(root, "book")
    ET.SubElement(book1, "title").text = "The Hitchhiker's Guide to the Galaxy"
    ET.SubElement(book1, "author").text = "Douglas Adams"
    ET.SubElement(book1, "year").text = "1979"

    book2 = ET.SubElement(root, "book")
    ET.SubElement(book2, "title").text = "The Lord of the Rings"
    ET.SubElement(book2, "author").text = "J.R.R. Tolkien"
    ET.SubElement(book2, "year").text = "1954"

    tree = ET.ElementTree(root)
    tree.write(filename)

def create_xml_file2(filename,BookArray,theSchmea):

    # passing in the xml schema
    
    root = ET.Element(theSchmea[0])

    # iterate through the book information
    for book in BookArray:
        abook = ET.SubElement(root,theSchmea[1])
        ET.SubElement(abook,theSchmea[2]).text = book[theSchmea[2]] 
        ET.SubElement(abook,theSchmea[3]).text = book[theSchmea[3]]
        ET.SubElement(abook,theSchmea[4]).text = str(book[theSchmea[4]])


    tree = ET.ElementTree(root)
    tree.write(filename)


def read_xml_file(filename):
    print("\nRead File  " + filename)
    """Reads the created XML file and prints book information."""
    tree = ET.parse(filename)
    # tree = ET.parse("zbooks1.xml")
    root = tree.getroot()


    # for book in root.iter("book"):
    for book in root:

        title = book.find("title").text
        author = book.find("author").text
        year = book.find("year").text

        print(f"Title: {title}")
        print(f"Author: {author}")
        print(f"Year: {year}")
        print()



if __name__ == "__main__":


    BookSchema = ["libary","book","title","author","year"]

    books = [
    {"title": "Introduction to Algorithms", "author": "Cormen", "year": 1989},
    {"title": "Clean Code", "author": "Martin", "year": 2012},
    {"title": "Structure and Interpretation of Computer Programs", "author": "Sussman", "year": 1985}
    ]

    history_books = [
    {"title": "Sapiens: A Brief History of Humankind", "author": "Yuval Noah Harari", "year": 2011},
    {"title": "Guns, Germs, and Steel: The Fates of Human Societies", "author":"Diamond", "year": 1997},
    {"title": "A Short History of Nearly Everything", "author": "Bryson", "year": 2003},
    {"title": "1491: New Revelations of the Americas Before Columbus", "author": "Mann", "year": 2005},
    {"title": "The Rise and Fall of the Roman Empire", "author": "Gibbon", "year": 1776}
]

    # write xml files

    zthefilename1 = "zbooks1.xml"
    zthefilename2 = "zbooks2.xml"

    create_xml_file1(zthefilename1)
    create_xml_file2(zthefilename2,history_books,BookSchema)

    # Read the files
    read_xml_file(zthefilename1)
    print("\n-------- part 2 ----------\n")
    read_xml_file(zthefilename2)

    print("\nbye\n")

"""
NOTE: The output has been prettified.
--- zbooks1.xml ---
<library>
   <book>
      <title>The Hitchhiker's Guide to the Galaxy</title>
      <author>Douglas Adams</author>
      <year>1979</year>
   </book>
   <book>
      <title>The Lord of the Rings</title>
      <author>J.R.R. Tolkien</author>
      <year>1954</year>
   </book>
</library>

--- zbooks2.xml ---
<libary>
	<book>
		<title>Sapiens: A Brief History of Humankind</title>
		<author>Yuval Noah Harari</author>
		<year>2011</year>
	</book>
	<book>
		<title>Guns, Germs, and Steel: The Fates of Human Societies</title>
		<author>Jared Diamond</author>
		<year>1997</year>
	</book>
	<book>
		<title>A Short History of Nearly Everything</title>
		<author>Bill Bryson</author>
		<year>2003</year>
	</book>
	<book>
		<title>1491: New Revelations of the Americas Before Columbus</title>
		<author>Charles C. Mann</author>
		<year>2005</year>
	</book>
	<book>
		<title>The Rise and Fall of the Roman Empire</title>
		<author>Edward Gibbon</author>
		<year>1776</year>
	</book>
</libary>


--- Program Output ---

Read File  zbooks1.xml
Title: The Hitchhiker's Guide to the Galaxy   
Author: Douglas Adams
Year: 1979

Title: The Lord of the Rings
Author: J.R.R. Tolkien
Year: 1954


-------- part 2 ----------


Read File  zbooks2.xml
Title: Sapiens: A Brief History of Humankind  
Author: Yuval Noah Harari
Year: 2011

Title: Guns, Germs, and Steel: The Fates of Human Societies
Author: Diamond
Year: 1997

Title: A Short History of Nearly Everything   
Author: Bryson
Year: 2003

Title: 1491: New Revelations of the Americas Before Columbus
Author: Mann
Year: 2005

Title: The Rise and Fall of the Roman Empire  
Author: Gibbon
Year: 1776


bye


"""
```



## Program Summary

**Purpose:**

- Creates XML files containing book information.
- Reads and displays the contents of these XML files.

**Key Components:**

1. **XML Schema:** Defines the structure of the XML data, including elements like `library`, `book`, `title`, `author`, and `year`.
1. **Book Data:** Stores book information in arrays of dictionaries, with each dictionary representing a book and its details.
1. XML Creation Functions:
   - `create_xml_file1`: Creates a hardcoded XML file with two books.
   - `create_xml_file2`: Creates an XML file based on a given book array and XML schema.
1. XML Reading Function:
   - `read_xml_file`: Parses an XML file, extracts book information, and prints it to the console.

**Overall Flow:**

1. Defines the XML schema and book data arrays.
1. Creates two XML files using the defined functions.
1. Reads and displays the contents of both XML files.

**Key Points:**

- The program demonstrates how to create and read XML files in Python using the `xml.etree.ElementTree` module.
- It highlights the importance of an XML schema for defining data structure.
- The code provides a basic example of working with XML data.

