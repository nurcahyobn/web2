```dart

import 'package:flutter/material.dart';


void main() => runApp(new MyApp());


class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Flutter Demo',
      theme: new ThemeData(
       primarySwatch: Colors.blue,
      ), //ThemeData
      home: new MyHomePage(),
    ); // MaterialApp
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => new _MyHomePageState();
}
class _MyHomePageState extends State<MyHomePage> {
  bool _enabled = false;
  
  @override
  Widget build(BuildContext context) {
    var _onPressed;
    if (_enabled) {
      _onPressed = () {
        print("tap");
      };
    }
    return new Scaffold(
     appBar: new AppBar(
      title: new Text("Selly Nurika Putri"),
     ), // AppBar
      body: new ListView(
        children: <Widget>[
          new ListTile(
            title: new RaisedButton(
              child: new Text("Demo Me"),
              onPressed: _onPressed,
            ), // RaisedButton
          ), // ListTile
          new SwitchListTile(value: _enabled, onChanged: (bool value) {
            setState(() {
              _enabled = value;
            });
                    
          }), // SwitchListTile                       
        ], // <widget> []
      ), // ListView
    ); // Scaffold
  }
}

```
