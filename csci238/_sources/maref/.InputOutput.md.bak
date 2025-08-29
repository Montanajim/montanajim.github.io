# Input Output



## Null Safety

- The Dart language comes with sound null safety.

- Null safety prevents errors that result from unintentional access of variables set to `null`. For example, if a method expects an integer but receives `null`, your app causes a runtime error. This type of error, a null dereference error, can be difficult to debug.

- With sound null safety variables are ‘non-nullable’ by default: They can be assigned only values of the declared type (e.g. `int i=42`), and never be assigned `null`. You can specify that a type of a variable is nullable (e.g. `int? i`), and only then can they contain either a `null` *or* a value of the defined type.

- Sound null safety changes potential **runtime errors** into **edit-time** analysis errors, by flagging when any non-nullable variable hasn’t been initialized with a non-null value or is being assigned a `null`. This allows you to fix these errors before deploying your app.

  https://dart.dev/null-safety



```{Warning}
 In Dart 2.x SDKs, you can enable or disable sound null safety through configuration of the project SDK constraint. To learn more, see Enabling/disabling null safety.

Dart 3–planned for a mid-2023 release– will require sound null safety. It will prevent code from running without it. All existing code must be migrated to sound null safety to be compatible with Dart 3. To learn more, see the Dart 3 sound null safety tracking issue.
```



## Code

If a variable or object can be null, then it must have the "__?__" operator by the data type.  Note that the Null Check "**!** " is attached to the end of the variable.



## Lecture Code



``` Dart
import 'dart:io';

// MUST BE RAN IN THE ACTUAL TERMINAL - POWERSHELL OR CMD
// Null Safety
// https://www.tutorialkart.com/dart/null-safety


void inputExample() {
  String? myName;
  double myNum = 0.0;
  var myDog;

  stdout.write('Please enter your name: ');
  myName = stdin.readLineSync();

  stdout.writeln("Your name is " + myName!);

  try {
    stdout.write('Please a number: ');
    myNum = double.parse(stdin.readLineSync()!);

    stdout.writeln("Your number is " + myNum.toString()!);

  } catch (e) {
    stdout.writeln("No number was entered");
  }

  stdout.write('Please enter your dog: ');
  myDog = stdin.readLineSync();
  stdout.writeln("Your dog is " + myDog);

}

main(List<String> arguments) {
  inputExample();
}

```

