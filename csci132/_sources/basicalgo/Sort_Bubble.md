# Bubble Sort

## Key Ideas

* Bubble Sort



```{admonition} Definition
**Bubble Sort** is a simple sorting algorithm that repeatedly iterates through the list or array. It compares adjacent elements and swaps them if they are in the wrong order. The algorithm repeatedly passes through the list until the list is sorted. It is a comparison sort and is named for the way smaller or larger elements "bubble" to the top of the list.
```



# Performance

Bubble sort has a worst-case and average complexity of On^2^.



##  Visualizations

[Visual Aglo](https://visualgo.net/en/sorting)

[Toptal](https://www.toptal.com/developers/sorting-algorithms)

[Comparison Sorting Algorithms](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html)

[Sort Visualizer](https://www.sortvisualizer.com/)



## Videos

<iframe width="560" height="315" src="https://www.youtube.com/embed/xli_FI7CuzA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/lyZQPjUT5B4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
---



## Lecture Code

```java
/*
 * Programmer: James Goudy
 * Project: Bubble Sort
 */
package com.mycompany.bubblesort_lecturecode;

import java.util.Random;

class BubbleSort {

    // arrInt is an array of integers
    // numDataElements is the actual count 
    // of elements of data in the array
    // algorithm assumes the data is contiguous
    int arrInt[];
    int numDataElments;

    public BubbleSort(int[] arrInt, int numDataElments) {
        this.arrInt = arrInt;
        this.numDataElments = numDataElments;
    }

    public void Sort() {
        // 
        int n = numDataElments;

        for (int c = 0; c < n; c++) {
            for (int j = 1; j < (n); j++) {
                
                // check if the left element is 
                // greater to the one on the right
                // "Bubble" the lowest to the left

                if (arrInt[j - 1] > arrInt[j]) {
                    // swap left element arr[j-1]
                    // with the one on the right and arr[j]
                    
                    // store left one in temp
                    int temp = arrInt[j - 1];
                    //copy the right into the left
                    arrInt[j - 1] = arrInt[j];
                    //copy the left into the right
                    arrInt[j] = temp;
                }
            }
        }
    }

}

public class BubbleSort_LectureCode {

    static int arrSize = 8;
    //static int theArray[] = new int[arrSize];
    static int theArray[] ={3,60,35,2,45,320,5,1}; 
    
    static void fillTheArray()
    {
        Random RNG  = new Random();
        for(int c = 0; c < arrSize; c++)
        {
            theArray[c] = RNG.nextInt(0,(arrSize*10));
        }
    }
    
    static void printArray(int anArray[], int numOfDataElements)
    {
        System.out.println("");
        for (int i = 0; i < numOfDataElements; i++) {
            System.out.print(anArray[i] + " ");
        }
        System.out.println("\n--------------\n");
        
    }
    
    public static void main(String[] args) {
       
        // option to randomly fill the array
        //fillTheArray();
        
        printArray(theArray, arrSize);
        
        BubbleSort bs = new BubbleSort(theArray, arrSize);
        bs.Sort();
        
        printArray(theArray, arrSize);
               
        
    }
}

/*
3 60 35 2 45 320 5 1 
--------------


1 2 3 5 35 45 60 320 
--------------
*/
```



---

End Of Topic



