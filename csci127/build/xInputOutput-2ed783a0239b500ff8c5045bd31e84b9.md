# Input / Output - Files And Folders




File input/output (I/O) is the process of reading and writing data to files. This is a fundamental operation in computer science, as it allows programs to store data persistently and retrieve it later.

There are two main types of file I/O:

- **Text file I/O:** This type of I/O involves reading and writing text-based data. Text files are typically stored in plain text format, which means that they can be easily read and edited by humans.
- **Binary file I/O:** This type of I/O involves reading and writing binary data. Binary files are typically used to store non-text data, such as images, audio, and video.

File I/O is typically performed using the following steps:

1. **Open the file:** This step creates a connection to the file and prepares it for reading or writing.
1. **Read or write data:** This step reads data from the file or writes data to the file.
1. **Close the file:** This step releases the connection to the file and closes it.

Here is an example of how to read a text file using the Python programming language:

```python
with open('file.txt', 'r') as file:
  data = file.read()
  print(data)
```

This code will read the contents of the file `file.txt` and print it to the console.

Here is an example of how to write a text file using the Python programming language:

```python
with open('file.txt', 'w') as file:
  file.write('Hello, world!')
```

This code will write the string `Hello, world!` to the file `file.txt`.

File I/O is an important concept in computer science, as it allows programs to store data persistently and retrieve it later. File I/O is used in a wide variety of applications, including:

- **Saving and loading data:** Programs can use file I/O to save data to files and load it later. This is useful for storing data that needs to be persisted across program runs.
- **Communicating with other programs:** Programs can use file I/O to communicate with each other by exchanging data through files. This is useful for tasks such as sharing data or exchanging configuration settings.
- **Creating and modifying files:** Programs can use file I/O to create and modify files. This is useful for tasks such as creating log files or generating reports.

File I/O is a fundamental operation in computer science, and it is essential for any program that needs to store data persistently or communicate with other programs or systems.



## Lecture Code

