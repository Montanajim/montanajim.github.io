# Stateless Routes

## Key Ideas

* Key Widgets
  * Material App
  * Scaffold
  * Icon Button



## Routes

> Routes are an attribute in the Material App Widget.  They allow for the creation of multiple "pages" in a Flutter App.



## Lecture Code

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
      home: HomePage(),
      debugShowCheckedModeBanner: false,
      routes: <String, WidgetBuilder>{
        "/HomePage": (BuildContext context) => HomePage(),
        "/SecondPage": (BuildContext context) => SecondPage(),
        "/ThirdPage": (BuildContext context) => ThirdPage(),
        "/FourthPage": (BuildContext context) => FourthPage()
      }));
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            title: const Text("HomePage"), 
            backgroundColor: Colors.deepOrange),
        body: ListView(children: [
          Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Container(
                    padding: const EdgeInsets.all(40.0),
                    color: Colors.tealAccent,
                    alignment: Alignment.center,
                    child: const Text(
                        "This is \nmy travel app.\nIsn't it great",
                        style: TextStyle(fontSize: 36.0))),

                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                Row(mainAxisAlignment: MainAxisAlignment.center, children: [
                  IconButton(
                      icon: const Icon(Icons.airplanemode_active,
                          color: Colors.red),
                      padding: EdgeInsets.zero,
                      iconSize: 70.0,
                      onPressed: () {
                        Navigator.of(context).pushNamed("/SecondPage");
                      }),
                  IconButton(
                      icon: const Icon(Icons.train, color: Colors.blueAccent),
                      padding: EdgeInsets.zero,
                      iconSize: 70.0,
                      onPressed: () {
                        Navigator.of(context).pushNamed("/ThirdPage");
                      }),
                  IconButton(
                      icon: const Icon(Icons.directions_car_outlined,
                          color: Colors.green),
                      padding: EdgeInsets.zero,
                      iconSize: 70.0,
                      onPressed: () {
                        Navigator.of(context).pushNamed("/FourthPage");
                      }),
                ]),
                const Text("Home Page")
              ])
        ]));
  }
}

class SecondPage extends StatelessWidget {
  const SecondPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            title: const Text("Second Page"),
            backgroundColor: Colors.deepOrange),
        body: ListView(children: [
          Container(
              padding: const EdgeInsets.all(40.0),
              alignment: Alignment.center,
              child: const Text("This is the plane",
                  style: TextStyle(fontSize: 36))),
          Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                IconButton(
                    icon: const Icon(Icons.home, color: Colors.blue),
                    padding: EdgeInsets.zero,
                    iconSize: 70.0,
                    onPressed: () {
                      Navigator.of(context).pushNamed("/HomePage");
                    }),
              ])
        ]));
  }
}

class ThirdPage extends StatelessWidget {
  const ThirdPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            title: const Text("Third Page"),
            backgroundColor: Colors.deepOrange),
        body: ListView(children: [
          Container(
              padding: const EdgeInsets.all(40.0),
              color: Colors.tealAccent,
              alignment: Alignment.center,
              child: const Text("This is the train",
                  style: TextStyle(fontSize: 36))),
          Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                IconButton(
                    icon: const Icon(Icons.home, color: Colors.blue),
                    padding: EdgeInsets.zero,
                    iconSize: 70.0,
                    onPressed: () {
                      Navigator.of(context).pushNamed("/HomePage");
                    }),
              ])
        ]));
  }
}

class FourthPage extends StatelessWidget {
  const FourthPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            title: const Text("Fourth Page"),
            backgroundColor: Colors.deepOrange),
        body: ListView(children: [
          Container(
              padding: const EdgeInsets.all(40.0),
              color: Colors.tealAccent,
              alignment: Alignment.center,
              child: const Text("This is the automobile",
                  style: TextStyle(fontSize: 36))),
          Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                const Text(
                  "Content Here",
                  style: TextStyle(fontSize: 36, fontWeight: FontWeight.bold),
                ),
                IconButton(
                    icon: const Icon(Icons.home, color: Colors.blue),
                    padding: EdgeInsets.zero,
                    iconSize: 70.0,
                    onPressed: () {
                      Navigator.of(context).pushNamed("/HomePage");
                    }),
              ])
        ]));
  }
}

```

## Screenshots

![image-20221012121755164](maimages/stateless1.png)

![image-20221012121902941](maimages/stateless2.png)

![image-20221012122018939](maimages/stateless3.png)

![image-20221012122135516](maimages/Stateless4.png)