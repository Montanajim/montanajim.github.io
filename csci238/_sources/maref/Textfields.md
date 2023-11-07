# Textfields



```dart
import 'package:flutter/material.dart';
/*
  A Textfield need two things.
  1. The textfield needs to be connected to a controller
  2. Values in the textfield can be read or edited in the 
     setState in a stateful widget.
*/


void main() {
  runApp(const MaterialApp(home: MyApp()));
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);
  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> {

  // these controllers need to be connected to the textfields
  TextEditingController tc1 = TextEditingController();
  TextEditingController tc2 = TextEditingController();

  // global variable to hold the concatenated string
  String textValue = "";

  // listener function
  void onPressed() {
      
    // NOTE - setState is the function that allow you to change
    // the 
    setState(() {
      textValue = "${tc1.text} ${tc2.text}";
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text("Text Box Example"),
        ),
        body: ListView(padding: const EdgeInsets.all(10), children: [
          Column(children: [

            Row(mainAxisAlignment: MainAxisAlignment.spaceAround, children: [
              const Text("Box 1"),
              SizedBox(
                  width: 60,
                  height: 20,
                  child: TextField(
                    controller: tc1,
                    keyboardType: TextInputType.text,
                  ))
            ]),


            Row(mainAxisAlignment: MainAxisAlignment.spaceAround, children: [
              const Text("Box 2"),
              SizedBox(
                  width: 60,
                  height: 20,
                  child: TextField(
                    controller: tc2,
                  ))
            ]),

            Text(textValue),

            ElevatedButton(onPressed: onPressed, child: const Text("Enter"))
          ])
        ]));
  }
}

```

