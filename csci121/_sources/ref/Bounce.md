# Bounce Balls Animation



<img src="assets/Bounce_Rev24.gif" alt="2024-04-11_11-55-01" style="zoom: 67%;" />



**Initial Setup:**

- It imports necessary libraries for Swing components, random number generation, timers, and colors.
- The `Frame1` class inherits from `javax.swing.JFrame` which represents the main window of the application.

**Global Variables:**

- `panelTimer`: A timer object to control repainting of the panel where balls bounce.
- `TimerStatus`: Boolean flag to track if the timer is running.
- `RNG`: Instance of `Random` class to generate random values.
- Initial ball properties like `x`, `y`, `radius`.
- `clockTick`: Time interval between timer ticks (in milliseconds).
- `alBalls`: An `ArrayList` to store bouncing ball objects.
- `RNG2`: Another random number generator (potentially for future use).

**Constructor (`Frame1`):**

- Initializes the frame and sets its layout.
- Sets `TimerStatus` to `false` initially.
- Creates another random number generator (`RNG2`).
- Positions the frame in the center of the screen.

**`PanelClock` method:**

- Creates a new `Timer` object with `clockTick` interval and an anonymous `ActionListener`.
- The `actionPerformed` method of the listener iterates through `alBalls`, calling their `moveBall` method to update their positions.
- It then loops through all components in `jPanel1` (which should be the balls), retrieves their objects using casting, and sets their locations based on their `xpos` and `ypos` values in the `Ball` class.
- It repaints the panel (`jPanel1`) and reduces the timer delay to a smaller value (presumably for smoother animation).
- Finally, starts the timer.

**Event Handlers:**

- ```
  jbttnAddBallActionPerformed
  ```

  : triggered when the "Add Ball" button is clicked.

  - Creates a new `Ball` object.
  - Sets random ball properties like radius, speed, color, and initial position.
  - Adds the ball to the `jPanel1` panel and the `alBalls` list.
  - Starts the timer (`PanelClock`) if it's not already running.

- ```
  jbttnDeleteBallActionPerformed
  ```

  : triggered when the "Delete Ball" button is clicked.

  - Tries to remove the first ball from `jPanel1` and `alBalls` 
  - Repaints the panel.

- ```
  jbttnClearAllActionPerformed
  ```

  : triggered when the "Clear All" button is clicked.

  - Removes all components from `jPanel1`.
  - Clears the `alBalls` list.

This code demonstrates how to create a simple bouncing ball animation with Swing. The balls update their positions based on random directions and repaint themselves within the panel.

---



![image-20240411111208708](assets/image-20240411111208708-1712858934213-7.png)

<div style="page-break-after:always"></div>

## Project File

J2_Bounce_Rev24.java

```java
/*
Project: Bounce
Description: Animate Bouncing Balls
Programmer: James Goudy
Date: April, 2024
 */
package j2_bounce_rev24;

/**
 *
 * @author jgoudy
 */
public class J2_Bounce_Rev24 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        
        // Instatiate a new frame
        Frame1 myFrame = new Frame1();
        myFrame.setVisible(true);
        myFrame.setSize(730,575);
        
        
    }
    
}/*
Project: Bounce
Description: Animate Bouncing Balls
Programmer: James Goudy
Date: April, 2024
 */
package j2_bounce_rev24;

/**
 *
 * @author jgoudy
 */
public class J2_Bounce_Rev24 {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        
        // Instatiate a new frame
        Frame1 myFrame = new Frame1();
        myFrame.setVisible(true);
        myFrame.setSize(730,575);
        
        
    }
    
}
```



<div style="page-break-after:always"></div>

## Frame1.java

