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

![image-20250417151933254](\\assets\image-20250417151933254.png)

## Ball_R.java



```java
/*
*******************************************
    BALL R
*******************************************

 */
package j2_threaddemoboxes;

import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JComponent;

/**
 *
 * @author jgoudy
 */
public class Ball_R extends JComponent implements Runnable {

    private volatile Thread ballThread;
    private volatile boolean threadSuspended = false;

    private int msize;
    private int mxpos = 0;
    private int mypos = 0;
    private int mspeed = 1;
    private int mxdir = 1;
    private int mydir = 1;
    private Color mcolor;
    private int mcvwidth;
    private int mcvheight;
    private int mrise = 1;
    private int mrun = 1;

    private long speedInterval;

    public void Ball(int size, int xpos, int ypos, int speed, int rise, int run, int cvwidth, int cvheight) {

        this.msize = size;
        this.mxpos = xpos;
        this.mypos = ypos;
        mrise = rise;
        mrun = run;
        //mspeed = speed;
        speedInterval = speed;
        mcvwidth = cvwidth;
        mcvheight = cvheight;

        mcolor = Color.blue;
        //this.setSize(mcvwidth,mcvheight);

        ballThread = new Thread(this);
       // ballThread.start();

    }

    public void paintComponent(Graphics g) {

        //super.paintComponent(g); 
        g.setColor(mcolor);
        g.fillOval(mxpos, mypos, msize, msize);

    }

    public void newLocation(int xpos, int ypos) {
        mxpos = xpos;
        mypos = ypos;

    }

    private void moveTheBall() {
        if (mxpos > mcvwidth - msize) {
            mxdir = mxdir * -1;
            mxpos = mcvwidth - msize - 1;
            if (mcolor == Color.blue) {
                mcolor = Color.red;
            } else {
                mcolor = Color.blue;
            }

        } else if (mxpos < -1) {
            mxdir = mxdir * -1;
            mxpos = 0;
            mcolor = Color.green;
        }

        if (mypos > mcvheight - msize) {
            mydir = mydir * -1;
            mypos = mcvheight - msize;
            mcolor = Color.white;

        } else if (mypos < -1) {
            mydir = mydir * -1;
            mypos = 0;
            mcolor = Color.lightGray;
        }

        mxpos = mxpos + (mxdir * mrun);
        mypos = mypos + (mydir * mrise);
        //setLocation(mxpos, mypos);
        
        repaint();

    }

    public void run() {
        Thread thisThread = Thread.currentThread();
        while (ballThread == thisThread) {
            try {
                Thread.sleep(speedInterval);

                synchronized (this) {
                    while (threadSuspended && ballThread == thisThread) {
                        wait();
                    }

                    //put code here
                    //-----------------
                    moveTheBall();
                   

                    //---------------
                }
            } catch (InterruptedException e) {
            }

        }
    }

    public synchronized void stopBall() {
        ballThread = null;
        notify();
    }

    public synchronized void startBall() {
        threadSuspended = false;
       ballThread.start();
    }

    public synchronized void pauseBall() {
        threadSuspended = true;
    }

    public synchronized void resumeBall() {
        threadSuspended = false;
        notify();
    }
}

```



---

## Ball_R_Wave.java



