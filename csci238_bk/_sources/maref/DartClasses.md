# Dart Classes





## Lecture Code

```Dart
//Example 1
class thebase {
  int a;
  int b;

  thebase(this.a, this.b);

  get geta => a;
  get getb => b;

  int add_ab() {
    return (a + b);
  }
}

class thechild extends thebase {
  int c;
  int d;

  //note the field names from the parent class a and b
  thechild( this.c, this.d, int a, int b) : super(a, b);

  get geta => c;
  get getb => d;
}

// --------------------------

//example 2
class Person {
  String firstname;
  String lastname;
  String city;

//empty constructor
  Person();

//named constructors
//varible names must match to use this technique.

  Person.setallinfo(this.firstname, this.lastname, this.city);

  Person.setfirstlast(this.firstname, this.lastname);

  /*
    
    Person.setfirstlast(String firstname, String lastname)
    {
        //The constructor can be written like this
        //if there needs to have addition code for setup
    }

  */










//Setters and Getters

  set setfirstname(String value) => firstname = value;
  get setfirstname => firstname;

  set setlastname(String value) => lastname = value;
  get getlastname => lastname;

  set setcity(String value) => city = value;
  get getcity => city;

  String allInfo() {
    return (firstname + " " + lastname + ", " + city);
  }
}
// --------------------------

class Worker extends Person {
  String company;
  String title;
  double salary;
  //starting with an underscore means its hidden.
  String _memo;

  //empty constructor
  Worker() {
    _memo = "Great Worker";
  }

  //create named constructor
  //note the parent fields in the constructor
  //in this case we are using placeholders fn and ln
  //instead of the field names of firstname and lastname
  Worker.setWorkerInfo(
      this.company, this.title, this.salary, String fn, String ln)
      : super.setfirstlast(fn, ln);

  Worker.setWorkerAllInfo(
      this.company, this.title, this.salary, String fn, String ln, String cty)
      : super.setallinfo(fn, ln, cty);
/*
      Worker.setWorkerAllInfo(
      this.company, this.title, this.salary, String fn, String ln, String cty)
      : super.setallinfo(fn, ln, cty)
      {
           //The constructor can be written like this
        //if there needs to have addition code for setup

      }

*/







  //setters and getters
  set setcompany(String value) => company = value;
  get getcompany => company;

  set settitle(String value) => title = value;
  get gettitle => title;

  set setsalary(double value) => salary = value;
  get getsalary => salary;

  set setmemo(String value) => _memo = value;
  get getmemo => _memo;

  String AllWorkerInfo() {
    return (lastname +
        ", " +
        firstname +
        " - " +
        company +
        " " +
        title +
        " " +
        salary.toString() +
        " ");
  }
}

main(List<String> arguments) {
  //empty list - note it is var variable name = <datatype>{empty braces};
  var people = <Person>{};
  var workers = <Worker>{};

  var numPeople = 10;

  //example 1
  print("\n Example 1");
  thechild myObj = new thechild(10, 20, 30, 40);

  print(myObj.add_ab());


  //example 2
  print("\n Example 2");
  Person p1 = new Person.setallinfo("Bubba", "Smith", "kalispell");
  print(p1.allInfo());

  //create people and store in array
  print("\nCreate and print people");

  for (int c = 0; c < numPeople; c++) {
    Person p2 = new Person.setallinfo(
        "Bob" + c.toString(), "Doe" + c.toString(), "Dayton" + c.toString());
    people.add(p2);
  }

  for (Person value in people) {
    print(value.allInfo());
  }

  for(int c = 0; c < numPeople; c++)
  {
          Person w1 = new Worker.setWorkerAllInfo("MyCorp", 
          "Software Engineer", 
          90000, 
          "Bob" + c.toString(), 
          "Doe" + c.toString(), 
          "Dayton" + c.toString());

          workers.add(w1);

  }

    for (Worker value in workers) {
    print(value.AllWorkerInfo());
  }
}

```

