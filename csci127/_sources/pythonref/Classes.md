# Classes

## Key Ideas

* classes
* objects
* inheritance



```{admonition} Definition
**Class** is code that acts like a blueprint.  "Objects" are made from classes. Classes can represent things in terms of code. For example, they could represent a *car* - make, model, year; a *dog* - dog name, breed, color; a *person* - first name, last name, address, city, state; etc.
```





## Lecture Code

### Example 1 - Cars

```python
# -*- coding: utf-8 -*-
"""
Created on Mon Oct 2019

@author: jgoudy
"""

class car:
    
    
    
    carspeed = 0
    carengineOn = True
    
    
    # constructor  - there can only be one in python
    def __init__(self, carmake="",carmodel="",caryear="", carcolor=""):
        self.carspeed = 0
        self.carengineOn = False
        self.carmake = carmake
        self.carmodel = carmodel
        self.caryear= caryear
        self.carcolor = carcolor
    
    # __str__  defines what print() or str() is printed for the obje
    # example print(car) = what is defined here is what will be printed
    def __str__(self):
        return ("Make: " + self.carmake + "\n" + \
                "Model: " + self.carmodel + "\n" + \
                "Year: " + self.caryear + "\n" + \
                "Color: " + self.carcolor + "\n")
    

    # __str__ must return string object 
    # whereas __repr__ can return any python expression.
    #https://docs.python.org/3/reference/datamodel.html
    # when possible it should return a string
    
    def __repr__(self):
        return (self.carmake+","+ self.carmodel+","+ self.caryear+","+ self.carcolor)
  
    
    @property
    def make(self):
        return self.carmake    
    @make.setter
    def make(self, value):
        self.carmake = value
       
    @property
    def model(self):
        return self.carmodel    
    @model.setter
    def model(self, value):
        self.carmodel = value
       
    @property
    def year(self):
        return self.caryear    
    @year.setter
    def year(self, value):
        self.caryear = value
       
    @property
    def color(self):
        return self.carcolor    
    @color.setter
    def color(self, value):
        self.carcolor = value
    
    @property
    def speed(self):
        return self.carspeed
    
    @property
    def engineOn(self):
        return self.carengineOn

    def startCar(self):
        self.carengineOn = True
        
    def stopCar(self):
        self.carengineOn = False
        
   
    def accelerate(self,speed = 5):
        if (self.carengineOn == True) :
            self.carspeed += speed
            print("aaargh")
        else:
            print("Start the car")
      
      
    def deccelerate(self,speed = 5):
        if self.carspeed > 0:
            self.carspeed -= speed
        else:
            self.carspeed = 0
        print("car is stopped")
                
    
    def honk(self):
        print("beep beep")
# --------------------------------------------------        

def main():
    
   mycar1 = car()
   
   mycar2 = car("Ford", "Mustang","1967","red")
    
   mycar2.accelerate()
   mycar2.startCar()
   mycar2.accelerate()
   print(mycar2.speed)
   mycar2.accelerate()
   print(mycar2.speed)
   mycar2.accelerate(50)
   print(mycar2.speed)
   mycar2.deccelerate(70)
   
   print("The color of my car is " + mycar2.color)
   mycar2.color = "blue"
   print("The color of my car is " + mycar2.color)
   
   mycar1.honk()
     
   print("\bye bye")
    
main()


```



### Example 2 - Person / Worker /  Voter

