## Second Program

```python

"""
Programmer: James Goudy
Date: 
Assignment:
    
2nd program

Problem 1 : Calculate the circumference of a circle
Formula:    C = 2πR   
            C - circumference
            π - pi 3.14
            R - Radius
            D - Diameter

Problem 2 : Calculate the volume of a prism
Formula:    V = lwd
            V - Volume
            l - length
            w - width
            d - depth

Exit Message

DO NOT SINGLE SPACE USE THE WHITE SPACE APPROPRIATELY

Pattern
Ask a question / get data
manipulate the data
Give back the answer

 """
 
 
""" Circumference of a circle """ 
answer = 0.0
r = 0.0
#note: their are not constants in python - designate in all caps
PI = 3.1416 
 
print("\n\nCalculate the circumference of a circle")

r = float(input("Enter the radius  "))

answer = 2.0 * r * PI
answer = round(answer, 2)

print("The circumference of the circle is " + str(answer))
 
""" Volume of a prism """
print("\n---------\nCalculate the volume of a prism")

l = float(input("Enter the length "))
w = float(input("Enter the width "))
d = float(input("Enter the depth  "))

answer = l * w * d
answer = round(answer, 2)

print("The volume of the prism is " + str(answer))

# Exit
print("\nThank you for using Goudy Software")
 
```



---

End of Topic



