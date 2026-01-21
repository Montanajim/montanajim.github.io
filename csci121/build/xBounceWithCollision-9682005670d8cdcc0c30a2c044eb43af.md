# Bounce With Collision



## Introduction

This Java program creates a graphical window where you can add multiple colored balls. These balls move around within a defined area, bouncing realistically off the edges of that area. Crucially, the balls also detect collisions with each other and bounce off one another. You can add new balls, delete the oldest ball, or clear all balls from the screen using the provided buttons



- **Object-Oriented Programming (OOP):** Demonstrates class design (`Ball`, `Frame1`), encapsulation (hiding data in `Ball` with getters/setters), inheritance (`Ball extends JComponent`, `Frame1 extends JFrame`), polymorphism (`paintComponent` override), and object interaction (`Frame1` managing `Ball` objects).
- **GUI Programming (Java Swing):** Shows use of standard components (`JFrame`, `JPanel`, `JButton`), creating custom visual components (`Ball`), handling events (`ActionListener` for timer/buttons), custom drawing (`paintComponent`), and layout management (absolute positioning).
- **Animation and Timing:** Uses `javax.swing.Timer` for the animation loop, manages object state changes over time, and uses `repaint()` to update the display visually.
- **Collision Detection & Simple Physics:** Implements boundary checking (wall bouncing), object-to-object collision detection (distance check), and collision response (swapping vectors, resolving overlap).
- **Data Structures:** Utilizes `ArrayList` to manage a dynamic collection of `Ball` objects and demonstrates iterating over collections.



## Frame Class