```java
/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/GUIForms/JFrame.java to edit this template
 */
package j2_bounce_rev24;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.util.Random;
import javax.swing.Timer;
import java.awt.Color;
import javax.swing.JComponent;

/**
 *
 * @author jgoudy
 */
public class Frame1 extends javax.swing.JFrame {

    // Global Variables
    Timer panelTimer;  //this will control the repaint of the panel
    boolean TimerStatus;
    
    
    Random RNG = new Random();
    // Setup to show one can instantiate an object later
    Random RNG2;
    
    
    // initial ball info
    int x = 1;
    int y = 1;
    int radius = 25;

    // Timer Tick
    int clockTick = 100;
    
    // Arraylist to hold the balls
    ArrayList<Ball> alBalls = new ArrayList();


    // constructor
    public Frame1() {
        initComponents();

        TimerStatus = false;

        RNG2 = new Random();

        this.setLocationRelativeTo(null);

    }

    private void PanelClock() {

        panelTimer = new Timer(clockTick, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {

                for (Ball item : alBalls) {
                    item.moveBall();
                }

                for (int i = 0; i < jPanel1.getComponentCount(); i++) {
                    Ball js = (Ball) jPanel1.getComponent(i);
                    jPanel1.getComponent(i).setLocation(js.getXpos(), js.ypos);
                }


                jPanel1.repaint();
                panelTimer.setDelay(20);
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
    private void initComponents() {

        jPanel1 = new javax.swing.JPanel();
        jLabel1 = new javax.swing.JLabel();
        jbttnAddBall = new javax.swing.JButton();
        jbttnDeleteBall = new javax.swing.JButton();
        jbttnClearAll = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jPanel1.setBorder(javax.swing.BorderFactory.createLineBorder(new java.awt.Color(0, 0, 0)));

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 591, Short.MAX_VALUE)
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 364, Short.MAX_VALUE)
        );

        jLabel1.setFont(new java.awt.Font("Segoe UI", 1, 24)); // NOI18N
        jLabel1.setText("Bounce");

        jbttnAddBall.setText("Add Ball");
        jbttnAddBall.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnAddBallActionPerformed(evt);
            }
        });

        jbttnDeleteBall.setText("Delete Ball");
        jbttnDeleteBall.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnDeleteBallActionPerformed(evt);
            }
        });

        jbttnClearAll.setText("Clear All");
        jbttnClearAll.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnClearAllActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(62, 62, 62)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jLabel1)
                    .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(jbttnAddBall, javax.swing.GroupLayout.PREFERRED_SIZE, 100, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(18, 18, 18)
                        .addComponent(jbttnDeleteBall, javax.swing.GroupLayout.PREFERRED_SIZE, 100, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(18, 18, 18)
                        .addComponent(jbttnClearAll, javax.swing.GroupLayout.PREFERRED_SIZE, 100, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addContainerGap(69, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(42, 42, 42)
                .addComponent(jLabel1)
                .addGap(18, 18, 18)
                .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(18, 18, 18)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jbttnAddBall)
                    .addComponent(jbttnDeleteBall)
                    .addComponent(jbttnClearAll))
                .addContainerGap(15, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void jbttnAddBallActionPerformed(java.awt.event.ActionEvent evt) {                                             

        // create a ball
        Ball aball = new Ball();

        // ball characteristics
        aball.setVisible(true);
        aball.setRadius(RNG.nextInt(40) + 10);
        aball.setBallspeed(RNG.nextInt(50) + 5);
        aball.setCompHeight(jPanel1.getHeight());
        aball.setCompWidth(jPanel1.getWidth());
        aball.setXpos(1);
        aball.setYpos(1);
        aball.setSlopeRun(RNG.nextInt(10) + 1);
        aball.setSlopeRise(RNG.nextInt(10));
        aball.setBallColor(new Color(RNG.nextInt(256),
                RNG.nextInt(256), RNG.nextInt(256)));

        // area where we bounce the balls
        //aball.setSize(jPanel1.getWidth(), jPanel1.getHeight());
        aball.setSize(2 * radius, 2 * radius);

        // add the ball to the panel
        jPanel1.add(aball);
        alBalls.add(aball);

       // aball.startBall();

        if (!TimerStatus) {
            PanelClock();
            TimerStatus = true;
        }
    }                                            

    private void jbttnDeleteBallActionPerformed(java.awt.event.ActionEvent evt) {                                                

        try {

            // uncomment to remove the last ball added
            //    jPanel1.remove(jPanel1.getComponentCount() - 1);
            
            // remove first ball added
            jPanel1.remove(alBalls.get(0));
            alBalls.remove(0);
            
            jPanel1.repaint();

        } catch (Exception e) {
        }


    }                                               

    private void jbttnClearAllActionPerformed(java.awt.event.ActionEvent evt) {                                              
        
        // Remove all balls from the pannel
        jPanel1.removeAll();
        
        // Reset the arraylist
        alBalls.clear();
       
        
    }                                             

    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
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
            public void run() {
                new Frame1().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private javax.swing.JLabel jLabel1;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JButton jbttnAddBall;
    private javax.swing.JButton jbttnClearAll;
    private javax.swing.JButton jbttnDeleteBall;
    // End of variables declaration                   
}

```

