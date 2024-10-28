# Datepicker and Timepicker



This Flutter code creates an app that allows users to select and display dates and times using pickers. Here's a brief overview:

1. **Main Function**: It initializes and runs the Flutter app, setting `MyHomePage` as the home widget.

2. **MyHomePage Widget**: 
   - This is a stateful widget that manages the state of the home page, which contains the UI and functionality for selecting dates and times.
   - The state class, `_MyHomePageState`, contains variables to store selected date and time values, which are displayed as text.

3. **Date and Time Selection**: 
   - Three buttons (`getDate()`, `getDate2()`, and `getTime()`) trigger date or time pickers.
   - `theDate()`: Opens a basic date picker dialog.
   - `theDate2()`: Opens a date picker with an input mode.
   - `theTime()`: Opens a time picker with an input mode.
   - The selected values update the display through the `setState()` method, ensuring the UI reflects changes.

4. **UI Layout**: 
   - The layout consists of a vertical list that includes buttons to select dates and times and text widgets to display the selected values. 
   - The app's interface uses a simple `Scaffold` with an app bar, buttons, and text fields within a `ListView`.

This app demonstrates basic state management, UI layout, and date/time picker integration in Flutter.



## The code



```dart
import 'package:flutter/material.dart';

// Main function to run the app
void main() {
  runApp(const MaterialApp(home: MyHomePage()));
}

// Stateful widget to manage the home page
class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key});

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

// State class for MyHomePage
class _MyHomePageState extends State<MyHomePage> {
  // Static variables to hold the current date and time
  static DateTime _date = DateTime.now();
  static TimeOfDay _time = TimeOfDay.now();

  // Strings to display the selected date and time in different formats
  String myDate1 = "";
  String myDate2 = "";
  String myTime1 = "";

  // Widget to display the 'Select Date' button for the first date picker
  Widget getDate() {
    return ElevatedButton(
        style: ElevatedButton.styleFrom(
            shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(10))),
        onPressed: () {
          setState(() {
            theDate(); // Calls the function to select the date
          });
        },
        child: const Text("Select Date"));
  }

  // Function to show the first date picker dialog
  theDate() async {
    _date = (await showDatePicker(
        context: context,
        initialDate: DateTime.now(),
        firstDate: DateTime(2000, 1, 1),
        lastDate: DateTime(3000, 1, 1)))!;

    // Updates the displayed date in 'myDate1' after selection
    setState(() {
      if (_date.toString() != "") {
        myDate1 = "${_date.month} / ${_date.day} / ${_date.year}";
      } else {
        myDate1 = "";
      }
    });
  }

  // -----------------------------------------------------------------------

  // Widget to display the 'Select Date' button for the second date picker
  Widget getDate2() {
    return ElevatedButton(
        style: ElevatedButton.styleFrom(
            shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(10))),
        onPressed: () {
          setState(() {
            theDate2(); // Calls the function to select the date
          });
        },
        child: const Text("Select Date"));
  }

  // Function to show the second date picker dialog (with input mode)
  theDate2() async {
    _date = (await showDatePicker(
        context: context,
        initialDate: DateTime.now(),
        firstDate: DateTime(2000, 1, 1),
        lastDate: DateTime(3000, 1, 1),
        initialEntryMode: DatePickerEntryMode.input))!;

    // Updates the displayed date in 'myDate2' after selection
    setState(() {
      if (_date.toString() != "") {
        myDate2 = "${_date.month} / ${_date.day} / ${_date.year}";
      } else {
        myDate2 = "";
      }
    });
  }

  // Function to show the time picker dialog
  theTime() async {
    _time = (await showTimePicker(
      context: context,
      initialTime: TimeOfDay.now(),
      initialEntryMode: TimePickerEntryMode.input,
    ))!;

    // Updates the displayed time in 'myTime1' after selection
    setState(() {
      if (_date.toString() != "") {
        myTime1 = "${_time.hourOfPeriod} : ${(_time.minute < 10) ? "0${_time.minute}" : _time.minute.toString()}${_time.period.toString() == "DayPeriod.pm" ? " pm" : " am"}";
      } else {
        myTime1 = "";
      }
    });
  }

  // ---------------------------------------------------------------

  // Widget to display the 'Select Time' button
  Widget getTime() {
    return ElevatedButton(
        style: ElevatedButton.styleFrom(
            shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(10))),
        onPressed: () {
          setState(() {
            theTime(); // Calls the function to select the time
          });
        },
        child: const Text("Select Time"));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: const Text("Date Pickers")),
        body: ListView(
            padding: const EdgeInsets.all(20.0),
            children: [
              Column(
                  children: [
                    // Title text for the page
                    const Text('Time / Date Picker',
                        style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold)),
                    
                    // First date picker button and display
                    getDate(),
                    Text(myDate1),

                    // Second date picker button and display
                    getDate2(),
                    Text(myDate2),

                    // Time picker button and display
                    getTime(),
                    Text(myTime1),

                    // Display the raw date and time values
                    Text(_time.toString()),
                    Text(_date.toString())
                  ])
            ]));
  }
}

```