```java

package j2_bounce_rev25_collision;

import j2_bounce_rev25_collision.Ball;
import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.util.Random;
import javax.swing.Timer;

/*
Bounce Balls
Programmer: James Goudy
Rev: April, 2024 / Modified: 4/2025 for inter-ball collision
 */

public class Frame1 extends javax.swing.JFrame {

        // Global Variables
    Timer panelTimer;  //this will control the repaint of the panel
    boolean TimerStatus;


    Random RNG = new Random();
    // Setup to show one can instantiate an object later
    // Random RNG2; // RNG2 seems unused, consider removing


    // initial ball info (defaults for adding balls)
    // int x = 1; // No longer needed here
    // int y = 1; // No longer needed here
    // int radius = 25; // Default radius used below


    // Timer Tick speed (delay in milliseconds)
    int clockTick = 20; // Reduced for smoother animation

    // Arraylist to hold the balls
    ArrayList<Ball> alBalls = new ArrayList<>(); // Use diamond operator

    
    
    
    /**
     * Creates new form Frame1
     */
    public Frame1()
    {
        initComponents();
        
                TimerStatus = false;
        // RNG2 = new Random(); // Unused

        this.setLocationRelativeTo(null);
        this.setTitle("Bouncing Balls with Collision"); // Set a title
    }
    
        private void PanelClock() {
            
            
            panelTimer = new Timer(clockTick, new ActionListener() {
                @Override
                public void actionPerformed(ActionEvent e)
                {


                // 1. Move all balls (calculate next position based 
                //    on velocity and wall collision)
                for (Ball ball : alBalls) {
                    ball.moveBall();
                }

                // 2. Check for and handle collisions between balls
                for (int i = 0; i < alBalls.size(); i++) {
                    for (int j = i + 1; j < alBalls.size(); j++) {
                        Ball ball1 = alBalls.get(i);
                        Ball ball2 = alBalls.get(j);

                        if (ball1.collidesWith(ball2)) {
                            // Collision detected!
                            // Resolve overlap first to prevent sticking
                            ball1.resolveCollision(ball2);
                            // Swap movement vectors for a simple bounce effect
                            ball1.swapMovement(ball2);

                            // Alternative: Simple reverse (less realistic)
                            // ball1.reverse();
                            // ball2.reverse();
                        }
                    }
                }


                // 3. Update the visual location of each ball component on the panel
                // Use the calculated xpos/ypos which are now adjusted for collisions
                for (Ball ballComponent : alBalls) {
                    // Ball IS the component, just set its location
                    ballComponent.setLocation(ballComponent.getXpos(), ballComponent.getYpos());
                }


                // 4. Repaint the panel to show updated ball positions
                // Note: Repainting the panel itself might not be enough if balls are separate components.
                // Repainting each ball or the container might be necessary depending on Swing's behavior.
                // Calling revalidate() and repaint() on the container (jPanel1) is generally robust.
                 //jPanel1.revalidate(); // Recalculate layout if sizes changed (e.g., radius)
                 jPanel1.repaint();    // Redraw the panel and its children

                // panelTimer.setDelay(20); // Delay is set when creating the timer
            }           
            });

        panelTimer.start();

    }
    

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents()
    {

        jPanel1 = new javax.swing.JPanel();
        jbttnAddBall = new javax.swing.JButton();
        jbttnDelete = new javax.swing.JButton();
        jbttnClear = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jPanel1.setBorder(javax.swing.BorderFactory.createLineBorder(new java.awt.Color(0, 0, 0)));

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 600, Short.MAX_VALUE)
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 317, Short.MAX_VALUE)
        );

        jbttnAddBall.setText("Add");
        jbttnAddBall.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnAddBallActionPerformed(evt);
            }
        });

        jbttnDelete.setText("Delete");
        jbttnDelete.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnDeleteActionPerformed(evt);
            }
        });

        jbttnClear.setText("Clear");
        jbttnClear.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnClearActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(39, 39, 39)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(jbttnAddBall, javax.swing.GroupLayout.PREFERRED_SIZE, 88, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(33, 33, 33)
                        .addComponent(jbttnDelete, javax.swing.GroupLayout.PREFERRED_SIZE, 93, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(27, 27, 27)
                        .addComponent(jbttnClear, javax.swing.GroupLayout.PREFERRED_SIZE, 88, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addContainerGap(99, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(41, 41, 41)
                .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(31, 31, 31)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jbttnAddBall)
                    .addComponent(jbttnDelete)
                    .addComponent(jbttnClear))
                .addContainerGap(42, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void jbttnClearActionPerformed(java.awt.event.ActionEvent evt)                                           
    {                                               
        // Stop the timer if it's running
        if (TimerStatus) {
            panelTimer.stop();
            TimerStatus = false;
        }

        // Remove all ball components from the panel
        jPanel1.removeAll();

        // Clear the list of balls
        alBalls.clear();

        // Repaint the empty panel
        //jPanel1.revalidate();
        jPanel1.repaint();


    }                                          

    private void jbttnDeleteActionPerformed(java.awt.event.ActionEvent evt)                                            
    {                                                
        // Remove the first ball added (FIFO)
        if (!alBalls.isEmpty()) {
            Ball ballToRemove = alBalls.remove(0); // Remove from list first
            jPanel1.remove(ballToRemove); // Then remove component from panel
            //jPanel1.revalidate();
            jPanel1.repaint();
        }

        // Stop timer if no balls left
        if (alBalls.isEmpty() && TimerStatus) {
            panelTimer.stop();
            TimerStatus = false;
        }
    }                                           

    private void jbttnAddBallActionPerformed(java.awt.event.ActionEvent evt)                                             
    {                                                 
        // create a ball
        Ball aball = new Ball();
        int r = RNG.nextInt(25) + 10; // Radius between 10 and 34
        aball.setRadius(r);

        // Set boundaries based on panel size *and* ball radius
        aball.setCompHeight(jPanel1.getHeight());
        aball.setCompWidth(jPanel1.getWidth());

        // Set initial position randomly within bounds (considering radius)
        aball.setXpos(RNG.nextInt(jPanel1.getWidth() - 2 * r));
        aball.setYpos(RNG.nextInt(jPanel1.getHeight() - 2 * r));

        // ball characteristics
        aball.setVisible(true);
        // aball.setBallspeed(RNG.nextInt(50) + 5); // Speed not directly used in movement yet
        aball.setSlopeRun(RNG.nextInt(5) + 1);  // Keep slopes reasonable
        aball.setSlopeRise(RNG.nextInt(5) + 1); // Ensure non-zero rise initially
        aball.setXDir(RNG.nextBoolean() ? 1 : -1); // Random initial direction
        aball.setYDir(RNG.nextBoolean() ? 1 : -1); // Random initial direction

        aball.setBallColor(new Color(RNG.nextInt(256),
                RNG.nextInt(256), RNG.nextInt(256)));

        // Set the component's bounds (position and size)
        // Position is set via setLocation in the timer loop
        // Size is set implicitly by setRadius -> setSize
        aball.setSize(aball.getRadius() * 2, aball.getRadius() * 2);

        // add the ball component to the panel and the list
        // Ensure Null Layout is set on jPanel1 in the designer or code for absolute positioning
        jPanel1.setLayout(null); // Make sure layout is null
        jPanel1.add(aball);
        alBalls.add(aball);

        // Start the master timer if it's not running
        if (!TimerStatus) {
            PanelClock();
            TimerStatus = true;
        }

        jPanel1.repaint(); // Repaint after adding
    }                                            

    /**
     * @param args the command line arguments
     */
    public static void main(String args[])
{
    /* Set the Nimbus look and feel */
    //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
    /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
     */
    try {
        for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
            if ("Nimbus".equals(info.getName())) {
                javax.swing.UIManager.setLookAndFeel(info.getClassName());
                break;
            }
        }
    } catch (ClassNotFoundException ex) {
        java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    } catch (InstantiationException ex) {
        java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    } catch (IllegalAccessException ex) {
        java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    } catch (javax.swing.UnsupportedLookAndFeelException ex) {
        java.util.logging.Logger.getLogger(Frame1.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    }
    //</editor-fold>

    /* Create and display the form */
    java.awt.EventQueue.invokeLater(new Runnable() {
        public void run()
        {
            new Frame1().setVisible(true);
        }
    });
}

    // Variables declaration - do not modify                     
    private javax.swing.JPanel jPanel1;
    private javax.swing.JButton jbttnAddBall;
    private javax.swing.JButton jbttnClear;
    private javax.swing.JButton jbttnDelete;
    // End of variables declaration                   
}

```



