# Pictures and Sound



## Build Sequence

Why the setup calls in the `Frame1` constructor is a logical and common way to organize GUI setup code, especially helpful for beginners:

1. **Create the Container First:**

   - `myFrame = new JFrame("Picture and Sound");`
   - **Why first?** This line creates the main window object (`JFrame`). Think of it like getting the main box or the foundation before you can put anything inside it or build upon it. *Everything* else in the GUI will belong to this frame in some way. You can't add panels, buttons, or menus to a window that doesn't exist yet.

2. **Prepare Data/Resources (Optional but Good Practice):**

   - `loadDogsPaths();`
   - **Why early?** This method gets the list of image file paths ready. While it doesn't directly build a visible part of the GUI, it prepares data that *will be needed* later by other components (specifically, the `setupDogButton` method needs these paths for its action listener). Getting data ready before setting up the components that use it prevents potential errors and keeps related logic together.

3. **Build Components That Need Other Components:**

   - `setupMenu();`
   - **Why before `setupFrame`?** This creates the menu bar (`JMenuBar`) and its contents. The menu bar itself needs to be *attached* to the `JFrame`. The `setupFrame` method likely contains the line `myFrame.setJMenuBar(myMenuBar);`. Therefore, the menu bar must *exist* before you try to attach it in `setupFrame`.

4. **Configure the Main Container:**

   - `setupFrame();`
   - **Why here?** This method sets up the properties of the main window itself – its size, layout (even if `null`), what happens when you close it, and crucially, it attaches the menu bar created in `setupMenu`. It prepares the "stage" where the other visual elements will be placed. It needs `myFrame` (created first) and `myMenuBar` (created by `setupMenu`) to be ready.

5. **Create and Add Child Components (Panels):**

   - `setupDogPanel();`
   - `setupShapePanel();`
   - **Why after `setupFrame`?** These methods create the custom panels (`DogPanel`, `ShapePanel`) where drawing will occur. They need the `myFrame` object to exist so they can be added to its content area (using `myFrame.add(...)`). They are the main visual building blocks *inside* the frame.

6. **Create and Add Interactive Controls (Buttons):**

   - `setupDogButton();`

   - `setupShapeButton();`

   - Why last (or after the components they control)?

      These methods create the buttons.

     - They need the `myFrame` to exist so they can be added to it.

     - Crucially, their action listeners
       
       > [!TIP]
       >
       > (the code that runs when clicked) often need references to the components they interact with.)
       >

       - `setupDogButton` needs `dogPanel` (to tell it to draw) and the `dogImagePaths` (loaded earlier).
       - `setupShapeButton` needs `shapePanel` (to tell it which shape to draw).
       
     - Placing the button setup *after* the panels they control ensures those panels exist and are ready to be referenced by the button's actions.

**Key Takeaways:**

- **Dependency Order:** The sequence respects dependencies. You create things before you use or add them to something else.
- **Logical Grouping:** It groups related setup tasks into separate, well-named methods (like `setupMenu`, `setupDogPanel`), making the constructor cleaner and the code easier to understand and modify.
- **Readability:** Following this logical flow makes the code read more naturally, showing the progression from the main container down to the individual interactive elements.