```python
class Person:
    """ Represents a person. """

    # python can only have one constructor
    def __init__(self, first_name="", last_name="", town=""):
        self.first_name = first_name
        self.last_name = last_name
        self.town = town

    # describes the class person
    def __str__(self):
        return self.first_name + ", " + self.last_name + ", " + self.town
    
    # falls back to this if there is no __str__ - used in debugging
    def __repr__(self):
        return self.first_name + ", " + self.last_name + ", " + self.town


    #CANNOT HAVE VARIABLE NAME SAME AS FUNCTION NAME

    @property
    def firstname(self):
        return self.first_name

    @firstname.setter
    def firstname(self, first_name):
        self.first_name = first_name

    @property
    def lastname(self):
        return self.last_name

    @lastname.setter
    def lastname(self, last_name):
        self.last_name = last_name

    @property
    def city(self):
        return self.town

    @city.setter
    def city(self, town):
        self.town = town

    # methods
    def full_name(self):
        """ Returns the full name (first and last name) as a string """
        return self.first_name + " " + self.last_name
    
    def full_name_city(self):
        """ Returns first, last and city as string """
        return self.first_name + " " + self.last_name + self.city
    
    def username(self):
        """ returns the username as string """
        return self.first_name[0] + self.last_name
    
# --------------- End Of Person ---------------

class Worker(Person):
    """ represents a worker """
    
    def __init__(self, first_name = "", last_name= "", town= "",
                 job_title= "", company_name= "", wages=0):
        self.job_title = job_title
        self.company_name = company_name
        self.wages = wages

        Person.__init__ (self, first_name, last_name, town)

    # describes the class person
    def __str__(self):
        return self.first_name + ", " + self.last_name + ", " + self.town 
               + " "  + self.job_title + ", " + self.company_name + 
               ", " +str(self.wages)
               
    # falls back to this if there is no __str__ - used in debugging               
    def __repr__(self):
        return self.first_name + ", " + self.last_name + ", " + self.town 
               + " "  + self.job_title + ", " + self.company_name + 
               ", " +str(self.wages)

    @property
    def jobtitle(self):
        return self.job_title

    @jobtitle.setter
    def jobtitle(self, title_value):
        self.job_title = title_value

    @property
    def company(self):
        return self.company_name

    @company.setter
    def company(self, company_value):
        self.company_name = company_value

    @property
    def salary(self):
        return self.wages

    @salary.setter
    def salary(self, wages_value):
        self.wages = wages_value
# --------------- End Of Worker ---------------

class Voter(Person):
    """ Represents a voter based on Person """
    def __init__(self, first_name = "", last_name= "", town= "",
                 precient_number= 0, party_name= ""):
        self.precient_number = precient_number
        self.party_name = party_name

        Person.__init__ (self, first_name, last_name, town)
        
    def __str__(self):
        return self.first_name + " " + self.last_name + " " + self.town 
           + " "  + str(self.precient_number) + " " + self.party_name
    
    # falls back to this if there is no __str__ - used in debugging
    def __repr__(self):
        return self.first_name + ", " + self.last_name + ", " + self.town 
           + ", "  + str(self.precient_number) + ", " + self.party_name
    
    @property
    def precient(self):
        """represents the precient of the voter as a string """
        return self.precient_number
    
    @precient.setter
    def precient(self, precient_value):
        self.precient_number = precient_value
    
    @property
    def party(self):
        """represents the party of the voter as a string"""
        return self.party_name
    
    @party.setter
    def party(self, party_value):
        self.party_name = party_value

# --------------- End Of Voter --------------- 
        

def main():

    qty  = 5

    
    print("Create Person")
#    p1 = Person("John", "Doe", "Anywhere")

    p1 = Person("John","Doe","Kali")
    p1.firstname = "Jimbo"
    p1.lastname = "Smith"
    p1.city = "Whitefish"

    print(p1)
    print(p1.full_name())
    print(p1.first_name)
    print(p1.lastname)
    print(p1)

    p2 = Person("Sally", "Smith", "Polson")
    #change first and last name of p2
    p2.first_name = "Bonnie"
    p2.last_name = "Bond"
    print(p2)

    # create a list of people
    people = []
    
    for i in range(qty):                
        px = Person("John" + str(i), 
                    "Doe" + str(i),
                    "Kali" + str(i))
        people.append(px)
        print(people[i].first_name + " "+ people[i].last_name)
    
    print()        
    
    # create workers
    w1 = Worker("Tom", "Tune", "New York", "Dancer", "Broadway", 100000)
    print(w1)

    w2 = Worker()
    w2.firstname = "Ira"
    w2.lastname = "Money"
    w2.company = "IRS"
    w2.jobtitle = "Auditor"
    w2.salary = 90000


    print(w2)    
    
    print()
    
    # create a list of workers
    workers = []
   
    
    
    for i in range(qty):                
        wx = Worker("John" + str(i), 
                    "Doe" + str(i),"",
                    "Programmer" + str(i))
        workers.append(wx)
        print(workers[i].first_name + " "+ 
              workers[i].last_name  + " " +
              workers[i].jobtitle)
    
    print()

    # create voters
    v1 = Voter("Abe", "Lincoln", "Springfield", 17, "Republican")
    v2 = Voter()
    
    v2.firstname = "Charles"
    v2.lastname = "Daily"
    v2.city = "Chicago"
    v2.precient_number= 1
    v2.party ="Democrat"
    print(v1)
    print(v2)
    
    print()
   
    # create a list of voters
    voters = []
    
    for i in range(qty):                
        vx = Voter("John" + str(i), 
                    "Doe" + str(i),"","",
                    "Independent" + str(i))
        voters.append(vx)
        print(voters[i].firstname + " "+ 
              voters[i].lastname  + " " +
              voters[i].party) 


    print("bye")

main()

```