Okay, let's look at the `Frame1.java` code. If `Ball.java` is the blueprint for a single bouncing ball, then `Frame1.java` is like the **director and the stage** for the whole show.

Think of it as the main program window you see and interact with. Here's what it does, step-by-step, for a freshman CS student:

1. **It's the Main Window:** The line `public class Frame1 extends javax.swing.JFrame` means `Frame1` defines the main window of your application. `JFrame` is Java's standard class for creating windows with borders, title bars, close buttons, etc.

2. Sets Up the Stage:

   - Inside `Frame1`, there's a `jPanel1`. This is a blank panel within the window, acting as the "stage" or container where the balls will actually bounce around.
   - The `initComponents()` method (usually auto-generated by GUI builders like NetBeans) sets up this panel, along with the buttons ("Add Ball", "Delete Ball", "Clear All") and the title label ("Bounce"). It arranges them visually within the `Frame1` window.

3. **Keeps Track of the Balls:** It uses an `ArrayList<Ball> alBalls = new ArrayList();`. An `ArrayList` is just a flexible list that can grow or shrink. `Frame1` uses this list to keep track of every single `Ball` object that is currently active in the animation.

4. Handles User Actions:

   - When you click the "Add Ball" button, the `jbttnAddBallActionPerformed` method runs. It creates a *new* `Ball` object (using the `Ball` blueprint), gives it random properties (size, color, speed, starting position), adds this new ball to the `alBalls` list, and physically places the ball component onto the `jPanel1` stage.
   - Similarly, `jbttnDeleteBallActionPerformed` removes a ball from the list and the stage, and `jbttnClearAllActionPerformed` removes all of them.

