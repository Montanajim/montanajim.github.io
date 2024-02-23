# Menus



**Java menus** provide a convenient way for users to choose from several options within a graphical user interface. Let’s dive into the details:

## **Menu Basics**:

- A menu allows users to select one option from a list of choices.
- Other components that offer similar one-of-many choices include combo boxes, lists, radio buttons, spinners, and toolbars.
- Menus are typically not placed directly with other UI components. Instead, they appear either in a **menu bar** or as a **popup menu**.
- A **menu bar** contains one or more menus and is usually positioned along the top of a window.
- A **popup menu** remains invisible until the user triggers it with a platform-specific mouse action (e.g., right-clicking) over a component.

## **Components in a Menu**:

- Menus consist of several related components:
  - **Menu Bar**: Contains menus and is usually located at the top of a window.
  - **Menus**: Represent a group of related options.
  - **Menu Items**: The actual choices within a menu.
  - **Radio Button Menu Items**: Allow single selection from a group.
  - **Check Box Menu Items**: Enable multiple selections.
  - **Separators**: Divide menu items visually.
  - Menu items can have text, images, or both.

## **Hierarchy and Activation**:

- Menu items (including menus) are essentially buttons.
- When a menu is activated (e.g., clicked), it displays a **popup menu** containing its menu items.



## Lecture Code

```java
/*
Project: Menu
Programmer: James Goudy

This program demonstrates how to programmically create a menus
 */
package jx_menu;

import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.InputEvent;
import java.awt.event.KeyEvent;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JMenu;

import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.KeyStroke;

class MenuDemo {

    // create our controls
    JFrame Frame1 = new JFrame();

    JMenuBar mb = new JMenuBar();

    JMenu mn_File = new JMenu();
    JMenu mn_MyMenu = new JMenu();

    JMenuItem mi_example1 = new JMenuItem("Example 1");
    JMenuItem mi_example2 = new JMenuItem("Example 2");
    JMenuItem mi_example3 = new JMenuItem("Example 3");
    JMenuItem mi_example4 = new JMenuItem("Example 4");
    JMenuItem mi_example5 = new JMenuItem("Example 5");
    JMenuItem mi_Quit = new JMenuItem();

    JLabel lblMenuPress = new JLabel();

    public MenuDemo() {

        Color frameColor = Color.lightGray;

        setupMenu1(Frame1);
        setupMenu2(Frame1);

        setUpTheJFrame(Frame1, 800, 600, "Menu Demo", frameColor, true);

        setupLabel(Frame1, lblMenuPress, 300, 250, 150, "---", 14);

        Frame1.repaint();
    }

    // Make sure the menu is setup before the frame
    // Setup the File menu
    private void setupMenu1(JFrame frm) {

        // Set the text for the first menu
        mn_File.setText("File");

        // add an ActionListener to each menuItem
        // note that the program is calling an action listener
        mi_example1.addActionListener(myActionListner);
        mi_example2.addActionListener(myActionListner);

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

        // add menu items to menu
        mn_File.add(mi_example1);
        mn_File.add(mi_example2);

        mn_File.addSeparator();

        // add the Menu item to Menu
        mn_File.add(mi_Quit);

        // add the menu to the menubar
        mb.add(mn_File);

        // set the menubar to the form
        frm.setJMenuBar(mb);

    }

    private void setupMenu2(JFrame frm) {

        // make sure that setupMenu2 runs after setup Menu1
        // set text for the second menu
        mn_MyMenu.setText("My Menu");

        // add an ActionListener to each menuItem
        // note that the menu item is adding an action listener
        // myactionListener if programmed later in the code.
        mi_example3.addActionListener(myActionListner);
        mi_example4.addActionListener(myActionListner);
        mi_example5.addActionListener(myActionListner);

        // Add the menu items to the menu
        mn_MyMenu.add(mi_example3);
        mn_MyMenu.add(mi_example4);

        mn_MyMenu.addSeparator();

        // Add the menu item to teh menu
        mn_MyMenu.add(mi_example5);

        // add the menu to menubar
        mb.add(mn_MyMenu);

    }

    ActionListener myActionListner = new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            // e is the thing that was clicked on
            
            // e.getSource tells it to get the thing that was clicked on
            // which in this case is the menu item
            // since e could be anything it needs to be identified by the 
            // (JMenuItem)
            JMenuItem x = (JMenuItem) e.getSource();
            
            // get the text from the menu item and set it in the JLablel
            lblMenuPress.setText(x.getText());

        }
    };

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

}

public class Jx_Menu {

    public static void main(String[] args) {

        MenuDemo demo1 = new MenuDemo();

    }

}

```