```java
/*
*******************************************
    BALL R WAVE
*******************************************

 */
package j2_threaddemoboxes;

import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JComponent;

/**
 *
 * @author jgoudy
 */
public class Ball_R_Wave extends JComponent implements Runnable {

    private volatile Thread ballThread;
    private volatile boolean threadSuspended = false;

    private int msize;
    private int mxpos = 30;
    private int mypos = 0;
    private int mspeed = 1;
    private int mxdir = 1;
    private int mydir = 1;
    private Color mcolor;
    private int mcvwidth;
    private int mcvheight;
    private int mrise = 1;
    private int mrun = 1;

    double wangle = 0;
    double wangleVel = 0.5;
    double wamplitude = 30;
    private double wx, wy = 0;

    private long speedInterval;

    public void Ball(int size, int xpos, int ypos,
            int speed, int rise, int run, int cvwidth, int cvheight) {

        this.msize = size;
        this.mxpos = xpos;
        this.mypos = ypos;
        mrise = rise;
        mrun = run;
        //mspeed = speed;
        speedInterval = speed;
        mcvwidth = cvwidth;
        mcvheight = cvheight;

        mcolor = Color.blue;
        //this.setSize(mcvwidth,mcvheight);

        ballThread = new Thread(this);
        // ballThread.start();

    }

    public void paintComponent(Graphics g) {

        super.paintComponent(g);
        g.setColor(mcolor);
        g.fillOval(mxpos, mypos, msize, msize);

    }

    public void newLocation(int xpos, int ypos) {
        mxpos = xpos;
        mypos = ypos;

    }

    private void moveTheBall() {
        if (mxpos > mcvwidth - msize) {
            mxdir = mxdir * -1;
            mxpos = mcvwidth - msize - 1;
            if (mcolor == Color.blue) {
                mcolor = Color.red;
            } else {
                mcolor = Color.blue;
            }

        } else if (mxpos < -1) {
            mxdir = mxdir * -1;
            mxpos = 0;
            mcolor = Color.green;
        }

        if (mypos > mcvheight - msize) {
            mydir = mydir * -1;
            mypos = mcvheight - msize;
            mcolor = Color.white;

        } else if (mypos < -1) {
            mydir = mydir * -1;
            mypos = 0;
            mcolor = Color.lightGray;
        }

        double zzz = 0;
        zzz = (wamplitude * Math.sin(wangle));

        mypos = (int) (wamplitude * Math.sin(wangle)) / 1 + (mcvheight / 2 - 10);

        wangle = wangle + wangleVel;

        mxpos = mxpos + (mxdir * mrun);
//        mypos = mypos + (mydir * mrise);
        //setLocation(mxpos, mypos);
        repaint();

    }

    public void run() {
        Thread thisThread = Thread.currentThread();
        while (ballThread == thisThread) {
            try {
                Thread.sleep(speedInterval);

                synchronized (this) {
                    while (threadSuspended && ballThread == thisThread) {
                        wait();
                    }

                    //put code here
                    //-----------------
                    moveTheBall();

                    //---------------
                }
            } catch (InterruptedException e) {
            }

        }
    }

    public synchronized void stopBall() {
        ballThread = null;
        notify();
    }

    public synchronized void startBall() {
        threadSuspended = false;
        ballThread.start();
    }

    public synchronized void pauseBall() {
        threadSuspended = true;
        notify();
    }

    public synchronized void resumeBall() {
        threadSuspended = false;
        notify();
    }
}

```





---

## Ball_R_Wave_V.java