5. Manages the Animation (The Heartbeat):

    This is the most important part!

   - `Frame1` has a `Timer panelTimer`. Think of this as a metronome or a heartbeat for the animation. It "ticks" at regular intervals (every `clockTick` milliseconds).

   - The `PanelClock()` method sets up and starts this timer.

   - Every time the timer ticks

     , the code inside the 

     ```
     actionPerformed
     ```

      method runs. This is the animation loop:

     - **Tell Balls to Move:** It goes through the `alBalls` list and tells *each* ball to run its `moveBall()` method. This updates each ball's internal position and handles bouncing off the walls.
     - **Check for Ball Collisions:** It then uses nested loops to check every possible pair of balls in the list. For each pair, it asks `if (ball1.collidesWith(ball2))`. If they *are* colliding, it calls methods (`resolveCollision`, `swapMovement`) to make them bounce off each other realistically.
     - **Update the Screen:** After calculating all the new positions (including adjustments from collisions), it goes through the list *again*. For each ball, it calls `ballComponent.setLocation(x, y)` to visually move the ball component to its new coordinates on `jPanel1`.
     - **Redraw:** Finally, it calls `jPanel1.repaint()`. This tells the Java graphical system, "Okay, I've moved everything, now redraw the panel (and all the balls on it) so the user sees the changes."

6. **Starts the Program:** The `public static void main(String args[])` method is the universal starting point for any Java application. Its job here is simply to create the `Frame1` window and make it visible on your computer screen.

**In Simple Terms:**

`Frame1` is the manager. It sets up the window and the bouncing area (`jPanel1`). It keeps a list of all the balls. It responds to button clicks to add or remove balls. Most importantly, it runs a timer that acts as the animation's heartbeat. On each heartbeat, it tells all the balls to move, checks if they bump into each other, updates their visual positions on the screen, and redraws everything.



---



## Ball Class