```java
/*

Developer: James Goudy
Rev: 2025

 */
package j2_pictures_sound_rev25;

import java.awt.Color;
import java.awt.FontMetrics;
import java.awt.Graphics;
import java.awt.image.BufferedImage;
import java.io.IOException;
import javax.imageio.ImageIO;
import javax.sound.sampled.AudioInputStream;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.Clip;
import javax.sound.sampled.UnsupportedAudioFileException;
import javax.swing.BorderFactory;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JPanel;

class DogPanel extends JPanel {

    // create a buffered image and a boolean status flag
    BufferedImage dogImage;
    boolean drawDog = false;

    // variables for the height and width of the panel
    int width;
    int height;

    public DogPanel(int width, int height)
    {

        this.width = width;
        this.height = height;

    }

    public void setDogImage(BufferedImage dogpix)
    {
        this.dogImage = dogpix;
        this.drawDog = true;
        repaint();
    }

    @Override
    protected void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        
        // ensure there is a dog pix and it is not null
        if (drawDog && dogImage != null) {
            g.drawImage(dogImage, 0, 0, width, height, this);
        }
    }
}

class ShapePanel extends JPanel {

    public enum ShapeChoice {
        CIRCLE, SQUARE, WORD
    }
    public ShapeChoice myShapeChoice;

    String myString;

    int width;
    int height;

    public ShapePanel(int width, int height)
    {

        // set the panel width, height, default String, and default shape
        this.width = width;
        this.height = height;
        myString = "Hello";
        myShapeChoice = ShapeChoice.CIRCLE;

    }

    public void setTheString(String theString)
    {
        this.myString = theString;
    }

    public void drawShape(ShapeChoice myShapechoice)
    {
        this.myShapeChoice = myShapechoice;
        repaint();
    }

    @Override
    protected void paintComponent(Graphics g)
    {
        super.paintComponent(g);

        // FontMeterics is used to get the string width
        FontMetrics fontMetrics = g.getFontMetrics();

        // based on the enum - draw a circle, square or string
        // the 5,5 are setting the shape 5 pixels over and 5 down
        // the -10 will insure there is a 5 pixel space all around the shape
        
        switch (myShapeChoice) {

            case CIRCLE -> {
                g.setColor(Color.red);
                g.fillOval(5, 5, width - 10, height - 10);
            }
            case SQUARE -> {
                g.setColor(Color.blue);
                g.fillRect(5, 5, width - 10, height - 10);
            }
            case WORD -> {
                g.setColor(Color.darkGray);
                g.drawString(myString,
                        (width - fontMetrics.stringWidth(myString)) / 2,
                        height / 2);
            }
            default -> {
                g.setColor(Color.yellow);
                g.fillOval(5, 5, width - 10, height - 10);
            }
        }

    }
}

class Frame1 {

    // Create Frame
    JFrame myFrame;

    // Create Panels To Put On Frame
    DogPanel dogPanel;
    ShapePanel shapePanel;

    // Create counter to cycle through shapes
    int shapeCntr = 0;

    // Create menubar, menu and one menu item to put on menu
    JMenuBar myMenuBar = new JMenuBar();
    JMenu myMenuFile = new JMenu("File");
    JMenuItem myMenuItemQuit = new JMenuItem("Quit");

    // Create a dog image variable and an array to keep their file paths
    BufferedImage dogImage;
    String[] dogImagePaths = new String[5];

    // Create counter to cycle through dogs
    int dogCntr = 0;

    // create the buttons
    JButton mybttnDrawDog = new JButton("Draw Dog");
    JButton mybttnDrawShape = new JButton("Draw Shape");

    public Frame1()
    {

        // instansiate a new Frame
        myFrame = new JFrame("Picture and Sound");

        // functions to build the GUI
        loadDogsPaths();
        setupMenu();
        setupFrame();
        setupDogPanel();
        setupShapePanel();
        setupDogButton();
        setupShapeButton();

    }

    private void setupMenu()
    {

        // add exit to menuItem
        myMenuItemQuit.addActionListener(e -> System.exit(0));

        // add quit it File Menu
        myMenuFile.add(myMenuItemQuit);

        // Add File Menu to File Bar
        myMenuBar.add(myMenuFile);

    }

    private void setupFrame()
    {

        // setup basic frame
        int width = 800;
        int height = 600;

        // set layout manager
        myFrame.setLayout(null);

        // set close behavior of frame
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // add menu        
        myFrame.setJMenuBar(myMenuBar);

        // setup size, visibility and screen location
        myFrame.setSize(width, height);
        myFrame.setVisible(true);
        myFrame.setLocationRelativeTo(null);
    }

    private void setupDogPanel()
    {

        // set panel dimensions
        int width = 300;
        int height = 200;

        // instansiate a new dogpanel, set location and dimensions,
        // create a border, set visibility and add it to the frame.
        dogPanel = new DogPanel(width, height);

        dogPanel.setBounds(25, 75, 300, 200);
        dogPanel.setBorder(BorderFactory.createLineBorder(Color.blue, 3));
        dogPanel.setVisible(true);

        myFrame.add(dogPanel);
    }

    private void setupShapePanel()
    {
        // set panel dimensions
        int width = 200;
        int height = 200;

        // instansiate a new dogpanel, set location and dimensions,
        // create a border, set visibility and add it to the frame.
        shapePanel = new ShapePanel(width, height);

        shapePanel.setBounds(350, 75, 200, 200);
        shapePanel.setBorder(BorderFactory.createLineBorder(Color.blue, 3));
        shapePanel.setVisible(true);

        myFrame.add(shapePanel);
    }

    private void setupDogButton()
    {

        // setup button dimensions and location
        
        int buttonWidth = 100;
        int buttonHeight = 25;

        int xpos = 25;
        int ypos = 25;

        // setup the action listener - what happens when the button is press
        
        mybttnDrawDog.addActionListener(e -> {
  
            // the remainder is being calculated.  This will correspond
            // to the array index for the dog paths
            
            int dogChoice = dogCntr % dogImagePaths.length;
            

            try {

                // alternative way
                //dogImage = ImageIO.read(new File(dogImagePaths[dogChoice]));
                
                // read in a dog image
                dogImage = 
                 ImageIO.read(getClass().getResource(dogImagePaths[dogChoice]));

                // update the dog image on the dog panel
                dogPanel.setDogImage(dogImage);

                // bark
                bark();
                
            } catch (IOException ex) {

                System.out.println(ex.getMessage());
            }
            
            dogCntr++;

        });

        // set the button location and dimensions, set the visibility,
        // and add it to the frame
        
        mybttnDrawDog.setBounds(xpos, ypos, buttonWidth, buttonHeight);
        mybttnDrawDog.setVisible(true);

        myFrame.add(mybttnDrawDog);

    }

    private void setupShapeButton()
    {

        // setup button dimensions and location
        
        int buttonWidth = 200;
        int buttonHeight = 25;

        int xpos = 350;
        int ypos = 25;

        // setup the action listener - what happens when the button is press
        
        mybttnDrawShape.addActionListener(e -> {

            
            // calculate the button choices for the shape. 
            // by using the remainder, the choices will always be 0,1,2
            
            int choice = shapeCntr % 3;


            switch (choice) {
                case 0:
                    shapePanel.drawShape(ShapePanel.ShapeChoice.CIRCLE);
                    break;
                case 1:
                    shapePanel.drawShape(ShapePanel.ShapeChoice.SQUARE);
                    break;
                case 2:
                    shapePanel.drawShape(ShapePanel.ShapeChoice.WORD);
                    break;
                default:
                    break;
            }

            // increment the counter 
            shapeCntr++;

        });

        // set the button location and dimensions, set the visibility,
        // and add it to the frame
        
        mybttnDrawShape.setBounds(xpos, ypos, buttonWidth, buttonHeight);
        mybttnDrawShape.setVisible(true);

        myFrame.add(mybttnDrawShape);

    }

    private void loadDogsPaths()
    {

        for (int i = 0; i < dogImagePaths.length; i++) {

            // NOTE: THE SLASHES MUST LEAN TO THE RIGHT
            // NOTE: THE SLASHES MUST LEAN TO THE RIGHT!!!
            // Building the string paths to the dog.
            // Assumes the file is in the src folder.
            
            dogImagePaths[i] = "/images/images/dog" + (i + 1) + ".jpg";

        }

    }

    private void bark()
    {

        // get the string path of where the file is located
        // from below it assumes it is in the src file
        
        String soundPath = "/Sounds/howl.wav";

        try {
            
            // create a sound clip
            Clip barkclip = AudioSystem.getClip();

           // create an audiostream
           AudioInputStream inputStream
           = AudioSystem.getAudioInputStream(getClass().getResource(soundPath));

            // open the stream
            barkclip.open(inputStream);

            // play the stream
            barkclip.start();

            // demonstrates that a clip can be looped
            barkclip.loop(2);

        } catch (UnsupportedAudioFileException e) {
            System.out.println(e.getMessage());
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }

    }

}

public class J2_Pictures_Sound_Rev25 {

    public static void main(String[] args)
    {

        Frame1 myFrame = new Frame1();

    }

}

```

