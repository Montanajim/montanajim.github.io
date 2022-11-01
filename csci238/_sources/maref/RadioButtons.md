# Radio Buttons

## Key Ideas

* Key Widgets
  * radio



```{note}
The __groupValue__  is the value of the selected radio button and it binds all of the radio buttons that use it.
```



## Lecture Code

```dart
//radio buttons

import 'package:flutter/material.dart';

String larryPhoto = "images/larry.jpg";
String curlyPhoto = "images/curly.jpg";
String moePhoto = "images/moe.jpg";
String shempPhoto = "images/shemp.jpg";

void main() {
  runApp(const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: MyApp()));
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  int _groupValue2 = 0;
  int _groupValue3 = 0;

  String _groupValue1 = "Larry";

  String larry = "Larry";
  String curly = "Curly";
  String moe = "Moe";

  String selectStooge = "images/larry.jpg";
  String selectStooge2 = "images/larry.jpg";

  TextEditingController text1Controller = TextEditingController();

  Widget makeRadioButtons1() {
    return Row(children: [
      Column(children: [
        Row(children: [
          const Text("Larry", style: TextStyle(fontSize: 18),),
          Radio(
            value: larry,
            groupValue: _groupValue1,
            autofocus: true,
            onChanged: (value) {
              setState(
                () {
                  _groupValue1 = larry;
                  text1Controller.text = value.toString();
                  selectStooge = larryPhoto;
                },
              );
            },
          )
        ]),
        Row(children: [
          const Text("Curly",style: TextStyle(fontSize: 18),),
          Radio(
            value: curly,
            groupValue: _groupValue1,
            onChanged: (value) {
              setState(
                () {
                  _groupValue1 = curly;
                  text1Controller.text = value.toString();
                  selectStooge = curlyPhoto;
                },
              );
            },
          )
        ]),
        Row(children: [
          const Text("Moe",style: TextStyle(fontSize: 18),),
          Radio(
            value: moe,
            groupValue: _groupValue1,
            onChanged: (value) {
              setState(
                () {
                  _groupValue1 = moe;
                  text1Controller.text = value.toString();
                  selectStooge = moePhoto;
                },
              );
            },
          )
        ]),
      ]),
      Padding(
          padding: const EdgeInsets.all(10.0),
          child: Container(
              child: Image.asset(selectStooge, width: 100, fit: BoxFit.cover)))
    ]);
  }

//-------------------------------------------

  Widget makeRadioButtons2() {
    List<Widget> list = <Widget>[];

    var StoogeList = ["Larry", "Curly", "Moe", "Shemp"];

    for (int i = 0; i < StoogeList.length; i++) {
      list.add(
          SizedBox(
            width: 150,
            height: 50,
            child:
          Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              crossAxisAlignment: CrossAxisAlignment.center,
          children: [
        Text(StoogeList[i].toString(),style: TextStyle(fontSize: 18),),
        Radio(
          value: i,
          groupValue: _groupValue2,
          onChanged: (value) {
            setState(() {
              _groupValue2 = i;

              if (value == 0) {
                selectStooge2 = larryPhoto;
              } else if (value == 1) {
                selectStooge2 = curlyPhoto;
              } else if (value == 2) {
                selectStooge2 = moePhoto;
              } else if (value == 3) {
                selectStooge2 = shempPhoto;
              }

              text1Controller.text = value.toString();
            });
          },
        )
      ])));
    }

    Column mycolumn = Column(children: list);

    Row myrow = Row(children: [
      mycolumn,
      Padding(
          padding: const EdgeInsets.all(5.0),
          child: Container(
              child: Image.asset(selectStooge2, width: 150, fit: BoxFit.cover)))
    ]);

    return myrow;
  }

  //-------------------------------------------
  void _setTextField1(String value) {
    setState(() {
      text1Controller.text = value.toString();
    });
  }

  Widget makeTextBox() {
    return Container(
        padding: const EdgeInsets.all(20.0),
        alignment: Alignment.centerLeft,
        child: Column(crossAxisAlignment: CrossAxisAlignment.start, children: [
          const Text(
            "Item Selected",
            style: TextStyle(fontWeight: FontWeight.bold, fontSize: 18),
          ),
          TextField(controller: text1Controller, onChanged: _setTextField1)
        ]));
  }

  //--------------------------------------------
  Widget makeRadioTiles() {
    List aNames = ['Bob', 'Betty', 'Beau', 'Brian'];
    List jTitle = ['Doctor', 'Engineer', 'Barber', 'Coder'];

    List<Widget> list = <Widget>[];

    for (int i = 0; i < 4; i++) {
      list.add(RadioListTile(
          value: i,
          groupValue: _groupValue3,
          activeColor: Colors.green,
          controlAffinity: ListTileControlAffinity.trailing,
          title: Text('Name: ' + aNames[i]),
          subtitle: Text('Job Title: ' + jTitle[i]),
          onChanged: (value) {
            setState(() {
              _groupValue3 = i;
              text1Controller.text =
                  aNames[i].toString() + " - " + jTitle[i].toString();
            });
          }));
    }

    Column column = Column(children: list);

    return column;
  }

  // --------------------------------------------
  // Note how clean the widget build is programmed by
  // using widget function calls
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: const Text("Radio Buttons")),
        body:  ListView
          (padding: const EdgeInsets.all(20.0), children: [
          Column(children: [
            makeTextBox(),
            const Divider(height: 20, thickness: 5, color: Colors.black),
            makeRadioButtons1(),
            const Divider(height: 20, thickness: 5, color: Colors.black),
            makeRadioButtons2(),
            const Divider(height: 20, thickness: 5, color: Colors.black),
            makeRadioTiles(),
            const Divider(height: 20, thickness: 5, color: Colors.black),
          ])
        ]) //listview
        );
  }
}

```



