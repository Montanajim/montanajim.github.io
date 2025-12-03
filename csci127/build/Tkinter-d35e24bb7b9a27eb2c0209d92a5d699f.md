# Tkinter

Tkinter stands for *Tk interface*.  **tkinter** is the standard Python interface for creating Graphical User Interfaces (GUI).  It can run on Windows, macOS, and Linux. 

``` {admonition} Note
The **Geometry** is the command to actually place the form on the screeen.
```



## Lecture Code

```python
"""
calculator

NOTE- MOST OF THE FORM CONTROLS/WIDGETS ARE
WRITTEN AS GLOBAL

"""

import tkinter as tk
from tkinter import messagebox
import sys


def addBoxes():

    try:
        ans = 	float(inNum1.get("1.0", "end")) + \
            	float(inNum2.get("1.0", tk.END))
    except:
        ans = "Error"

    lblAns["text"] = ans


def addButtonClick(event):
    addBoxes()


def focus_next_widget(event):
    event.widget.tk_focusNext().focus()
    return("break")


def boxClear(event):
    clearBoxes()


def clearBoxes():
    
    # the clearBoxes is also used in a "non" 
    # event function
    
    inNum1.delete("1.0", "end")
    inNum2.delete("1.0", "end")
    lblAns["text"] = ""


def close_window():

    # if you don't want to show the messagebox
    # the if statement can be deleted. The destroy
    # and exit commands are still required.
    # Tab them appropriately.
    if messagebox.askokcancel("Quit", "Do you want to quit?"):
        
        # these two are always required
        theFrame.destroy()
        sys.exit(0)

# sometimes you will it root
theFrame = tk.Tk()


# add title
theFrame.title("Calculator")

# set the height and width
frameWidth = 250
frameHeight = 150

# get the screen width and height
scrnH = theFrame.winfo_screenheight()
scrnW = theFrame.winfo_screenwidth()

# calculate the center of window
xpos = int((scrnW/2) - (frameWidth/2))
ypos = int((scrnH/2) - (frameHeight/2))

# set geometry - This command places the frame on the screen with the
# hegith x width and the position xpos, ypos in the window
# theFrame.geometry('250x150+200+200')

# Note the code is building a string
# 250X150 + xpos + ypos
theFrame.geometry(str(frameWidth)+"x" + str(frameHeight)+"+" +
                  str(xpos)+"+"+str(ypos))

# frame widgets need to be global

# label 1
tk.Label(theFrame, text="Num 1", bg="#3300CC", fg="white").place(x=10, y=10)

# add an input box 1
inNum1 = tk.Text(theFrame, height=1, width=10)
inNum1.place(x=100, y=10)
inNum1.bind("<Tab>", focus_next_widget)

# label 2
tk.Label(theFrame, text="Num 2", bg="#3300CC", fg="white").place(x=10, y=40)

# add an input box 1
inNum2 = tk.Text(theFrame, height=1, width=10)
inNum2.place(x=100, y=40)
inNum2.bind("<Tab>", focus_next_widget)

bttnAdd = tk.Button(theFrame, text="Add", height=1, width=10, command=addBoxes)
bttnAdd.place(x=100, y=70)

# bind button to multiple events
bttnAdd.bind("<Return>", addButtonClick)
bttnAdd.bind("<Button-1>", addButtonClick)
bttnAdd.bind("<Tab>", focus_next_widget)

# add answer label
lblAns = tk.Label(theFrame, text="Answer")
lblAns.place(x=10, y=70)

# add clear button
bttnClr = tk.Button(theFrame, text="Clear", fg="#000080",
                    height=1, width=10, command=clearBoxes)
bttnClr.place(x=100, y=100)

# bind our bind to events
bttnClr.bind("<Return>", boxClear)
bttnClr.bind("<Button-1>", boxClear)
bttnClr.bind("<Tab>", focus_next_widget)

# use this to close the window
# note that you have to write the close_window function
theFrame.protocol("WM_DELETE_WINDOW", close_window)

# main loop
theFrame.mainloop()

```