```java
/*
*******************************************
    BALL R WAVE V
*******************************************

 */
package j2_threaddemoboxes;

import java.awt.Color;
import java.awt.Graphics;
import javax.swing.JComponent;

/**
 *
 * @author jgoudy
 */
public class Ball_R_Wave_V extends JComponent implements Runnable {

    private volatile Thread ballThread;
    private volatile boolean threadSuspended = false;

    private int msize;
    private int mxpos = 30;
    private int mypos = 0;
    private int mspeed = 1;
    private int mxdir = 1;
    private int mydir = 1;
    private Color mcolor;
    private int mcvwidth;
    private int mcvheight;
    private int mrise = 1;
    private int mrun = 1;

    double wangle = .5;
    double wangleVel = 0.3;
    double wamplitude = 30;
    private double wx, wy = 0;

    private long speedInterval;

    public void Ball(int size, int xpos, int ypos, int speed, int rise, int run, int cvwidth, int cvheight) {

        this.msize = size;
        this.mxpos = xpos;
        this.mypos = ypos;
        mrise = rise;
        mrun = run;
        //mspeed = speed;
        speedInterval = speed;
        mcvwidth = cvwidth;
        mcvheight = cvheight;

        mcolor = Color.blue;
        //this.setSize(mcvwidth,mcvheight);

        ballThread = new Thread(this);
        // ballThread.start();

    }

    public void paintComponent(Graphics g) {

        //super.paintComponent(g); 
        g.setColor(mcolor);
        g.fillOval(mxpos, mypos, msize, msize);
        

    }

    public void newLocation(int xpos, int ypos) {
        mxpos = xpos;
        mypos = ypos;

    }

    private void moveTheBall() {
        if (mxpos > mcvwidth - msize) {
            mxdir = mxdir * -1;
            mxpos = mcvwidth - msize - 1;
            if (mcolor == Color.blue) {
                mcolor = Color.red;
            } else {
                mcolor = Color.blue;
            }

        } else if (mxpos < -1) {
            mxdir = mxdir * -1;
            mxpos = 0;
            mcolor = Color.green;
        }

        if (mypos > mcvheight - msize) {
            mydir = mydir * -1;
            mypos = mcvheight - msize;
            mcolor = Color.white;

        } else if (mypos < -1) {
            mydir = mydir * -1;
            mypos = 0;
            mcolor = Color.lightGray;
        }

        double zzz = 0;
        zzz = (wamplitude*Math.sin(wangle));
        
        mxpos = (int)(wamplitude*Math.sin(wangle))/1 + (mcvwidth/2 - 10);

        wangle = wangle + wangleVel;
        
        mxpos = mxpos + (mxdir * mrun);
        mypos = mypos + (mydir * mrise);
        //setLocation(mxpos, mypos);
       repaint();

    }

    public void run() {
        Thread thisThread = Thread.currentThread();
        while (ballThread == thisThread) {
            try {
                Thread.sleep(speedInterval);

                synchronized (this) {
                    while (threadSuspended && ballThread == thisThread) {
                        wait();
                    }

                    //put code here
                    //-----------------
                    moveTheBall();

                    //---------------
                }
            } catch (InterruptedException e) {
            }

        }
    }

    public synchronized void stopBall() {
        ballThread = null;
        notify();
    }

    public synchronized void startBall() {
        threadSuspended = false;
       ballThread.start();
    }

    public synchronized void pauseBall() {
        threadSuspended = true;
        notify();
    }

    public synchronized void resumeBall() {
        threadSuspended = false;
        notify();
    }
}

```









---



## Frame1.java



