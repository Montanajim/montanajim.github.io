# Building A String Using Combo, Lists, and Textfield



![image-20250321152932642](./assets/image-20250321152932642-1742592580768-1.png)



```java
/*
Developer: James Goudy

The provided Java program defines a simple GUI application using 
the Swing framework. The application displays several user interface 
components such as a JTextField, JComboBox, JList, JTextArea, and 
JButton within a main JFrame. Each component is positioned manually 
using absolute positioning, as the layout manager is set to null. 
The application demonstrates how to build a concatenated string from 
various form elements, then display that result in a multi-line text area.


 */
package j2_textfield_combo_list_buildstring;

//import java.awt.List;
import java.awt.Color;
import java.awt.Font;
import java.util.List;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import javax.swing.DefaultListModel;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JList;
import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.KeyStroke;
import javax.swing.ListSelectionModel;

/**
 *
 * @author jgoudy
 */
public class J2_Textfield_Combo_List_BuildString {

    // creating our application frame and controls
    static JFrame       myFrame     = new JFrame();
    static JTextField   myTextField = new JTextField();
    static JComboBox    myCombo     = new JComboBox();
    static JList        myList      = new JList();
    static JButton      myButton    = new JButton();
    static JTextArea    myTextArea  = new JTextArea();
    static JMenuBar     myMenuBar   = new JMenuBar();
    static JLabel       myLabel     = new JLabel();

    static int xpos = 50;
    static int ypos = 50;
    static int spacing = 20;

    public static void main(String[] args)
    {
        setupApp();

    }

    private static void setupApp()
    {
        // helper functions to build the 

        // Build the menubar first
        // then add it to the frame
        setupMenuBar();
        
        setupFrame();
        
        setupJLabel();

        setupTextField();

        setupCombo();

        setupList();

        setupTextArea();

        setupButton();

    }




    private static void setupMenuBar(){

        // Create a new "File" menu
        JMenu myMenuFile = new JMenu("File");
    
        // Create a new menu item (initially without text)
        JMenuItem myMenuQuit = new JMenuItem();
        
        // Set the text label for the Quit menu item
        myMenuQuit.setText("Quit");
        
        // demonstrate colors
        myMenuQuit.setBackground(Color.yellow); 
        myMenuQuit.setForeground(Color.blue);    
        
        // adding the keyboard shortcut
         // Set Ctrl+Q as shortcut
        myMenuQuit.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_Q, 
                                            KeyEvent.CTRL_DOWN_MASK ));
        // Exit the program when selected
        myMenuQuit.addActionListener(e -> System.exit(0));  
        
        // Add the Quit item to the File menu
        myMenuFile.add(myMenuQuit);
                
        // Make the menu bar visible and add the File menu to it
        myMenuBar.setVisible(true);
        myMenuBar.add(myMenuFile);
        
        // Attach the menu bar to the main application frame
        myFrame.setJMenuBar(myMenuBar);
    }
    
    
    private static void setupFrame()
    {

        // frame size 575 x 460
        myFrame.setSize(575, 460);

        // set location
        myFrame.setLocationRelativeTo(null);

        // set visibility
        myFrame.setVisible(true);

        // set close action
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // layout manager
        myFrame.setLayout(null);
        
        // set title
        myFrame.setTitle("Building Strings");
        
    }

    
    private static void setupJLabel(){
    
        // set text
        myLabel.setText("Building Strings");
        
        // set fontsize
        // Sets the label's font to bold with size 24, 
        // retaining the original font name.
        // Retrieves the current font name and 
        // creates a new Font object with updated style and size.
        myLabel.setFont(new Font(myLabel.getFont().getName(),Font.BOLD,24));
        
        // set size
        myLabel.setSize(200, myLabel.getFont().getSize()+ 4);
                
        // set visibility
        myLabel.setVisible(true);
        
        // Set position
        myLabel.setLocation(50, 10);
        
        // add to frame
        myFrame.add(myLabel);
    
    }
    
    private static void setupTextField()
    {

        // size 200 x 25
        myTextField.setSize(200, 25);

        // set location
        myTextField.setLocation(xpos, ypos);

        // set visibility
        myTextField.setVisible(true);

        // add to frame
        myFrame.add(myTextField);

        ypos = ypos + 25 + spacing;

    }

    private static void setupCombo()
    {

        // combo items
        String[] myItems = {"Lions", "Tigers", "Bears"};

        //  size 200 x 25
        myCombo.setSize(200, 25);

        // set location
        myCombo.setLocation(xpos, ypos);

        // set visibility
        myCombo.setVisible(true);

        // add data
        for (String value : myItems) {
            myCombo.addItem(value);
        }
        // ALTERNATIVE WAY TO ADD DATA        
        //        for(int i = 0; i < myItems.length; i++)
        //        {
        //            myCombo.addItem(myItems[i]);
        //        }



                // add to frame
                myFrame.add(myCombo);

                ypos = ypos + 25 + spacing;

            }

    private static void setupList()
    {

        // combo items
        String[] myItems = {"Planes", "Trains", "Automobiles", "Bikes"};

        //  size  200 x 210
        myList.setSize(200, 210);

        // set location
        myList.setLocation(xpos, ypos);

        // set visibility
        myList.setVisible(true);

        // multi select
        myList.setSelectionMode(ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);

        // add data
        DefaultListModel myListModel = new DefaultListModel();
        
        // add data
        for (String value : myItems) {
            myListModel.addElement(value);
        }

        myList.setListData(myItems);

        // add to frame
        myFrame.add(myList);

    }

    private static void setupTextArea()
    {

        //  size  200 x 260
        myTextArea.setSize(200, 260);

        // set location
        myTextArea.setLocation(300, 90);

        // set visibility
        myTextArea.setVisible(true);

        // Add to Frame
        myFrame.add(myTextArea);

    }

    private static void setupButton()
    {

        // frame size 200 x 25
        myButton.setSize(200, 25);

        // set location
        myButton.setLocation(300, 50);

        // set visibility
        myButton.setVisible(true);

        // set text
        myButton.setText("Create List");
        
        
        // this is the button press
        myButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e)
            {
                String myString = "";
                
                // Build the string
                myString = "TextField: " + myTextField.getText() + "\n";

                myString = myString + "Combo: "
                        + myCombo.getSelectedItem() + "\n";

                List mySelectedItems = myList.getSelectedValuesList();

                myString = myString + "ListBox: \n";

                for (Object value : mySelectedItems) {
                    myString = myString + value + "\n";
                }

                myTextArea.setText(myString);

            }
        });
        
        
        // ALTERNATIVE Way To Add Action Listener
        //        ActionListener myActionListener = new ActionListener() {
        //            @Override
        //            public void actionPerformed(ActionEvent e)
        //            {
        //                System.out.println("Hello World");
        //            }
        //        };
        //        
        //        
        //        myButton.addActionListener(myActionListener);


        // add to frame
        myFrame.add(myButton);

    }

}

```

