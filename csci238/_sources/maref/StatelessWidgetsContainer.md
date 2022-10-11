# Stateless Widgets - Container

## Key Ideas

* Key Widgets

  * [Scaffold](https://api.flutter.dev/flutter/material/Scaffold-class.html)

  * [ListView](https://api.flutter.dev/flutter/widgets/ListView-class.html)

  * [Text](https://api.flutter.dev/flutter/widgets/Text-class.html)

  * [RichText](https://api.flutter.dev/flutter/widgets/RichText-class.html)
    * TextSpan

  * [Divider](https://api.flutter.dev/flutter/material/Divider-class.html)





> **NOTE:**
>
> Containers can not go past physical boundaries unless they are in a container that can.

## Example Code

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MaterialApp(home: MyStateLessWidget()));
}

class MyStateLessWidget extends StatelessWidget {
  //constructor
  const MyStateLessWidget({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: const Text("Home Page")),
        backgroundColor: Colors.indigo,
        body: Container(
            padding: const EdgeInsets.all(5.0),
            child: Column(
                //CrossAxisAlignment start, end, center, stretch
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: <Widget>[
                  Text("Happy Day"),
                  Text("The Beatles",
                      style: TextStyle(color: Colors.lime, fontSize: 24.0)),
                  Divider(color: Colors.red, thickness: 9.00),
                  MyRichText.allInfo("Bubba", "Smith", "Shepard", "Fido"),
                  MyRichText.allInfo("Suzy", "Jones", "Collie", "Lassie"),
                  Divider(color: Colors.red, thickness: 9.00),
                  MyCard(
                      title: const Text("I Love Boats"),
                      icon: const Icon(
                        Icons.directions_boat_outlined,
                        size: 40.0,
                        color: Colors.red,
                      )),
                  MyCard(
                      title: const Text("I Love Airplanes"),
                      icon: const Icon(
                        Icons.airplanemode_active,
                        size: 40.0,
                        color: Colors.blue,
                      )),
                  Row(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      mainAxisAlignment: MainAxisAlignment.center,
                      children: [
                        MyCard(
                            title: const Text("I Love Boats"),
                            icon: const Icon(
                              Icons.directions_boat_outlined,
                              size: 40.0,
                              color: Colors.red,
                            )),
                        MyCard(
                            title: const Text("I Love Airplanes"),
                            icon: const Icon(
                              Icons.airplanemode_active,
                              size: 40.0,
                              color: Colors.blue,
                            )),
                      ]),
                ]) //end of column
            ) //end of container
        );
  }
}

class MyRichText extends StatelessWidget {
  String _ownerFN = "";
  String _ownerLN = "";
  String _dogBreed = "";
  String _dogName = "Barky";

  MyRichText.allInfo(
      this._ownerFN, this._ownerLN, this._dogBreed, this._dogName);

  @override
  Widget build(BuildContext context) {
    return Container(
        decoration: BoxDecoration(
          border: Border.all(color: Colors.yellow, width: 5.0),
          borderRadius: BorderRadius.circular(10.0),
          color: Colors.lightBlueAccent,
        ), //bd
        margin: const EdgeInsets.fromLTRB(50, 5, 0, 20),
        padding: const EdgeInsets.all(10.0),
        child: Column(
            //crossAxisAlignment start, center, end, stretch
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              RichText(
                  text: TextSpan(children: <TextSpan>[
                const TextSpan(
                    text: 'Owner: ',
                    style: TextStyle(fontWeight: FontWeight.bold)),
                TextSpan(text: _ownerFN + ' ' + _ownerLN)
              ])), //end of Rich Text
              RichText(
                  text: TextSpan(children: <TextSpan>[
                const TextSpan(
                    text: 'Dog Name: ',
                    style: TextStyle(fontWeight: FontWeight.bold)),
                TextSpan(text: _dogName)
              ])), //end of Rich Text
              RichText(
                  text: TextSpan(children: <TextSpan>[
                const TextSpan(
                    text: 'Dog Breed: ',
                    style: TextStyle(fontWeight: FontWeight.bold)),
                TextSpan(text: _dogBreed)
              ])), //end of Rich Text
            ])); //end of container
  } //end of WidgetBuild
}

class MyCard extends StatelessWidget {
  final Widget title;
  final Widget icon;

  // constructor
  MyCard(
      {Key? key,
      this.title = const Text(""),
      this.icon = const Icon(Icons.ac_unit)})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
        padding: const EdgeInsets.all(10.0),
        child: Card(
            child: Container(
                padding: const EdgeInsets.all(10.0),
                child: Column(children: <Widget>[title, icon]))));
  }
}

```



<img src="./maimages/StatelessWidgets_Container.png" style="zoom:75%;" />