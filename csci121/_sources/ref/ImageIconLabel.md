# Add Image Using Image Icon Label



An `ImageIcon` in Java is a class from the `javax.swing` package that encapsulates an image to be used in Swing components. When paired with a `JLabel`, it enables the display of images within the graphical user interface.

## **Definition and Purpose**

- **`ImageIcon`** is a subclass of `javax.swing.Icon`.
- It is typically used to load and manage images (like `.jpg`, `.png`, `.gif`) and render them in UI elements.

## **Common Uses**

- **Display in `JLabel`**: Most common use. Assign an `ImageIcon` to a `JLabel` to show an image:

  ```java
  JLabel label = new JLabel(new ImageIcon("path/to/image.jpg"));
  ```

- **Buttons and Menus**: Used to add icons to `JButton`, `JMenuItem`, etc.

  ```java
  JButton button = new JButton(new ImageIcon("icon.png"));
  ```

- **Toolbars**: Icons in `JToolBar` often use `ImageIcon`.

## **Key Features**

- Supports image formats via Java’s built-in `ImageIO`.
- Handles automatic repainting of components when icons change.
- Can be created from files, URLs, or byte arrays.

### **Reference**

- Java SE Documentation: [`ImageIcon`](https://docs.oracle.com/en/java/javase/17/docs/api/java.desktop/javax/swing/ImageIcon.html)



## Example Code

```java
/*
 Developer: James Goudy
 Description: A simple Java Swing application to read and display an image using a JLabel.
 */

 package filereading;


 import java.awt.Image;
 import java.awt.image.BufferedImage;
 import java.io.IOException;
 import java.net.URL;
 import javax.imageio.ImageIO;
 import javax.swing.*;
 
 public class FileReading {
 
     public static void main(String[] args) {
         SwingUtilities.invokeLater(ImageViewerFrame::new);
     }
 }
 
 class ImageViewerFrame {
     
     
     // global variables
     private BufferedImage image;
 
     private final JFrame frame;
     
     private final JMenuBar menuBar = new JMenuBar();
     private final JMenu fileMenu = new JMenu("File");
     private final JMenuItem quitItem = new JMenuItem("Quit");
     
     private final JLabel imageLabel = new JLabel();
 
     
     // constructor
     public ImageViewerFrame() {
         
         
         frame = new JFrame("Image Viewer");
 
         // helper functions
         setupMenu();
         setupFrame();
         loadImage("/images/dog6.jpg");
         setupImageLabel();
 
         frame.setVisible(true);
     }
 
     private void setupMenu() {
         
         // setup quit menuitem
         quitItem.addActionListener(e -> System.exit(0));
         
         // add quitItem to the menu
         fileMenu.add(quitItem);
         
         // add menu to memubar
         menuBar.add(fileMenu);
         
         // add menubar to Frame
         frame.setJMenuBar(menuBar);
     }
 
     private void setupFrame() {
         
         // frame dimensions
         int width = 800;
         int height = 600;
         
         // set what happens on close
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         
         // set framesize layoutmanager and screen location
         frame.setSize(width,height);
         frame.setLayout(null);
         frame.setLocationRelativeTo(null);
     }
 
     private void loadImage(String filePath) {
         
         try {
             URL imageUrl = getClass().getResource(filePath);
             
             // test for  file path
             if (imageUrl == null) {
                 
                 // show error pane if not found
                 JOptionPane.showMessageDialog(frame, 
                                "Image not found: " + filePath,
                                "Error", JOptionPane.ERROR_MESSAGE);
                 return;
             }
             
             image = ImageIO.read(imageUrl);
             
         } catch (IOException e) {
             // show error pane
             JOptionPane.showMessageDialog(frame, 
                     "Failed to load image: " + e.getMessage(),
                     "Error", JOptionPane.ERROR_MESSAGE);
         }
     }
 
     private void setupImageLabel() {
         
         int width = 300;
         int heigth = 200;
         
         if (image != null) {
             
             // scale image
             Image scaledImage = image.getScaledInstance(width, heigth, Image.SCALE_SMOOTH);
             
             // add image to image icon
             ImageIcon icon = new ImageIcon(scaledImage);
             
             imageLabel.setIcon(icon);
             
             // center the picture on the label
             imageLabel.setHorizontalAlignment(SwingConstants.CENTER);
             imageLabel.setVerticalAlignment(SwingConstants.CENTER);
             
             // set image location and size
             imageLabel.setBounds(50,50,width, heigth);
             
             // add imagelabel to frame
             frame.add(imageLabel);
         }
     }
 }
 
```



The build sequence of this Java Swing program involves several key steps that follow a clear flow from application startup to GUI rendering. Below is a breakdown of the execution (build) sequence from class loading through GUI display:

------

### **1. Application Entry Point**

- The `main` method in the `FileReading` class is the entry point:

  ```java
  SwingUtilities.invokeLater(ImageViewerFrame::new);
  ```

- This line schedules the creation of a new `ImageViewerFrame` instance on the Event Dispatch Thread (EDT), ensuring thread safety for Swing components (ref: [Oracle Swing Tutorial](https://docs.oracle.com/javase/tutorial/uiswing/concurrency/initial.html)).

------

### **2. Construction of `ImageViewerFrame`**

- The constructor of `ImageViewerFrame` is called:

  ```java
  public ImageViewerFrame() {
      ...
      setupMenu();
      setupFrame();
      loadImage("/images/dog6.jpg");
      setupImageLabel();
      frame.setVisible(true);
  }
  ```

  It initializes the GUI step-by-step:

#### a. `setupMenu()`

- Initializes menu components:
  - Adds "Quit" menu item with action listener to terminate the application.
  - Adds the menu item to the menu, then attaches the menu bar to the `JFrame`.

#### b. `setupFrame()`

- Sets up the frame:
  - Dimensions, close operation, layout manager (`null` = absolute positioning), and centering the window on the screen.

#### c. `loadImage(String filePath)`

- Attempts to load an image from the classpath using `getClass().getResource(filePath)`.
- If successful, loads the image into a `BufferedImage` via `ImageIO.read`.
- Displays error dialogs if the image is not found or cannot be read.

#### d. `setupImageLabel()`

- If the image is loaded:
  - Scales it to 300×200 using `Image.SCALE_SMOOTH`.
  - Wraps the scaled image in an `ImageIcon` and sets it on a `JLabel`.
  - Positions the label on the frame with absolute coordinates.
  - Adds the label to the frame.

#### e. `frame.setVisible(true)`

- Displays the fully constructed GUI window.

------

### **Key Notes**

- **Absolute positioning (`null` layout manager)** is used, so components are manually sized and placed.
- **Classpath resource loading**: The image must reside in `/images/dog6.jpg` relative to the classpath root.
- The use of **`invokeLater()`** aligns with Swing’s requirement to create and update GUI components on the EDT for thread safety.

------

Would you like a diagram of the object construction and method call sequence?

