# Bottom Navigation Bar

 ## Key Widgets

* Scaffold



```{admonition} Note
**Bottom Navigation Bar** is a property of the Scaffold.  There are three important properties *items*, *currentIndex*, and *onTap*. *items* setup the bottom buttons. *currentIndex* is the button index that was tapped. *onTap* is the listener for the button. The onTap should call the setState() function in order to update the screen and change the index.
```



## Lecture Code

```dart
import 'package:flutter/material.dart';



void main() {
  runApp(const MaterialApp(home: MyApp()));
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  
  int selectedIndex = 0;

  static const TextStyle myStyle =
      TextStyle(fontSize: 36, fontWeight: FontWeight.bold);

  static List<Widget> _widgetOptions = [
    Text('Index 0: People', style: myStyle),
    Text('Index 1: Weekend', style: myStyle),
    Text('Index 2: Message', style: myStyle),
    myWidget
  ];

  // 50 cities
  static List cities = [
    "New York","Los Angeles","Chicago","Miami","Dallas","Houston",
    "Philadelphia","Atlanta","Washington","Boston","Phoenix","Detroit",
    "San Francisco","Seattle","San Diego","Minneapolis","Tampa",
    "Brooklyn","Denver","Queens","Baltimore","Las Vegas","St. Louis",
    "Riverside","Portland","San Antonio","Sacramento","San Juan",
    "San Jose","Orlando","Cleveland","Pittsburgh","Manhattan","Austin",
    "Cincinnati","Indianapolis","Kansas City","Columbus","Charlotte",
    "Virginia Beach","Bronx","Milwaukee","Providence","Jacksonville",
    "Salt Lake City","Nashville","Raleigh","Memphis","Richmond","Louisville"
  ];
 
  // This is a custom widget to show that any widget can be placed 
  // in the body - via a list.
  // NOTE: This is Widget is defined as a variable.
  static Widget myWidget = Scrollbar(
      thickness: 10.0,
      thumbVisibility: true,
      radius: Radius.elliptical(5, 30),
      child: ListView.builder(
          primary: true,
          itemCount: 50,
          itemBuilder: (BuildContext context, int index) {
            return Container(
                height: 50,
                color: index.isEven ? Colors.black26 : Colors.grey[200],
                child: Padding(
                    padding: const EdgeInsets.all(10),
                    child: Text('City: ' + cities[index],
                        style: TextStyle(color: Colors.yellow))));
          }));

  void onItemTapped(int index) {
    setState(() {
      selectedIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: const Text("Bottom Nav")),
        body: Center(child: _widgetOptions.elementAt(selectedIndex)),
        bottomNavigationBar: BottomNavigationBar(
          items: const [
            BottomNavigationBarItem(
                icon: Icon(Icons.people),
                label: 'People',
                backgroundColor: Colors.red),
            BottomNavigationBarItem(
                icon: Icon(Icons.weekend),
                label: 'Weekend',
                backgroundColor: Colors.green),
            BottomNavigationBarItem(
                icon: Icon(Icons.message),
                label: 'Message',
                backgroundColor: Colors.indigo),
            BottomNavigationBarItem(
                icon: Icon(Icons.location_city),
                label: 'Cities',
                backgroundColor: Colors.teal),
          ],
          currentIndex: selectedIndex,
          selectedItemColor: Colors.amber[800],
          onTap: onItemTapped,
        ) //End Of Bottom Navigation
        );
  }
}

```

