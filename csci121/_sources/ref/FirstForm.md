# First Form





##  JFrame

**Basic Properties:**

- **Title:** The text displayed on the title bar of the window.

- **Size:** Width and height of the window in pixels.

- **Location:** The position of the window on the screen, specified by the x and y coordinates of its top-left corner.

- **Resizable:** Determines whether the user can resize the window.

- **Visible:** Determines whether the window is displayed on the screen.

- **Icon:** The icon displayed in the title bar and taskbar.

- **Default Close Operation:** Defines what happens when the user tries to close the window (e.g., hide, dispose, exit the application).

  

**Content Pane:**

- **Layout:** The *layout manager* used to organize the components within the frame. Different layout managers offer different ways to arrange components (e.g., BorderLayout, FlowLayout, GridLayout).
- **Components:** The set of graphical components (buttons, text fields, labels, etc.) displayed within the frame.



**Behavior Properties:**

- **Modal:** Determines whether the window blocks interaction with other windows while it's open.
- **Always on Top:** Determines whether the window stays on top of other windows.
- **Focusable:** Determines whether the window can receive keyboard focus.
- **Minimizable:** Determines whether the user can minimize the window to the taskbar.
- **Maximizable:** Determines whether the user can maximize the window to fill the screen.



**Look and Feel:**

- **Look and feel:** Defines the overall visual appearance of the frame and its components (e.g., Windows, Metal, Nimbus).
- **Font:** The default font used for text within the frame.
- **Colors:** The default colors used for various elements of the frame (e.g., background, foreground, border).



**Accessibility:**

- **Accessible name:** A description of the frame for assistive technologies like screen readers.
- **Accessible description:** A more detailed description of the frame's purpose and content.



**Additional Properties:**

- **Glass pane:** A transparent component that can be used to block user interaction with the underlying components.
- **Root pane:** The top-level container that holds the frame's content.
- **JMenuBar:** The menu bar displayed at the top of the frame.
- **WindowListener:** Objects that are notified when specific events occur (e.g., window opens, closes, minimizes).

------



##  JLabel:

- **text:** The main content of the label, displayed as a single line of text.
- **font:** Controls the typeface, size, and style of the displayed text.
- **foreground:** Sets the color of the text.
- **background:** Sets the color background behind the text.
- **horizontalAlignment:** Controls the horizontal alignment of the text within the label (LEFT, RIGHT, CENTER).
- **verticalAlignment:** Controls the vertical alignment of the text within the label (TOP, BOTTOM, CENTER).
- **icon:** An optional image displayed alongside the text.
- **enabled:** Sets whether the label is visible and usable (true for active, false for disabled).
- **tooltip:** A short explanatory text displayed when hovering over the label.
- **border:** Optional border around the label for visual styling.
- **mnemonic:** A specific key that, when pressed, focuses the associated component (useful for accessibility).

------



## JTextField

### Basic Properties:



- **Text:** This is the actual content displayed in the field.
- **Columns:** Specifies the preferred width of the field in characters.
- **Editable:** This boolean flag determines whether users can modify the text.
- **Enabled:** This boolean flag determines whether the field is usable or disabled.
- **Visible:** This boolean flag determines whether the field is visible on the screen.
- **Font:** This sets the typeface, size, and style of the text.
- **Foreground:** This sets the color of the text.
- **Background:** This sets the color of the field's background.
- **Alignment:** This determines how text is positioned within the field (left, center, right).



**Input Formatting:**

- **Document:** This allows you to set custom filters and restrictions on the type of text that can be entered (e.g., numbers only, specific format).
- **Caret position:** This specifies where the cursor appears in the field.
- **Selection:** This allows you to highlight a portion of the text.



**Event Handling:**

- **Action command:** This defines the text sent when the user performs an action (e.g., pressing Enter) in the field.
- **Action listeners:** These are objects that respond to actions performed in the field.
- **Focus listeners:** These are objects that are notified when the field gains or loses focus.



