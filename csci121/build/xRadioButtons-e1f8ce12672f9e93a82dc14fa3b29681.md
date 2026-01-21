# Radio Buttons

## **Properties**:

- **Text**: You can set the display text for the radio button using the `setText(String s)` method.
- **Selected State**: The `isSelected()` method allows you to check whether the radio button is currently selected.
- **Enabled/Disabled**: You can enable or disable the radio button using the `setEnabled(boolean b)` method.
- **Icon**: The `setIcon(Icon icon)` method lets you set an icon for the radio button.
- **Mnemonic**: You can assign a keyboard shortcut (mnemonic) to the radio button using the `setMnemonic(int a)` method.

## **Events**:

- **Action Event**: When a radio button is pressed and released, an `ActionEvent` is sent. You can handle this event using an `ActionListener`.
- **Item Event**: When the selection state of the radio button changes, an `ItemEvent` is generated. You can handle this event using an `ItemListener`.

 In Java, an **ActionListener** is an interface that allows you to handle action events triggered by user interactions with components such as buttons, menu items, or text fields. When the user performs a specific action (e.g., clicks a button or presses Enter in a text field), an action event occurs, and the registered ActionListener responds to it.



## ButtonGroup

Is a class that allows you to group together a set of radio buttons. When you create a group of radio buttons using a ButtonGroup, only one radio button within that group can be selected at a time. Here are the key points about ButtonGroup:

1. **Purpose**:
   - A ButtonGroup ensures that only one radio button in the group can be selected simultaneously.
   - It prevents users from selecting multiple radio buttons within the same group.
1. **Usage**:
   - To create a ButtonGroup:
     - Instantiate a new ButtonGroup object: `ButtonGroup group = new ButtonGroup();`
     - Add individual radio buttons to the group using the `add(AbstractButton button)` method: `group.add(radioButton1);`
1. **Behavior**:
   - When a radio button is selected, any previously selected radio button in the same group is automatically deselected.
   - Radio buttons within the same group share the same selection state.



## ActionListener:

1. **Purpose**:

   - An ActionListener defines what should happen when a specific action occurs on a component.
   - It is commonly used for handling button clicks, menu selections, or other user interactions.

1. **Implementation**:

   - To create an ActionListener, you can either:

     - Implement the `ActionListener` interface directly in your class.
     - Extend a class that already implements `ActionListener`.

   - The only method in the ActionListener interface is

     ```
     actionPerformed(ActionEvent e)
     ```

     - This method is called when the associated action event occurs.
     - The `ActionEvent` object provides information about the event and its source.

1. **Registration**:

   - To use an ActionListener:

     - Create an instance of your event handler class (which implements ActionListener).

     - Register this instance as an action listener on the relevant component using `addActionListener(this)`.

       

## Code