```java

package j2_bounce_rev25_collision;

/*
Bounce Balls
Programmer: James Goudy
Rev: April, 2024 / Modified: 4/2025 for inter-ball collision
 */


import java.awt.Color;
import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;
import javax.swing.JComponent;
import javax.swing.Timer;

import java.awt.Color;

import java.util.Random;

import java.awt.Color;

import java.util.Random;

/**
 *
 * @author jgoudy
 */
public class Ball extends JComponent {

    // private members
    // position of the ball (top-left corner)
    int xpos = 1;
    int ypos = 1;

    // direction of the ball - forward or backwards
    int xdir = 1;
    int ydir = 1;

    // size of the panel: these are going to be defaults
    // Note: compWidth and compHeight will now represent the maximum center x/y coordinates
    int compWidth = 500;
    int compHeight = 500;

    // angle of the ball (movement step size)
    int slopeRun = 1;
    int slopeRise = 1;

    // speed (not currently used in movement logic, but kept for potential future use)
    int ballspeed = 2;

    // radius of the ball
    int radius = 25;

    // Timer (seems unused within Ball class itself, consider removing if not needed here)
    // Timer bTimer;

    // ball color
    Color ballColor;

    Random RNG;

    // boolean wasReversed = false; // Removed as collision logic is moved to Frame1

    //-------------------------------------------------------
    // Constructor
    public Ball() {
        RNG = new Random();
        ballColor = Color.blue;
        // Set component size based on radius for drawing
        this.setSize(radius * 2, radius * 2);
        this.setPreferredSize(this.getSize()); // Important for layout managers
    }

    // Setters
    public void setXpos(int xpos) {
        // Ensure xpos stays within bounds if set externally
        this.xpos = Math.max(0, Math.min(xpos, compWidth - radius));
    }

    public void setYpos(int ypos) {
        // Ensure ypos stays within bounds if set externally
        this.ypos = Math.max(0, Math.min(ypos, compHeight - radius));
    }

    // Getters for position (top-left)
    public int getXpos() {
        return xpos;
    }

    public int getYpos() { // Corrected method name from getYPos to getYpos
        return ypos;
    }

    // Getters for Center Coordinates
    public int getCenterX() {
        return xpos + radius;
    }

    public int getCenterY() {
        return ypos + radius;
    }


    //-------------------------------------------------------
    // Setters for component bounds (adjust based on radius)
    public void setCompWidth(int containerWidth) {
         // Max center x-coordinate is container width minus radius
        this.compWidth = containerWidth - radius;
    }

    public void setCompHeight(int containerHeight) {
        // Max center y-coordinate is container height minus radius
        this.compHeight = containerHeight - radius;
    }

    // Setters and Getters for movement properties
    public void setSlopeRun(int slopeRun) {
        this.slopeRun = slopeRun;
    }

    public int getSlopeRun() {
        return slopeRun;
    }

    public void setSlopeRise(int slopeRise) {
        this.slopeRise = slopeRise;
    }

    public int getSlopeRise() {
        return slopeRise;
    }

    public void setBallspeed(int ballspeed) {
        this.ballspeed = ballspeed;
    }

    public int getBallspeed() { // Added getter
        return ballspeed;
    }

    public void setRadius(int radius) {
        this.radius = radius;
        // Update component size when radius changes
        this.setSize(radius * 2, radius * 2);
        this.setPreferredSize(this.getSize());
    }

    public int getRadius() { 
        return this.radius;
    }

    public void setBallColor(Color ballColor) {
        this.ballColor = ballColor;
    }

    public Color getBallColor() { 
        return ballColor;
    }

    public int getXDir() {
        return xdir;
    }

    public void setXDir(int xdir) {
        this.xdir = xdir;
    }

    public int getYDir() {
        return ydir;
    }

    public void setYDir(int ydir) {
        this.ydir = ydir;
    }

    //-------------------------------------------------------
    // Draw the ball
    @Override
    public void paintComponent(Graphics g) {
        super.paintComponent(g);
        // Graphics context is relative to the component's top-left corner (0,0)
        g.setColor(ballColor);
        // Draw the oval filling the component bounds
        g.fillOval(0, 0, radius * 2, radius * 2);
    }

    //-------------------------------------------------------
    public void moveBall() {
        // Calculate next potential center position
        int nextCenterX = getCenterX() + (xdir * slopeRun);
        int nextCenterY = getCenterY() + (ydir * slopeRise);

        // Check for collision on the left and right walls based on center position
        if (nextCenterX > compWidth) { // Hit right wall
            xdir *= -1;
            // Adjust position to be exactly at the boundary to avoid overshooting
            xpos = compWidth - radius;
        } else if (nextCenterX < radius) { // Hit left wall
             xdir *= -1;
             // Adjust position to be exactly at the boundary
             xpos = 0;
        }

        // Check for collision on the top and bottom walls based on center position
        if (nextCenterY > compHeight) { // Hit bottom wall
            ydir *= -1;
            // Adjust position to be exactly at the boundary
            ypos = compHeight - radius;
        } else if (nextCenterY < radius) { // Hit top wall
             ydir *= -1;
             // Adjust position to be exactly at the boundary
             ypos = 0;
        }

        // Update the position (top-left corner) based on direction and slope
        // Use the potentially updated directions
        xpos += (xdir * slopeRun);
        ypos += (ydir * slopeRise);

        // Ensure position doesn't go out of bounds after adjustment (safety check)
        xpos = Math.max(0, Math.min(xpos, compWidth - radius));
        ypos = Math.max(0, Math.min(ypos, compHeight - radius));
    }

     //-------------------------------------------------------
    // Method to reverse direction (can be used for simple collision response)
    public void reverse() {
        xdir *= -1;
        ydir *= -1;
    }

    // Method to swap movement vectors with another ball
    public void swapMovement(Ball other) {
        int tempXDir = this.xdir;
        int tempYDir = this.ydir;
        int tempSlopeRun = this.slopeRun;
        int tempSlopeRise = this.slopeRise;

        this.setXDir(other.getXDir());
        this.setYDir(other.getYDir());
        this.setSlopeRun(other.getSlopeRun());
        this.setSlopeRise(other.getSlopeRise());

        other.setXDir(tempXDir);
        other.setYDir(tempYDir);
        other.setSlopeRun(tempSlopeRun);
        other.setSlopeRise(tempSlopeRise);
    }

    // Method to check collision with another ball
    public boolean collidesWith(Ball other) {
        if (this == other) { // A ball cannot collide with itself
            return false;
        }

        int dx = this.getCenterX() - other.getCenterX();
        int dy = this.getCenterY() - other.getCenterY();
        // Use distance squared to avoid expensive square root calculation
        double distanceSq = dx * dx + dy * dy;

        int sumRadii = this.radius + other.radius;
        double sumRadiiSq = sumRadii * sumRadii;

        return distanceSq < sumRadiiSq;
    }

     // Method to resolve collision by slightly moving balls apart
     // This helps prevent balls from sticking together
     public void resolveCollision(Ball other) {
         int dx = this.getCenterX() - other.getCenterX();
         int dy = this.getCenterY() - other.getCenterY();
         double distance = Math.sqrt(dx * dx + dy * dy);
         int sumRadii = this.radius + other.radius;

         // Calculate overlap amount
         double overlap = sumRadii - distance;

         if (overlap > 0 && distance > 0) { // Check distance > 0 to avoid division by zero
             // Calculate normalized direction vector (dx/distance, dy/distance)
             double moveX = (dx / distance) * (overlap / 2.0); // Move each ball by half the overlap
             double moveY = (dy / distance) * (overlap / 2.0);

             // Update positions (move them apart along the collision axis)
             // Ensure positions stay within bounds
             this.xpos = Math.max(0, Math.min(this.compWidth - this.radius, (int)(this.xpos + moveX)));
             this.ypos = Math.max(0, Math.min(this.compHeight - this.radius, (int)(this.ypos + moveY)));

             other.xpos = Math.max(0, Math.min(other.compWidth - other.radius, (int)(other.xpos - moveX)));
             other.ypos = Math.max(0, Math.min(other.compHeight - other.radius, (int)(other.ypos - moveY)));
         } else if (distance == 0) {
             // If balls are exactly on top of each other, move one randomly
             this.xpos = Math.max(0, Math.min(this.compWidth - this.radius, this.xpos + RNG.nextInt(3) - 1));
             this.ypos = Math.max(0, Math.min(this.compHeight - this.radius, this.ypos + RNG.nextInt(3) - 1));
         }
     }
}

```



