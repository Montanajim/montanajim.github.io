# Game Piece - Dynamically Adding Pieces to a Panel



**Summary:**

This Java code creates a graphical user interface (GUI) application using the Swing library. It demonstrates a custom component called `GamePiece`. The application displays a 4x4 grid of these `GamePiece` objects within a panel. Alongside the grid, there are control buttons that allow the user to randomly change the colors, text, or both, displayed on the game pieces, as well as a button to reset them to a default state.

**Detailed Analysis:**

1. **GUI Setup (`J2x_Game_Piece_Demo` class):**

   - **Components:** It defines standard Swing components: a main window (`JFrame`), a panel (`JPanel`) to hold the game pieces, several buttons (`JButton`), and a label (`JLabel`).

   - Data Storage:

     - `myAl`: An `ArrayList` to hold the 16 `GamePiece` objects.
     - `colorAl`: An `ArrayList` to store predefined `Color` objects.
     - `myWords`: A `String` array containing predefined words.

   - Functionality Variables:

     - `RNG`: A `Random` object for generating random numbers.
     - `myTimer`: A `Timer` object to create an animation-like effect when randomizing.
     - `xChoice`: An integer (`int`) that determines *what* the timer should randomize (1=colors, 2=words, 3=both).

   - **Layout:** The code manually sets the size and position of the frame, panel, label, and buttons using absolute coordinates (`setSize`, `setLocation`).

   - Initialization (`main`, `setupApp`, `setupFrame`, etc.):

      The 

     ```
     main
     ```

      method calls 

     ```
     setupApp
     ```

     , which in turn calls helper methods to:

     - Configure the main window (`setupFrame`).
     - Configure the panel (`setupPanel`).
     - Create and position the buttons, adding `ActionListener`s to them (`setupButtons`).
     - Configure and position the label (`setupJLabel`).
     - Create the 16 `GamePiece` instances, set their initial properties, add `MouseListener`s, and add them to the panel (`PieceSetup`).
     - Populate the list of available colors (`colorSetup`).
     - Initialize the `Timer` (`setupApp`).

2. **`GamePiece` Class:**

   - **Custom Component:** This class extends `JComponent`, making it a custom drawable Swing component.
   - **State:** Each `GamePiece` has its own `pieceColor` (a `Color` object) and `letters` (a `String`).
   - **Painting (`paintComponent`):** This crucial method defines *how* a `GamePiece` looks. It draws a black rectangle as a border, then fills a slightly smaller rectangle inside with the `pieceColor`, and finally draws the `letters` string centered horizontally within the piece.
   - **Getters/Setters:** Provides methods (`getPieceColor`, `setPieceColor`, `getLetters`, `setLetters`) to access and modify the piece's state. Importantly, the `set` methods call `repaint()` to ensure the component redraws itself whenever its color or text changes.

3. **Event Handling:**

   - Mouse Events (`PieceSetup`):

      Each 

     ```
     GamePiece
     ```

      has a 

     ```
     MouseListener
     ```

     . When the mouse interacts with a piece:

     - `mouseClicked`: Color changes to white.
     - `mousePressed`: Color changes to red.
     - `mouseReleased`: Color changes to white.
     - `mouseEntered`: Color changes to light gray (hover effect).
     - `mouseExited`: Color changes back to white.

   - Button Actions (`setupButtons`):

     - `myBttnRndColors`, `myBttnRndWords`, `myBttnRndBoth`: These buttons set the `xChoice` variable accordingly (1, 2, or 3) and start the `myTimer`.
     - `myBttnReset`: This button iterates through all `GamePiece`s in the `myAl` list and resets their text to "----" and color to yellow.

   - Timer Action (`myActList`):

     - When `myTimer` is running, it fires an event every 40 milliseconds.

     - The 

       ```
       actionPerformed
       ```

        method checks 

       ```
       xChoice
       ```

       :

       - If 1, it picks a random color and applies it to a random `GamePiece`.
       - If 2, it picks a random word and applies it to a random `GamePiece`.
       - If 3, it does both (random color to a random piece, random word to *another* random piece).

     - This happens repeatedly for 150 cycles (150 * 40ms = 6 seconds), creating a shuffling effect, after which the timer stops itself.

In essence, the application displays a grid of interactive tiles (GamePieces) and provides controls to randomly shuffle their appearance (color and/or text) for a short duration or reset them.



