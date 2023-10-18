# Reading A Text File

## Key Ideas

* Future builder

This example shows how to read a text file.  In order to do this, the future builder widget is used. 

In Flutter, the snapshot component of the FutureBuilder widget wraps your data with properties. It provides the state of your connection so that you can determine and update your view according to state changes.  The snapshot's ConnectionState property can have four possible values that you can query to determine the state of your future: 

- Waiting: The connection state field is in this state
- Done: The data and error fields of the snapshot change only in this state
- Pending: The snapshot can have information in any event, when the connection state is as yet waiting
- Loaded: Data has been loaded

The FutureBuilder widget is used to create widgets based on the latest snapshot of interaction with a Future. It is necessary for the Future to be obtained earlier either through a change of state or a change in dependencies. 
With FutureBuilder, you can: 

- Run asynchronous functions
- Update your UI based on the function's output
- Determine the current state of a future
- Choose what to show while the data is loading



## Dart File



```dart
import 'package:flutter/material.dart';

/*
NOTE: assets/weshallfight_short.txt
The this folder and file needs to be added
to the project folder.

The image folder and file needs to be updated
in the yaml file.

weshallfight_short.txt is a textfile.  Substitute it with a file of your own.

Below is the section of the yaml file you need to add / edit.
SPACING NEEDS TO BE EXACT!!!!!!

  # To add assets to your application, add an assets section, like this:
  assets:
    - assets/weshallfight_short.txt
 */

void main() {
  runApp(const MaterialApp(home: MyApp()));
}

class MyApp extends StatefulWidget {

  const MyApp({super.key});

  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> {

  // remember that FutureBuilder is a widget
  Widget getTextFile() {
    return FutureBuilder(
        future: DefaultAssetBundle.of(context)
            .loadString("assets/weshallfight_short.txt"),
        builder: (context, snapshot) {
          return Text(snapshot.data ?? '', softWrap: true);
        });
  }

  // remember that FutureBuilder is a widget
  Widget getRichTextFile() {
    return FutureBuilder(
        future: DefaultAssetBundle.of(context)
            .loadString("assets/weshallfight_short.txt"),
        builder: (context, snapshot) {
          //Richtext Example
          return RichText(
              text: TextSpan(
                  text: (snapshot.data ?? ''),
                  style: TextStyle(
                      color: Colors.indigo[800],
                      fontFamily: "Courier New",
                      fontWeight: FontWeight.bold,
                      fontSize: 18)));
        });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            title:
                const Text("Read Text File", style: TextStyle(fontSize: 36))),
        body: ListView(padding: const EdgeInsets.all(20.0), children: [
            const Text(
              "Winston Churchill Speech",
              style: TextStyle(fontWeight: FontWeight.bold,fontSize: 24),
            ),
            getTextFile(),
            const Divider(thickness: 10),
            getRichTextFile(),
            const Divider(thickness: 10)
        ]));
  }
}

```



## Text File



weshallfight_short.txt

```
The British Empire and the French Republic, linked together in their cause and in their need, will defend to the death their native soil, aiding each other like good comrades to the utmost of their strength. Even though large tracts of Europe and many old and famous States have fallen or may fall into the grip of the Gestapo and all the odious apparatus of Nazi rule, we shall not flag or fail. We shall go on to the end, we shall fight in France, we shall fight on the seas and oceans, we shall fight with growing confidence and growing strength in the air, we shall defend our Island, whatever the cost may be, we shall fight on the beaches, we shall fight on the landing grounds, we shall fight in the fields and in the streets, we shall fight in the hills; we shall never surrender, and even if, which I do not for a moment believe, this Island or a large part of it were subjugated and starving, then our Empire beyond the seas, armed and guarded by the British Fleet, would carry on the struggle, until, in God’s good time, the New World, with all its power and might, steps forth to the rescue and the liberation of the old.
```



## Pubsec Yaml

```yaml
name: flutter_read_text_rev_b
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
# In iOS, build-name is used as CFBundleShortVersionString while build-number is used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
# In Windows, build-name is used as the major, minor, and patch parts
# of the product and file versions while build-number is used as the build suffix.
version: 1.0.0+1

environment:
  sdk: '>=3.0.5 <4.0.0'

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
  flutter_lints: ^2.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter packages.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  assets:
  #   - images/a_dot_burr.jpeg
  #   - images/a_dot_ham.jpeg
    - assets/weshallfight_short.txt

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/assets-and-images/#resolution-aware

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

