# Car App Version 2



```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'dart:async';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "Flutter Cars",
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.red,
      ),
      home: const MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key});

  @override
  MyHomePageState createState() => MyHomePageState();
}

class MyHomePageState extends State<MyHomePage> {
  List<dynamic> data = [];
  String statusUpdate = "Getting Data - Please Wait";

  // Fetch data from the API
  Future<void> getData() async {
    try {
      Uri url = Uri.parse("https://flutter.locusnoesis.com/carinfo.php");
      http.Response response = await http.post(url);

      if (response.statusCode == 200) {
        setState(() {
          data = jsonDecode(response.body);
          statusUpdate = "Data Loaded Successfully";
        });
      } else {
        setState(() {
          statusUpdate = "Failed to load data. Status: ${response.statusCode}";
        });
      }
    } catch (e) {
      setState(() {
        statusUpdate = "Error: $e";
      });
    }
  }

  @override
  void initState() {
    super.initState();
    getData();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text("Flutter Cars"), centerTitle: true),
      body: Column(
        children: [
          Container(
            alignment: Alignment.centerLeft,
            padding: const EdgeInsets.all(20),
            child: Text(
              "Cars for Sale",
              style: TextStyle(
                color: Colors.indigo[800],
                fontWeight: FontWeight.bold,
                fontSize: 18.0,
              ),
              textAlign: TextAlign.left,
            ),
          ),
          Expanded(
            child: data.isEmpty
                ? Center(child: Text(statusUpdate))
                : ListView.builder(
              itemCount: data.length,
              itemBuilder: (BuildContext context, int index) {
                return Card(
                  child: ListTile(
                    title: Text(
                      "${data[index]['year']} ${data[index]['make']}",
                    ),
                    subtitle: Text(
                      "${data[index]['model']} ${data[index]['body_styles']}",
                    ),
                  ),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}

/*
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'dart:async';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: "Flutter Cars",
        debugShowCheckedModeBanner: false,
        theme: ThemeData(
          primarySwatch: Colors.red,
        ),
        home: const MyHomePage());
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key});

  @override
  MyHomePageState createState() => MyHomePageState();
}

class MyHomePageState extends State<MyHomePage> {
  static dynamic data;
  static String statusUpdate = "Getting Data - Please Wait";


  // run on start

  static Future getData() async {
    print("Made it here");
     Uri url = Uri.parse("flutter.locusnoesis.com/carinfo.php");
    // var url = Uri.https("www.google.com");
    http.Response response = await http.post(url);

    // final headers = {
    // 'Content-Type': 'application/json',
    // 'Access-Control-Allow-Origin': '*',
    // };
    //http.Response response = await http.post(url, headers: headers);
    //print('Response status: ${response.statusCode}');
    //statusUpdate = ('Response status: ${response.statusCode}');
    // print('Response body: ${response.body}');
    //statusUpdate('Response body: ${response.body}');

    data = await jsonDecode(response.body);

    return data;
  }

  Widget myWidget = FutureBuilder(
      future: getData(),
      builder: (BuildContext context, AsyncSnapshot snapshot) {

        print(snapshot.data);

        if (snapshot.hasData) {
          return ListView.builder(
              itemCount: data.length,
              itemBuilder: (BuildContext context, int index) {
                return Card(
                    child: Column(
                        mainAxisAlignment: MainAxisAlignment.center,
                        mainAxisSize: MainAxisSize.min,
                        children: [
                      ListTile(
                          title: Text(
                              "${data[index]['year']} ${data[index]['make']}"),
                          subtitle: Text(
                    "${data[index]['model']} ${data[index]['body_styles']}"))
                    ]));
              });
        } // end of if

       // return  Text();
      });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: const Text("Flutter Cars"), centerTitle: true),
        body: Column(children: [
          Container(
              alignment: Alignment.centerLeft,
              padding: const EdgeInsets.all(20),
              child: Text("Cars for Sale",
                  style: TextStyle(
                      color: Colors.indigo[800],
                      fontWeight: FontWeight.bold,
                      fontSize: 18.0),
                  textAlign: TextAlign.left)),
          Expanded(child: myWidget)
        ]));
  }
}
*/
```