### Example 3 - getters and setters

```python
# -*- coding: utf-8 -*-
"""
@author: jgoudy
"""
class class1:
    
    # The traditional "old" style of creating getters and setters
    
    def __init__(self, number = 0):
        self.number = number
        
    # getter method
    def get_Number(self):
        return self.number
    
    # setter method
    def set_Number(self, value):
        self.number = value
        
# ---------------- End of class 2 -----------------
        
class class2:
    
    # using properties 
    # using a property allows the object code to be cleaner
    # and users of the class will not have to make changes to their code
    
    def __init__(self, anumber = 0):
        self.anumber = anumber
        
    # getter method
    def get_Number(self):
        return self.anumber
    
    # setter method
    def set_Number(self, value):
        self.anumber = value
    
    # function to delete the number attribute
    def del_Number(self):
        del self.anumber
    
    # TURN SETTERS AND GETTERS INTO PROPERTIES
    number = property(get_Number, set_Number, del_Number, "Stores a number")

# ---------------- End of class 2 -----------------
   
class class3:
   
    
    # THE PYTHONIC WAY
    # This is the preferred way of doing setters and getters.  
    
    # this is a getter method

    def __init__(self, anumber = 0):
        self.anumber = anumber
    
    @property
    def number(self):
        return self.anumber
    
    # this is the setter method
    @number.setter
    def number(self, value):
        self.anumber = value
        
    @number.deleter
    def number(self):
        del self.anumber
# ---------------- End of class 3 -----------------

def main():
    
    #Old way
    mc1 = class1()
    mc1.set_Number(42)
    print(mc1.get_Number())
    
    
    print("\n----------\n")
    mc2 = class2()
    mc2.number = 52
    print(mc2.number)
    
    
    print("\n----------\n")
    mc3 = class3()
    mc3.number = 62
    print(mc3.number)
    
    
    
main()


```



### Example 4 - Trains

```python

# Remember - 7:45
# finish with worker
# try catch

"""
Train
	id
	engine
	caboose
	start
	destination
	traincars
"""

import random

class train:

    #constructor
    def __init__(self, a_trainid, a_start="Whitefish", a_destination=""):
        self.a_trainid = a_trainid
        self.a_start = a_start
        self.a_destination = a_destination

        #list  hold our train cars
        self.traincars = []
    
    
        #add an engine to our train
        self._addengine()


    # ---- properties
    @property
    def trainid(self):
        return self.a_trainid
    @trainid.setter
    def trainid(self, value):
        self.a_trainid = value

    @property
    def start(self):
        return self.a_start
    @start.setter
    def start(self, value):
        self.a_start = value

 
    @property
    def destination(self):
        return self.a_destination
    @destination.setter
    def destination(self, value):
        self.a_destination = value


    # add our methods
    def _addengine(self):
        self.traincars.append("engine")

    def addcar(self,value):
        self.traincars.append(value)

    def addcaboose(self):
        self.traincars.append("caboose")

    def printtrain(self):
        print("\n" + self.trainid + " " + self.start + " to " + 
              self.destination)

        for i in range(len(self.traincars)):
            print("\t" + self.traincars[i])

        print("")

# ----------------------- end of class --------------------------------


mytrains = []

def printmytrains(alist):

    print(len(alist))
    for i in range(len(alist)):
        print(alist[i].printtrain())


#create a method to create train with random cars
def createtrain():

    #create a list car types
    cartypes = ["flat","box","tanker","passenger","ore"]

    #create a list of towns
    towns = ["Denver", "Seattle", "Missoula", "Kalispell",
            "Whitefish", "Chicago","New York", "Clarksville"]

    #randomly  pick a number to determine number of trains
    rnd = random.randint(0,50)

    #loop to create the trains
    for i in range(rnd):
    
        rndtemp = random.randint(0,len(towns)-1)
        astart = towns[rndtemp]

        rndtemp = random.randint(0,len(towns)-1)
        adest = towns[rndtemp]

        # call the class to create a train
        tx = train("T"+str(i),astart,adest)

        # add some random cars to our newly created train
        randtemp = random.randint(0,25)

        # add the cars to the train
        for i in range(randtemp):
            rndcar = random.randint(0,len(cartypes)-1)
            tx.addcar(cartypes[rndcar])

        tx.addcaboose()

        mytrains.append(tx)

 

def main():
    
    train1 = train("ML11","Helena","Missoula")
    for i in range(10):
        train1.addcar("boxcar")
    train1.addcaboose()

    train1.printtrain()

    createtrains()
    printmytrains(mytrains)


main()



```