Okay, let's break down the `Ball.java` code. Imagine you're building a simple game or animation with bouncing balls on the screen. This `Ball.java` file acts as the **blueprint** for creating each individual ball object.

Think of it like this: `Ball.java` is the recipe, and every time you follow the recipe (create a `new Ball()`), you get an actual ball that can be put onto the screen (the `JPanel` in `Frame1.java`).

Here's a summary of what the `Ball` class does, explained simply:

1. **It's a Visual Thing:** The class `Ball extends JComponent`. In Java's Swing library (used for creating graphical user interfaces), a `JComponent` is basically something you can see on the screen. So, every `Ball` object is a visual component.

2. Knows Its Properties:

    Each ball object keeps track of its own information:

   - **Position:** `xpos`, `ypos` store the coordinates (like on a graph) of the ball's top-left corner within its container panel.
   - **Size:** `radius` determines how big the ball is.
   - **Color:** `ballColor` stores the ball's color.
   - **Movement Direction:** `xdir` and `ydir` tell the ball if it's currently moving left/right (`xdir` is 1 for right, -1 for left) and up/down (`ydir` is 1 for down, -1 for up).
   - **Speed/Angle:** `slopeRun` and `slopeRise` determine how many pixels the ball moves horizontally and vertically in each step. Changing these changes the ball's speed and angle.
   - **Boundaries:** `compWidth` and `compHeight` store the width and height of the area the ball is allowed to bounce within.

3. **Can Draw Itself:** The `paintComponent(Graphics g)` method is like the ball's instruction manual for drawing itself. When the program needs to display the ball, it calls this method, which draws a filled oval using the ball's current `ballColor` and `radius`.

4. Knows How to Move:

    The `moveBall()`  method contains the logic for updating the ball's position in each frame or time step.

   - It first checks if the ball is about to hit one of the edges (walls) of its container panel. It does this by looking ahead at where the ball's *center* will be in the next step.
   - If it detects a wall hit, it reverses the corresponding direction (`xdir` or `ydir`) so the ball "bounces" off. It also adjusts the position slightly to prevent the ball from going slightly past the wall.
   - Finally, it updates the `xpos` and `ypos` based on the current direction (`xdir`, `ydir`) and speed/angle (`slopeRun`, `slopeRise`).