##  Pubsec YAML

```yaml
name: radiobuttonsdemo
description: A new Flutter project.

# The following line prevents the package from being accidentally published to
# pub.dev using `flutter pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev

# The following defines the version and build number for your application.
# A version number is three numbers separated by dots, like 1.2.43
# followed by an optional build number separated by a +.
# Both the version and the builder number may be overridden in flutter
# build by specifying --build-name and --build-number, respectively.
# In Android, build-name is used as versionName while build-number used as versionCode.
# Read more about Android versioning at https://developer.android.com/studio/publish/versioning
# In iOS, build-name is used as CFBundleShortVersionString while build-number used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
version: 1.0.0+1

environment:
  sdk: ">=2.12.0 <3.0.0"

# Dependencies specify other packages that your package needs in order to work.
# To automatically upgrade your package dependencies to the latest versions
# consider running `flutter pub upgrade --major-versions`. Alternatively,
# dependencies can be manually updated by changing the version numbers below to
# the latest version available on pub.dev. To see which dependencies have newer
# versions available, run `flutter pub outdated`.
dependencies:
  flutter:
    sdk: flutter


  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter

  # The "flutter_lints" package below contains a set of recommended lints to
  # encourage good coding practices. The lint set provided by the package is
  # activated in the `analysis_options.yaml` file located at the root of your
  # package. See that file for information about deactivating specific lint
  # rules and activating additional ones.
  flutter_lints: ^1.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  assets:
  #   - images/a_dot_burr.jpeg
    - images/larry.jpg
    - images/curly.jpg
    - images/moe.jpg
    - images/shemp.jpg

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/assets-and-images/#resolution-aware.

  # For details regarding adding assets from package dependencies, see
  # https://flutter.dev/assets-and-images/#from-packages

  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  # fonts:
  #   - family: Schyler
  #     fonts:
  #       - asset: fonts/Schyler-Regular.ttf
  #       - asset: fonts/Schyler-Italic.ttf
  #         style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/custom-fonts/#from-packages

```



## App Image

![Radio Buttons App](./maimages/radiobuttons.png)