Temp file



```
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';
import 'dart:io';

class SQLDB{

  String dbName;
  static var db;
  var path;

  SQLDB(this.dbName){

    setupDB()

  }

  setupDB() async{

    // check if DB exists
    if(await File(path).exists())
    {
      return;
    }

    db = await openDatabase(
        path,
        version: 1,
        onCreate: await (db) async {
          myCreateTable(db);
        }
    );

  }

  // create a table in sqflite
  myCreateTable(Database db) async {
    await db.execute('''
       CREATE TABLE tblCar (
       id       INTEGER, 
       Make     TEXT,
       Model    TEXT,
       Caryear  TEXT,
       Carcolor TEXT)
      ''');
  }

}
```

