# TextFields



TextFields are essential UI components in Flutter that allow users to input and edit text. They are highly customizable and can be used for various purposes, such as:

- **Form input:** Collecting user information like names, emails, and addresses.

- **Search bars:** Enabling users to search for content within an app.

- **Chat messages:** Allowing users to send and receive text messages.

- **Note-taking:** Providing a space for users to write and edit notes.

  

**Key Properties of TextFields:**

- **`controller`:** Manages the text within the TextField.

- **`decoration`:** Customizes the appearance of the TextField, including the border, hint text, and error messages.

- **`onChanged`:** A callback function that is called whenever the text in the TextField changes.

- **`keyboardType`:** Specifies the type of keyboard that should be displayed (e.g., `TextInputType.number`, `TextInputType.emailAddress`).

- **`obscureText`:** Hides the text input (e.g., for passwords).

- **`maxLines`:** Sets the maximum number of lines allowed in the TextField.

- **`maxLength`:** Limits the maximum number of characters that can be entered.

  

```dart
import 'package:flutter/material.dart';
/*
  A Textfield need two things.
  1. The textfield needs to be connected to a TextEditingController
  2. Values in the textfield can only be read or edited in the 
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
    // the values of variables
    setState(() {
      textValue = "${tc1.text} ${tc2.text}";
    });
  }

   @override
  Widget build(BuildContext context) {
    
    // varibles for the SizedBox  
    double theBoxWidth = 120;
    double theBoxHeigth = 40;

    return Scaffold(
        appBar: AppBar(title: const Text("Text Box Example")),
        body: ListView(padding: const EdgeInsets.all(10.0), children: [
          Column(children: [
              
            Row(mainAxisAlignment: MainAxisAlignment.spaceAround, children: [
              const Text("Box 1"),
              SizedBox(
                  width: theBoxWidth,
                  height: theBoxHeigth,
                  child: TextField(
                      controller: tc1, keyboardType: TextInputType.text))
            ]),
              
            Row(mainAxisAlignment: MainAxisAlignment.spaceAround, children: [
              const Text("Box 2"),
              SizedBox(
                  width: theBoxWidth,
                  height: theBoxHeigth,
                  child: TextField(
                      controller: tc2, keyboardType: TextInputType.text))
            ]),
              
            Text(textValue),
              
            ElevatedButton(onPressed: onPressed, child: const Text("Click Me"))
          ])
        ]));
  }
}

```

**Customization:**

You can customize TextFields extensively using the `InputDecoration` class. Here are some common customizations:

- **Border:** Change the border style, color, and width.
- **Hint text:** Set the hint text that appears when the TextField is empty.
- **Label text:** Add a label text that floats above the TextField when it is focused.
- **Error text:** Display error messages below the TextField.
- **Prefix/suffix icons:** Add icons before or after the text input.
- **Counter text:** Show the current character count.

**Additional Tips:**

- For more complex text input scenarios, consider using packages like `flutter_masked_text` or `intl` for formatting and validation.
- Ensure accessibility by providing appropriate labels and hints for screen readers.
- Validate user input to prevent errors and ensure data quality.