```java
/*
Eningeer: James Goudy
 */
/**
 *
 * @author Goudy
 */
package j2x_game_piece_demo;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.util.ArrayList;
import java.util.Random;
import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JComponent;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.Timer;
import javax.swing.border.Border;

public class J2x_Game_Piece_Demo {

    // Create GUI Components
    static JFrame myFrame = new JFrame();
    static JPanel myPanel = new JPanel();
    static JButton myBttnRndColors = new JButton("Random Colors");
    static JButton myBttnRndWords = new JButton("Random Words");
    static JButton myBttnRndBoth = new JButton("Random Both");
    static JButton myBttnReset = new JButton("Reset");
    static JLabel myLabel = new JLabel("Game Pieces");

    // ----------- Global Variables -------------------
    //Arraylist to hold game pieces
    static ArrayList<GamePiece> myAl = new ArrayList();

    //Arraylist to hold colors
    static ArrayList<Color> colorAl = new ArrayList();

    //Array to hold words
    static String[] myWords = {"DOG", "CAT", "COW", "PUP",
        "JAR", "STAR", "YEP", "CAR",
        "BOOK", "FLIP", "****", "####",
        "SHOW", "SHOE", "SOCK", "BOAT",
        "JET", "RAIN", "TV", "RADIO", "?",
        "DAISY", "ZIPPY", "HIPPY", "TRIPPY", "FLUFFY"};

    //Random number generator
    static Random RNG;

    //Timer for shuffling colors and text
    static Timer myTimer;

    //choice for determine if text, colors or both are shuffled
    static int xChoice = 0;

    //create a dimension for the box
    static Dimension myDim = new Dimension(400, 400);

    // button placement and size
    static int bttnxpos = 500;
    static int bttnypos = 50;
    static int bttnSpacing = 25;

    static int bttnLength = 150;
    static int bttnHeight = 25;

    //create an action listener
    static ActionListener myActList = new ActionListener() {

        //variable to hold random choice
        int rc = 0;

        //counter - the shuffles
        int cntr = 0;

        @Override
        public void actionPerformed(ActionEvent arg0)
        {

            try {
                switch (xChoice) {
                    case 1:
                        //random choice - colors
                        rc = RNG.nextInt(colorAl.size());

                        myAl.get(RNG.nextInt(myAl.size())).
                                setPieceColor(colorAl.get(rc));
                        break;
                    case 2:
                        //random choice - worlds
                        rc = RNG.nextInt(myWords.length);

                        myAl.get(RNG.nextInt(myAl.size())).
                                setLetters(myWords[rc]);
                        break;
                    case 3:
                        // random choice colors and words
                        rc = RNG.nextInt(colorAl.size());

                        myAl.get(RNG.nextInt(myAl.size())).
                                setPieceColor(colorAl.get(rc));

                        //random choice
                        rc = RNG.nextInt(myWords.length);

                        myAl.get(RNG.nextInt(myAl.size())).
                                setLetters(myWords[rc]);
                        break;
                }

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }

            cntr++;

            if (cntr == 150) {
                myTimer.stop();
                cntr = 0;
            }
        }
    };

    public static void main(String[] args)
    {

        setupApp();

    }

    // helper function to setup GUI
    private static void setupApp()
    {

        RNG = new Random();

        setupFrame();

        setupPanel();

        setupButtons();
        
        setupJLabel();

        PieceSetup();

        colorSetup();

        //setup timer
        myTimer = new Timer(40, myActList);

    }

    private static void setupFrame()
    {

        // frame size 
        myFrame.setSize(725, 525);

        // set location
        myFrame.setLocationRelativeTo(null);

        // set visibility
        myFrame.setVisible(true);

        // set close action
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // layout manager
        myFrame.setLayout(null);

        // set title
        myFrame.setTitle("Game Pieces");

    }

    static void setupPanel()
    {

        // set panel size
        myPanel.setSize(myDim);

        // set visible
        myPanel.setVisible(true);

        // set location
        myPanel.setLocation(50, 50);

        // set border
        Border myPanelBorder = BorderFactory.createLineBorder(Color.BLACK, 2);
        myPanel.setBorder(myPanelBorder);

        myFrame.add(myPanel);

    }

    private static void setupButtons()
    {

        // set size
        myBttnRndColors.setSize(bttnLength, bttnHeight);
        myBttnRndWords.setSize(bttnLength, bttnHeight);
        myBttnRndBoth.setSize(bttnLength, bttnHeight);
        myBttnReset.setSize(bttnLength, bttnHeight);

        // set Visible
        myBttnRndColors.setVisible(true);
        myBttnRndWords.setVisible(true);
        myBttnRndBoth.setVisible(true);
        myBttnReset.setVisible(true);

        // set location
        myBttnRndColors.setLocation(bttnxpos, bttnypos);
        bttnypos = bttnypos + bttnHeight + bttnSpacing;

        myBttnRndWords.setLocation(bttnxpos, bttnypos);
        bttnypos = bttnypos + bttnHeight + bttnSpacing;

        myBttnRndBoth.setLocation(bttnxpos, bttnypos);
        bttnypos = bttnypos + bttnHeight + bttnSpacing;

        myBttnReset.setLocation(bttnxpos, bttnypos);
        bttnypos = bttnypos + bttnHeight + bttnSpacing;

        // set actionlisteners
        myBttnRndColors.addActionListener(e -> {

            xChoice = 1;
            myTimer.start();
        });

        myBttnRndWords.addActionListener(e -> {

            xChoice = 2;
            myTimer.start();
        });

        myBttnRndBoth.addActionListener(e -> {

            xChoice = 3;
            myTimer.start();
        });

        myBttnReset.addActionListener(e -> {

            for (int cntr = 0; cntr < myAl.size(); cntr++) {
                myAl.get(cntr).setLetters("----");
                myAl.get(cntr).setPieceColor(Color.yellow);
            }

        });

        myFrame.add(myBttnRndColors);
        myFrame.add(myBttnRndWords);
        myFrame.add(myBttnRndBoth);
        myFrame.add(myBttnReset);

    }

    private static void setupJLabel()
    {

        // set text
        myLabel.setText("Game Pieces");

        // set fontsize
        // Sets the label's font to bold with size 24, 
        // retaining the original font name.
        // Retrieves the current font name and 
        // creates a new Font object with updated style and size.
        myLabel.setFont(new Font(myLabel.getFont().getName(), Font.BOLD, 24));

        // set size
        myLabel.setSize(200, myLabel.getFont().getSize() + 4);

        // set visibility
        myLabel.setVisible(true);

        // Set position
        myLabel.setLocation(50, 10);

        // add to frame
        myFrame.add(myLabel);

    }

    // Piece Setup
    static void PieceSetup()
    {
        //setup the pieces

        int x = 0;
        int y = 0;

        for (int c = 1; c <= 16; c++) {

            //create a new gamepiece
            GamePiece gp = new GamePiece();

            //set the location, size , visiblility and color
            gp.setLocation(x, y);
            gp.setSize(100, 100);
            gp.setVisible(true);
            gp.setPieceColor(Color.black);

            //note what each of the mouse events are doing
            gp.addMouseListener(new MouseListener() {
                @Override
                public void mouseClicked(MouseEvent arg0)
                {

                    gp.setPieceColor(Color.white);
                }

                @Override
                public void mousePressed(MouseEvent arg0)
                {
                    gp.setPieceColor(Color.red);
                }

                @Override
                public void mouseReleased(MouseEvent arg0)
                {
                    gp.setPieceColor(Color.white);
                }

                @Override
                public void mouseEntered(MouseEvent arg0)
                {
                    gp.setPieceColor(Color.lightGray);
                }

                @Override
                public void mouseExited(MouseEvent arg0)
                {
                    gp.setPieceColor(Color.white);
                }
            });

            //add the gamepiec to the arraylist and then to the panel
            myAl.add(gp);
            myPanel.add(gp);

            //increment x and y to the location of the next gamepiece
            x = x + 100;

            if ((c % 4) == 0) {
                y = y + 100;
                x = 0;
            }
        }
        //refresh the panel
        myPanel.repaint();
    }

    static void colorSetup()
    {

        //add colors to the color arrraylist
        colorAl.add(Color.blue);
        colorAl.add(Color.cyan);
        colorAl.add(Color.magenta);
        colorAl.add(Color.red);
        colorAl.add(Color.orange);
        colorAl.add(Color.green);
        colorAl.add(Color.yellow);
        colorAl.add(Color.pink);
        colorAl.add(Color.lightGray);

    }

} // end of program  class

// *************  GAME PIECE CLASS *****************
class GamePiece extends JComponent {

    Color pieceColor = Color.white;

    String letters = "GP";

    public GamePiece()
    {

        this.setForeground(pieceColor);

        this.setVisible(true);

    }

    @Override
    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);

        Font myFont = new Font("Lucida Console", Font.BOLD, 18);

        //NOTE: ORDER IS EVERYTHING!
        g.setColor(Color.black);
        g.fillRect(0, 0, 100, 100);
        g.setColor(pieceColor);
        g.fillRect(5, 5, 90, 90);
        g.setColor(Color.black);

        g.setFont(myFont);

        //CENTER TEXT HORIZONTALLY
        int width = g.getFontMetrics().stringWidth(letters);
        int left = (100 - width) / 2;
        g.drawString(letters, left, 60);

    }

    //SETTERS AND GETTERS
    public Color getPieceColor()
    {
        return pieceColor;
    }

    public void setPieceColor(Color pieceColor)
    {
        this.pieceColor = pieceColor;
        this.repaint();
    }

    public String getLetters()
    {
        return letters;
    }

    public void setLetters(String letters)
    {
        this.letters = letters;
        this.repaint();
    }

}


```

