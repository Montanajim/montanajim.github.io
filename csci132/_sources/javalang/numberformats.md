# Number Formats

## Key Ideas

* Limiting decimal places
* Leading zeros
* Left padding
* Formatting numbers to have comas
* Formatting phone numbers
* Formatting dates and time



Example Code

```java
/*
	Number Formats
	Programmer: James Goudy
*/
package numberdateformats;

import java.math.BigInteger;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.util.Scanner;

public class NumberDateFormats
{

    //A function for left padding
    public static String LeftPadding(String input, 
            int totalWidth, char paddingCharacter)
    {
            String output = null;       //Outpout String
            int PaddingLength = 0;
            
            //Set oupt to input
            output = input; 
            
            //calculate the amount of padding
            PaddingLength = totalWidth - input.length();    
            
            //Add padding in front of input
            for(int cntr = 0; cntr <PaddingLength; cntr++)
            {
                output = paddingCharacter + output;
            }
                
            return output;
    }
    
    
    /**
     * @param args the command line arguments
     */
    public static void main(String[] args)
    {
        double answer = 0;
        double num1 = 1.0;
        double num2 = 3.0;
        String phoneNumber = "5554065555";
        double bigNumber = 123456789.1277;

        //DateTime(int year, int month, int day, 
        //         int hours, int minutes, int seconds)
        LocalDateTime myDate = LocalDateTime.of(2030, 8, 5, 20, 7, 9);

        answer = num1 / num2;

        //
        System.out.println("Answer is " + answer);

        //output using place holders
        System.out.println("\nOutput using placeholders");
        System.out.println(num1 + " \\ " + num2 + " = " + answer);

        //The first line is using the "ToString"
        //The second line is using String.format()
        // Limit answer to two decimal places 
        // # means if there is a number display it
        System.out.println("\nLimit Answer To Two Decimal Places");
        System.out.println("Answer is " + String.format("%.2f", answer));

        // Leading Zero - use 0 or 0's
        System.out.println("\nLimit answer to 3 decimal places"
                + "\nand include 2 leading zeros");
        System.out.println("Answer is " + String.format("%06.3f", answer));

        // Format a telephone number
        System.out.println("\nFormat a telephone number");
        System.out.println(String.format("(%s) %s-%s",
                phoneNumber.substring(0, 3),
                phoneNumber.substring(3, 6),
                phoneNumber.substring(6, 10)));
        
        // format number to include commas
        // 0's used after a decimal point 
        // means always display that those decimal places 
        System.out.println("\nFormat number to include commas");
        System.out.println(String.format("%,f", bigNumber));
        //System.out.println(String.format("{0:0,0.00}", bigNumber));

        //Date Examples
        System.out.println("\n\nDate Examples");
        System.out.println(String.format("%1$tm/%1$td/%1$ty", myDate));
        System.out.println(String.format("%1$tM/%1$td/%1$tY", myDate));
        System.out.println(String.format("%1$tA %1$tB %1$td, %1$tY", myDate));
        System.out.println(String.format("%1$ta %1$tb %1$td, %1$tY", myDate));
        System.out.println(String.format("%1$tB %1$td, %1$tY "
                + "%1$tI:%1$tM:%1$tS %1$tp", myDate));
        System.out.println(String.format("%1$tB %1$td, %1$tY "
                + "%1$tH:%1$tM:%1$tS", myDate));

        
        //Left Padding Example
        System.out.println(LeftPadding(String.valueOf(122.33), 10, '-'));
        System.out.println(LeftPadding(String.valueOf( 2.33), 10, '-'));
        System.out.println(LeftPadding(String.valueOf( 88882.56), 10, '-'));
        System.out.println(LeftPadding(String.valueOf( 
                String.format("%06.2f", answer)), 10, '-'));
        System.out.println(LeftPadding(String.valueOf(
                String.format("%03.2f", answer)), 10, '-'));
        System.out.println(LeftPadding(String.valueOf( 
                String.format("%1.4f", answer)), 10, '-'));
        
        // Exit Program
        System.out.println("\n\nPress Enter To Quit");

    }

}

/*
Answer is 0.3333333333333333

Output using placeholders
1.0 \ 3.0 = 0.3333333333333333

Limit Answer To Two Decimal Places
Answer is 0.33

Limit answer to 3 decimal places
and include 2 leading zeros
Answer is 00.333

Format a telephone number
(555) 406-5555

Format number to include commas
123,456,789.127700


Date Examples
08/05/30
07/05/2030
Monday August 05, 2030
Mon Aug 05, 2030
August 05, 2030 08:07:09 pm
August 05, 2030 20:07:09
----122.33
------2.33
--88882.56
----000.33
------0.33
----0.3333


Press Enter To Quit


*/
```



---

