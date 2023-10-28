# Drawer Navigation



```dart
//drawer Example rev 3 - fall 23
import 'package:flutter/material.dart';

//NOTE: Drawer content can be separated out and then used
// in multiple "pages/routes" - See Page1 and Page2
Drawer myDrawer(BuildContext context) {
  return Drawer(
      child: ListView(padding: EdgeInsets.zero, children: [
    DrawerHeader(
        decoration: BoxDecoration(
          image: const DecorationImage(
            image: AssetImage("images/fvcc111.jpg"),
            fit: BoxFit.cover,
          ),
          borderRadius: BorderRadius.circular(40),
          color: Colors.yellow[800],
        ),
        child: const Text("Drawer Title")),
    ListTile(
      title: const Text("Home Page"),
      onTap: () {
        Navigator.of(context).pushNamed("/HomePage");
      },
    ),
    ListTile(
      title: const Text("Page 1"),
      onTap: () {
        Navigator.of(context).pushNamed("/Page1");
      },
    ),
    ListTile(
      title: const Text("Page 2"),
      onTap: () {
        Navigator.of(context).pushNamed("/Page2");
      },
    )
  ]));
}

void main() {
  runApp(MaterialApp(
      home: const MyApp(),
      debugShowCheckedModeBanner: false,
      routes: <String, WidgetBuilder>{
        "/HomePage": (BuildContext context) => const MyApp(),
        "/Page1": (BuildContext context) => const Page1(),
        "/Page2": (BuildContext context) => const Page2()
      }));
}

class MyApp extends StatefulWidget {
  // constructor
  const MyApp({Key? key}) : super(key: key);

  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Drawer Example")),
      backgroundColor: Colors.white,
      drawer: Drawer(
          child: ListView(padding: EdgeInsets.zero, children: [
        DrawerHeader(
            decoration: BoxDecoration(
              image: const DecorationImage(
                image: AssetImage("images/fvcc111.jpg"),
                fit: BoxFit.cover,
              ),
              borderRadius: BorderRadius.circular(40),
              color: Colors.yellow[800],
            ),
            child: const Text("Drawer Title")),
        ListTile(
          title: const Text("Home Page"),
          onTap: () {
            Navigator.of(context).pushNamed("/HomePage");
          },
        ),
        ListTile(
          title: const Text("Page 1"),
          onTap: () {
            Navigator.of(context).pushNamed("/Page1");
          },
        ),
        ListTile(
          title: const Text("Page 2"),
          onTap: () {
            Navigator.of(context).pushNamed("/Page2");
          },
        )
      ])),
      body: ListView(
        padding: const EdgeInsets.all(20),
        children: const [Text("Home Page\nThis is the homepage")],
      ),
    );
  } // End of Widget Build
} // end of class

class Page1 extends StatefulWidget {
  // constructor
  const Page1({Key? key}) : super(key: key);

  @override
  Page1State createState() => Page1State();
}

class Page1State extends State<Page1> {
  String myString = "Have a great day\n";
  String appendText = "Have a great day\n";

  @override
  Widget build(BuildContext context) {
    for (int c = 0; c < 25; c++) {
      myString = myString + appendText;
    }

    return Scaffold(
        appBar: AppBar(title: const Text("Page 1")),
        drawer: myDrawer(context),
        body: ListView(
            padding: const EdgeInsets.all(20),
            children: [const Text("Page 1 content"), Text(myString)]));
  }
}

class Page2 extends StatefulWidget {
  // constructor
  const Page2({Key? key}) : super(key: key);

  @override
  Page2State createState() => Page2State();
}

class Page2State extends State<Page2> {
  String myString = "Have a bad day\n";
  String appendText = "Have a bad day\n";

  @override
  Widget build(BuildContext context) {
    for (int c = 0; c < 25; c++) {
      myString = myString + appendText;
    }

    return Scaffold(
        appBar: AppBar(title: const Text("Page 2")),
        drawer: myDrawer(context),
        body: ListView(padding: const EdgeInsets.all(20), children: [
          const Text("Page 2 content"),
          Text(myString),
        ]));
  }
}

```

