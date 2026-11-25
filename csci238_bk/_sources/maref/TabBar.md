# Tab Bar

The *tab bar* is part of the *app bar* widget. 

```{admonition} Note
The **tab controller** controls the **TabBarView** widget.  When a different tab is selected, the controller changes the scaffold view in the body to the corresponding tab content.
```



The **TabBar** widget has some animation to it.  All animations can be timed to a clock. In order for the animation to run smoothly the interface *with SingleTickerProviderStateMixin* is applied to the '\_MyAppState' class.  This interface allows the animation to synch with the cpu clock to provide smooth animation, which is used in the tab bar controller.



## Lecture Code

```dart
import 'package:flutter/material.dart';
//flutter_tabbar_rev2
//Rev Date 20211031

void main() {
  runApp(const MaterialApp(home: MyApp()));
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> with SingleTickerProviderStateMixin {

  // ------- Global Variables ------------------------------------ 
    
  late TabController _tabController;

  String quote1 = "Well, ain't this place a geographical oddity. "
      "Two weeks from everywhere!";

  String quote2 = "The ebb and flow of the Atlantic tides, "
      "the drift of the continents, "
      "the very position of the sun along its ecliptic. "
      "THESE are just a FEW of the things "
      "I control in my world! Is that clear?";

  String quote3 = " It's a hundred and six miles to Chicago, "
      "we've got a full tank of gas, "
      "half a pack of cigarettes, "
      "it's dark, and we're wearing sunglasses.";

  final List<Tab> mytabs = <Tab>[
    const Tab(text: "Oh Brother"),
    const Tab(text: "GI Jane"),
    const Tab(text: "Blues Brothers")
  ];

  TextStyle myQuoteStyle = const TextStyle( fontSize: 36,
                                      fontFamily: 'PermanentMarker',
                                      );
    
  // ------------- End of Global Variables--------------
    
  // Set up tab controller  
  @override
  void initState() {
    super.initState();
    _tabController = TabController(vsync: this, length: mytabs.length);
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }
// ----------- end of tab controller-------------------
 
// ----------- setup tabs -----------------------------    
    
    
  myTab1() {
    return ListView(
      padding: const EdgeInsets.all(20.0),
      children: [
        Text(
          quote1,
          style: myQuoteStyle,
        )
      ],
    );
  }

  myTab2() {
    return ListView(
      padding: const EdgeInsets.all(20.0),
      children: [
        Text(
          quote2,
          style: myQuoteStyle,
        )
      ],
    );
  }

  myTab3() {
    return ListView(
      padding: const EdgeInsets.all(20.0),
      children: [
        Text(
          quote3,
          style: myQuoteStyle,
        )
      ],
    );
  }

// --------------------------------------------------
    
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text("Tabs"),
          bottom: TabBar(
            controller: _tabController,
            indicatorColor: Colors.amber,
            tabs: mytabs,
          ),
        ),
        body: TabBarView(
          controller: _tabController,
          children: [myTab1(), myTab2(), myTab3()],
        ));
  }
}
```



###  pubpec.yaml 



The extraneous comments have been deleted.  Note how the fonts have been changed.  The *PermanentMarker* font has been imported and the '.tff' file has been saved in a folder called **fonts** which is in the folder **assets**. 



```yaml
name: tabbar_demo
description: A new Flutter project.

publish_to: 'none' 

version: 1.0.0+1

environment:
  sdk: '>=2.18.2 <3.0.0'

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter

  flutter_lints: ^2.0.0

flutter:

  uses-material-design: true

  # To add assets to your application, add an assets section, like this:
  # assets:
  #   - images/a_dot_burr.jpeg
  #   - images/a_dot_ham.jpeg


  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  fonts:
    - family: PermanentMarker
      fonts:
        - asset: Assets/Fonts/PermanentMarker-Regular.ttf


```



![Tab Bar ](maimages/tabbar.png)