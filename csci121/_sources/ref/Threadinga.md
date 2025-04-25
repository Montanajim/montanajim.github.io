# Threading



In computing, a **process** is an instance of a computer program that is being executed. Each process has its own memory space. **Threading**, in the context of Java (and other programming languages), is a way to achieve **concurrency** *within* a single process.

Think of a process like a workshop.

- A **single-threaded** process is like having only **one worker** in the workshop. This worker has to do every task sequentially (e.g., build a chair part by part, paint it, then package it). If one task takes a long time (like waiting for paint to dry), the entire workshop's progress stops.
- A **multi-threaded** process is like having **multiple workers** (threads) in the same workshop. They all share the same tools and materials (the process's memory space). One worker can build the chair parts, another can paint a finished chair, and a third can package a painted one, potentially all happening *concurrently* or *interleaved*. This allows the workshop (the program) to make progress on multiple tasks simultaneously, leading to better efficiency and responsiveness.

**Key Concepts of Java Threading:**

1. Concurrency vs. Parallelism:
   - **Concurrency:** Tasks *appear* to run at the same time. The system switches between tasks rapidly, giving the illusion of simultaneous execution, even on a single-core processor.
   - **Parallelism:** Tasks *actually* run at the same time on different processor cores. This requires a multi-core processor. Java threading enables both concurrency and, on suitable hardware, parallelism.
2. **Shared Memory:** Threads within the same Java process share the same memory space (heap memory). This makes communication between threads relatively easy (they can access the same objects) but also introduces challenges like race conditions if access to shared data isn't carefully managed.
3. **Thread Lifecycle:** Threads go through various states (e.g., NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED).
4. Benefits:
   - **Responsiveness:** Keep applications (especially GUIs) responsive by performing long-running tasks in background threads.
   - **Performance:** Utilize multi-core processors effectively for computationally intensive tasks.
   - **Resource Sharing:** Efficient sharing of resources compared to creating separate processes.
5. Challenges:
   - **Complexity:** Writing correct concurrent code is harder than single-threaded code.
   - **Synchronization Issues:** Need to manage access to shared data to prevent race conditions (where the outcome depends on the unpredictable timing of thread execution).
   - **Deadlock:** Two or more threads waiting indefinitely for each other to release resources.
   - **Livelock:** Threads are active but unable to make progress.
   - **Starvation:** One thread is perpetually denied access to resources.



## Example Code

**Overall Program Summary**

This Java application demonstrates the use of multithreading within a Swing GUI framework. It presents a window containing three distinct panels, each capable of hosting an animated ball. Users can independently control the animation within each panel using "Start"/"Stop" and "Pause"/"Resume" buttons. When started, each ball runs on its own dedicated thread, calculating its movement according to a predefined path (bouncing, horizontal wave, or vertical wave) and redrawing its position asynchronously.

The program effectively showcases how background threads can manage computationally intensive or time-based tasks like animation without freezing the main user interface thread (Event Dispatch Thread). It utilizes core Java threading concepts like `Runnable`, `Thread`, `volatile`, `synchronized`, `wait()`, and `notify()`, along with Swing's mechanism (`SwingUtilities.invokeLater`) for safely updating the GUI from these background threads. This separation ensures the application remains responsive while animations are running.



## Ball

**Ball Class Summary**

The `Ball` class serves a dual purpose: it's a graphical component (`JComponent`) responsible for drawing a colored circle, and it's a `Runnable` task that controls its own animation logic on a separate thread. Each `Ball` instance manages its position (`xpos`, `ypos`), size, color, movement direction (`xdir`, `ydir`), speed (`sleepTime`), and path type (bounce or wave). Its `run()` method contains the main animation loop, which periodically updates the ball's position, checks for collisions with the panel boundaries (reversing direction and changing color upon impact), and then schedules a repaint on the Event Dispatch Thread using `SwingUtilities.invokeLater`. The class includes synchronized methods (`startBall`, `stopBall`, `pauseBall`, `resumeBall`) and uses `volatile` variables and `wait`/`notify` mechanisms to safely manage the thread's lifecycle and state changes (like pausing) from other threads.

```java
/*
Developer: James Goudy
The ball class is to be added to a JPanel. 
This program is to demonstate threads.
Project: J2_Threading_Rev25

 */
package j2_threading_rev25;

import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JComponent;
import javax.swing.SwingUtilities;

/**
 *
 * @author jgoudy
 */
public class Ball extends JComponent implements Runnable {

    // thread variables
    private volatile Thread ballThread;
    private volatile boolean threadSuspended;

    // When class elements are public, there is no ability to check if the
    // data is correct as compared to setters and getters.
    // In many cases, using getter and setters is the better way.
    
    
    // component dimension - usually overlaid a jpanel
    public int compWidth;
    public int compHeight;

    // graphic properties
    // will use this for both height and width
    public int ballSize = 10;
    public volatile Color color;

    // position of graphic on component panel
    public volatile int xpos = 0;
    public volatile int ypos = 0;

    // direction based on slope
    public int rise = 1;
    public int run = 2;

    // direction based on slope
    public int xdir = 1;
    public int ydir = 1;

    // since this is a thread, we need a sleep time
    public long sleepTime = 10;

    // ball path - 1 is bounce, 2 is horizontal wave, 3 is vertical wave
    //public int ballPath;
    public enum BallPath {
        BOUNCE, HORIZONTAL_WAVE, VERTICAL_WAVE
    }
    public BallPath currentBallPath;

    // variables for wave action
    public double waveAngle = 0.1;
    public double waveAngleVelocity = 0.5;
    public double waveAmplitude = 30;

    // constructors
    public Ball()
    {
        ballThread = new Thread(this);
        color = Color.blue;
    }

    public Ball(int compWidth, int compHeight, int ballSize, Color color,
            int xpos, int ypos, int rise, int run)
    {
        this.compWidth = compWidth;
        this.compHeight = compHeight;
        this.ballSize = ballSize;
        this.color = color;
        this.xpos = xpos;
        this.ypos = ypos;
        this.rise = rise;
        this.run = run;

        threadSuspended = false;

        ballThread = new Thread(this);

    }

    @Override
    public void run()
    {
        Thread thisThread = Thread.currentThread();

        while (ballThread == thisThread) {
            try {
                Thread.sleep(sleepTime);

                synchronized (this) {

                    // this is for pausing the thread
                    while (threadSuspended && ballThread == thisThread) {
                        wait();
                    }

                    //put code here
                    //-----------------
                    moveBall();

                    //---------------
                }
            } catch (InterruptedException e) {
            }

        }

    }

    @Override
    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        g.setColor(this.color);
        g.fillOval(xpos, ypos, ballSize, ballSize);

    }

    public void moveBall()
    {

        checkIfBallHitASide();

        switch (currentBallPath) {
            case BOUNCE -> {
                // ball bounces when hits side
                xpos = xpos + (xdir * run);
                ypos = ypos + (ydir * rise);

            }
            case HORIZONTAL_WAVE -> {
                // ball travels a horizontal wave
                ypos = (int) (waveAmplitude * Math.sin(waveAngle))
                        + (compHeight / 2 - 10);
                xpos = xpos + (xdir * run);

                waveAngle = waveAngle + waveAngleVelocity;

            }
            case VERTICAL_WAVE -> {
                // ball travels vertical wave
                xpos = (int) (waveAmplitude * Math.sin(waveAngle))
                        + (compWidth / 2 - 10);
                ypos = ypos + (ydir * rise);

                waveAngle = waveAngle + waveAngleVelocity;

            }
            default -> {
                currentBallPath = BallPath.BOUNCE;
            }
        }
       
        // schedule repaint on the EDT (wait until the tread is done)
        SwingUtilities.invokeLater(() -> {
            repaint();
        });

    }

    private void checkIfBallHitASide()
    {
        // check right and left
        if (xpos > compWidth - ballSize) {
            // check if ball hits/exceeds right side
            xdir = xdir * -1;
            xpos = compWidth - ballSize - 1;
            if (color == Color.blue) {
                color = Color.red;
            } else {
                color = Color.blue;
            }

        } else if (xpos <= 0) {
            // check if ball hits/exceeds left side
            xdir = xdir * -1;
            xpos = 0;
            color = Color.green;
        }

        // check bottom and top
        if (ypos > compHeight - ballSize) {
            // check if ball hits/exceeds bottom side
            ydir = ydir * -1;
            ypos = compHeight - ballSize;
            color = Color.yellow;

        } else if (ypos <= 0) {
            // check if ball hits/exceeds top side
            ydir = ydir * -1;
            ypos = 0;
            color = Color.lightGray;
        }

    }

    // start stop pause resume thread - the ball
    public synchronized void stopBall()
    {
        ballThread = null;
        
        // notify is to let the other threads and 
        // the main program know that this thread
        // is no longer in existence 
        
        notify();
    }

    public synchronized void startBall()
    {
        threadSuspended = false;
        ballThread.start();
    }

    public synchronized void pauseBall()
    {
        threadSuspended = true;
    }

    public synchronized void resumeBall()
    {
        threadSuspended = false;
        
        // notify is to let the other threads
        // and the main program  know that the
        // thread is starting up again
        
        notify();
    }

}

```



---

## Frame1.java

**Frame1 Class Summary**

The `Frame1` class defines the main application window using `javax.swing.JFrame` and contains the user interface elements. It sets up three `JPanel` components, each acting as a container for a `Ball` animation, along with corresponding "Start"/"Stop" and "Pause"/"Resume" buttons for each panel. `Frame1` is responsible for orchestrating the creation, addition, and removal of `Ball` instances within their respective panels in response to button clicks. It maintains state variables (`isBallStartedX`, `isBallPausedX`) to track the status of each ball and toggle the button functionalities appropriately. The action listeners for the buttons call the relevant control methods (`startBall`, `stopBall`, `pauseBall`, `resumeBall`) on the correct `Ball` object stored in an array, effectively linking the UI controls to the underlying animation threads.



``` java
/*

Developer: James Goudy
The purpose of this program is to demonstrate the use of threads in Java.
Project Name: J2_Threading_Rev25
 */
package j2_threading_rev25;


import javax.swing.JPanel;

/**
 *
 * @author jgoudy
 */
public class Frame1 extends javax.swing.JFrame {

    // an array to keep track of the balls
    Ball[] balls = new Ball[3];

    
    // status variables for ball
    boolean isBallStarted1 = true;
    boolean isBallStarted2 = true;
    boolean isBallStarted3 = true;
    

    boolean isBallPaused1 = true;
    boolean isBallPaused2 = true;
    boolean isBallPaused3 = true;
    
    /**
     * Creates new form Frame1
     */
    public Frame1()
    {
        initComponents();

        this.setLocationRelativeTo(this);

    }

    private void addBall(JPanel jp, int ballSize, Ball.BallPath ballpath,
            int sleepTime, int rise, int run, int arrayIndex)
    {

        Ball nb = new Ball();

        // set characteristics of the ball
        // set ball path
        switch (ballpath) {
            case Ball.BallPath.BOUNCE -> {
                nb.currentBallPath = Ball.BallPath.BOUNCE;
            }
            case Ball.BallPath.HORIZONTAL_WAVE-> {
                nb.currentBallPath = Ball.BallPath.HORIZONTAL_WAVE;
            }
            case Ball.BallPath.VERTICAL_WAVE -> {
                nb.currentBallPath = Ball.BallPath.VERTICAL_WAVE;
            }
            default -> {
                nb.currentBallPath = Ball.BallPath.BOUNCE;
            }
        }

        nb.compHeight = jp.getHeight();
        nb.compWidth = jp.getWidth();
        nb.ballSize = ballSize;
        nb.rise = rise;
        nb.run = run;
        nb.sleepTime = sleepTime;

        // remember when a component (ball) is added to a panel
        // the visibility, the size of the component, height and width
        // and the location of the top right corner has to be set
        nb.setVisible(true);
        nb.setSize(jp.getWidth(), jp.getHeight());
        nb.setLocation(0, 0);

        //nb.startBall();
        jp.add(nb);
        balls[arrayIndex] = nb;

    }

    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">//GEN-BEGIN:initComponents
    private void initComponents()
    {

        jPanel1 = new javax.swing.JPanel();
        jbttnStart1 = new javax.swing.JButton();
        jbttnPause1 = new javax.swing.JButton();
        jPanel2 = new javax.swing.JPanel();
        jbttnStart2 = new javax.swing.JButton();
        jbttnPause2 = new javax.swing.JButton();
        jPanel3 = new javax.swing.JPanel();
        jbttnStart3 = new javax.swing.JButton();
        jbttnPause3 = new javax.swing.JButton();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jPanel1.setBackground(new java.awt.Color(255, 255, 255));
        jPanel1.setBorder(javax.swing.BorderFactory.createLineBorder(new java.awt.Color(0, 0, 0), 2));

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 0, Short.MAX_VALUE)
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 275, Short.MAX_VALUE)
        );

        jbttnStart1.setText("Start");
        jbttnStart1.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnStart1ActionPerformed(evt);
            }
        });

        jbttnPause1.setText("Pause");
        jbttnPause1.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnPause1ActionPerformed(evt);
            }
        });

        jPanel2.setBackground(new java.awt.Color(255, 255, 255));
        jPanel2.setBorder(javax.swing.BorderFactory.createLineBorder(new java.awt.Color(0, 0, 0), 2));

        javax.swing.GroupLayout jPanel2Layout = new javax.swing.GroupLayout(jPanel2);
        jPanel2.setLayout(jPanel2Layout);
        jPanel2Layout.setHorizontalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 0, Short.MAX_VALUE)
        );
        jPanel2Layout.setVerticalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 275, Short.MAX_VALUE)
        );

        jbttnStart2.setText("Start");
        jbttnStart2.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnStart2ActionPerformed(evt);
            }
        });

        jbttnPause2.setText("Pause");
        jbttnPause2.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnPause2ActionPerformed(evt);
            }
        });

        jPanel3.setBackground(new java.awt.Color(255, 255, 255));
        jPanel3.setBorder(javax.swing.BorderFactory.createLineBorder(new java.awt.Color(0, 0, 0), 2));

        javax.swing.GroupLayout jPanel3Layout = new javax.swing.GroupLayout(jPanel3);
        jPanel3.setLayout(jPanel3Layout);
        jPanel3Layout.setHorizontalGroup(
            jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 0, Short.MAX_VALUE)
        );
        jPanel3Layout.setVerticalGroup(
            jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 275, Short.MAX_VALUE)
        );

        jbttnStart3.setText("Start");
        jbttnStart3.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnStart3ActionPerformed(evt);
            }
        });

        jbttnPause3.setText("Pause");
        jbttnPause3.addActionListener(new java.awt.event.ActionListener()
        {
            public void actionPerformed(java.awt.event.ActionEvent evt)
            {
                jbttnPause3ActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(59, 59, 59)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false)
                    .addComponent(jPanel1, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnStart1, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnPause1, javax.swing.GroupLayout.DEFAULT_SIZE, 204, Short.MAX_VALUE))
                .addGap(38, 38, 38)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false)
                    .addComponent(jPanel2, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnStart2, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnPause2, javax.swing.GroupLayout.DEFAULT_SIZE, 204, Short.MAX_VALUE))
                .addGap(39, 39, 39)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false)
                    .addComponent(jPanel3, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnStart3, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnPause3, javax.swing.GroupLayout.PREFERRED_SIZE, 204, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addContainerGap(75, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(70, 70, 70)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(jPanel3, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(30, 30, 30)
                        .addComponent(jbttnStart3)
                        .addGap(30, 30, 30)
                        .addComponent(jbttnPause3))
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(30, 30, 30)
                        .addComponent(jbttnStart2)
                        .addGap(30, 30, 30)
                        .addComponent(jbttnPause2))
                    .addGroup(layout.createSequentialGroup()
                        .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(30, 30, 30)
                        .addComponent(jbttnStart1)
                        .addGap(30, 30, 30)
                        .addComponent(jbttnPause1)))
                .addContainerGap(25, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>//GEN-END:initComponents

    private void jbttnStart1ActionPerformed(java.awt.event.ActionEvent evt)//GEN-FIRST:event_jbttnStart1ActionPerformed
    {//GEN-HEADEREND:event_jbttnStart1ActionPerformed

        // toggle the start button to stop
        if (isBallStarted1) {
            jbttnStart1.setText("Stop");
            addBall(jPanel1, 20, Ball.BallPath.BOUNCE, 10, 1, 1, 0);
            balls[0].startBall();
            isBallStarted1 = false;
        } else {
            jbttnStart1.setText("Start");
            balls[0].stopBall();
            balls[0] = null;
            jPanel1.removeAll();
            jPanel1.repaint();

            // reset the pause button
            isBallStarted1 = true;
            isBallPaused1 = true;
            jbttnPause1.setText("Pause");
        }


    }//GEN-LAST:event_jbttnStart1ActionPerformed

    private void jbttnPause1ActionPerformed(java.awt.event.ActionEvent evt)//GEN-FIRST:event_jbttnPause1ActionPerformed
    {//GEN-HEADEREND:event_jbttnPause1ActionPerformed

        try {

            if (isBallPaused1) {
                jbttnPause1.setText("Resume");
                balls[0].pauseBall();
                isBallPaused1 = false;
            } else {
                jbttnPause1.setText("Pause");
                balls[0].resumeBall();
                isBallPaused1 = true;
            }
        } catch (Exception e) {
            
            // in production we would log the error
        }

    }//GEN-LAST:event_jbttnPause1ActionPerformed

    private void jbttnStart2ActionPerformed(java.awt.event.ActionEvent evt)//GEN-FIRST:event_jbttnStart2ActionPerformed
    {//GEN-HEADEREND:event_jbttnStart2ActionPerformed
        
        
        // toggle the start button to stop
        if (isBallStarted2) {
            jbttnStart2.setText("Stop");
            addBall(jPanel2, 20, Ball.BallPath.HORIZONTAL_WAVE, 25, 1, 1, 1);
            balls[1].startBall();
            isBallStarted2 = false;
        } else {
            jbttnStart2.setText("Start");
            balls[1].stopBall();
            balls[1] = null;
            jPanel2.removeAll();
            jPanel2.repaint();

            // reset the pause button
            isBallStarted2 = true;
            isBallPaused2 = true;
            jbttnPause2.setText("Pause");
        }
        
        


    }//GEN-LAST:event_jbttnStart2ActionPerformed

    private void jbttnPause2ActionPerformed(java.awt.event.ActionEvent evt)//GEN-FIRST:event_jbttnPause2ActionPerformed
    {//GEN-HEADEREND:event_jbttnPause2ActionPerformed
        try {

            if (isBallPaused2) {
                jbttnPause2.setText("Resume");
                balls[1].pauseBall();
                isBallPaused2 = false;
            } else {
                jbttnPause2.setText("Pause");
                balls[1].resumeBall();
                isBallPaused2 = true;
            }
        } catch (Exception e) {
            
            // in production we would log the error
        }
    }//GEN-LAST:event_jbttnPause2ActionPerformed

    private void jbttnStart3ActionPerformed(java.awt.event.ActionEvent evt)//GEN-FIRST:event_jbttnStart3ActionPerformed
    {//GEN-HEADEREND:event_jbttnStart3ActionPerformed
        // toggle the start button to stop
        if (isBallStarted3) {
            jbttnStart3.setText("Stop");
            addBall(jPanel3, 20, Ball.BallPath.VERTICAL_WAVE, 40, 1, 1, 2);
            balls[2].startBall();
            isBallStarted3 = false;
        } else {
            jbttnStart3.setText("Start");
            balls[2].stopBall();
            balls[2] = null;
            jPanel3.removeAll();
            jPanel3.repaint();

            // reset the pause button
            isBallStarted3 = true;
            isBallPaused3 = true;
            jbttnPause3.setText("Pause");
        }
    }//GEN-LAST:event_jbttnStart3ActionPerformed

    private void jbttnPause3ActionPerformed(java.awt.event.ActionEvent evt)//GEN-FIRST:event_jbttnPause3ActionPerformed
    {//GEN-HEADEREND:event_jbttnPause3ActionPerformed
        try {

            if (isBallPaused3) {
                jbttnPause3.setText("Resume");
                balls[2].pauseBall();
                isBallPaused3 = false;
            } else {
                jbttnPause3.setText("Pause");
                balls[2].resumeBall();
                isBallPaused3 = true;
            }
        } catch (Exception e) {
            
            // in production we would log the error
        }
    }//GEN-LAST:event_jbttnPause3ActionPerformed

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

    // Variables declaration - do not modify//GEN-BEGIN:variables
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JButton jbttnPause1;
    private javax.swing.JButton jbttnPause2;
    private javax.swing.JButton jbttnPause3;
    private javax.swing.JButton jbttnStart1;
    private javax.swing.JButton jbttnStart2;
    private javax.swing.JButton jbttnStart3;
    // End of variables declaration//GEN-END:variables
}

```