```java
/*
Project:        Radio Buttons
Description:    This shows how to programmically create radio buttons.
                And, to make an appropriate selection if a radio button is 
                selected.
                The program allows the user to click a radio button for a dog.
                It then displays the dog in the a label. And the user
                has the option of getting a description of the dog by
                clicking the button or hitting the enter key.
                Note: That the radio buttons are assign to a radio button group.

Programmer:     James Goudy
 */
package j2x_5_radiobuttons;

import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.InputEvent;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import javax.swing.ButtonGroup;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JRadioButton;
import javax.swing.JTextArea;
import javax.swing.KeyStroke;

class Frame1 {

    // create our controls
    // Frame
    JFrame Frame1 = new JFrame();

    // Menu Bar
    JMenuBar mb = new JMenuBar();
    JMenu mn_File = new JMenu();
    JMenuItem mi_Quit = new JMenuItem();

    // Radio Buttons
    JRadioButton jrbGolden = new JRadioButton();
    JRadioButton jrbLab = new JRadioButton();
    JRadioButton jrbSpring = new JRadioButton();

    ButtonGroup jbgDog = new ButtonGroup();

    // Labels
    JLabel lblSelectedDog = new JLabel();

    // Text
    JTextArea jtaDescription = new JTextArea();

    // Description Button
    JButton jbttnDesc = new JButton();

    // Descriptions
String GoldDesc = """
Golden retrievers, known for their radiant coats 
and sunny personalities, are beloved companions prized 
for their gentle nature and intelligence. These 
versatile dogs excel as both family pets and 
working partners, offering unwavering loyalty, 
eagerness to please, and boundless enthusiasm 
for life's adventures.                  
""";

    String LabDesc = """
Black Labradors, with their sleek, shiny coats 
and expressive eyes, are the most popular 
color variation of this beloved breed. These 
medium-sized dogs boast a playful and 
affectionate personality, making them excellent 
companions for families and active individuals. 
Renowned for their intelligence and eagerness 
to please, black Labs excel in training and are 
often employed as guide dogs, service dogs, and 
even search and rescue partners. However, their 
boundless energy requires ample daily exercise 
and mental stimulation to keep them happy and 
well-behaved.
""";

    String SpringDesc = """
Springer spaniels are energetic and intelligent 
dogs known for their sweet nature and playful 
spirit. These medium-sized bundles of joy boast 
a soft, double coat in various colors and a gentle 
expression that melts hearts. Bred for hunting, 
they possess impressive stamina and agility, making 
them excellent companions for active families and 
outdoor enthusiasts. However, their eagerness to 
please and trainability also make them adaptable 
to different lifestyles, as long as their need 
for exercise and mental stimulation is met.
""";

    // final means that the varaible contents cannot change
    // making the following variable "final", will allow 
    // the variables to be used in the switch statement
    final String gldText = "Golden Retreiver";
    final String labText = "Labrador";
    final String sprngText = "Springer Spaniel";

    ActionListener aclGolden = new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            lblSelectedDog.setText(gldText);
            jtaDescription.setText("");
        }
    };

    ActionListener aclSpring = new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            lblSelectedDog.setText("Springer Spaneil");
            jtaDescription.setText("");
        }
    };

    ActionListener aclLab = new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            lblSelectedDog.setText(labText);
            jtaDescription.setText("");
        }
    };

    public Frame1() {

        int frameWidth = 750;
        int frameHeight = 350;

        int rbxPos = 20;
        int rbyPos = 20;

        int vspacing = 50;

        int rbWidth = 150;
        int rbHeight = 25;

        // -----------  Frame Setup -------------------------------
        // this has to go before setting up the frame
        setupMenu1(Frame1);

        // frame setup
        setUpTheJFrame(Frame1, frameWidth, frameHeight,
                "Radio Buttons", Color.white, true);

        // -----------  Radio Buttons Setup -----------------------
        // add the radio buttons after the frame has been setup
        setupRadioButtons(jrbGolden, rbxPos, rbyPos, rbWidth, rbHeight, jbgDog,
                gldText, true, true, Frame1, aclGolden);

        setupLabel(Frame1, lblSelectedDog, 200, rbyPos, rbWidth, gldText, 12);

        rbyPos = rbyPos + vspacing;
        

        setupRadioButtons(jrbLab, rbxPos, rbyPos, rbWidth, rbHeight, jbgDog,
                labText, true, true, Frame1, aclLab);

        rbyPos = rbyPos + vspacing;

        setupRadioButtons(jrbSpring, rbxPos, rbyPos, rbWidth, rbHeight, jbgDog,
                sprngText, true, true, Frame1, aclSpring);

        // -----------  Description Button Setup ------------------
        // add the jbutton
        setupButton(Frame1, jbttnDesc, 200, 72, rbWidth, "Description", 12);
        
        // -----------  TextArea Setup -----------------------------
        // add the description text
        setupTextArea(Frame1, jtaDescription , 400, 20, 400, 500, 
                "---", 12,false);

        Frame1.repaint();

    }

    private void setUpTheJFrame(JFrame jf1, int frameWidth, int frameHeight,
            String frameTitle, Color frameColor,
            boolean turnLayoutManagerOff) {

        // Set the initial dimensions of the JFrame's window
        jf1.setSize(frameWidth, frameHeight);

        // Set the JFrame title
        jf1.setTitle(frameTitle);

        // Apply a custom background color to the content pane
        // The content pane is the area where items are added to
        // the frame
        jf1.getContentPane().setBackground(frameColor);

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
        // disable the default layout manager
        if (turnLayoutManagerOff) {
            jf1.setLayout(null);
        }
    }

    // Make sure the menu is setup before the frame
    // Setup the File menu
    private void setupMenu1(JFrame frm) {

        // Set the text for the first menu
        mn_File.setText("File");

        // setup the quit menu item
        mi_Quit.setText("Quit");

        // set the ctrl-Q shortcut for quitting
        mi_Quit.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_Q,
                InputEvent.CTRL_DOWN_MASK));

        // add an action listener to close down the program
        mi_Quit.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.exit(0);
            }
        });

        mn_File.addSeparator();

        // add the Menu item to Menu
        mn_File.add(mi_Quit);

        // add the menu to the menubar
        mb.add(mn_File);

        // set the menubar to the form
        frm.setJMenuBar(mb);

    }

    private void setupRadioButtons(JRadioButton jrb, int xpos, int ypos,
            int rbWidth, int rbHeight, ButtonGroup jbg, String rbText,
            boolean rbVisible, boolean rbSelected,
            JFrame frm, ActionListener acl) {

        // Set position on frame
        jrb.setLocation(xpos, ypos);

        // set the size
        jrb.setSize(rbWidth, rbHeight);

        // set visiblity
        jrb.setVisible(rbVisible);

        // alternative placement
        //jrb.setBounds(xpos, ypos, rbWidth, rbHeight);
        
        // select it
        jrb.setSelected(rbSelected);

        // set button text
        jrb.setText(rbText);
        jrb.addActionListener(acl);

        // add radio button to Radio Button Group
        jbg.add(jrb);

        // add radio button to form
        frm.add(jrb);

        frm.repaint();
    }

    private void setupLabel(JFrame jf1, JLabel lbl,
            int xpos, int ypos, int lblWidth,
            String theText, float labelSize) {
        // Set the font size to 12 points
        // NOTE: Have to do this before we add the text
        lbl.setFont(lbl.getFont().deriveFont(labelSize));

        // Set the preferred size of the label
        lbl.setSize(lblWidth, (int) labelSize + 8);

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
    
    private void setupTextArea(JFrame jf1, JTextArea jta,
            int xpos, int ypos, int jtaWidth,int jtaHeight,
            String theText, float fontSize, boolean jtaIsEditable) {
        // Set the font size to 12 points
        // NOTE: Have to do this before we add the text
        jta.setFont(jta.getFont().deriveFont(fontSize));

        // Set the preferred size of the label
        jta.setSize(jtaWidth,jtaHeight);

        // Set the text content of the label
        jta.setText(theText);

        // Make the label visible
        jta.setVisible(true);

        // Position the label at coordinates (10, 10) within the window
        jta.setLocation(xpos, ypos);
                
        // Set editable status
        jta.setEditable(jtaIsEditable);
        
        // Add the label to the window's content pane
        jf1.add(jta);  // Assuming jf1 is the main window object      

        // Request the window to be redrawn, reflecting the added label
        jf1.repaint();
    }

    private void setupButton(JFrame jf1, JButton bttnABttn,
            int xpos, int ypos, int bttnWidth,
            String bttnText, float fsize) {

        // Set the font size to 12 points
        // NOTE: Have to do this before we add the text
        bttnABttn.setFont(bttnABttn.getFont().deriveFont(fsize));

        // Set the preferred size of the label
        bttnABttn.setSize(bttnWidth, (int) fsize + 8);

        // Set the text content of the label
        bttnABttn.setText(bttnText);

        // Make the label visible
        bttnABttn.setVisible(true);

        // Position the label at coordinates (xpos, ypos) within the window
        bttnABttn.setLocation(xpos, ypos);

        // This action listener listens for the mouse click
        bttnABttn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                theButtonAction(bttnText);
            }
        });

        // This key listener is for listening for the keyboard actions
        bttnABttn.addKeyListener(new KeyListener() {

            // For Reference
            @Override
            public void keyTyped(KeyEvent e) {

            }

            // listen only for the "Enter" key
            @Override
            public void keyPressed(KeyEvent e) {

                if (e.getKeyCode() == KeyEvent.VK_ENTER) {
                    theButtonAction(bttnText);
                }
            }

            // For Reference
            @Override
            public void keyReleased(KeyEvent e) {

            }
        });

        // Add the label to the window's content pane
        jf1.add(bttnABttn);  // Assuming jf1 is the main window object

        // Request the window to be redrawn, reflecting the added label
        jf1.repaint();

    }

    private void theButtonAction(String bttnText) {
  
        if(jrbGolden.isSelected())
        {
            jtaDescription.setText(GoldDesc);
        }else if(jrbLab.isSelected())
        {
            jtaDescription.setText(LabDesc);
        }
        else if(jrbSpring.isSelected())
        {
            jtaDescription.setText(SpringDesc);
        }
        

    }
} // End of class

// --------------------------------------------------------
public class J2x_5_RadioButtons {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        Frame1 myFrame = new Frame1();
    }

}

```

