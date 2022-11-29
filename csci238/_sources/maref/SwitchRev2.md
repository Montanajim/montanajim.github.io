# Switch Rev2



``` {admonition} Note
Changing to the Opacity to 0 (zero) will
make it disappear, but keep the space

Changing the visibility to false will
collapse the space.
```



## Lecture Code

```dart
import 'package:flutter/material.dart';
/*
NOTE:

Changing to the Opacity to 0 (zero) will
make it disappear, but keep the space

Changing the visibility to false will
collapse the space.

 */


void main(){
  runApp( const MaterialApp(
    home:  MyApp(),
  ));
}

class MyApp extends StatefulWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  _State createState() =>  _State();
}

//State is information of the application that can change over time or when some actions are taken.
class _State extends State<MyApp>{

  bool _value1 = false;
  bool _value2 = true;
  bool _value3 = false;

  bool _vstatus1 = true;
  bool _vstatus2 = true;
  bool _vstatus3 = true;

  String messageOff = "Switch is off";
  String messageOn = "Switch is on";
  String displayMessage = "Switch is off";

  // void _onChanged1(bool value) => setState(() => _value1 = value);
  // void _onChanged2(bool value) => setState(() => _value2 = value);

  void _onChanged1(bool value)
  {
    setState(() {
      //note that uniqueKey() has to be set in the text to
      //allow the text to be updated

      displayMessage = value ? messageOn : messageOff;
      //note that _value1 is setting the on/off position of the state
      _value1 = value ? true: false;


    });

  }

  void _onChanged2(bool value)
  {
    setState(() {

      _value2 = !_value2;
    });

  }

  void _onChanged3(bool value)
  {
    setState(() {

      _vstatus2 = !_vstatus2;
      _value3 = !_vstatus2;
    });

  }

  @override
  Widget build(BuildContext context) {
    return  Scaffold(
      appBar:  AppBar(
        title:  const Text('Switch Example'),
      ),
      //hit Ctrl+space in intellij to know what are the options you can use in flutter widgets
      body:  Container(
        padding:  const EdgeInsets.all(32.0),
        child:  ListView(
            children:[  Column(
              children: <Widget>[
                Row(
                    children: [
                      const Text("Switch 1",style: TextStyle(color:Colors.indigo),),
                      Switch(value: _value1, onChanged: _onChanged1),]
                ),
                Text(displayMessage,key: UniqueKey(),),
                const Divider(thickness: 3,height: 10,),
                SwitchListTile(
                  value: _value2,
                  onChanged: _onChanged2,
                  title:  const Text('Toggle Box',
                      style:  TextStyle(fontWeight: FontWeight.bold,
                          color: Colors.red)),
                ),
                AnimatedOpacity(opacity: _value2?1.0: 0.0,
                    duration: const Duration(milliseconds: 500),
                    child:
                    Container(
                      width:100,
                      height: 100,
                      color: Colors.indigo[800],

                    )
                ),
                const Divider(thickness: 3,height: 10,),
                SwitchListTile(title: const Text("Hide Box 2"),
                    value: _value3,
                    onChanged: _onChanged3),
                Row(
                    children:[
                      Visibility(
                          visible: _vstatus1,
                          child:
                          Container(
                              height: 100,
                              width: 100,
                              color: Colors.green[200],
                              child: Text("Box1"))),
                      Visibility(
                          visible: _vstatus2,
                          child:
                          Container(
                              height: 100,
                              width: 100,
                              color: Colors.blue[200],
                              child: Text("Box2"))),
                      Visibility(
                          visible: _vstatus3,
                          child:
                          Container(
                              height: 100,
                              width: 100,
                              color: Colors.yellow,
                              child: Text("Box3"))),
                    ]
                )
              ],
            ),
            ]
        ),
      ),
    );
  }
}
```