``` java
/*

 */
package j2_threaddemoboxes;

/**
 *
 * @author jgoudy
 */
public class Frame1 extends javax.swing.JFrame {

    /**
     * Creates new form Frame1
     */
    Ball_R ball1;
    Ball_R_Wave ball2;
    Ball_R_Wave_V ball3;

    int pauseStatus1 = 1;
    int pauseStatus2 = 1;
    int pauseStatus3 = 1;

    int startStatus1 = 1;
    int startStatus2 = 1;
    int startStatus3 = 1;

    public Frame1() {
        initComponents();
        
        this.setLocationRelativeTo(null);

        this.setTitle("Thread Demo");
        
    }

    /**
     * This method is called from within the constructor to
     * initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is
     * always regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jPanel1 = new javax.swing.JPanel();
        jPanel2 = new javax.swing.JPanel();
        jPanel3 = new javax.swing.JPanel();
        jbttnStart1 = new javax.swing.JButton();
        jbttnStart2 = new javax.swing.JButton();
        jbttnStart3 = new javax.swing.JButton();
        jbttnPause1 = new javax.swing.JButton();
        jbttnPause2 = new javax.swing.JButton();
        jbttnPause3 = new javax.swing.JButton();
        jMenuBar1 = new javax.swing.JMenuBar();
        jMenu1 = new javax.swing.JMenu();
        jMenuItem_Quit = new javax.swing.JMenuItem();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jPanel1.setBorder(javax.swing.BorderFactory.createEtchedBorder());

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 146, Short.MAX_VALUE)
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 145, Short.MAX_VALUE)
        );

        jPanel2.setBorder(javax.swing.BorderFactory.createEtchedBorder());

        javax.swing.GroupLayout jPanel2Layout = new javax.swing.GroupLayout(jPanel2);
        jPanel2.setLayout(jPanel2Layout);
        jPanel2Layout.setHorizontalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 0, Short.MAX_VALUE)
        );
        jPanel2Layout.setVerticalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 145, Short.MAX_VALUE)
        );

        jPanel3.setBorder(javax.swing.BorderFactory.createEtchedBorder());

        javax.swing.GroupLayout jPanel3Layout = new javax.swing.GroupLayout(jPanel3);
        jPanel3.setLayout(jPanel3Layout);
        jPanel3Layout.setHorizontalGroup(
            jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 147, Short.MAX_VALUE)
        );
        jPanel3Layout.setVerticalGroup(
            jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 145, Short.MAX_VALUE)
        );

        jbttnStart1.setText("Start");
        jbttnStart1.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnStart1ActionPerformed(evt);
            }
        });

        jbttnStart2.setText("Start");
        jbttnStart2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnStart2ActionPerformed(evt);
            }
        });

        jbttnStart3.setText("Start");
        jbttnStart3.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnStart3ActionPerformed(evt);
            }
        });

        jbttnPause1.setText("Pause");
        jbttnPause1.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnPause1ActionPerformed(evt);
            }
        });

        jbttnPause2.setText("Pause");
        jbttnPause2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnPause2ActionPerformed(evt);
            }
        });

        jbttnPause3.setText("Pause");
        jbttnPause3.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jbttnPause3ActionPerformed(evt);
            }
        });

        jMenu1.setText("File");

        jMenuItem_Quit.setAccelerator(javax.swing.KeyStroke.getKeyStroke(java.awt.event.KeyEvent.VK_Q, java.awt.event.InputEvent.CTRL_MASK));
        jMenuItem_Quit.setText("Quit");
        jMenuItem_Quit.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jMenuItem_QuitActionPerformed(evt);
            }
        });
        jMenu1.add(jMenuItem_Quit);

        jMenuBar1.add(jMenu1);

        setJMenuBar(jMenuBar1);

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                    .addGroup(javax.swing.GroupLayout.Alignment.LEADING, layout.createSequentialGroup()
                        .addGap(80, 80, 80)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                            .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jbttnStart1, javax.swing.GroupLayout.PREFERRED_SIZE, 151, javax.swing.GroupLayout.PREFERRED_SIZE)))
                    .addGroup(layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(jbttnPause1, javax.swing.GroupLayout.PREFERRED_SIZE, 151, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addGap(59, 59, 59)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false)
                    .addComponent(jPanel2, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                    .addComponent(jbttnStart2, javax.swing.GroupLayout.DEFAULT_SIZE, 151, Short.MAX_VALUE)
                    .addComponent(jbttnPause2, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                .addGap(49, 49, 49)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jPanel3, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jbttnStart3, javax.swing.GroupLayout.PREFERRED_SIZE, 151, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jbttnPause3, javax.swing.GroupLayout.PREFERRED_SIZE, 151, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addContainerGap(106, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(70, 70, 70)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jPanel3, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addGap(31, 31, 31)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jbttnStart1)
                    .addComponent(jbttnStart2)
                    .addComponent(jbttnStart3))
                .addGap(18, 18, 18)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                        .addComponent(jbttnPause1)
                        .addComponent(jbttnPause2))
                    .addComponent(jbttnPause3))
                .addContainerGap(101, Short.MAX_VALUE))
        );

        pack();
    }// </editor-fold>                        

    private void addBall1() {
        int speed = 20;
        int size = 20;
        int rise = 3;
        int run = 1;
        int xdir = 1;
        int ydir = 1;

        ball1 = new Ball_R();
        ball1.Ball(size, 10, 10, speed, rise, run, jPanel1.getWidth(), jPanel1.getHeight());
        ball1.setLocation(0, 0);
        ball1.setSize(jPanel1.getWidth(), jPanel1.getHeight());
        jPanel1.add(ball1);

    }

    private void addBall2() {
        int speed = 25;
        int size = 20;
        int rise = 3;
        int run = 1;
        int xdir = 1;
        int ydir = 1;

        ball2 = new Ball_R_Wave();
        ball2.Ball(size, 20, 30, speed, rise, run, jPanel2.getWidth(), jPanel2.getHeight());
        ball2.setLocation(0, 0);
        ball2.setSize(jPanel2.getWidth(), jPanel2.getHeight());
        jPanel2.add(ball2);

    }

    private void addBall3() {
        int speed = 35;
        int size = 20;
        int rise = 3;
        int run = 4;
        int xdir = 1;
        int ydir = 1;

        ball3 = new Ball_R_Wave_V();
        ball3.Ball(size, 10, 10, speed, rise, run, jPanel3.getWidth(), jPanel3.getHeight());
        ball3.setLocation(0, 0);
        ball3.setSize(jPanel3.getWidth(), jPanel3.getHeight());
        jPanel3.add(ball3);

    }

    private void jbttnStart1ActionPerformed(java.awt.event.ActionEvent evt) {                                            
        // TODO add your handling code here:

        if (startStatus1 == 1) {
            jbttnStart1.setText("Stop");
            addBall1();
            ball1.startBall();
            startStatus1 = startStatus1 * -1;
        } else {
            jbttnStart1.setText("Start");
            ball1.stopBall();

            jPanel1.removeAll();
            jPanel1.repaint();
            startStatus1 = startStatus1 * -1;
        }
    }                                           

    private void jbttnStart2ActionPerformed(java.awt.event.ActionEvent evt) {                                            
        if (startStatus2 == 1) {
            jbttnStart2.setText("Stop");
            addBall2();
            ball2.startBall();
            startStatus2 = startStatus2 * -1;
        } else {
            jbttnStart2.setText("Start");
            ball2.stopBall();

            jPanel2.removeAll();
            jPanel2.repaint();
            startStatus2 = startStatus2 * -1;
        }
    }                                           

    private void jbttnStart3ActionPerformed(java.awt.event.ActionEvent evt) {                                            
        if (startStatus3 == 1) {
            jbttnStart3.setText("Stop");
            addBall3();
            ball3.startBall();
            startStatus3 = startStatus3 * -1;
        } else {
            jbttnStart3.setText("Start");
            ball3.stopBall();

            jPanel3.removeAll();
            jPanel3.repaint();
            startStatus3 = startStatus3 * -1;
        }
    }                                           

    private void jbttnPause1ActionPerformed(java.awt.event.ActionEvent evt) {                                            
        if (pauseStatus1 == 1) {
            jbttnPause1.setText("Resume");
            ball1.pauseBall();
            pauseStatus1 = pauseStatus1 * -1;
        } else {
            jbttnPause1.setText("Pause");
            ball1.resumeBall();
            pauseStatus1 = pauseStatus1 * -1;
        }
    }                                           

    private void jbttnPause2ActionPerformed(java.awt.event.ActionEvent evt) {                                            

        if (pauseStatus2 == 1) {
            jbttnPause2.setText("Resume");
            ball2.pauseBall();
            pauseStatus2 = pauseStatus2 * -1;
        } else {
            jbttnPause2.setText("Pause");
            ball2.resumeBall();
            pauseStatus2 = pauseStatus2 * -1;
        }

    }                                           

    private void jbttnPause3ActionPerformed(java.awt.event.ActionEvent evt) {                                            
        if (pauseStatus3 == 1) {
            jbttnPause3.setText("Resume");
            ball3.pauseBall();
            pauseStatus3 = pauseStatus3 * -1;
        } else {
            jbttnPause3.setText("Pause");
            ball3.resumeBall();
            pauseStatus3 = pauseStatus3 * -1;
        }
    }                                           

    private void jMenuItem_QuitActionPerformed(java.awt.event.ActionEvent evt) {                                               
       
        System.exit(0);
        
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
    private javax.swing.JMenu jMenu1;
    private javax.swing.JMenuBar jMenuBar1;
    private javax.swing.JMenuItem jMenuItem_Quit;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JButton jbttnPause1;
    private javax.swing.JButton jbttnPause2;
    private javax.swing.JButton jbttnPause3;
    private javax.swing.JButton jbttnStart1;
    private javax.swing.JButton jbttnStart2;
    private javax.swing.JButton jbttnStart3;
    // End of variables declaration                   
}

```