**Additional Properties:**

- **Tooltip:** This provides a short informational message that appears when the user hovers over the field.
- **Border:** This defines the visual appearance of the field's border.
- **Accessible name:** This describes the field for assistive technologies like screen readers.



## Example Code

```java
/*
Progam: First Form - Basic Calculator

Function:   The purpose of the program is to add and subtract two numbers
            It also needs to have a clear button

Programmer: James Goudy ©2024

 */
package j2x_1_firstform;

import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import javax.swing.*;

// Class to create and manage a basic JFrame
class form1 {

    // remember that when a control is created
    // it has no dimensions, no location,
    // and its visibility is set to false.
    
    // create the frame
    JFrame jf1 = new JFrame("First Form");
    
    // create the lablels
    JLabel jlbl_Title = new JLabel();
    JLabel jlblBox1 = new JLabel();
    JLabel jlblBox2 = new JLabel();
    JLabel jlblAns = new JLabel();
    JLabel jlblAnsValue = new JLabel();
    
    // create the textfields
    JTextField jtxt1 = new JTextField();
    JTextField jtxt2 = new JTextField();
    
    // create the buttons
    JButton jbttnAdd = new JButton();
    JButton jbttnSub = new JButton();
    JButton jbttnClear = new JButton();
    
    // create a customize color
    Color myColor = new Color(210, 180, 140);
    
    // Constructor to initialize the form
    public form1() {
        
        int TitleSz = 24;       // Title Size
        int TextSz = 12;        // Text Size
             
        // Call the method to set up the JFrame
        setUpTheJFrame();

        // add Title label to the form
        setupLabelBox(jlbl_Title, 10, 10, "Calculator", TitleSz);
        
        // setup the first textfield with a lablel
        setupLabelBox(jlblBox1, 10, 50, "First Number",TextSz);
        setupTextFields(jtxt1, 150, 50,12);

        // setup the second textfield with a label
        setupLabelBox(jlblBox2, 10, 75, "Second Number", TextSz);
        setupTextFields(jtxt2, 150, 75,12);

        // setup the answer label and a labele to hold the answer
        setupLabelBox(jlblAns, 10, 100, "Answer",TextSz);
        setupLabelBox(jlblAnsValue, 150, 100, "---",TextSz);

        // setup the buttons
        setMathButtons(jbttnAdd, 10, 125, "+");
        setMathButtons(jbttnSub,60, 125,"-");
        setMathButtons(jbttnClear, 110, 125, "C");
    }

	// Private method to configure the JFrame's visual 
        // and behavioral properties
	private void setUpTheJFrame() {

		// Set the initial dimensions of the JFrame's window
		jf1.setSize(400, 250); 

		// Apply a custom background color to the content pane
                // The content pane is the area where items are added to 
                // the frame
		jf1.getContentPane().setBackground(myColor);  

		// Make the JFrame visible on the screen, 
                // allowing users to interact with it
		jf1.setVisible(true);

		// Center the JFrame on the user's screen for optimal visibility
		jf1.setLocationRelativeTo(null);

		// Specify the program's termination behavior 
                // when the JFrame is closed
		// Exit the program when the frame is closed
		jf1.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  

		// Disable the default layout manager, allowing 
		// for manual component positioning
		 // Note: Manual layout can be more complex to manage
		jf1.setLayout(null); 
	}


    private void setupLabelBox(JLabel lbl, int xpos, int ypos, 
            String theText, float labelSize) {
        // Set the font size to 12 points
        // NOTE: Have to do this before we add the text
        lbl.setFont(lbl.getFont().deriveFont(labelSize));

        // Set the preferred size of the label
        lbl.setSize(150, (int)labelSize + 8);

        // Set the text content of the label
        lbl.setText(theText);

        // Make the label visible
        lbl.setVisible(true);

        // Position the label at coordinates (10, 10) within the window
        lbl.setLocation(xpos, ypos);

        // Add the label to the window's content pane
        jf1.add(lbl);  // Assuming jf1 is the main window object

        // Request the window to be redrawn, reflecting the added label
        jf1.repaint();
    }

    private void setupTextFields(JTextField jtxt, 
            int xpos, int ypos, float fsize) {
        // Set the font size to 12 points
        // NOTE: Have to do this before we add the text
        jtxt.setFont(jtxt.getFont().deriveFont(12f));

        // Set the preferred size of the label
        jtxt.setSize(100, (int)fsize + 8);

        // Set the text content of the label
        jtxt.setText("0");

        // Make the label visible
        jtxt.setVisible(true);

        // Position the label at coordinates (10, 10) within the window
        jtxt.setLocation(xpos, ypos);

        // Add the label to the window's content pane
        jf1.add(jtxt);  // Assuming jf1 is the main window object

        // Request the window to be redrawn, reflecting the added label
        jf1.repaint();
    }

    private void setMathButtons(JButton jbttnMath, int xpos, int ypos,
            String mathOp) {

        // Set the font size to 12 points
        // NOTE: Have to do this before we add the text
        jbttnMath.setFont(jbttnMath.getFont().deriveFont(12f));

        // Set the preferred size of the label
        jbttnMath.setSize(45, 45);

        // Set the text content of the label
        jbttnMath.setText(mathOp);

        // Make the label visible
        jbttnMath.setVisible(true);

        // Position the label at coordinates (xpos, ypos) within the window
        jbttnMath.setLocation(xpos, ypos);

        // This action listener listens for the mouse click
        jbttnMath.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
				// the string operator is passed to the function
                               
                mathCalc(mathOp);
                
                // in production, if there are complex operations
                // or many lines of code, then writing out
                // separate functions may be preferable
            }
        });

        // This key listener is for listening for the keyboard actions
        jbttnMath.addKeyListener(new KeyListener() {
            
            // For Reference
            @Override
            public void keyTyped(KeyEvent e) {

            }

            // listen only for the "Enter" key
            @Override
            public void keyPressed(KeyEvent e) {

                if (e.getKeyCode() == KeyEvent.VK_ENTER) {
                    mathCalc(mathOp);
                }
            }

            // For Reference
            @Override
            public void keyReleased(KeyEvent e) {
                
            }
        });

        // Add the label to the window's content pane
        jf1.add(jbttnMath);  // Assuming jf1 is the main window object

        // Request the window to be redrawn, reflecting the added label
        jf1.repaint();

    }

    /**    Function to do the appropriate Math operation.
            Note that the operation sign is being passed to the function */
    private void mathCalc(String mathOp) {
        double ans = 0.0;

        try {
            switch (mathOp) {
                case "+" -> {
                    // Retreive the text from the textfield 
                    // and parse it into a double datatype
                    ans = Double.parseDouble(jtxt1.getText())
                            + Double.parseDouble(jtxt2.getText());
                    
                    // place the answer in the Answer Value label
                    jlblAnsValue.setText(String.valueOf(ans));
                }
                case "-" -> {
                    ans = Double.parseDouble(jtxt1.getText())
                            - Double.parseDouble(jtxt2.getText());
                    jlblAnsValue.setText(String.valueOf(ans));
                }
                case "C" -> {
                    // Clear the textfields by setting the 
                    // contents to an empty string
                    jtxt1.setText("");
                    jtxt2.setText("");
                    jlblAnsValue.setText(""); 
                    
                    // Place the cursor in the first textfield
                    // using the requestFocus command
                    jtxt1.requestFocus();
                }

            }
        } catch (Exception e) {
            jlblAnsValue.setText("You had an error");
            jtxt1.setText("");
            jtxt2.setText("");
            jtxt1.requestFocus();
        }
    }

}

public class J2x_1_firstform {

    public static void main(String[] args) {
        // create a frame window
        form1 myForm = new form1();
    }

}

```

