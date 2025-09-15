# 📘 Flutter Widget Shortcuts

| **Widget**    | **Shortcut Purpose**                                     | **Mini Example**                                             |
| ------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| **Scaffold**  | Full-page layout (app bar, body, FAB, nav).              | `Scaffold(appBar: AppBar(title: Text("Hi")), body: Text("Hello"));` |
| **ListView**  | Scrollable list of widgets.                              | `ListView(children:[Text("One"), Text("Two")]);`             |
| **Text**      | Simple styled text.                                      | `Text("Hello", style: TextStyle(fontSize: 18));`             |
| **RichText**  | Multi-style text in one block.                           | `RichText(text: TextSpan(text:"Hi ", children:[TextSpan(text:"World", style: TextStyle(fontWeight: FontWeight.bold))]));` |
| **TextSpan**  | A styled substring inside `RichText` (can be clickable). | `TextSpan(text:"Tap me", style: TextStyle(color: Colors.blue));` |
| **Divider**   | Thin line to separate content.                           | `Divider(color: Colors.grey);`                               |
| **Container** | Flexible box for styling, padding, size, background.     | `Container(padding: EdgeInsets.all(8), color: Colors.red, child: Text("Boxed"));` |