```python
# -*- coding: utf-8 -*-
"""
Created on Wed Mar 30 10:47:56 2022

@author: jgoudy

James Goudy
"""
import os
import subprocess
import shutil


# All uservariables begin with x

# globals
xDirName = ""
xBasePath = ""
xFilePath = ""

def makeDirectory():
    
    # tell the function to use the global variables
    
    global xDirName 
    global xBasePath
    global xFilePath

    
    # having a basename is helpful if 
    # you have to make multiple folders
    # in a particualar folder
    
    # join the base with the directory name
    
    xpath = os.path.join(xBasePath,xDirName)
    print("xpath: "+ xpath)
    
    # make the directory
    
    os.mkdir(xpath)
    
    # Example of making directories
    # xpath value is currently c:/z/zmyDir
    # The following code will create a folder
    # for each letter in the alphabet
    
    xBasePath = xpath + "/"
    
    xletters = "abcdefghijklmnopqrstuvwxyz"
    
    for xx in xletters:
        os.mkdir((xBasePath + xx))
        
    print(xBasePath)
    
    input("1. Check if letter folders created.\nPress enter to continue")
    
    # note will will add projects 
    # to c:/z/zmyDir/misc/projects
    # note we did not create a misc directory
    # using makedirs will allow us to
    # create the missing folder automatically
    
    os.makedirs("c:/z/zmyDir/misc/projects")
    
    input("2. Check for the misc folder\nPress enter to continue")
    
    # check if directory exists
    
    xstatus = os.path.isdir("c:/z/zmyDir/misc/projects")
    if(xstatus):
        print("\nDirectory exists\n")
    else:
        print("\nDirectory does not exists")
    

    xstatus = os.path.isdir("c:/z/zmyDir/misc/bubba")
    if(xstatus):
        print("\nDirectory exists\n")
    else:
        print("\nDirectory does not exists")
        


def addFile():
    
    # tell the function to use the global variables

    
    global xDirName 
    global xBasePath
    global xFilePath
    
    print(xBasePath)
    
    # create file path
    
    
    xfilename = "xfile1.txt"
    xpath = xBasePath+ "a/" + xfilename
    
    # xpath = xpath + xfilename
    
    print(xpath)
    
    # add a file to the "a" folder
    
    # 'w' create a file - creates new file if it doesn't exist
    # overwrites data if it does exist
    
    xfw = open(xpath, 'w')
    
    
    """
    Read Only ('r'): Open text file for reading. If the file does not exist, 
    raises I/O error. This is also the default mode in which
    the file is opened.

    Read and Write ('r+'): Open the file for reading and writing. 
    Raises I/O error if the file does not exist.

    Write Only ('w'): Open the file for writing. 
    Existing data is truncated and over-written. 
    Creates the file if the file does not exist.

    Write and Read ('w+'): Open the file for reading and writing. 
    Existing data is truncated and over-written. 

    Append Only ('a'): Open the file for writing. 
    The file is created if it does not exist.  
    Data is added to the end of the file.

    Append and Read ('a+'): Open the file for reading and writing. 
    The file is created if it does not exist. 
    Data is added to the end of the file.
    """  
    
    input("3. Check to see if file was created\nPress enter to continue")
    
    # write text to file
    for c in range(10):
        xfw.write(str(c+1) + ". Sample text\r\n")
        
    # close the file when done writing
    xfw.close()
    
    # append to the file
    xfw = open(xpath, 'a')
    
    # add some text to the end
    for c in range(10):
        xfw.write(str(c+1) + "z. ZZZ Sample text\r\n")
        
    # close the file when done writing
    xfw.close()    
    
    xFilePath = xpath
    print("xxx: " + xpath)
    
    # In order to use subprocess.Popen which opens the file directory
    # the slashes have to be reversed
    xpath = swapSlash(xpath)
    
    # subprocess will open the operating system file explorer in windows
    # c:/z/zmyDir/a/  
    # subprocess.Popen(r'explorer /select,"C:\z\zmyDir\a\xfile1.txt"')
    subprocess.Popen(r'explorer /select,"' + xpath + '"' )
    
    input("4. Exploer window opened\nPress enter to continue")
    
    
def deleteFile():

    # delete a file
      
    # tell the function to use the global variables
      
    global xFilePath
      
    print("Delete / remove : " + xFilePath)
    
    # check if file exists and remove it
    if os.path.exists(xFilePath):
        os.remove(xFilePath)
    else:
        print("File could not be found and was not deleted")

    # you can also use the os.unlink command as well to delete a file
    
    input("5. Check if file was deleted\nPress enter to continue")

def deleteFolders():
    
    '''
    remove() throws an exception if the file doesn't exist, 
    while shutil. rmtree() doesn't care if the directory is empty or not.
    '''
    
    # remove the 'a' directory 
    # os.chmod('c:\\z\\zmyDir\\b', stat.S_IXOTH)
    os.rmdir('c:\\z\\zmyDir\\b')
    
    input("5a. Check if b folder was deleted\n" + \
          "Press enter to continue")    
    
    # remove all directories 
    choice = input("Delete all directories y/n : ").lower()
    
    if choice == "y":
        try:
            xtemp = "c:\\z\\zmyDir\\"
            shutil.rmtree(xtemp)
            print("ok")
            
        except Exception as e:
           print(e) 
    
    input("5. Check if all created folders were deleted\n" + \
          "Press enter to continue")
    
def swapSlash(aString):
    
    newString = ""
    
    for l in aString:
        if l == "/":
            newString = newString + "\\"
        else:
            newString = newString + l
            
    # print(newString)
    
    return newString
              
    
def main():
    
    print("working\n")
    
    # access global variables
    
    global xDirName 
    global xBasePath
    
    
    # directory name variable
    
    xDirName = "zmyDir"
    
    # basename 
    # in this case make sure you have a 
    # z folder on your c drive
    
    xBasePath = "c:/z/"

    # remove the example code if previous ran and still existing    
    try:
        xtemp = xBasePath+xDirName
        shutil.rmtree(xtemp)
        
    except Exception as e:
       print(e)
         
    
    # main program code
    
    makeDirectory()
    
    addFile()
    
    deleteFile()
    
    deleteFolders()
    
    print("\nbye bye")
    
main()
```

