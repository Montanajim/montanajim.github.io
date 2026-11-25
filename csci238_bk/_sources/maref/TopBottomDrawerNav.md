# Top Bottom Drawer Navigation 



This example incorporates three navigation methods: Top Tabs, Bottoms Tabs, and Side Drawer.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
      home: const MyApp(),
      debugShowCheckedModeBanner: false,
      routes: <String, WidgetBuilder>{
        "/HomePage": (BuildContext context) => const MyApp()
      }));
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  MyAppState createState() => MyAppState();
}

class MyAppState extends State<MyApp> with SingleTickerProviderStateMixin {
  late TabController _tabController;
  late int _selectedIndex = 0;

  String montanaCities = """
Here are 5 cities Montana:

1.  Helena
2.  Kalispell
3.  Whitefish
4.  Missoula
5.  Bozeman
  """;

  String coloradoCities = """
Here are 5 cities Colorado:

1.  Denver
2.  Boulder
3.  Pueblo
4.  Aspen
5.  Telluride
  """;

  String wyomingCities = """
Here are 5 cities Wyoming:

1.  Cheynne
2.  Casper
3.  Laramie
4.  Gillette
5.  Rock Springs
  """;

  List<Tab> topTabs = <Tab>[
    const Tab(text: "Montana"),
    const Tab(text: "Colorado"),
    const Tab(text: "Wyoming")
  ];

  Widget myTab1() {
    return ListView(
      padding: const EdgeInsets.all(10),
      children: [Text(montanaCities)],
    );
  }

  Widget myTab2() {
    return ListView(
      padding: const EdgeInsets.all(10),
      children: [Text(coloradoCities)],
    );
  }

  Widget myTab3() {
    return ListView(
      padding: const EdgeInsets.all(10),
      children: [Text(wyomingCities)],
    );
  }

  List<Widget> myContentWidgets(BuildContext content) {
    return <Widget>[myTab1(), myTab2(), myTab3()];
  }

  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: topTabs.length, vsync: this);
  }

  @override
  void dispose() {
    _tabController.dispose();
    super.dispose();
  }

  void _onBottomTap(int index) {
    setState(() {
      _selectedIndex = index;
      _tabController.index = index;
    });
  }

  Drawer myDrawer(BuildContext context) {
    return Drawer(
      child: ListView(
        padding: const EdgeInsets.fromLTRB(5, 45, 5, 5),
        children: [
          const SizedBox(
              height: 100,
              child: DrawerHeader(
                  decoration: BoxDecoration(
                    color: Colors.blue,
                  ),
                  child: Text("States"))),
          ListTile(
            title: const Text("Montana"),
            onTap: () {
              _onBottomTap(0);
            },
          ),
          ListTile(
            title: const Text("Colorado"),
            onTap: () {
              _onBottomTap(1);
            },
          ),
          ListTile(
            title: const Text("Wyoming"),
            onTap: () {
              _onBottomTap(2);
            },
          ),
        ],
      ),
    );
  }

  BottomNavigationBar theBottomNavBar() {
    return BottomNavigationBar(
      showSelectedLabels: true,
      showUnselectedLabels: true,
      items: const <BottomNavigationBarItem>[
        BottomNavigationBarItem(icon: Icon(Icons.android), label: 'Montana'),
        BottomNavigationBarItem(icon: Icon(Icons.android), label: 'Colorado'),
        BottomNavigationBarItem(icon: Icon(Icons.android), label: 'Wyoming'),
      ],
      currentIndex: _selectedIndex,
      onTap: _onBottomTap,
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Top Drawer Bottom Nav"),
        bottom: TabBar(
          controller: _tabController,
          tabs: topTabs,
          indicatorColor: Colors.amber[800],
          onTap: _onBottomTap,
        ),
      ),
      drawer: myDrawer(context),
      body: TabBarView(
          controller: _tabController, children: [myTab1(), myTab2(), myTab3()]),
      bottomNavigationBar: theBottomNavBar(),
    );
  }
}

```

