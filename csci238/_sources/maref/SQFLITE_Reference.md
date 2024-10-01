# SQFLITE

**Purpose:** The code demonstrates how to create and interact with a local SQLite database in a Flutter application. It covers basic operations like creating a table, inserting data, querying data, and deleting data.

**Key Components:**

1. **Database Setup:**
   - `getDatabasesPath()` retrieves the path to the device's database directory.
   - `join()` combines the path and database name to create the full path.
   - `openDatabase()` opens or creates the database.
   - `onCreate` callback is used to create the table and insert initial data.
1. **Data Manipulation:**
   - `rawInsert()` is used to insert data into the table.
   - `rawQuery()` is used to execute custom SQL queries.
   - `myGetData()` retrieves all data from the `tblcar` table.
   - `myGetMakesX()` retrieves data where the `Model` starts with 'X'.
   - `myDeleteModel()` deletes data based on the `Make` field.
1. **Data Display:**
   - The code iterates through the retrieved data and prints it to the console.

## Reference Code

```dart
import 'package:flutter/material.dart';
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';
import 'dart:io';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  static String dbName = "xCar.db";
  static var db;
  var path;

  // constructor
  _MyHomePageState() {
    myDatabaseSetup();
  }

  myDatabaseSetup() async {
    var databasesPath = await getDatabasesPath();
    path = join(databasesPath, dbName);

    // check if DB exists
    if(await File(path).exists())
    {
      print("DB exists");
    }

    String xsqlstmt = """
    INSERT INTO tblcar(id,Make,Model) VALUES
           (1,'Ford','F150'),
            (2,'Chevy','Tahoe'),
            (3,'Volkswagen','Bug'),
            (33, 'Ford','Mustang'),
            (4,'Scion','XB'),
            (5,'Scion','XC'),
            (6,'Scion','XA');
    """;

    // delete the previous database
    deleteDatabase(path);

    // open / create database
    db = await openDatabase(
        path,
        version: 1,
        onCreate: (db, version) async {
          await myCreateTable(db);
          await db.rawInsert(xsqlstmt);
          await db.rawInsert(
              "INSERT INTO tblcar(id,Make,Model) VALUES" + "(200,'Chevy','Tahoe')");
        });

    await myInsertStartRecords();

    // when you do a select query in sqflite
    // it will return a List of Map data
    // Think of it as each row of data is
    // a position in the list. And each record is a Map (key, value)
    List<Map<String, dynamic>> myDataSet;

    // call a function to query the data
    myDataSet = await myGetData();

    // print on piece of data
    // third record Model
    print(myDataSet[2]['Model']);

    // iterate through the data
    for (int c = 0; c < myDataSet.length; c++) {
      print(myDataSet[c]['Model'] + " " + myDataSet[c]['Make']);
    }
    myDataSet = await myGetMakesX();
    print(myDataSet);

    print("\n---------------------\n");

    String fd = "Scion";
    await myDeleteModel(fd);
    myDataSet = await myGetData();
    for (int c = 0; c < myDataSet.length; c++) {
      print(myDataSet[c]['Model'] + " " + myDataSet[c]['Make']);
    }


  }

  // function to query data from the database
  Future myGetData() async {
    var data = db.rawQuery('SELECT * From tblcar Order By Make, Model');
    return data;
  }

  Future myGetMakesX() async{
    var data = db.rawQuery("""SELECT * 
                              FROM tblcar 
                              WHERE Model LIKE 'X%';
                              """);
    return data;
  }

  Future myDeleteModel(String ModelData) async{
    var data = db.rawQuery( "DELETE FROM tblcar " +
        "WHERE Make LIKE '" + ModelData  + "'");
    return data;
  }


  // create a table in sqflite
  myCreateTable(Database db) async {
    await db.execute('''
       CREATE TABLE tblCar (id INTEGER, 
       Make   TEXT,
       Model  TEXT)
      ''');
  }

  Future myInsertStartRecords() async {

    String xsqlstmt = """
      INSERT INTO tblcar(id,Make,Model) VALUES
              (10000,'Ford','F150'),
              (20000,'Chevy','Tahoe'),
              (30000,'Volkswagen','Bug'),
              (40000,'Scion','XB'),
              (50000,'Scion','XC'),
              (60000,'Ford','Focus');
      """;

    await db.rawInsert(xsqlstmt);

  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        ),
        body: ListView(
          children: const [
            Text("This is a test"),
          ],
        ) // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}

/*
pubpsec.yaml
dependencies:
  flutter:
    sdk: flutter
  sqflite: ^2.3.0
  path: ^1.8.3

 */
```

