# Loops - Typewriter Simulation



This is a fun little exercise.



```python
# -*- coding: utf-8 -*-
"""
Created on Thu Sep 15 18:54:58 2022

@author: jgoudy
"""
import sys
import time

winText = "Even though large tracts of Europe " + \
    "and many old and famous States have fallen or " + \
    "may fall into the grip of the Gestapo and " + \
    "all the odious apparatus of Nazi rule, " + \
    "we shall not flag or fail. We shall go on to the end, " + \
    "we shall fight in France, we shall fight on the seas and oceans, " + \
    "we shall fight with growing confidence and " + \
    "growing strength in the air, " + \
    "we shall defend our Island, whatever the cost may be, " + \
    "we shall fight on the beaches, " + \
    "we shall fight on the landing grounds, " + \
    "we shall fight in the fields and in the streets, " + \
    "we shall fight in the hills; we shall never surrender, " + \
    "and even if, which I do not for a moment believe, " + \
    "this Island or a large part of it were subjugated and starving, " + \
    "then our Empire beyond the seas, armed and " + \
    "guarded by the British Fleet, would carry on the struggle, " + \
    "until, in God’s good time, the New World, " + \
    "with all its power and might, steps forth to the rescue and " + \
    "the liberation of the old. - Winston Churchill"


def typeText(someText):
    
    # program is to approximately 60 chars per line
    # and not split words
    chrcount = 0
    
    for l in range(len(someText)):
        
        sys.stdout.write(someText[l])
        
        chrcount +=1
        if(chrcount > 60 and someText[l] == " "):
            sys.stdout.write("\n")
            chrcount = 0
        
        
        time.sleep(.02)
        
        

def main():
    
    theText = winText;
    typeText(theText)


main()

```



