# IO Read Data File



## Key Ideas

* Read a comma-separated file



## Lecture Code



```java
/*
 * Programmer: James Goudy
 * Project: IO_CSV_Demo Rev 2 20220630
 */
package com.company.my.j1_io_csv_demo_rev2;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;


/**
 *
 * @author jgoudy
 */
class readCSV_Scanner {

}

class readCSV_BufferedReader {

    BufferedReader br;
    FileReader fr;
    int numCols;
    int numRows;
    // br.mark(0);

    String filePath;

    public readCSV_BufferedReader(String filePath) {

        this.filePath = filePath;

        createBufferedReader(filePath);

    }

    private void createBufferedReader(String thefilePath) {
        try {
            br = new BufferedReader(new FileReader(thefilePath));
            

        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }

    }

  

    private void getArrayDimensions() {

        String inputLine = "";

        try {

            // skip the header row        
            br.readLine();

            // count rows
            while ((inputLine = br.readLine()) != null) {
                numRows++;
            }

            //reset buffered reader
            createBufferedReader(this.filePath);

            // calculate columns
            inputLine = br.readLine();
            String[] inputArrary = inputLine.split(",");
            numCols = inputArrary.length;

            System.out.println("Rows = " + numRows);
            System.out.println("Cols = " + numCols);

        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }

    }

    public String[][] readDataIntoArray() {
        
        getArrayDimensions();
        
        String[][] dataArray = new String[numRows][numCols];
        String inputLine;
        
        int rowCount = 0;

        // reset buffered reader
        createBufferedReader(this.filePath);

        try {

            // skip the header row        
            br.readLine();

            // br.readline reads the input file line
            // and stores it in inputline within the while statement
            
            while ((inputLine = br.readLine()) != null) {

                // split the inputline into a string array
                String[] inputArrary = inputLine.split(",");
                
                // add the data from the inputArray to the dataArray
                for(int i = 0; i < inputArrary.length; i++)
                {
                    dataArray[rowCount][i] = inputArrary[i];
                }
                System.out.println("");

                rowCount++;
            }

        } catch (IOException ex) {
            System.out.println(ex.getMessage());
        }

        return dataArray;
    }

    public int getNumCols() {
        return numCols;
    }

    public int getNumRows() {
        return numRows;
    }
       

}

public class J1_IO_CSV_Demo_Rev2 {

    public static void main(String[] args) {

        String[][] theArray;
        
        String dataFile = "c:\\z\\citydata.csv";
        readCSV_BufferedReader br = new readCSV_BufferedReader(dataFile);
        
        theArray = new String[br.getNumRows()][br.getNumCols()];
        
        try {
           // This will over write the current array
           // with the returned array with the new dimensions
           theArray = br.readDataIntoArray(); 
        } catch (Exception e) {
            
            System.out.println(e.getMessage());
        }
        
        for (int r = 0; r < br.getNumRows(); r++) {
            for(int c = 0; c < br.getNumCols(); c++)
            {
                System.out.print(theArray[r][c] + " ");
            }
            System.out.println("");
        }
        

        System.out.println("\nbye");
    }
}


/*
 citydata.csv
 Key,Town,State,Population
 1,New York,New York,18713220
 2,Los Angeles,California,12750807
 3,Chicago,Illinois,8604203
 4,Miami,Florida,6445545
 5,Dallas,Texas,5743938
 6,Philadelphia,Pennsylvania,5649300
 7,Houston,Texas,5464251
 8,Atlanta,Georgia,5449398
 9,Washington,District of Columbia,5379184
 10,Boston,Massachusetts,4688346
 11,Phoenix,Arizona,4219697
 12,Seattle,Washington,3789215
 13,San Francisco,California,3592294
 14,Detroit,Michigan,3506126
 15,San Diego,California,3220118
 16,Minneapolis,Minnesota,2977172
 17,Tampa,Florida,2908063
 18,Denver,Colorado,2876625
 19,Brooklyn,New York,2559903
 20,Queens,New York,2230722
 21,Riverside,California,2107852
 22,Baltimore,Maryland,2106068
 23,Las Vegas,Nevada,2104198
 24,Portland,Oregon,2074775
 25,San Antonio,Texas,2049293
 26,St. Louis,Missouri,2024074
 27,Sacramento,California,1898019
 28,Orlando,Florida,1822394
 29,San Jose,California,1798103
 30,Cleveland,Ohio,1710093
 31,Pittsburgh,Pennsylvania,1703266
 32,Austin,Texas,1687311
 33,Cincinnati,Ohio,1662691
 34,Kansas City,Missouri,1636715
 35,Manhattan,New York,1628706
 36,Indianapolis,Indiana,1588961
 37,Columbus,Ohio,1562009
 38,Charlotte,North Carolina,1512923
 39,Virginia Beach,Virginia,1478868
 40,Bronx,New York,1418207
 41,Milwaukee,Wisconsin,1365787
 42,Providence,Rhode Island,1203230
 43,Jacksonville,Florida,1181496
 44,Salt Lake City,Utah,1098526
 45,Nashville,Tennessee,1081903
 46,Richmond,Virginia,1075798
 47,Memphis,Tennessee,1066967
 48,Raleigh,North Carolina,1038738
 49,New Orleans,Louisiana,1020886
 50,Louisville,Kentucky,1005654
 *
 */

```



---

End of Topic









