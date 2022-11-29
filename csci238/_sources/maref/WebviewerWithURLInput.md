# Webviewer With URL Input



## Lecture Code

```dart
//webview_url
// developer: James Goudy

import 'package:flutter/material.dart';
import 'dart:io';
import 'package:webview_flutter/webview_flutter.dart';

void main() {
  runApp(const MaterialApp(home: WebViewExample()));
}

class WebViewExample extends StatefulWidget {
  const WebViewExample({Key? key}) : super(key: key);

  @override
  WebViewExampleState createState() => WebViewExampleState();
}

class WebViewExampleState extends State<WebViewExample> {
  var myFocusNode = FocusNode();

  TextEditingController myTextController = TextEditingController();
  String myUrl = "https://www.google.com";

  @override
  void initState() {
    super.initState();

    if (Platform.isAndroid) WebView.platform = SurfaceAndroidWebView();

    myTextController.text = "www.google.com";
  }

  @override
  void dispose() {
    myTextController.dispose();
    super.dispose();
  }

  void bttnPressed() {
    setState(() {
      myUrl = "https://${myTextController.text}";
    });

    myTextController.text = "";
    FocusScope.of(context).requestFocus(myFocusNode);
  }

  void clearTextField()
  {
    myTextController.clear();

  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(title: const Text('Webview URL Example')),
        body: ListView(children: <Widget>[
          Row(
              children: [
            const Text('Enter Url:'),
            Expanded(
                child: TextField(
                    controller: myTextController,
                    focusNode: myFocusNode,
                    decoration: const InputDecoration(
                        border: OutlineInputBorder(
                            borderSide: BorderSide(
                                color: Colors.indigo,
                                width: 2.0,
                                style: BorderStyle.solid))),
                    textInputAction: TextInputAction.newline,
                    onSubmitted: (value) {
                      bttnPressed();
                      myTextController.text = "";
                      FocusScope.of(context).requestFocus(myFocusNode);
                    })),
            Container( 
                margin: const EdgeInsets.all(10),
                child: ElevatedButton(
                onPressed: clearTextField,
                child: const Text("Clear"))
            )]),
          const Divider(height: 10, thickness: 3, color: Colors.red),
          SizedBox(
              height: MediaQuery.of(context).size.height,
              width: MediaQuery.of(context).size.width,
              child:

              WebView(
                key: UniqueKey(),
                initialUrl: myUrl,
                javascriptMode: JavascriptMode.unrestricted,
              ))
        ]));
  }
}

```

