# File, Folder - Creation and Deletion

## Key Ideas

 * Objectives
 * Global Variables
 * Creating directories
 * Deleting Directories
 * Creating files
 * Reading Files
 * Deleting Files



## Lecture Code

``` java
/*
 * Programmer: James Goudy
 * Project: File, folder creation and deletion
 */
package io_demo;

/**
 *
 * @author jgoudy
 */
/*
 * Objectives
 * Global Variables
 * Creating directories
 * Deleting Directories
 * Creating files
 * Reading Files
 * Deleting Files
 */
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;

public class IO_Demo {

    //Gloabal variable - used by all functions
    static String xStrPath;
    //static double[][] myArray;

    //Create a directory
    static void ioCreateDirectory() {

        boolean checkDir;

        //import java.nio.file Path
        //import java.nio.file Paths - helper class
        //Path sets a path for a file or directory
        Path xPath = Paths.get(xStrPath);

        //true if the file does exist; 
        //false if the file does not exists or its existence cannot be determined
        checkDir = Files.exists(xPath);

        if (checkDir) {
            System.out.println("Directory Already Exists");
            return;
        }

        try {
            //Creates a directory - note that 
            //it uses the path that was just created
            //Note that Files requires it to be in
            //try - catch statement
            Files.createDirectory(xPath);
        } catch (Exception e) {
            System.out.println("Could not create directory");
        }
    }

    //Delete a directory
    //Note: in order to delete a directory it must be empty first
    static void ioDeleteDirectory() {
        Path xDeletePath = Paths.get(xStrPath);

        try {
            Files.delete(xDeletePath);
        } catch (Exception e) {
            System.out.println("Could not delete the direcotry");
        }
    }

    //Write a text file
    static void ioCreateTextFile() {
        xStrPath = "c:\\zJavaTemp\\myFile1.txt";
        String text1;
        String text2;
        boolean fileCheck;

        Path pathNewFile = Paths.get(xStrPath);

        fileCheck = Files.isRegularFile(pathNewFile)
                & Files.isReadable(pathNewFile)
                & Files.isExecutable(pathNewFile);

        try {

            BufferedWriter fw = null;

            if (fileCheck) {
                fw
                        = Files.newBufferedWriter(pathNewFile,
                                StandardCharsets.UTF_8,
                                StandardOpenOption.APPEND);
            } else {
                fw
                        = Files.newBufferedWriter(pathNewFile,
                                StandardCharsets.UTF_16,
                                StandardOpenOption.CREATE);
            }

            /*
             * Charatersets
             * StandardCharsets.UTF_8;
             * StandardCharsets.US_ASCII;
             * StandardCharsets.UTF_16;
             *
             * Opening and deleting files
             * StandardOpenOption.CREATE_NEW;
             * StandardOpenOption.APPEND;
             * StandardOpenOption.DELETE_ON_CLOSE;
             * StandardOpenOption.TRUNCATE_EXISTING;
             * StandardOpenOption.DELETE_ON_CLOSE;
             */
            
            //Note for windows \r\n has to be used in combination
            //For universal newlines, use the newline method
            text1 = "xx This is how you write a file. ";
            text2 = "(You store user input in a variable then write it. \r\n";

            for (int cntr = 0; cntr < 10; cntr++) {
                fw.write(text1);
                fw.newLine();
                fw.write(text2);

                fw.flush();
            }

            fw.close();
        } catch (Exception e) {
            System.out.println("Could not write the file");
        }

    }

    //Read a text file
    static void ioReadFile() {
        xStrPath = "c:\\zJavaTemp\\myFile1.txt";
        String intext1;
        String text2;
        boolean fileCheck;

        Path pathOpenFile = Paths.get(xStrPath);

        //check if the files is real, 
        //the file is readable, the file is not locked
        fileCheck = Files.isRegularFile(pathOpenFile)
                & Files.isReadable(pathOpenFile)
                & Files.isExecutable(pathOpenFile);

        if (!fileCheck) {
            System.out.println("File could not be opened");
            return;
        }

        try {

            //We will use the newBufferedReader
            //to read in our text file
            BufferedReader fr = Files.newBufferedReader(
                    pathOpenFile,
                    StandardCharsets.UTF_8);

            while ((intext1 = fr.readLine()) != null) {
                System.out.println(intext1);
            }

            fr.close();
        } catch (Exception e) {
            System.out.println("Could not read the file");
        }

    }

    static void ioDeleteFile() {

        xStrPath = "c:\\zJavaTemp\\myFile1.txt";

        //Get the path of the file to delet
        Path xPath = Paths.get(xStrPath);

        try {
            Files.delete(xPath);
            System.out.println("File successfully deleted");
        } catch (Exception e) {
            System.out.println("File not deleted");
        }

    }

    public static void main(String[] args) {

        char xdeleteDir = 'n';

        //Note that this is a global variable
        xStrPath = "c:\\zJavaTemp";

        ioCreateDirectory();

        xdeleteDir = 'n';
        if (xdeleteDir == 'y') {
            ioDeleteDirectory();
        }

        //Creating and and Reading a Textfile
        ioCreateTextFile();
        ioReadFile();

        // Toggle the comment to delete the file          
        // ioDeleteFile();
    }
}

```



---

End of Topic