5. Knows How to Interact with Other Balls:

   - `collidesWith(Ball other)`: This method checks if this ball is currently overlapping with another ball (`other`). It calculates the distance between their centers and compares it to the sum of their radii. If the distance is smaller, they've collided.
   - `swapMovement(Ball other)`: This is one way to handle a collision. It makes the two colliding balls swap their direction and speed/angle variables. It's a simple way to simulate a bounce between them.
   - `resolveCollision(Ball other)`: Sometimes, when balls collide, they might get stuck together slightly. This method gently pushes the two colliding balls apart just enough so they aren't overlapping anymore, making the collision look smoother.

6. **Can Change Its Properties:** The class includes many "getter" (like `getRadius()`, `getCenterX()`) and "setter" (like `setRadius(int r)`, `setBallColor(Color c)`) methods. These allow other parts of the program (like `Frame1.java`) to get information about a ball or change its properties after it's been created.

**In a Nutshell:**

The `Ball.java` class defines everything a single ball needs to know and do: its appearance (size, color), its position, how to move, how to bounce off walls, and how to detect and react to collisions with other balls. It's a self-contained blueprint for creating individual, interactive ball objects that can be managed and animated by another class like `Frame1`.



## Coding and Computer Science Concepts

If you were using this code in a freshman computer science course, it would effectively highlight several important coding techniques and concepts:

1. **Object-Oriented Programming (OOP):**
   - **Class Design:** Demonstrates how to define classes (`Ball`, `Frame1`) to represent real-world concepts or application components.
   - **Encapsulation:** The `Ball` class hides its internal state (like `xpos`, `ypos`, `radius`) and provides controlled access through getter and setter methods.
   - **Inheritance:** Shows how classes can inherit properties and behaviors from parent classes (`Ball extends JComponent`, `Frame1 extends JFrame`). `Ball` inherits the ability to be a visual component, and `Frame1` inherits the features of a standard window.
   - **Polymorphism:** The `Ball` class overrides the `paintComponent` method inherited from `JComponent` to provide its specific drawing behavior.
   - **Object Interaction:** `Frame1` creates and manages multiple `Ball` objects, storing them in a list and calling their methods (`moveBall`, `collidesWith`, etc.), demonstrating how objects collaborate.
2. **GUI Programming (using Java Swing):**
   - **Components:** Introduces basic GUI elements like windows (`JFrame`), panels (`JPanel`), and buttons (`JButton`).
   - **Custom Components:** Shows how to create a custom visual component (`Ball`) by extending `JComponent` and implementing custom drawing logic.
   - **Event Handling:** Uses `ActionListener` to respond to events, specifically timer ticks (`panelTimer`) for animation and button clicks (`jbttnAddBall`, etc.) for user interaction.
   - **Drawing:** Demonstrates basic 2D drawing using the `Graphics` object within `paintComponent` (drawing ovals).
   - **Layout Management:** Uses absolute positioning (`setLayout(null)`) within `jPanel1` to place the balls at specific coordinates.
3. **Animation and Timing:**
   - **Timers:** Employs `javax.swing.Timer` to create a discrete animation loop, triggering updates at regular intervals.
   - **State Management:** Shows how the state of objects (`Ball` positions and directions) is updated over time within the timer's event handler.
   - **Repainting:** Highlights the necessity of calling `repaint()` to refresh the display and show the updated state after changes have been made.
4. **Collision Detection and Simple Physics:**
   - **Boundary Checking:** Implementing logic to detect when an object hits the edge of its container (`moveBall` checking against `compWidth`, `compHeight`).
   - **Object Interaction Logic:** Developing algorithms to detect collisions between multiple objects (`collidesWith` using distance formula).
   - **Collision Response:** Implementing simple reactions to collisions (reversing direction for walls, swapping vectors for ball-ball collisions).
5. **Data Structures:**
   - **Collections:** Uses `ArrayList` (`alBalls`) to store and manage a variable number of `Ball` objects, demonstrating dynamic data structures.
   - **Iteration:** Shows how to iterate over collections (the `ArrayList`) to process each object (e.g., moving each ball, checking collisions).

These techniques provide a practical context for understanding core CS concepts beyond basic syntax, connecting OOP, algorithms (collision detection), data structures, and event-driven programming within a visual application.