<div style="page-break-after:always"></div>

## BALL

```java
/*
Bounce Balls
Programmer: James Goudy
Rev: April, 2024
 */
package j2_bounce_rev24;

import java.awt.Color;
import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;
import javax.swing.JComponent;
import javax.swing.Timer;

/**
 *
 * @author jgoudy
 */
public class Ball extends JComponent {

    // private members
    // position of the ball
    int xpos = 1;
    int ypos = 1;

    // direction of the ball - forward or backwards
    int xdir = 1;
    int ydir = 1;

    // size of the panel: these are going to be defaults
    int compWidth = 500;
    int compHeight = 500;

    // angle of the ball
    int slopeRun = 1;
    int slopeRise = 1;

    // speed
    int ballspeed = 2;

    // radius of the ball
    int radius = 25;

    // Timer
    Timer bTimer;

    // ball color
    Color ballColor;

    Random RNG;

    boolean wasReversed = false;

    //-------------------------------------------------------
    
    // Constructor
    public Ball() {

        RNG = new Random();
        ballColor = Color.blue;

    }

    // Setters
    public void setXpos(int xpos) {
        this.xpos = xpos;
    }

    public void setYpos(int ypos) {
        this.ypos = ypos;
    }

    public int getXpos() {
        return xpos;
    }

    public int getYPos() {
        return ydir;
    }


    //-------------------------------------------------------
    
    public void setCompWidth(int compWidth) {
        this.compWidth = compWidth - (radius);
    }

    public void setCompHeight(int compHeight) {
        this.compHeight = compHeight - (radius);
    }

    public void setSlopeRun(int slopeRun) {
        this.slopeRun = slopeRun;
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

    public void setRadius(int radius) {
        this.radius = radius;
    }

    public void setBallColor(Color ballColor) {
        this.ballColor = ballColor;
    }

    //-------------------------------------------------------
    
    // Draw the ball
    @Override
    public void paintComponent(Graphics g) {
        super.paintComponent(g);

        g.setColor(Color.white);

        // un comment below to visualize the bounding box
        //g.fillRect(0, 0, radius, radius);
        g.setColor(ballColor);
        g.fillOval(0, 0, radius, radius);
    }

    
    //-------------------------------------------------------
    
    public void moveBall() {

        // check for collision on the left and right of the panel
        if (xpos > compWidth) {
            xdir = xdir * -1;
            xpos = compWidth - 1 - (radius);
        } else if (xpos < -1) {
            xdir = xdir * -1;
            xpos = 0 + (RNG.nextInt(10));
        }

        // check for collision on the top and bottom of the panel
        if (ypos > compHeight) {
            ydir = ydir * -1;
            ypos = compHeight - 1 - (radius);
        } else if (ypos < -1) {
            ydir = ydir * -1;
            ypos = 0 + (RNG.nextInt(10));
        }

        //System.out.println(radius);
        // increment the x and y positions
        ypos = ypos + (ydir * slopeRise);
        xpos = xpos + (xdir * slopeRun);

        // System.out.println(xpos + " " + ypos);
    }

    //-------------------------------------------------------
    
    
    //--- USED IF COLLISION IS PROGRAMMED ON FRAME 1---------
    
    // Used for collision if frame 1 is coded for collision
    public boolean getWasReversed() {
        return wasReversed;
    }

    public void setWasReversed() {
        this.wasReversed = true;
    }

    public void resetWasReversed() {
        this.wasReversed = false;
    }
    
    public void reverse() {

        xdir = xdir * -1;
        ydir = ydir * -1;

    }

}

```



